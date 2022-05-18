# dependabot

dependabot 是 github 提供的一项，用于自动监测和更新代码库依赖包的服务。

完整的帮助文档参考 [dependabot](https://docs.github.com/cn/code-security/dependabot)。



## 为什么使用

对于符合条件的依赖库，dependabot 会自动生成升级的 pull request。

所以事实上，使用 denpendabot 就是利用维护者的强迫症，使得维护者主动去更新或拒绝依赖库的新版本。

在自动生成的 pull request 中，会包含

- Release notes
- Changelog
- Commits

等附加信息帮助维护者进行决策。



当同时维护多个相互之间存在依赖关系的代码库时，dependabot 也能提醒维护者。



除了常规的版本更新之外，dependabot 还会检测安全性更新，并生成警报(Dependabot alerts)。



## 如何使用

在代码库根目录下的 `.github/` 目录中增加一个符合格式要求的 `dependabot.yml` 配置文件即可启用。

配置文件的格式参考：[dependabot.yml 文件的配置选项](https://docs.github.com/cn/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file)。



### 重要的配置项

以这样一份配置文件为例：

```
version: 2
updates:
  - package-ecosystem: "cargo"
    directory: "/venus-worker"
    schedule:
      interval: "daily"
    allow:
      - dependency-name: "storage-proofs-core"
      - dependency-name: "forest_json_utils"
      - dependency-name: "forest_address"
      - dependency-name: "forest_cid"
      - dependency-name: "fil_clock"
      - dependency-name: "multiaddr"
      - dependency-name: "filecoin-proofs-api"
      - dependency-name: "filecoin-proofs"
      - dependency-name: "fil_types"

  - package-ecosystem: "gomod"
    directory: "/venus-sector-manager"
    schedule:
      interval: "daily"
    allow:
      - dependency-name: "github.com/filecoin-project/venus"
```



- `package-ecosystem: "cargo"`

  这一项的内容决定将要使用使用哪种依赖管理器，目前已支持 [包管理器](https://docs.github.com/cn/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file#package-ecosystem)。

- `directory: "/venus-worker"`

  这一项的内容决定将要监测的库的根目录，是以代码库根目录为基准的相对路径。

- `schedule:`

  这一项的内容决定监测的频率

- `allow / ignore`：

  这一项的内容相当于监测过程中的依赖包 白名单 / 黑名单