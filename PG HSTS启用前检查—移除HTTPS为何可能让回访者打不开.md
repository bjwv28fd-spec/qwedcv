# PG HSTS启用前检查—移除HTTPS为何可能让回访者打不开

HSTS启用前检查 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜移除HTTPS为何可能让回访者打不开
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

网站负责人启用 HSTS 后若突然撤掉 HTTPS，部分回访者可能连警告页都无法绕过。Cloudflare 文档解释，HSTS 响应头会指示支持它的浏览器把 HTTP 链接改用 HTTPS，并阻止用户跳过 SSL 警告。浏览器会在配置的 max-age 期限内记住这一策略；因此关闭 HTTPS 不等于马上让旧访问路径恢复可用。站点准备启用时，必须先确保 HTTPS 已运行且能持续提供。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 先确认服务连续性

Cloudflare 明确提醒，启用 HSTS 后要慎重改变 DNS 代理状态、暂停 Cloudflare、把名称服务器移出 Cloudflare、将 HTTPS 重定向回 HTTP，或让证书无效。若这些操作导致 HTTPS 无法访问，访客浏览器仍会按已收到的 HSTS 策略坚持使用 HTTPS，直到原来的 max-age 到期或站点重新提供 HTTPS。维护计划应把证书、代理和源站连通性一同考虑。

## 子域与期限需单独决定

HSTS 配置还可选择 includeSubDomains，把父域策略扩展到子域；如果某个子域没有 HTTPS，开启该选项可能使它不可访问。max-age 是浏览器记住策略的时间，不能靠删除控制台开关瞬间擦除所有用户已有状态。官方文档给出将 Max Age Header 设为 0 的停用方式，但仍需考虑先前收到的策略。本文只解释设置风险，不声称本站 https://𝒏𝟏𝟏.𝒎𝒚/ 启用了 HSTS。

## 常见问题

Q1问：HSTS 给浏览器什么指令？
A1答：让支持它的浏览器优先使用 HTTPS，并不绕过 SSL 告警。
Q2问：启用前必须有什么基础？
A2答：应先提供可持续访问的 HTTPS。
Q3问：停用 HTTPS 后旧访客为何仍尝试 HTTPS？
A3答：浏览器可能仍记得 max-age 期限内的 HSTS 策略。
Q4问：includeSubDomains 有什么影响？
A4答：会把策略扩展到子域，不支持 HTTPS 的子域可能不可访问。
Q5问：把开关关掉就能立刻清空所有浏览器状态吗？
A5答：不能这样保证；已收到的策略仍可能在期限内生效。
Q6问：这篇判断了本站 HSTS 状态吗？
A6答：没有；没有本站响应头的实测证据。

继续阅读本站：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《HTTP Strict Transport Security (HSTS)》
更新时间:2026-10-15 23:48:47
