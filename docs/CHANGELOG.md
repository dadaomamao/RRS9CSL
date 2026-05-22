# Changelog

本文件记录本仓库公开维护摘要。规则行为是否变化，以对应提交中实际修改的规则文件或文档为准；不适合公开的细节不在本文保留。

## 2026-05-22

### Network routing contingency note

- 当前网络环境恶化严重，普通软路由需要预备随时有可能切换到 eSIM 节点，后续需要做严格流量智能分流。

### AI Gemini local block

- 将 `AI.list` 中 Gemini / NotebookLM / AI Studio / MakerSuite / DeepMind / Generative Language / AI Platform 相关生效规则全部改为注释保留。
- Gemini 硬智力过低、幻觉严重，暂停使用并在本地予以屏蔽。
- `ProxyLite.list` 中 Gemini 系服务规则已由远端手动删除；本次同步该远端状态，不重新加入代理列表。
- `GoogleAccountAiUS.list` 指谷歌 AI 专用 list，单列最小化 Gemini 系服务，作为屏蔽用入口。
- 本次不触碰 Claude / Anthropic、OpenAI、Grok、Cursor 或金融相关规则块。

### eSIM Google AI route disabled after Gemini line test

- 将 `eSIM-AI.list` 中 Google AI / Gemini / NotebookLM / AI Studio 相关生效规则全部改为注释保留。
- Gemini 实测只能使用微软专线；其他线路无法正常无感使用。
- 因上述实测结果，Google AI / Gemini 相关规则只保留在通用补充代理和 `AI.list` 网络中，不接入 eSIM 网络。
- 本次只调整 `eSIM-AI.list` 的 Google AI 相关规则，不触碰 Claude / Anthropic、OpenAI、Grok 或其他规则块。

## 2026-05-21

### eSIM Google AI rule narrowing and security review

- 在 `eSIM-AI.list` 中重新启用 Google AI / Gemini / NotebookLM / AI Studio 相关精修规则，但继续保持 Claude / Anthropic 分流禁用边界不变。
- 将明显过宽或不属于 eSIM AI 精修入口的 Google 规则继续保持注释，包括普通 Google 搜索、YouTube、广告统计、通用静态资源、通用内容资源、通用容器和过宽 Google API 后缀。
- 将 `DOMAIN-KEYWORD,gemini` 保持注释状态，避免误伤 Google Gemini 之外的同名服务，尤其避免虚拟货币相关服务被关键词错误命中。
- 本次只启用更明确的 Google AI、NotebookLM、AI Studio、Generative Language、AI Platform、DeepMind、MakerSuite 和必要鉴权相关规则。
- 信息安全审查结论：通过。本次 diff 未发现敏感对象命中、攻击性测试措辞、凭据或密钥处理、主机环境修改、第三方规则复制、外部依赖安装、联网执行要求或普通 Google / YouTube / 广告统计误收。

## 2026-05-19

### ProxyLite forum, media, and custom proxy maintenance

- 在 `ProxyLite.list` 增补 `aitodo.co`，并将未启用的 `DOMAIN-KEYWORD,1e100` 注释候选移到文件前部的域名关键字匹配区，保持该关键词仍不生效。
- 新增 t66y 论坛专用代理规则：`t66y.com` 与已确认媒体/附件子域 `ci.t66y.com`。
- 为 t66y 论坛用户常见外链媒体补充 `cloudflareaccess.com`、`cf-ipfs.com`、`imgur.com`、`postimg.cc`、`catbox.moe`；`cloudflare.com` 和 `cloudflare.net` 因已由 `AI.list` 生效规则覆盖，仅在本块注释保留，不重复启用。
- 新增 JavLibrary 核心域名 `javlibrary.com`；Cloudflare 和通用图床依赖沿用现有 `AI.list` / `ProxyLite.list` 覆盖，不重复增加。
- 将 t66y 与 JavLibrary 相关块移动到常规自定义域名补充列表前，便于人工审阅；该移动不改变这些规则的生效内容。

### Direct and AI route maintenance

