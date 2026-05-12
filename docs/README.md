# 文档入口

> [!IMPORTANT]
> 权利声明 / Rights Notice
>
> 本仓库自有文档和配置由 dadaomamao 保留全部权利。仓库中引用的第三方规则、项目名称、服务名称、域名、商标和链接仍归对应权利人所有。更多说明见 [NOTICE.md](NOTICE.md)。
>
> 本倉庫自有文件和配置由 dadaomamao 保留全部權利。倉庫中引用的第三方規則、項目名稱、服務名稱、網域、商標和連結仍歸對應權利人所有。更多說明見 [NOTICE.md](NOTICE.md)。
>
> All rights in the repository's own documentation and configuration are reserved by dadaomamao. Third-party rules, project names, service names, domain names, trademarks, and links referenced here remain the property of their respective rights holders. For more information, see [NOTICE.md](NOTICE.md).
>
> 本リポジトリ固有の文書及び設定については、dadaomamao がすべての権利を留保します。本リポジトリで参照される第三者の規則、プロジェクト名、サービス名、ドメイン名、商標及びリンクは、それぞれの権利者に帰属します。詳細は [NOTICE.md](NOTICE.md) を参照してください。
>
> 본 저장소의 자체 문서 및 설정에 관한 모든 권리는 dadaomamao가 보유합니다. 여기에서 참조되는 제3자 규칙, 프로젝트명, 서비스명, 도메인명, 상표 및 링크는 각각의 권리자에게 귀속됩니다. 자세한 내용은 [NOTICE.md](NOTICE.md)를 참조하십시오.

个人规则配置集合。

本仓库不是任何第三方规则项目的镜像，这里保存的是 `dadaomamao` 自用的补充规则，方便通过明确 raw URL 引用。

## 根目录约定

根目录只保留使用流程或维护流程真正需要直接读取的入口：

- `AI.list`
- `eSIM-AI.list`
- `ProxyLite.list`
- `Direct.list`
- `crypto.list`
- `AGENTS.md`

一般说明文档统一放在 `docs/`。这样做是为了减少自动读取流程把说明性 Markdown 当作规则输入的机会。

`AGENTS.md` 留在根目录，因为它是全仓库最高维护规则，不是规则列表。任何维护者或自动化在修改本仓库任何文件前，必须先读取根目录 [AGENTS.md](../AGENTS.md)。

## 文档导航

安全边界、人工确认和高风险对象以根目录 [AGENTS.md](../AGENTS.md) 为准。

规则入口、导入方式和日常使用见 [USAGE.md](USAGE.md)。权利、公开状态和第三方材料边界见 [NOTICE.md](NOTICE.md)。

维护记录见 [CHANGELOG.md](CHANGELOG.md)。

`docs/*.md` 只给人阅读，不是规则入口。

## 维护原则

见 [AGENTS.md](../AGENTS.md)。
