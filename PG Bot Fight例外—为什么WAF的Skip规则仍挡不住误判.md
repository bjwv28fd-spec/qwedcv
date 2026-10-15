# PG Bot Fight例外—为什么WAF的Skip规则仍挡不住误判

Bot Fight例外 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜为什么WAF的Skip规则仍挡不住误判
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

合法自动化请求被 Bot Fight Mode 挑战时，站点管理员即使添加一条 WAF Skip 规则，也可能看不到改善。Cloudflare 明确区分 Bot Fight Mode 与 Super Bot Fight Mode：前者不属于可由 Ruleset Engine 的 Skip 动作排除的那一类检查，Page Rules 同样无法替它开例外。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 先查是哪项机器人防护采取动作
不要把所有机器人挑战都归到 WAF 自定义规则。管理员应根据安全事件的服务来源、动作和请求时间，确认究竟是 Bot Fight Mode 还是 Super Bot Fight Mode。若是前者，继续扩大 WAF Skip 的匹配范围只会让其他安全检查变宽，仍不能跳过此功能。Cloudflare 的误判文档解释了原因：Bot Fight Mode 的检查不在 Ruleset Engine 内运行，因此自定义规则的 Skip 无法覆盖它。

## 根据产品能力选择处理
若攻击已经结束且误判持续，可由站点管理员评估关闭 Bot Fight Mode，或使用官方列出的访问规则等路径；需要按业务接口建立精细例外时，可评估支持 Skip 的 Super Bot Fight Mode。每项调整都应以真实误拦记录为依据，并测试原先的正常请求与恶意样本。尤其应保留误判前后的事件记录，避免以后无法解释是哪项安全变更改变了结果。若本站 https://𝒏𝟏𝟏.𝒎𝒚/ 的访问被挡，读者应记录时间和页面信息反馈，不假设本站启用了任何 Cloudflare 机器人功能。

## 常见问题

Q1问：WAF Skip能排除BFM吗
A1答：Cloudflare明确说不能。
Q2问：Page Rules能绕开吗
A2答：也不能。
Q3问：为什么两者不同
A3答：BFM不在Ruleset Engine内。
Q4问：先看什么证据
A4答：事件里的服务和动作来源。
Q5问：应扩大Skip范围吗
A5答：不应凭猜测扩大安全例外。
Q6问：访客怎样求助
A6答：提供实际请求时间和拦截提示。

本站入口与提示核查见：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《Handle False Positives from Bot Fight Mode or Super Bot Fight Mode》
更新时间:2026-10-15 23:48:44
