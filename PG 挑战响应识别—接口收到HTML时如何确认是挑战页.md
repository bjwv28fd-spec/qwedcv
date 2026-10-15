# PG 挑战响应识别—接口收到HTML时如何确认是挑战页

挑战响应识别 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜接口收到HTML时如何确认是挑战页
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

前端请求原本期待 JSON，结果收到 HTML，不应立刻断言是后端程序报错。Cloudflare 文档说明，若请求遇到 Challenge Page，响应会带 `cf-mitigated: challenge`；无论原请求是什么资源类型，挑战页的内容类型都是 `text/html`。因此应检查该次响应标头，以 `cf-mitigated` 识别挑战，再到安全事件中核对是哪项策略触发。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 不让前端把挑战页当数据解析

在 `fetch` 或 XHR 的响应处理处，先读 `cf-mitigated` 是否等于 `challenge`，再决定进入挑战相关的处理流程；若不是，再按业务协议解析 JSON 或其他格式。只靠 `Content-Type: text/html` 不能区分 Cloudflare 挑战、源站 HTML 错误页或正常网页。该标头只在挑战页响应上具有这一说明，不能拿它判断所有封锁、限速或源站故障的来源。

## 留下可复核的请求信息

保存发生时间、接口路径、响应状态、`cf-mitigated` 与 `Cf-Ray`，再到安全事件里查询。要避免对整个站点粗放关闭保护：先核对匹配规则和请求特征，再决定是否调整该接口的策略。若测试本站 https://𝒏𝟏𝟏.𝒎𝒚/ 的某个请求，也须以实际响应为准；本文没有证据表明本站已启用挑战或某类机器人防护。

## 常见问题

Q1问：挑战页可能伪装成 JSON 吗？
A1答：官方说明挑战页的内容类型是 `text/html`。
Q2问：识别挑战最直接看哪个标头？
A2答：检查 `cf-mitigated` 是否为 `challenge`。
Q3问：这个标头有其他有效值吗？
A3答：官方文档只定义 `challenge` 这个值。
Q4问：收到 HTML 就一定是 Cloudflare 挑战吗？
A4答：不一定，还需核对挑战标头。
Q5问：前端应该何时尝试 JSON 解析？
A5答：先排除挑战响应，再按接口协议解析。
Q6问：能据此判断本站开了哪些防护吗？
A6答：不能；须检查本站实际请求与后台配置。

继续阅读本站故障排查文章：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《Detect a Challenge Page response》
更新时间:2026-10-15 23:48:48
