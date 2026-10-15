# PG Full模式跳转环—源站把HTTPS改回HTTP为何打不开

Full模式跳转环 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜源站把HTTPS改回HTTP为何打不开
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

与 Flexible 模式的循环相反，Full 或 Full strict 已经让 Cloudflare 用 HTTPS 联系源站。如果源站却自动把 HTTPS 请求重定向到 HTTP，浏览器可能在两种协议之间反复兜圈。定位这类报错应先读完整跳转链，不能只盯着第一跳是不是加密。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 判断是哪一段改了协议
Cloudflare 文档分别画出了两种循环。Full 场景下，边缘发往源站的是 HTTPS，源站返回的 Location 又指向 HTTP；下一次访问会再次触发边缘的 HTTPS 处理。管理员可以对同一路径分别记录状态码、Location、触发者和目标主机名，区分源站应用、反向代理与 Cloudflare 边缘规则。若某条跳转只在登录后出现，还应检查应用层生成的绝对地址。

## 移除造成回退的源站规则
官方针对 Full 或 Full strict 冲突建议去掉源站将 HTTPS 改回 HTTP 的跳转。变更时保留加密服务与证书检查，先在测试路径验证，再看生产入口是否只有预期的一次跳转。检查本站 https://𝒏𝟏𝟏.𝒎𝒚/ 若遇到相同浏览器报错，提供起点、逐跳状态与最终错误给站点管理员；若查不到源站规则，也不能因此假定是 Cloudflare 出错或本站启用了该产品。

## 常见问题

Q1问：Full到源站用什么
A1答：使用HTTPS。
Q2问：哪个方向会导致此例循环
A2答：源站把HTTPS重定向到HTTP。
Q3问：只看第一跳够吗
A3答：不够，要看往返的完整Location。
Q4问：要关闭源站HTTPS吗
A4答：不需要，重点是去掉错误降级跳转。
Q5问：登录页单独出错查什么
A5答：查应用生成的绝对网址和代理规则。
Q6问：访客应记录什么
A6答：完整路径、时间及逐跳状态码。

继续核对本站访问入口：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《ERR_TOO_MANY_REDIRECTS》
更新时间:2026-10-15 23:48:44
