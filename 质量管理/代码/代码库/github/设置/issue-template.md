# issue template

使用 issue template 可以帮助维护者预设不同目的的 issue ，并为之分别设置不同的内容格式，方便提示提交者关注必要的说明，采集必要的信息。

可以参考官方文档 [为仓库配置议题模板](https://docs.github.com/cn/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository) 。



## 为什么使用

合理使用 issue template 可以：

1. 引导提交者逐步检查，在过程中尝试解决掉一些快速解决的问题
2. 引导提交者按照期望采集更多有价值的信息

总体来说，issue template 是通过降低提交者提交速度，提升思考量的方式，避免不必要的提交，同时帮助双方聚焦关键信息，降低后续沟通的成本。



## 如何使用

在代码库根目录下的 `.github/ISSUE_TEMPLATE` 目录中增加一个符合格式要求的 `.yml` 配置文件即可启用一个新的 issue template。

**注意：`config.tml`会被视作一份全局 issute template 配置。它与其他 `.yml` 文件的格式和作用都是不同的。**

这样一个 `.yml` 配置文件实际上是一份表单描述，遵循 [语法](https://docs.github.com/cn/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms) ，可用的表单元素参考 [GitHub 表单架构的语法](https://docs.github.com/cn/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-githubs-form-schema)。

以这样一份 `enhancement.yml` 为例：

```
name: 功能 / Enhancement
description:  "提议新功能，或改善已有功能 / New feature request or improvement suggestion"
labels: [enhancement]
body:
- type: checkboxes
  attributes:
    label: 模块 / Components
    description: |
      选择 bug 所在的模块。
      Please select the components you are filing a bug for
    options:
      - label: venus-sector-manager
        required: false
      - label: venus-worker
        required: false
      - label: 工具链 / toolchains
        required: false
      - label: 文档 / docs
        required: false
- type: textarea
  id: description
  attributes:
    label: 描述 / Description
    placeholder: |
      是否可以考虑...
      I suggest ...
  validations:
    required: true
```

由一个勾选组和一个文本框组成。



在设置好 issue template 后，用户通过 `New issue` 按钮创建时，会先进入一个 issue 类型选择页面，然后根据所选类型填写相应的信息。