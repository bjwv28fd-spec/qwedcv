# PG Flexible跳转环—源站强制HTTPS为何反复重定向

Flexible跳转环 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜源站强制HTTPS为何反复重定向
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

启用 HTTPS 后页面不停跳转，需先确认 Cloudflare 到源站的加密模式与源站重定向是否互相冲突。Flexible 模式让访客到边缘用 HTTPS，但边缘到源站仍发 HTTP；若源站每收到 HTTP 又跳回 HTTPS，下一轮请求会重复同一过程。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 把两段连接画成请求链
管理员可以从最初的访问协议开始，记录每次响应的状态码和 Location 目标，并分别标出边缘规则与源站规则。若看到访客发 HTTPS、Cloudflare 向源站发 HTTP、源站再要求 HTTPS，循环原因就比“清除浏览器缓存”更具体。Cloudflare 官方把这种组合列为 `ERR_TOO_MANY_REDIRECTS` 的典型原因；改设置前应先确认源站是否已有能用于 Full 模式的证书。

## 选择与源站能力相符的修复
官方列出的处理方式是移除源站的强制 HTTPS 重定向，或在源站配置证书后把加密模式改成 Full 或更高。不要仅为消除报错而关闭所有加密检查，也不要叠加另一条边缘跳转企图压过循环。修复后还应分别测试首页与实际报错的深层路径，确认每条路径的最终协议一致。核查本站 https://𝒏𝟏𝟏.𝒎𝒚/ 如果遇到循环，应提交完整地址和跳转链给管理员；本文只解释 Cloudflare 官方场景，不表明本站当前接入 Cloudflare。

## 常见问题

Q1问：Flexible到源站用什么
A1答：使用HTTP。
Q2问：为何浏览器仍显示HTTPS
A2答：那是访客到边缘的连接。
Q3问：源站跳转造成什么
A3答：HTTP与HTTPS请求会往复循环。
Q4问：改Full前要检查什么
A4答：源站需有可用证书和HTTPS服务。
Q5问：只清缓存有效吗
A5答：不能解决规则层的协议冲突。
Q6问：访客提供什么
A6答：起始地址和逐跳Location记录。

阅读本站更多站点访问说明：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《ERR_TOO_MANY_REDIRECTS》
更新时间:2026-10-15 23:48:44
