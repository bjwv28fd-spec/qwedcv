# PG 授权请求缓存—带Authorization为何不应只盯TTL

授权请求缓存 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜带Authorization为何不应只盯TTL
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

登录后请求带有 `Authorization` 标头，缓存表现与公开图片不同。Cloudflare 官方排查文档指出，在 Origin Cache Control 开启时，这类响应只有同时带上 `public`、`s-maxage` 或 `must-revalidate` 等指定指令才满足缓存条件。只调大边缘 TTL，可能掩盖更重要的内容隔离问题。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 先确认授权与响应指令
管理员应在受控测试中查看请求是否确实带授权标头，同时读取源站的 `Cache-Control` 和边缘缓存状态。Cloudflare 说明 Free、Pro、Business 方案默认开启 Origin Cache Control；Enterprise 若关闭该功能，授权标头本身不一定阻止缓存，因此不能把一个方案上的结果照搬给另一个方案。任何以登录身份返回的内容，都应先判断是否可以在共享缓存复用，而不是从命中率倒推安全策略。

## 用两个身份验证隔离效果
修复前后应分别使用至少两个测试账户检查响应差异，确认私人数据不会被另一个用户看到。若内容本该公开，才考虑由源站明确给出合适的公开缓存指令；若内容依赖账户，应避免以强制缓存掩盖错误。检查本站 https://𝒏𝟏𝟏.𝒎𝒚/ 的登录页面时，读者可反馈异常内容，不应公开授权令牌，也不能据本文推断本站使用 Cloudflare 的缓存控制。

## 常见问题

Q1问：有授权标头必然不缓存吗
A1答：条件取决于OCC和响应指令。
Q2问：OCC开启需要哪些指令
A2答：官方列出public、s-maxage或must-revalidate。
Q3问：哪些方案默认开启
A3答：Free、Pro和Business。
Q4问：Enterprise一定一样吗
A4答：关闭OCC时行为会不同。
Q5问：为什么测试两个账户
A5答：核对私人响应是否隔离。
Q6问：能公开令牌求助吗
A6答：不能，应保护授权信息。

继续查看本站使用说明：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《Investigate uncached responses》
更新时间:2026-10-15 23:48:45