- 在 `Direct.list` 增补 115 网盘相关直连规则，覆盖 `115.com`、`115cdn.com`、`115cdn.net`、`115cloud.cn`、`115cloud.com`、`115cloud.net`、`115img.com`、`115meta.com`、`115vod.com`、`116cd.cn`、`116cd.com`、`116cd.net`、`anxia.com`、`sq.cc`、`fhnfile.oss-cn-shenzhen.aliyuncs.com`、`fhnfile.cn-shenzhen.oss.aliyuncs.com`。
- 修正 `Direct.list` 中银联分组的注释格式，把误连在标题后的 `DOMAIN-SUFFIX,unionpay.com` 拆成独立注释规则；本次不重新启用该规则。
- 在 `AI.list` 中将 `DOMAIN-KEYWORD,sora` 改为注释保留，继续保留 `boursorama.com` 可能被 `sora` 字符串误命中的说明。
- 在 `AI.list` 增补 `dynamedex.com`，记录其循证医学和医学大模型相关用途。

### FinanceRealDNSDirect audit note and comment cleanup

- 在 `FinanceRealDNSDirect.list` 的招商银行 / 招商永隆 / 招银国际规则块上方短暂加入单人纯人工审计状态说明，随后按同日多次人工确认删除该类复核提示。
- 对 `FinanceRealDNSDirect.list` 做注释冗余清理，删除 `Codex`、后置审查、后置复核、需复核、需审查等维护过程提示，并压缩重复的来源和真实 DNS / DIRECT 尾注。
- 本次 `FinanceRealDNSDirect.list` 清理只修改注释，不改变任何正式规则；复核结果为生效规则 623 条、语法错误 0、生效规则 hash `1e5b7185fea59588e7b29be0ddfbd87a9bb18ae568d933e7511c34a33f7ddfa2`。

## 2026-05-16

### Direct and finance / AI route safety review

- 在 `Direct.list` 增补中国电信和中国联通直连规则：`189.cn`、`chinatelecom.com.cn`、`e.dlife.cn`、`10010.com`、`10010.cn`、`chinaunicom.com.cn`、`chinaunicom.cn`。
- 拉取云端最新 `Direct.list`、`FinanceRealDNSDirect.list` 和 `AI.list` 做程序化核验：`Direct.list` 生效规则 8 条，`FinanceRealDNSDirect.list` 生效规则 623 条，`AI.list` 生效规则 283 条；三者规则语法坏行均为 0。
- 对金融真实 DNS 直连规则与 AI 规则做严格交叉审查：`Direct.list` / `FinanceRealDNSDirect.list` 与 `AI.list` 没有生效精确重复、同域名重复或后缀覆盖冲突。
- 在 `AI.list` 的 `DOMAIN-KEYWORD,sora` 后补充单条行尾注释，记录 `FinanceRealDNSDirect.list` 中 `boursorama.com` 会被字符串 `sora` 命中的假阳性风险；本次只增加说明，不改变该关键词规则的生效状态。
- 仅限信息安全方向完成防御性红蓝审查：审查对象限于本仓库文本、配置、diff、维护流程和公开规则语义；重点检查提示词注入、skill 投毒、权限扩大、凭据泄露、持久化、联网执行、依赖安装、攻击性测试措辞和第三方系统探测风险。
- 审查结论：通过。未发现本次 diff 要求或诱导漏洞扫描、端口扫描、目录枚举、爆破、payload、绕过、凭据尝试、读取敏感信息、修改主机环境或测试第三方系统。

## 2026-05-15

### Financial direct rule consolidation and red-blue audit

