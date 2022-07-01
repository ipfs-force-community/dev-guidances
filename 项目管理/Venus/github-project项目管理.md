## 背景

为了让团队在开发意图，设计，流程上能够更好的和社区沟通，以及对社区输出思路和想法。`Venus`团队采用了`github project`为辅助，进行项目管理。尽量做到大多数开发事宜`issue`化，在项目中都有所体现。

## Github Project

### Github Issue

`Github issue`作为项目管理的核心。下面通过`issue名称：issue内容`的格式，对可以通过建立一个`issue`的事项列举：

- `Sprint XX`: 某个`Sprint`的所包含的`sprint`目标。每个目标以`task list`形式在`sprint`计划会前列举，供团队在计划会上讨论。参考[例子](https://github.com/filecoin-project/venus/issues/4972)。
- `[venus-xxx]发布vX.Y.Z`: `Venus`某个组件发布新版本。参考[例子](https://github.com/filecoin-project/venus/issues/4972)。
- `[venus-xxx]修复/新增/完善xxx功能`: `Venus`某个组件可以单个`PR`完成的一个开发任务。一个开发任务可以是一个`bug`，一个新`feature`，一个优化，等等。参考[例子](https://github.com/filecoin-project/venus/issues/4975)。
- `[venus-docs]xxxxxxx文档`: `venus-docs`或者某个组件文档撰写的相关任务。参考[例子](https://github.com/filecoin-project/venus/issues/5004)。

### Github Issue Label

`label`对帮助分类/统计`issue`有很大作用。为了团队能更好使用`label`，其设置也不宜过于繁琐。部分`label`的定义是`lotus`遗留下的一些产物。下面通过`label名称：label含义`的格式，对常用`label`进行[列举](https://github.com/filecoin-project/venus/issues)：

- `BU-chain-service`: 此`label`泛指`issue`与链服务有关。（这里`BU`指代`Business Unit`，把链服务视为一个业务流）
- `BU-deal-service`: 此`label`泛指`issue`与订单服务有关。
- `BU-storage-power-service`: 此`label`泛指`issue`与算力服务有关。因为`Venus`组件组织架构的问题，`venus-cluster`相关的开发`issue`主要在其本身的[repo](https://github.com/ipfs-force-community/venus-cluster)中进行。
- `C-dev-productivity`: 此`label`指`issue`与研发自身流程有关，并不包含实际的开发任务。（这里`C`指代`Category`）参考[例子](https://github.com/filecoin-project/venus/issues/4972)。
- `C-bug`: 此`label`指`issue`是一个`bug`。
- `C-docs`: 此`label`指`issue`与文档相关。
- `C-Testing`: 此`label`指`issue`是一个测试用例/需求。
- `community`: 此`label`指`issue`来自社区。
- `Epic`: 此`label`指`issue`是一个比较大的目标，他的完成可能涵盖多个`issue`。参考[例子](https://github.com/filecoin-project/venus/issues/4972)
- `design`: 此`label`指`issue`与设计相关。
- `P0`，`P1`，`P2`: 此`label`分别指`issue`的优先级。`P0`优先级最高。

### Github Issue Projects

`issue`不仅可以被`label`，也能被设置其对应的`projects`。当前`Venus`各组件的`issue`都需要被加入到[Venus Project](https://github.com/orgs/filecoin-project/projects/51)中，便于使用`github project`对`issue`进行可视化管理。

### Github Issue Asignees

`issue`通过被`asign`，把`issue`分配给指定人员。通过对`issue`进行`asign`，便于`github project`对任务执行人的可视化管理。也方便团队内部协作。

## issue提交流程

1. 提交新`issue`可参照上述`github issue`类型，依样对`issue`命名。例：

```
Sprint 50
[venus-market]发布v3.0.0
[venus-market]修复检索polling panic错误
```

2. 按`issue`[模版](https://github.com/filecoin-project/venus/tree/master/.github/ISSUE_TEMPLATE)的提示，添加对`issue`必要的描述。
3. 添加`issue`对应的`label`。`label`解释参见上述`Github Issue Label`部分。
4. 添加`issue`对应的`projects`，并点击`+1 more`，分配该`issue`的`sprint`。

## PR提交流程

1. 按照`PR`名称[规范](https://github.com/ipfs-force-community/dev-guidances/blob/master/%E8%B4%A8%E9%87%8F%E7%AE%A1%E7%90%86/%E4%BB%A3%E7%A0%81/git%E4%BD%BF%E7%94%A8/commit-message%E9%A3%8E%E6%A0%BC%E8%A7%84%E8%8C%83.md)要求，对`PR`命名。例：

```
feat: api: add GetParamStatus 
refactor: rename LOTUS_USE_FVM_EXPERIMENTAL
chore: remove GetPaymentVoucher log
```

2. `PR`描述使用诸如`resolve`, `close`, `fix`等[Github keywords](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword)来关联相关`issue`。例：

```
fix https://github.com/filecoin-project/venus/issues/4971
```

3. 添加`PR`对应的`projects`，并点击`+1 more`，分配该`PR`的`sprint`。

## Github Project面板介绍

### 不同view介绍

- `TODO List View`: 没有定义`sprint`的所有`issue`合集。可以理解为当前待完成的`issue`池。每个`sprint`计划会议之前，需要研发同学对各个`issue`过一遍，并挑选`issue`到新的`sprint`开发计划中。有疑问的，可在计划会中一起讨论。
- `Cur Sprint`: 被添加到当前`sprint`所有的`issue`的列表视图。可以方便的可视化查看有哪儿些研发被`assign`了哪儿些`issue`。
- `Cur Sprint BV`: 被添加到当前`sprint`所有的`issue`的卡片视图。可以方便的可视化哪儿些`issue`轮转到了哪儿个状态。
- `Last Sprint`: 被添加到上个`sprint`所有的`issue`的列表视图。方便可视化查看上个`sprint`的任务完成情况。
- `Next Sprint`: 被添加到下一个`sprint`所有的`issue`的列表视图。

### Status列/栏

当前[Github Project](https://github.com/orgs/filecoin-project/projects/51/views/8)状态包括：

- `No Status`: 当`issue`新加入至`projects`时，将被自动加入到`No Status`状态。
- `In Progress`: 受限于当前`github project`相对比较初级的自动化状态流转的条件。`issue`从`No Status`流转到`In Progress`暂时需要手动拖动。
- `In Review`: 当一个`PR`被要求有`review:changes_requested`时候，这个`PR`会自动被流转到`In Review`状态。前提是这个`PR`已经被添加到`venus project`。
- `Reviewed`: 当一个`PR`被`review:approved`，那么这个`PR`将被自动流转到`Reviewed`状态。
- `Done`: 当一个`PR`被合并，并且这个`PR`的描述中正确使用了诸如`resolve`, `close`, `fix`等[Github keywords](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword)来关联相关`issue`的时候，那么`issue`和`PR`都将自动流转到`Done`状态。

### Sprint列/栏

`Sprint`定义了`issue`对应的`sprint`。当`issue`没有定义`sprint`时，默认这个些`issue`会存在于[TODO List View](https://github.com/orgs/filecoin-project/projects/51/views/8)中，在每次`sprint计划会`之前，需要团队整理，并可虑是否加入到`sprint`的研发计划中。当定义`sprint`后，`issue`会出现在`venus project`中，对应的`sprint veiw`里面，方便可视化管理。

## 项目管理流程

在[Github Project](https://github.com/orgs/filecoin-project/projects/51/views/8)设置正确，`issue`和各组件`PR`都正确/规范提交的情况下，项目管理的开源和可视化已可达到不错的效果。

### Sprint开始

- `sprint`计划会议前对`TODO List view`中的`issue`提前整理，有疑问的可以在会上讨论。
- `sprint`计划会议前，建立该`Sprint`对应的`issue`。例: `Sprint 51`
- 召开`Sprint`计划会议，依照季度目标，确立`Sprint`目标，并在`Sprint issue`中以`task list`形式列出
- 依照制定的`sprint`目标，按需建立对应的`issue`。遵守`Sprint`开发`SMART`原则。

### Sprint进行中

- 根据`Sprint`制定的目标，认领相关`issue`，`asign`该`issue`任务，并完成`issue`对应的相关任务。
- 如在`Sprint`中，展开目标过程中，需要对`issue`进行修改/补充的，可以按需调整。
- 如在`Sprint`中，有突发`issue`需要处理，可以对`sprint`目标进行适当调整。

### Sprint完成

- `sprint`总结会议，对该`Sprint`每个目标完成度进行评估。
- 整理未完成`issue`，对其进行评估，视情况关闭或者加入`TODO List View`中。



