# PG Set-Cookie缓存—响应带Cookie为何静态文件没命中

Set-Cookie缓存 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜响应带Cookie为何静态文件没命中
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

同样是一张图片，源站若在响应里设置 `Set-Cookie`，Cloudflare 是否缓存不能只看文件扩展名。官方文档把默认缓存层级和 Origin Cache Control 状态一起列出：控制开启时会保留 Cookie 并不缓存；控制关闭时，在特定默认条件下会移除 Cookie 后缓存。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 先看源站究竟回了什么
管理员应检查实际响应的 `Set-Cookie`、`Cache-Control` 与 `CF-Cache-Status`，并核对区域的 Origin Cache Control 设置。不要因为图片名看起来是静态资源，就忽略应用服务器给每个访客设置会话 Cookie 的行为。Cloudflare 的矩阵还说明，若用 Cache Rules 把资源标成 Eligible for cache，却没有配置明确的边缘 TTL，带 Cookie 的响应可能反复返回 MISS，因为 Cookie 被保留而资源未被存储。

## 按内容敏感度决定修复
如果文件本来就不应携带个性化信息，维护者可检查应用为何给它发 Cookie；如果页面含个人数据，则不应为了提高命中率强行缓存。改动后要同时验证 Cookie 是否按预期保留、不同账号是否看到各自内容，并确认退出登录后不会读到上一位用户的数据。查看本站 https://𝒏𝟏𝟏.𝒎𝒚/ 的加载问题时，读者不应从一次 MISS 推断本站配置错误，更不能推断本站启用了 Cloudflare；需要实际请求和响应证据。

## 常见问题

Q1问：静态后缀保证缓存吗
A1答：不能，响应标头也影响决定。
Q2问：OCC开启时怎样
A2答：默认层级下保留Cookie且不缓存。
Q3问：OCC关闭一定安全可缓存吗
A3答：仍需核查内容是否个性化。
Q4问：为何反复MISS
A4答：Eligible规则下Cookie可能保留而不存储。
Q5问：检查哪些标头
A5答：Set-Cookie、Cache-Control和缓存状态。
Q6问：改动后重点测什么
A6答：不同账户内容与Cookie行为。

继续阅读本站页面排查资料：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《Head Requests and Set-Cookie Headers》
更新时间:2026-10-15 23:48:45