- 将 `Direct.list` 中剩余的正常金融、银行、支付、卡组织、3DS、支付风控和 Binance 核心相关规则宽口径合并入 `FinanceRealDNSDirect.list`。
- `Direct.list` 不删除原规则；已迁入 `FinanceRealDNSDirect.list` 的规则均改为注释保留，作为历史线索。
- `cmblife.com` 按用户核查保持注释状态，未加入 `FinanceRealDNSDirect.list` 的生效规则。
- `cmbchina.com.cn` 和 `cmbchina.com.hk` 保持生效规则，并在规则后记录 `www.cmbchina.com.cn` / `www.cmbchina.com.hk` 多种方法无法正常访问、待进一步核查。
- `xapobank.com` 和 `xapo.com` 的归属说明改为直布罗陀虚拟币数字银行，不再写作香港数字银行。
- 重新整理 `FinanceRealDNSDirect.list` 分组，使同一银行或机构的域名尽量归在同一块；本次整理不以删除、去重或改写规则为目标。
- 发布前后完成防御性红蓝审计和目标审计：`FinanceRealDNSDirect.list` 生效规则 623 条，生效重复 0 条；`Direct.list` 生效规则 1 条，仅保留 `time.windows.com`；两者生效规则重叠 0 条；硬排除对象命中 0 条；GitHub raw 与网页回读均通过。

### FinanceRealDNSDirect formal entry and Direct duplicate retention

- 将 `FinanceRealDNSDirect.list` 纳入仓库公开入口和使用说明，定位为金融真实 DNS 兼容直连清单，用于 `fake-ip-filter` 与 `RULE-SET,DIRECT`。
- 修正 `FinanceRealDNSDirect.list` 文件头里的旧名 `RRS9CSL.list` / `rrs9csl`，统一为 `FinanceRealDNSDirect.list` / `finance_realdns_direct`。
- 将 `Direct.list` 中与 `FinanceRealDNSDirect.list` 规则类型和域名完全一致的 167 条活动规则改为注释保留；不删除原文。

## 2026-05-13

### PayPal / 贝宝 direct rule local specialization

- 将 `Direct.list` 中与 PayPal / 贝宝 / Braintree 明确、极高置信度单独相关的 `paypal.com`、`paypalobjects.com`、`braintreegateway.com`、`braintree-api.com` 改为注释保留。
- 本地已有对应 PayPal / 贝宝 / Braintree 专用规则；公开通用 `Direct.list` 因 KISS 和性能考虑不再启用这四条。
- 其他支付网关、卡组织、3DS、支付风控和反欺诈依赖仍保持原状，不扩大到非 PayPal / Braintree 专属规则。
- 本次不删除规则原文，不触碰其他支付、风控或 3DS 规则。

### Dropbox provider text compatibility

- 将 `Dropbox.list` 中仍带行内说明的生效规则改为“整行说明 + 纯规则行”，方便以 `behavior: classical`、`format: text` 的 rule-provider 方式引用。
- 本次只调整注释位置，不改变任何生效规则；`DOMAIN,dropbox.zendesk.com` 和 `DOMAIN,paper-attachments.s3.amazonaws.com` 仍保持启用。
- 远端 raw 复核显示 `Dropbox.list` 仍为 27 条生效规则、6 条注释规则、0 条坏行、0 条生效规则行内注释。

### Dropbox list entry and strict audit

- 将 `Dropbox.list` 补入仓库公开入口、根目录说明和使用说明，使其成为正式维护的单独规则入口。
- 按 Dropbox 官方域名页面，将已确认的 Dropbox 官方域名在 `Dropbox.list` 中启用；`DOMAIN-KEYWORD,dropbox` 因匹配面过宽继续保持注释。
- 将 Dropbox 中的 Arkose 精确主机规则改为注释，Arkose 归属继续保留在 `AI.list`，避免 AI / 风控归属冲突。
- 保留 `DOMAIN,dropbox.zendesk.com` 作为 Dropbox 官方支持邮件域的精确匹配；不修改 `ProxyLite.list` 中更宽的 Zendesk 规则。
- 本次重大更新后执行最严格审计，结论为 `PASS_WITH_NOTES`：保留的跨列表覆盖均已说明归属或使用顺序，未发现坏行、敏感信息、攻击性测试措辞或越权文件改动。

## 2026-05-12

### KISS highest principle

