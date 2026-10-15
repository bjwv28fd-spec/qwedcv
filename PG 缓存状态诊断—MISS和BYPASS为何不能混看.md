# PG 缓存状态诊断—MISS和BYPASS为何不能混看

缓存状态诊断 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜MISS和BYPASS为何不能混看
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

网站负责人看到资源响应头中的 CF-Cache-Status 不是 HIT，不能把 MISS、BYPASS 和 DYNAMIC 都叫作“缓存失效”。Cloudflare 文档区分得很清楚：MISS 表示请求有缓存资格，但当时缓存里没有该对象，内容来自源站；BYPASS 表示本来可以尝试缓存，却因源站响应或相关配置不被保存；DYNAMIC 则表示请求阶段就没有缓存资格。三种状态对应的排查方向不同。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 先核对资格再看响应

若是 DYNAMIC，应查看路径扩展名、匹配的绕过规则或是否启用开发模式；默认不缓存的 HTML 往往在这一层被判为不合格。若是 BYPASS，则应读源站响应头，例如明确禁止缓存的 Cache-Control；即使规则设为 Eligible，源站说不存时也可能出现 BYPASS。MISS 是另一回事，先确认是否刚清除过缓存、是否在同一缓存位置重复请求，再看后续请求是否变为 HIT。

## 记录同一资源的观察条件

比较状态时应使用同一网址和请求方式，并记下时间、响应头与访问地点。缓存可能分布在不同数据中心；一次 MISS 后另一处再次 MISS，不自动证明规则失效。官方排障页建议先看 cf-cache-status，再沿对应状态继续检查。不要只凭加载速度猜状态，也别把浏览器本地缓存的结果当作边缘返回。本站入口 https://𝒏𝟏𝟏.𝒎𝒚/ 不表示本站响应头已被本文检测。

## 常见问题

Q1问：MISS 说明资源永远不会缓存吗？
A1答：不说明；它有资格缓存，只是当前查询未命中。
Q2问：BYPASS 常提示哪类问题？
A2答：请求原本有资格，但响应或配置阻止保存。
Q3问：DYNAMIC 与 BYPASS 一样吗？
A3答：不同；DYNAMIC 是请求阶段就不具缓存资格。
Q4问：HIT 代表什么？
A4答：目标资源在 Cloudflare 缓存中找到并提供。
Q5问：看一次 MISS 就能断定规则坏了吗？
A5答：不能；还应核对后续同条件请求和缓存位置。
Q6问：本文测试过本站缓存状态吗？
A6答：没有；这里只解释官方响应头含义。

继续阅读本站文章：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《Cloudflare cache responses》
- Cloudflare Docs《Investigate uncached responses》
更新时间:2026-10-15 23:48:47
