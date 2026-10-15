# PG Pages跳转文件—配置了_redirects为何函数路径不生效

Pages跳转文件 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜配置了_redirects为何函数路径不生效
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

Cloudflare Pages 项目放入 `_redirects` 文件后，静态路径能够跳转，某个由 Pages Functions 处理的路径却不跳，先确认该请求是否交给 Function。官方明确指出 `_redirects` 的规则应用于静态资源响应，不应用于 Functions 所服务的请求，即使文件中的模式匹配该 URL。此时要把相应逻辑移到 `/functions` 路由代码，或让该路径不再由 Function 接管。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 核查文件进入构建产物

`_redirects` 是无扩展名的纯文本文件，通常放在框架的 `public` 或 `static` 目录，以便构建后复制到最终静态资源目录。每行写一个来源、目标及可选状态码；格式错误会被忽略，不写状态码默认 302。先在部署产物里确认文件存在，再检查所测路径是否由静态资源提供。只看本地源代码里有文件，无法证明已随当前部署上线。

## 检查命中顺序

相同来源路径有多条规则时，靠前规则先应用；静态规则应排在动态规则前。若既在 Cloudflare 区域配置 Bulk Redirect，又在 Pages 写 `_redirects`，前者会先于 Pages 项目执行。本站 https://𝒏𝟏𝟏.𝒎𝒚/ 的阅读页面不能证明本站使用 Pages。站长排查时应同时检查部署产物、Functions 路由及边缘层跳转，找到实际处理请求的那一层。

## 常见问题

Q1问：`_redirects` 要加 `.txt` 吗？
A1答：不要，官方要求无扩展名的同名文件。
Q2问：省略状态码默认什么？
A2答：默认使用 302。
Q3问：Functions 路径会应用文件里的跳转吗？
A3答：不会，须在函数代码处理或调整路由。
Q4问：格式错误的一行会怎样？
A4答：该声明会被忽略。
Q5问：相同来源多条规则谁先执行？
A5答：文件中靠前的规则优先。
Q6问：还有 Bulk Redirect 时先看哪层？
A6答：先核对边缘 Bulk Redirect，再看 Pages 文件。

继续阅读本站页面发布专题：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《Redirects》
更新时间:2026-10-15 23:48:48