- 按三次明确确认，在 `AGENTS.md` 最高原则中新增“本仓库遵循 KISS 原则”。
- 保留既有“KISS 必须服从安全”边界，避免把简化理解为削弱安全、确认门槛或规则保留要求。
- 本次只更新全局维护文档和维护记录，不修改任何 `.list` 规则行或实际分流行为。

### eSIM AI maintenance boundary

- 将 `eSIM-AI.list` 补入 `AGENTS.md` 全仓库维护入口，并新增手机 / eSIM 场景的 AI 精修规则维护边界。
- 明确 `eSIM-AI.list` 不是 `AI.list` 的自动同步版、压缩版或替代版；其与 `AI.list` 的必要重叠属于场景化入口设计，不按普通跨列表重复自动清理。
- 本次只更新全局维护文档和维护记录，不修改任何 `.list` 规则行或实际分流行为。

### Repository red-blue review and rights documentation alignment

- 全仓库防御性红蓝审核通过。
- 重构了 `NOTICE.md`，并据此修正了 README 文档的对应部分。

### Maintenance stop rule for unexplained rules

- 按三次明确确认，`AGENTS.md` 最高原则新增 stop rule：不知道一条规则为什么存在或为什么不存在时，必须停止并询问用户，不得为补全、精简、归类、清理、去重或让规则看起来更合理而自作主张改变规则。

### AI list split for full and eSIM use

- 将 `AI.list` 恢复为本地可见版本中 active 规则最多的宽口径完整版本，用作默认 AI 规则入口。
- 新增 `eSIM-AI.list`，保留此前按手机 / eSIM 场景精修过的 AI 规则。
- `eSIM-AI.list` 将所有被注释停用的规则集中到文件顶部，以“为手机使用之故被精简”大组包裹，并按服务商分类保留原始注释规则；生效区保留 OpenAI / ChatGPT 核心链路及依赖，并重新启用 xAI / Grok 分组，上一轮恢复的 17 条 OpenAI / 依赖候选规则重新移回注释精简区。
- `eSIM-AI.list` 顶部新增醒目注释警示：本列表不得用于任何可能涉及 Claude / Anthropic 的分流场景。
- 本次不改变 `Direct.list`、`ProxyLite.list` 或 `crypto.list`。

### American Express / Amex domain review status

- 香港时间 2026 年 5 月 12 日 18:01，完成有充分理由支持的运通 / American Express / Amex 体系域名调整。
- 该调整等待第二人和第三人按相同流程再审。
- 在三审定谳前，如无充分理由支持，不要再对此域名块做大规模改动。
- 本条只记录维护状态，不修改 `.list` 或任何实际分流行为。

## 2026-05-11

### Alipay and WeChat Pay direct rule trial refinement

- 对支付宝 / 蚂蚁集团 / 网商银行，以及微信支付 / 财付通相关直连规则做有充分理由支撑的尝试性优化。
- 将两个支付服务族在 `Direct.list` 中单列为独立规则块，并补入本轮确认缺失的相关 `DOMAIN-SUFFIX` 规则。
- 本次按云端最新 `AGENTS.md` 重构后的风险矩阵和慢速路径口径执行；`AGENTS.md` 已重构为更明确的维护入口、风险等级和确认流程，本提交不再改动该文件。
- 后续继续观察和测试这些支付相关规则在真实使用场景中的稳定性；如无充分理由，不做额外扩大或收缩。

### Grok

- Grok 这门生意不配占用更多规则面积，最小可用就够了。

### 券商

- 死亡提醒我们：在投资和规则维护里，少动有时比频繁调整更接近长期收益纪律。

### OpenAI/GPT AI routing refinement

