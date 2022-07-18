## 背景

为了方便`Venus`团队内部协作，以及更好的对社区输出有意义的`ChangeLog`，本文档对`PR`命名进行了规范。

## 考量

- `PR命名规范`上，不同于[commit命名规范](https://github.com/ipfs-force-community/dev-guidances/blob/master/%E8%B4%A8%E9%87%8F%E7%AE%A1%E7%90%86/%E4%BB%A3%E7%A0%81/git%E4%BD%BF%E7%94%A8/commit-message%E9%A3%8E%E6%A0%BC%E8%A7%84%E8%8C%83.md)，PR包含的范围更大，可以包含多个`commit`
- 一定程度上参考`Lotus`当前的[做法](https://github.com/filecoin-project/lotus/blob/master/.github/pull_request_template.md)，便于从`Lotus`社区过来的朋友阅读理解
- 参考当前`Venus`已经在做的、使用上的[习惯](https://github.com/filecoin-project/venus/pulls?q=is%3Apr+is%3Aclosed)
- 参考当前`cluster`已经在做的、使用上的[习惯](https://github.com/ipfs-force-community/venus-cluster/pulls?q=is%3Apr+is%3Aclosed)
- 方便团队使用。`github`中有的参数，如，`PR`提交人姓名就不加入到`PR`标题中

## 规范

标题采用`<PR类型>: <范围>: <PR概括描述>`或者`<PR类型>: <PR概括描述>`的格式。

- `<范围>`为可选项
- 冒号采用英语冒号
- 冒号后面跟一个空格，然后再是其他文字
- `PR`标题统一采用英文进行描述

### <PR类型>

`PR类型`包括但不限于以下类型...

开发类：

- `feat: `新功能特性类型的PR
- `fix: `修复错误(bug)类型的PR
- `opt: `性能优化类型的PR
- `chore: `杂项类型的PR，构建或者辅助工具等等的变更
- `refactor: `代码重构类型的PR
- `test: `添加/改动/删除代码测试类型的PR

非开发类：

- `docs: `文档类型的PR
- `revert: `代码回滚类型的PR
- `backport: `[版本发布](https://github.com/filecoin-project/venus/blob/master/documentation/misc/release-issue-template.md)时，从`master`合并`feat`至开发分支类型的PR

### <范围>

`<范围>`为可选项。因为`Venus`已经将各组件功能有所划分，实际操作过程中不一定方便定义，可以有较大自定义空间。这里例举一些思路：

- `api: `该组件中和API相关的范围
- `cli: `该组件中和命令行相关的范围
- `chain: `该组件中和链相关的范围
- `venus-shared: `该组件中和`venus-shared`相关的范围

### <PR概括描述>

用概括性的语言，尽量对`PR`做出易于他人理解的描述性语言。从社区的角度来讲，`feat`, `fix`, `opt`, `docs`可能关注的人更多一些，描述也相对需要更加斟酌一些。

### 示例

- lotus：[fix: cli: break out of retrieval if provider cancels](https://github.com/filecoin-project/lotus/pull/8912)
- venus: [feat: venus-shared: api version / namespaces & helper func for rpc endpoint](https://github.com/filecoin-project/venus/pull/4782)
- venus: [chore: bump version to v1.6.0](https://github.com/filecoin-project/venus/pull/4993)
- cluster: [fix: preload builtin actors](https://github.com/ipfs-force-community/venus-cluster/pull/264)




