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
https://raw.githubusercontent.com/dadaomamao/RRS9CSL/refs/heads/main/crypto.list
```

使用时按下面的默认判断：

- `AI.list`：AI 服务相关规则。
- `eSIM-AI.list`：手机 / eSIM 场景使用的 AI 精修规则。
- `ProxyLite.list`：个人代理补充规则。
- `Direct.list`：直连补充规则。
- `crypto.list`：虚拟货币相关观察规则。

不要把 `docs/*.md` 加入规则入口。Markdown 文件只给人阅读，不能当作规则列表。

## 金融和虚拟货币域名

银行、券商、支付、虚拟货币、账户风控和实名验证相关域名，按更保守的规则处理。

默认原则：

- 明确属于金融或虚拟货币服务的域名，全部放在 `Direct.list`。
- 不能因为某个使用场景访问异常，就把公开 raw 规则改成代理。
- 如果同一条金融规则同时出现在多个列表里，不能按普通重复规则自动删除。先确认它在公开规则中是否已经直连。

不同使用场景的表现可能不同。同一服务在不同地理位置、运营商、DNS 和出口网络下也可能不同。若确实需要代理，优先在该使用场景自己的配置里覆盖，不改变公开默认直连原则。

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
2. 再检查对应域名是否已经在 `AI.list`、`ProxyLite.list`、`Direct.list` 或 `crypto.list` 中。
3. 如果要新增规则，优先添加最小域名后缀。
4. 不要一次加入过宽的关键词。
5. 如果是金融、银行、支付或虚拟货币域名，先确认公开 `Direct.list`。
6. 再根据实际使用场景做覆盖。

## 维护入口

维护规则见根目录 [AGENTS.md](../AGENTS.md)。