- 在 `AI.list` 顶部新增 OpenAI / ChatGPT / GPT 专项规则块，集中维护 OpenAI 核心入口、静态资源、用户内容、挑战验证、功能开关、iOS 完整性、企业 SSO、客服邮件订阅和遥测相关规则。
- 将过宽或本轮不纳入高置信口径的 OpenAI / Sora 相关旧规则改为注释保留，并统一写明这是基于 KISS 原则的尝试性精简。
- `js.stripe.com` 因支付直连和 OpenAI 订阅场景存在交叉，按用户两次确认仅保留为注释候选，不启用。
- 本次不触碰 Claude / Anthropic 明名规则，也不触碰 Sift、Arkose 和通用 Sentry / DataDog / Auth0 / Cloudflare 等可能服务 Claude 的共享基础设施规则。
- 校验结果：`git diff --check` 通过；规则语法检查 0 错误；OpenAI 置顶块精确匹配；`DOMAIN-KEYWORD,openai`、`DOMAIN-KEYWORD,chatgpt`、`DOMAIN-KEYWORD,sora`、`sora.com` 和 `js.stripe.com` 均非启用规则；四个列表没有新增完全重复启用规则。

### HSBC / Hang Seng domain review status

- 香港时间 2026 年 5 月 11 日 13:15，完成有充分理由支持的汇丰 / 恒生体系域名调整。
- 该调整等待第二人和第三人按相同流程再审。
- 在三审定谳前，如无充分理由支持，不要再对此域名块做大规模改动。
- 本条只记录维护状态，不修改 `.list` 或任何实际分流行为。

## 2026-05-10

### Markdown documentation refactor and Direct.list trial contraction

- 对仓库内 Markdown 维护文档做重构和精简，减少重复说明，把 AI 维护入口和关键规则收拢到根目录 `AGENTS.md`，其他说明保留在 `docs/`。
- 同步对 `Direct.list` 做尝试性精简，重点收敛重复或待复核的直连规则；规则行为是否变化，以对应提交中 `Direct.list` 的实际 diff 为准。
- 本条只说明公开摘要，不改变 `.list` 规则内容。

### Bank and UnionPay duplicate rule correction

- 恢复 `Direct.list` 顶部中国银行系、工商银行系、交通银行和银联 / 中国银联商务相关规则块。
- 收敛目标改为只处理下方分组中与顶部规则完全一致的重复启用规则；顶部规则保留为这些对象的有效位置。
- 同体系但不在确认清单内的相关规则继续保持注释停用。
- 本次不新增域名，不做第三方网站探测，不修改其他规则列表。

### Bank and UnionPay direct rule contraction

- 按三次人工确认，物理删除 `Direct.list` 中与确认清单完全一致的启用规则行；执行范围为中国银行系、工商银行系、交通银行和银联 / 中国银联商务相关 `DOMAIN-SUFFIX` 规则。
- 将同体系但不在确认清单内的相关规则改为注释停用。
- 本次不新增域名，不做第三方网站探测，不修改其他规则列表。
- 防御性审查确认：本记录不引导网络攻击、扫描、枚举、绕过、凭据尝试、信息读取或主机环境修改。

### Consolidate rules into AGENTS

- 删除重复维护入口，避免 AI 维护入口和人类说明文档重复维护同一批规则。
- 将仍有独立维护价值的内容并入根目录 `AGENTS.md`，包括各规则文件用途、完全重复规则口径、第三方内容合规审计和提交前检查。
- 同步更新 `docs/README.md` 和 `docs/USAGE.md` 的当前导航。
- 本次只重构 Markdown 维护文档，不修改 `.list` 或任何实际分流行为。

### README license and source notice placement

- 将 `docs/README.md` 尾部的“许可与来源”移动到文档入口顶部，使权利保留和第三方来源边界先于规则入口说明出现。
- 按 `docs/NOTICE.md` 的权利保留口径，将该段改写为简体中文、繁体中文、日语、英语和韩语五种简洁版本；简体中文为基准文本。
- 本次只修改 Markdown 维护文档，不修改 `.list` 或任何实际分流行为。

### AI-generated wording correction

- 修正由 AI 生成的明显错误和不当语句。
- 本记录不保留被修正的原文；本次只调整 Markdown 维护文档中的表述，不修改 `.list` 或任何实际分流行为。

### Multilingual notice review status

