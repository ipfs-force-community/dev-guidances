# webhooks

对应关键的代码库，维护者应当至少设置与 IM 沟通软件进行集成的 webhook。



## IM 集成

与 IM 集成的 webhook 应当保持精简，只提醒在我们的工作流程中必要的事件和信息，避免在正常的工作流程中产生过量的 IM 消息。

为了达成我们所预期的效果，应当有一款可以自定义事件筛选的 bot 工具。



### 应当包含的事件

我们认为这类 webhook 应当至少包含以下事件：

1. check runs

   - completed

   有助于了解 checks 的执行结果，以确认何时可以合并 pr，或根据失败的 checks 进行修复

2. issues

   - opened
   - reopened
   - deleted
   - assigned
   - unassigned

   有助于了解任务/社区报告的创建和分配

3. issue comments

   - created

   有助于了解任务/社区报告的新信息

4. pull requests

   - opened
   - closed
   - reopoened
   - assigned
   - unassigned
   - review requested
   - review request removed
   - ready to review

   有助于了解任务的执行情况

5. pull request reviews

   有助于了解任务的审阅情况

6. pull request review comments

   有助于了解任务的审阅情况

7. pull request review threads

   有助于了解任务的审阅情况

8. releases

   有助于了解版本发布的情况



### 谨慎包含的事件

对于数量较多、触发比较频繁，或在工作过程中不太关注的事件，我们应当谨慎处理，如

1. branch or tag
2. check runs 的其他
3. issues 的其他
4. issue comments 的其他