## 背景

`venus-docs`存在于这个[github repo](https://github.com/filecoin-project/venus-docs)中并有域名`venus.filecoin.io`指向其对应的`github page`。该文档继承了[PL](https://protocol.ai/)使用的`VuePress`框架作为生成静态`github page`的引擎。基于当前文档栈，本文档定义了`venus-docs`文档规范。

## 文档结构

当前文档有中，英语言。英文文档默认存在于`docs/`目录下。中文文档存在于`docs/zh/`目录下。链服务，算力服务，订单服务，组件，进阶，运维，6大板块对应了中英文档目录下各自的文件夹。

```bash
.
└── docs
    ├── advanced
    ├── cluster
    ├── guide
    ├── market
    ├── master
    ├── modules
    ├── operation
    └── zh
        ├── advanced
        ├── cluster
        ├── guide
        ├── market
        ├── master
        ├── mine
        ├── modules
        └── operation
```

通过类似如下`config.js`的配置，6大板块中的内容在左侧导航栏中进一步划分为大板块的中的细分类型。便于在内容不断增多后，快速找到所需的文档。

```javascript
[
    {
        title: '细分类目1',
        children: [
            // ...
        ]
    },
    {
        title: '细分类目2',
        children: [
        	// ...
        ]
    },
]
```

## 文档贡献规范

### 文档路径归属

按照上文文档结构，可按需在6大板块中适当增加细分类目，并添加文档至相应路径。当前参考细分类目如下：

```bash
└── Venus介绍
    ├── 前言
    ├── 文档导读
└── 链服务
    ├── 简述
    ├── 部署
└── 算力服务
    ├── 简述
    ├── 部署
    ├── 其他功能特性
└── 订单服务
    ├── 简述
    ├── 部署
└── 组件
    ├── 链服务组件 
    ├── 本地组件
└── 进阶
    ├── 进阶实战 
    ├── 本地开发
└── 运维
    ├── 运维实战 
    ├── 网络/组件升级
```

特别注意的是，组件板块中以外链至各组件自身的repo为主。`venus-docs`本身以流程文档为主。

### 文档名称

当新建文档时，统一使用小写英文字母加`-`隔开单词的模式。文档名称简洁介绍文档内容。例：

`what-is-venus.md`
`venus-cli.md`
`cluster-get-started.md`

### 文档章节

把文档需要介绍的内容做章节拆解。每个章节以`markdown`文本中的`##`开头。方便`VuePress`把章节标题编译至左侧导航栏。文档开头可简单介绍一下文档所说明的内容。例：

```bash
└── 新文档
    ├── 背景 
    ├── 章节1
    ├── 章节2
```

### 文档内容

- 流程文档为新手提供一步一步可执行的命令行，帮助其上手一个最小限度可以跑完流程的闭环。
- 流程说明要简洁。如需扩展，可提示相关外链。
- 每一步流程尽可能给出相关的验证逻辑。
- 文档内容以“授人以渔”为主。引导用户使用`--help`，日志查询等，寻找问题突破口。

### 文档测试

在给文档提交PR之前，使用`yarn docs:dev`，在本地环境`localhost:8080`确认修改无误。

## 文档书写规范

1. 灵活使用`vuepress`提供的"提示"和“注意”功能，让文档阅读更有层次。例：

	:::tip
	这是一个提示，vuepress生成绿色
	:::
	
	:::warning
	这是一个注意，vuepress生成黄色
	:::

2. 命令行开头使用`$`，利于读者区别于终端输出，前面就没有`$`。例：

	```bash
	$ whois google.com
	% IANA WHOIS server
	% for more information on IANA, visit http://www.iana.org
	% This query returned 1 object
	```

3. 文档链接尽量使用相对，而非绝对链接。例：

    ```markdown
	[相同目录可以直接用文件名](xiangtongmulu)
	[不同目录可以使用相对路径](/zh/cluster/new)
    ```


4. 灵活使用`markdown`的功能，把专用名词框起来。例：

	`venus-cluster`，`venus-market`，等等

5. 图片按需存放在`docs/.vuepress/public`路径下。