- 在 `docs/NOTICE.md` 写入多语言状态说明：简体中文为基准文本；其他语言版本为便利翻译；如有歧义或不一致，以简体中文版本为准。
- 保留并恢复 `docs/NOTICE.md` 中独立的繁体中文正文，避免多语言状态说明压掉繁体中文权利声明正文。
- 同步更新相关说明文档，要求后续维护多语言文本时保留语言状态说明和繁体中文正文。
- 本次只修改 Markdown 文档，不修改 `.list` 或任何实际分流行为。

### Disabled risk-dependency rules comment restoration

- 按 `AGENTS.md` 的注释保留规则恢复通用风险识别依赖小组；仅保留原规则文本，不启用。
- 恢复范围为通用风控和归因服务相关规则；这些规则在 `Direct.list` 中仍全部保持行首注释状态，因此不改变当前分流行为。
- 本次恢复依据是 `AGENTS.md` 的删除保护规则：维护时如需让规则失效，只能使用当前文件格式的注释形式保留原文并写明原因。
- 防御性审查确认：本条不重新启用规则，不新增网络测试或攻击性安全测试措辞。

### Public identifier cleanup

- 同步清理仓库内自有 raw URL、维护文档和相关规则名里的仓库标识。
- 公开标识保持固定格式，以降低规则 URL、配置和文档替换时发生格式错位的风险。
- 本次只处理仓库自身标识和 raw URL；不创建第三方规则文件，不恢复真实第三方上游 URL，也不新增可执行脚本、依赖安装、凭据读取、主机持久化或外部安全测试流程。
- 防御性审查确认：本次文字不引导网络攻击、扫描、枚举、绕过、凭据尝试、信息读取或主机环境修改。

### Third-party pointer cleanup

- 将有明确第三方上游指向的项目称呼替换为中性占位符。
- 这些占位符只表示隔离位置，不表示授权、来源归属或法律判断。
- 同步清理 `AGENTS.md`、`docs/README.md` 和 `docs/USAGE.md` 中非必要的独立项目称呼，改用更泛化的仓库或规则说明。
- 防御性审查确认：本次变更降低了第三方项目名暴露和错误归属风险；没有新增真实第三方上游 URL、真实占位目录、凭据读取、主机环境修改、联网测试要求或攻击性安全测试措辞。

### Compliance and third-party content audit

- 更新 `docs/NOTICE.md` 的第三方来源边界说明，明确避免拉取、复制、镜像、再分发、并入或改编第三方规则内容。
- 明确该说明只是技术隔离和合规控制措施，不构成法律意见，也不解释、判定、豁免或替代任何第三方许可证。
- 新增第三方内容合规审计规则：任何维护者在引入可能包含第三方规则或第三方材料的内容前，必须审计来源、许可证、复制范围、权利声明、署名或声明保留要求，以及是否可能触发强制性或不兼容开源协议义务。
- 本次文件级审计未发现已复制的第三方规则内容；该结论不构成法律意见，也不替代第三方项目自己的许可证、声明或条款。
- 本次只修改公开说明文档和维护记录，不修改 `.list` 或任何实际规则行为。

## 2026-05-09

### Maintenance rules

- 在根目录 `AGENTS.md` 新增规则注释格式：单条规则解释写在同一行规则后，用行尾 `#` 注释；独立成行的 `# ...` 只用于群块、小节或服务族标题。
- 明确这次是可读性改革，只定义注释位置和说明方式，不改变任何分流行为。
- 本次只修改 `AGENTS.md` 和本维护记录，不修改 `.list` 或其他实际规则配置。
- 防御性审查确认：新增文字不要求提示词注入、权限扩大、联网测试、漏洞扫描、执行命令、安装依赖、读取密钥或修改主机环境。
- 审计结论：这是仓库文本和配置层面的文档格式规范，不授权任何外部系统测试、主机配置改动或信息读取。

### Rules

