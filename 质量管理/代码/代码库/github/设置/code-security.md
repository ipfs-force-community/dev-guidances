# Code security and analysis

对于重要的代码库，我们应当启用 `Code security and analysis` 配置页中的一些基本选项，并按照一定规范去处理报警。



## 设置

应当进行以下设置：

- 启用 `Dependabot - Dependabot alerts`
- 启用 `Dependabot - Dependabot security updates`
- 在 `Access to alerts` 中配置本代码库的维护人员/组，以确保在人工处理时，pr 的审阅者能进行核对



## 处理 Dependabot Alerts

当项目的依赖库被报告出现安全问题时，dependabots 会根据配置，自动发起报警， 并尝试生成一个 `update pull request`。

同时，在项目的 `Security` 标签上会展示未处理的事件数量。

代码库的维护者必须关注 `Security` 的情况，并作出处理。处理时应当遵循以下规范：

- 对于自动生成的 `update pull request`，维护者核对报警信息与更新内容，确认无误后合并

- 对于无法自动生成 `update pull request` 的情形，维护者应当手动更新，由其他人审阅，确认无误后合并

- 对于此类 `pull request` ，审阅时应当额外关注：

  - 更新的依赖和版本是否符合报警描述

  - 依赖图谱文件（go.mod，Cargo.toml）与依赖锁定文件（go.sum，Cargo.lock）是否都进行了必要的改变。

    如果需要更新的不是直接依赖，那么图谱文件可能不需要更新。

