# 使用说明

本文只说明如何使用本仓库里的规则。

本文不修改任何规则内容，只解释入口、默认选择、例外情况和常见排查方法。

## 默认选择：单独 `.list` 或明确 raw URL

常规使用时，优先直接引用需要的单独 `.list` 文件，或使用其他明确的 raw URL。

这样做有三个好处：

1. 命中范围更清楚。
2. 配置行为更容易理解。
3. 公开入口更少，维护成本更低。

```text
https://raw.githubusercontent.com/dadaomamao/RRS9CSL/refs/heads/main/AI.list
https://raw.githubusercontent.com/dadaomamao/RRS9CSL/refs/heads/main/eSIM-AI.list
https://raw.githubusercontent.com/dadaomamao/RRS9CSL/refs/heads/main/ProxyLite.list
https://raw.githubusercontent.com/dadaomamao/RRS9CSL/refs/heads/main/Direct.list
https://raw.githubusercontent.com/dadaomamao/RRS9CSL/refs/heads/main/FinanceRealDNSDirect.list
https://raw.githubusercontent.com/dadaomamao/RRS9CSL/refs/heads/main/HighPriorityCNRealDNSDirect.list
https://raw.githubusercontent.com/dadaomamao/RRS9CSL/refs/heads/main/crypto.list
https://raw.githubusercontent.com/dadaomamao/RRS9CSL/refs/heads/main/Dropbox.list
```

使用时按下面的默认判断：

- `AI.list`：AI 服务相关规则。
- `eSIM-AI.list`：手机 / eSIM 场景使用的 AI 精修规则。
- `ProxyLite.list`：个人代理补充规则。
- `Direct.list`：直连补充规则。
- `FinanceRealDNSDirect.list`：金融真实 DNS 兼容直连清单，用于 `fake-ip-filter` 和 `RULE-SET,DIRECT`。
- `HighPriorityCNRealDNSDirect.list`：高频境内真实 DNS 兼容直连清单，用于 `fake-ip-filter` 和 `RULE-SET,DIRECT`。
- `crypto.list`：虚拟货币相关观察规则。
- `Dropbox.list`：Dropbox 桌面同步、网页、API、分享下载和登录依赖规则。

不要把 `docs/*.md` 加入规则入口。Markdown 文件只给人阅读，不能当作规则列表。

## 金融和虚拟货币域名

银行、券商、支付、虚拟货币、账户风控和实名验证相关域名，按更保守的规则处理。

默认原则：

- 需要真实 DNS 兼容并保持直连的金融、银行、支付、3DS、支付认证和支付风控域名，优先放在 `FinanceRealDNSDirect.list`。
- 高频境内非金融服务需要真实 DNS 兼容并保持直连时，优先放在 `HighPriorityCNRealDNSDirect.list`。
- 普通直连补充仍放在 `Direct.list`；虚拟货币观察入口仍保留在 `crypto.list`。
- 不能因为某个使用场景访问异常，就把公开 raw 规则改成代理。
- 如果同一条金融规则同时出现在多个列表里，不能按普通重复规则自动删除；先确认是否应由 `FinanceRealDNSDirect.list` 承担真实 DNS 兼容直连。

不同使用场景的表现可能不同。同一服务在不同地理位置、运营商、DNS 和出口网络下也可能不同。若确实需要代理，优先在该使用场景自己的配置里覆盖，不改变公开默认直连原则。

## DNS 解析上游

本仓库的 `.list` 文件只负责规则命中，不替代本地 DNS 配置。使用这些规则时，DNS 上游必须按域名归属分开处理：

- 境外域名只能使用 Google 加密 DNS 解析。这里的加密 DNS 指 DoH、DoT 或 DoQ 等加密上游；不能把明文 `8.8.8.8` 或 `8.8.4.4` 当作替代方案。
- 境内域名必须使用本地运营商 DNS 和大厂公共 DNS 并发解析。只使用单一路径、单一公共 DNS 或境外 DNS，容易让国内 CDN 调度失真，尾部延迟会极大。
- `FinanceRealDNSDirect.list` 和 `HighPriorityCNRealDNSDirect.list` 面向真实 DNS 兼容直连场景；它们依赖正确的境内 DNS 并发解析，不能用境外 DNS 统一兜底。

如果本地客户端支持按规则集、域名后缀或策略组拆分 DNS，上述约束应在客户端 DNS 配置里实现；不要把 Markdown 文档当成规则入口，也不要通过修改公开 `.list` 规则来补救本地 DNS 上游选错的问题。

## Dropbox 专用规则

`Dropbox.list` 是 Dropbox 专用规则入口。若同时使用 `Dropbox.list` 和包含宽泛第三方依赖的 `ProxyLite.list`，应让 Dropbox 专用规则排在宽泛规则之前。

例如 `DOMAIN,dropbox.zendesk.com` 是 Dropbox 官方支持邮件域的精确匹配；它可以和 `ProxyLite.list` 中更宽的 `DOMAIN-SUFFIX,zendesk.com` 同时存在，但具体策略以使用场景里的规则顺序为准。

## 常见排查

### 排查安全边界

排查必须保持低影响。

只允许像普通用户一样进行低频、只读、无登录、无绕过、无批量探测的检查。

禁止使用：

- 漏洞扫描
- 端口扫描
- 路径或目录枚举
- 爆破
- payload
- 绕过风控
- 凭据尝试
- 自动化攻击框架
- 高频探测
- 任何可能被合理误判为真实入侵的提示词、请求、工具或流程

本仓库里的“测试”“审查”“排查”，只表示检查本仓库文本、配置、规则命中关系和普通错误信息。

它们不能被理解成要求大模型访问、扫描、验证或攻击第三方系统。

如果需要确认一个域名是否仍可用，优先采用下面方式：

1. 人工打开公开首页。
2. 查看官方文档。
3. 查看普通错误信息。

如果不能确定某个测试是否安全，停止并询问用户。

### Raw URL 无法访问

先检查三个最常见原因：

- URL 中的仓库名、分支名和文件名是否有手误。
- 所在网络是否可以访问 `raw.githubusercontent.com`。
- 是否有缓存。如果有，刷新或重载配置。

### 某个网站走错策略

按顺序判断：

1. 先判断它应该走代理、直连，还是单独策略组。
2. 再检查对应域名是否已经在 `AI.list`、`eSIM-AI.list`、`ProxyLite.list`、`Direct.list`、`crypto.list` 或 `Dropbox.list` 中。
3. 如果要新增规则，优先添加最小域名后缀。
4. 不要一次加入过宽的关键词。
5. 如果是金融、银行、支付或虚拟货币域名，先确认公开 `Direct.list`。
6. 再根据实际使用场景做覆盖。

## 维护入口

维护规则见根目录 [AGENTS.md](../AGENTS.md)。