- 在 `ProxyLite.list` 新增 Todoist / Doist 独立小节，用于任务管理、API 和官方服务相关代理规则。
- 将 `DOMAIN-SUFFIX,todoist.com`、`DOMAIN-SUFFIX,todoist.net`、`DOMAIN-SUFFIX,doist.com` 从常规自定义域名补充列表移入 Todoist / Doist 专门小节。
- 新增 Todoist 入口、API、Developer 和 Status 显式主机规则。
- `DOMAIN-SUFFIX,cloudfront.net` 保留在常规自定义域名补充列表，并增加说明：它是 Todoist 官方要求的通用 CDN 依赖，不是 Todoist 专属域名。
- 保留现有 `DOMAIN-SUFFIX,instatus.com`，它可覆盖 Todoist 状态页底层状态服务，但不归入 Todoist 专区。
- 在 `ProxyLite.list` 将小雅相关规则整理为“明确小雅专门域名 / 小雅元数据镜像”和“暂不能明确，严格模式先注释”两组，并将两组规则全部改为注释状态。
- 将用途无法确认的关键词规则改为注释状态。
- 在维护规则中明确：小雅相关服务疑似不公平地使用维护者资源，存在滥用风险；进一步安全审计完成前，不要重新启用已注释的小雅相关域名，也不要新增、恢复或移动未经确认的小雅相关规则。
- 除 `ProxyLite.list`、维护规则和本维护记录外，本次未修改 `Direct.list`、`AI.list` 或 `crypto.list`。

## 2026-05-08

### Third-party source isolation

- 将第三方来源指向替换为仓库内不可用的隔离占位路径。
- 处理范围包括已启用和已注释的第三方来源行；保留原规则名、策略组名、行顺序、特殊规则前缀和注释状态。
- 本次不创建任何占位目录或规则文件，确保这些 URL 只是失效化隔离路径。
- 目的为降低不希望承担的上游协议、复制、镜像、再分发或强制开源风险；这是技术隔离说明，不构成法律意见。

### Documentation

- 将集中式组合配置从推荐入口改为例外路径。
- 明确调整原因：性能考虑和信息安全考虑。
- 明确维护规则：常规维护必须排除该配置；只有用户专门要求时才处理。
- `docs/USAGE.md` 改为推荐使用单独 `.list` 或其他明确 raw URL。
- 本次只修改 Markdown，不修改 `.list` 或任何实际规则行为。

### Rules

- 新增或修改 `Direct.list` 中卡支付、卡组织、3D 验证和支付风控相关规则，覆盖 Visa、Mastercard、Discover、Cybersource、Authorize.Net、Visa Secure、CardinalCommerce、EMVCo、PayPal / Braintree、Forter、Riskified、Signifyd、Stripe、Adyen、Checkout.com、Worldpay、Square / Block、Klarna、Afterpay、Affirm、Wise、Revolut、Payoneer 等支付、认证、收单、反欺诈和跨境支付依赖。
- 将 Claude / Anthropic 风控证据支持的 Sift 相关域名收敛到 `AI.list`。
- 从 `Direct.list` 的卡组织验证和支付风控分组移除上述 Sift 规则，避免 AI 风控依赖和直连规则冲突。
- 从 `Direct.list` 移除无可靠 LLM 风控公开证据的通用风控域名。
- 保留 `AI.list` 现有 Arkose 规则，作为 OpenAI 证据和 Claude / Anthropic 风控证据对应的 AI 依赖规则。
- 本次不修改 `crypto.list`。

### Maintenance rules

- 将非发达国家或地区金融域名的整理方式写入根目录 `AGENTS.md`：按机构归属和控制背景判断，不按域名后缀或所在地一刀切。
- 明确上述口径是用户指定的 KISS 原则实践：一切应尽可能简单，但不能过于简单。
- 在根目录 `AGENTS.md` 增加银行 / 支付风控与 AI 风控交叉规则。
- 每次实质修改 `.list` 文件时，都必须判断是否涉及银行、支付、账户风控、实名验证、刷卡验证、3DS、反欺诈和 AI 风控的交叉归属。
- 当银行 / 支付风控直连需求与 AI 风控代理需求冲突时，必须向用户明确说明冲突对象、两边风险和拟归属，并至少 2 次人工确认。
- 如果冲突牵涉 Claude / Anthropic，确认门槛提高到至少 4 次。
- 补充 Claude / Anthropic 域名的最高谨慎说明：由于 Claude 模型的信息安全相关风险过高，本仓库按高级持续性威胁级物理隔离口径维护相关规则。
- 明确这些规则具有防御性信息安全价值，并作为最后一道软件分流锁，不能按普通 AI 可用性补充项处理。
- 明确上述说明只用于本仓库防御性维护，不授权实际操作、测试、尝试破坏、证明或绕过隔离机制。

