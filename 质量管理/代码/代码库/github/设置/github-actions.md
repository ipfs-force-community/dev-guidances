# github-actions

用官方的定义来说，github-actions 就是一个CI(持续集成)、CD(持续交付)平台。

可以通过 [官方文档](https://docs.github.com/cn/actions) 了解更多信息。



## 为什么使用

使用 github-actions 的好处有以下几点：

1. 与代码、各种工作流程几乎无缝集成，尤其是在需要及时阻断下一步操作的环节
2. 有大量其他用户封装好的可复用的 actions

这些好处带来的开发体验：

1. 与 gitlab 这样 self-hosted 的代码托管平台提供的 CI/CD + pipelines/jobs 体系类似，主要体现在完整的工作流/事件支持；
2. 略好于做过深度集成的开发工具集如 github + CircleCI 、github + travisCI 类似，主要是体现在额外的 webhooks & github applications 的管理环节；
3. 要远远超出简单集成的 webhooks + event trigger + jobs/scripts 的组合。



同样，它也有一些局限：

1. 有额度限制
2. github 提供的运行容器硬件标准固定且较低

这些局限主要体现在“资源使用”上，可以通过 self-hosted runners 规避。



## 如何使用

在代码库根目录下的 `.github/workflows` 目录中增加一个符合格式要求的 `.yml` 配置文件即可启用一个新的  github-action。

配置文件的格式参考：[GitHub Actions 的工作流程语法](https://docs.github.com/cn/actions/using-workflows/workflow-syntax-for-github-actions)。



### 重要的配置项

以这样一份配置文件为例：

```
# This is a basic workflow to help you get started with Actions
name: check-rust-on-pr

# Controls when the workflow will run
on:
  pull_request:
    branches: [ main, release/** ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "check"
  check:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v2

      - name: dependencies
        run: sudo apt update && sudo apt install --reinstall ocl-icd-opencl-dev libhwloc-dev -y

      - name: setup rust
        uses: actions-rs/toolchain@v1
        with:
          toolchain: '1.60.0'

      - name: install components
        run: rustup component add --toolchain $(cat rust-toolchain) clippy rustfmt

      - name: check venus-worker
        run: make check-worker && make check-git
```



- `name: check-rust-on-pr `

  这一项的内容将会决定在 github 的工作流程中，显示的 action 名称；

  与直觉不同，配置文件的文件名并不会被用作 action 名称。

- ```
  on:
    pull_request:
      branches: [ main, release/** ]
  ```

  这一项将会决定 action 的触发条件；

  在这里，范例 action 将会在对指定的分支发起 `pull request` 时被触发；

  常用的触发条件还有 `push`，参考  [`on`](https://docs.github.com/cn/actions/using-workflows/workflow-syntax-for-github-actions#on)  、[触发工作流程的事件](https://docs.github.com/cn/actions/using-workflows/events-that-trigger-workflows)。

- ```
  # A workflow run is made up of one or more jobs that can run sequentially or in parallel
  jobs:
    # This workflow contains a single job called "check"
    check:
  ```

  这里定义了一个名为 `check` 的子任务，其后所有深一级缩进的配置项都是针对 `check` 这个子任务的；

  根据注释我们可知，一个 action 内允许存在多个子任务，这些子任务可以是顺序的，也可以是并发的。



#### 与以往的代码平台+CI平台的组合对比

作为和以往 CI / CD 执行方式的对比，我们可以看到：

1. name 用来描述一组任务的目的

2. on 类似于 “基于 webhooks 和特定事件的触发机制”

3. jobs 则是要执行的动作的集合，根据粒度，再划分为 子任务，或子任务中的步骤 (steps)

   事实上，actions - jobs - steps 这样一个三层结构在很多时候都可以根据实际情况来灵活划分



### 重要的、启用 action 的环节

我们认为，应当关注以下环节：

- 对于针对重要分支的 pr，

  应当启用：

  - 编译成功
  - 测试通过
  - 代码风格检查

  的 actions

- 对于针对重要分支的 push

  应当启用：

  - 编译成功
  - 编译结果发布

  的 actions

- 对于创建 tag，尤其是版本 tag

  应当启用：

  - 编译成功
  - 编译结果发布

  的 actions



### Tips

- 在 github 上，如果两个 jobs 都很耗时，且前后没有明显的依赖，如：后续任务依赖前置任务的结果，或者前置任务可以节省后置任务大量时间，那么它们更应该被拆分为两个 actions 并行来完成

- 在 `github-actions` 的编排中，使用 `actions/cache` 能够在一些条件下降低执行时间，无论从节约时间限额，还是缩短 review checks 的等待来说，都是十分有意义的。 

  以 venus-cluster 为例，在编排合理的情况下，cache 构建前后，

  - venus-worker: `36m5s => 18m26s`
  - venus-sector-manager: `4m19s => 3m46s`

  需要注意：

  1. cache 一般和编译的依赖清单绑定，如 golang 项目的 `go.sum`，rust 项目的 `Cargo.lock`
  2. 在使用 `actions/cache` 的情况下，倾向于认为，jobs 应该合并，而非如上一条 tip 所建议的那样进行拆分，这是为了尽可能复用 cache，同时避免 cache-miss 时重复构建
  3. 在 go 项目中，由于编译时间本身就比较短，所以节省的时间并不明显
  4. 观察日志可知，`venus-worker` 中涉及到 c/c++ 项目编译及链接的部分的耗时，即使在 cache 之后，也无法被消除，这可能跟编译过程本身有关，也可能跟 cache 目录的设置有关，有待进一步确认。

  参考阅读：

  - [actions/cache](https://github.com/actions/cache)
  - [缓存依赖项以加快工作流程](https://docs.github.com/cn/actions/using-workflows/caching-dependencies-to-speed-up-workflows)
  - [How I speeded up my Rust builds on GitHub ~30 times](https://ectobit.com/blog/speed-up-github-actions-rust-pipelines/)



