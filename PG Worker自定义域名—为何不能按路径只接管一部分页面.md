# PG Worker自定义域名—为何不能按路径只接管一部分页面

Worker自定义域名 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜为何不能按路径只接管一部分页面
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

为 Worker 添加 Custom Domain 后，同一主机下所有路径都进入脚本，并非路由规则异常。Cloudflare 文档说明 Custom Domain 把整个域名或子域名指向作为源站的 Worker；匹配时只看主机名，不考虑路径和查询参数。若原计划只让 `/api/` 经过 Worker，而其他网页继续到现有源站，应设计 Route 匹配路径，而不是把整站主机名直接绑定为 Worker 自定义域名。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 理解主机名级绑定

例如把 `api.example.com` 绑定给某脚本，请求 `/login` 或 `/user` 都会执行同一个 Worker；它不会因为路径不同自动转回旧源站。平台会为 Custom Domain 建立 DNS 记录及所需证书，但前提是该域名所在 Cloudflare 区域处于活动状态，且对应 Worker 存在。目标主机名若已有 CNAME，官方明确不能直接在该主机上创建 Custom Domain，须先检查冲突并规划迁移。

## 确认路由方案

有外部应用服务器且只需部分路径执行脚本，应检查 Route 的代理 DNS 前提和匹配表达式。若 Worker 就是整个主机的应用源站，Custom Domain 才是相应入口。本站 https://𝒏𝟏𝟏.𝒎𝒚/ 的阅读页面不能证明本站采用哪种 Worker 入口；站长应以自己后台的域名绑定和请求日志验证，避免把所有路径意外接到同一脚本。

## 常见问题

Q1问：Custom Domain 会匹配路径吗？
A1答：不会，绑定判断以主机名为准。
Q2问：查询参数能决定是否执行脚本吗？
A2答：不能作为 Custom Domain 的匹配条件。
Q3问：平台会代建什么？
A3答：文档说明会创建相应 DNS 记录并签发证书。
Q4问：已有 CNAME 可直接绑定吗？
A4答：官方提示不能在已有 CNAME 的主机名上创建。
Q5问：只想处理部分路径怎么办？
A5答：可考虑在已有代理主机名前设置 Route。
Q6问：本站是否已这样绑定？
A6答：本文没有核实本站后台，不作此判断。

继续阅读本站建站说明：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《Custom Domains》
更新时间:2026-10-15 23:48:48