## 2026-05-07

### Documentation layout

- 将一般说明性 Markdown 移入 `docs/`。
- 根目录继续保留 `AGENTS.md`，因为它是全仓库最高维护规则，不是规则列表。
- 重写 `docs/README.md`，明确根目录只保留规则入口和最高维护规则。
- 更新文档链接，避免 `docs/*.md` 被误当作规则入口。
- 本次文档布局整理没有修改 `AI.list`、`Direct.list`、`ProxyLite.list` 或 `crypto.list` 的任何规则行。

### Rules

- 完成 `Direct.list` 直连域名复核记录；本项只更新维护说明，不改变 `Direct.list` 的任何规则行。
- 完成 `ProxyLite.list` 中 emby-data 相关规则的可用性复核记录，并按结果只注释、不删除。
- `surrit.com` 不列入关停域名；维护口径改为“裸访问 403、只可能在特定来源、令牌或会话条件下可用”的特殊 CDN 域名。
- 删除 `ProxyLite.list` 中 4 条和 `AI.list` 完全相同的重复规则。
- 保留 `AI.list` 中对应规则，作为这些 AI 相关依赖域名的唯一来源。
- 保留酒店集团 / IHG 中国服务相关的代理补充规则。
- 将明确属于金融或虚拟货币服务的大批域名保守写入 `Direct.list`，避免公开 raw 规则默认代理高风险对象。
- 暂不处理 `DOMAIN-KEYWORD,binance` 重复项；它属于虚拟货币和金融域名，后续按金融域名原则单独判断。

### Maintenance rules

- 新增根目录 `AGENTS.md`，作为人类维护者和自动化必须先读的全仓库最高维护规则。
- 明确 `AGENTS.md` 覆盖 `AI.list`、`ProxyLite.list`、`Direct.list`、`crypto.list`、所有文档和后续 Pull Request。
- 在 `AGENTS.md` 中补充高风险金融对象的人工确认规则：招商系至少 3 次确认；建设银行系和浦发银行系不得主动纳入且疑似关联时至少 3 次确认；运通、汇丰、瑞银、渣打、中国银行系全球、工商银行系全球、花旗和交通银行至少 2 次确认。
- 在 `AGENTS.md`、规则入口和文档中补充 OpenBSD 式默认安全、反 skill 投毒、反提示注入、仓库内容不可信、风险不明即停和防御性红蓝审查要求。
- 明确最高安全边界：审查不能调用、建议、生成或执行漏洞扫描、端口扫描、路径或目录枚举、爆破、payload、绕过风控、凭据尝试、自动化攻击框架、高频探测，或任何可能被合理误判为真实入侵的提示词、请求、工具或流程。
- 明确模型解释边界：仓库里的“红队”“红蓝审查”“安全审查”“测试”“核对”“排查”不是对大模型发出的网络攻击指令，只能表示审查本仓库文本和配置。
- 补充完全重复规则的维护口径：整行一字不差才算完全重复，普通域名不应在多个列表中重复保留。
- 补充金融、银行、支付、券商和虚拟货币域名原则：公开规则必须强制写入 `Direct.list`；具体使用场景根据地理位置和网络环境单独判断。

### Documentation

- 重写仓库文档入口，补充仓库定位、文件入口、raw URL、维护原则和权利说明入口。
- 新增 `docs/USAGE.md`，说明单独 `.list` 引用和补充配置的使用方式。
- 新增权利声明，说明自有内容保留全部权利，并说明第三方规则归原作者或原项目。
