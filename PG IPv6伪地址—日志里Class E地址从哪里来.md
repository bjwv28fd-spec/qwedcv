# PG IPv6伪地址—日志里Class E地址从哪里来

IPv6伪地址 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜日志里Class E地址从哪里来
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

启用 Cloudflare Pseudo IPv4 后，源站日志出现 Class E 范围的 IPv4 形式地址，不能直接把它当作访客真实公网 IPv4。官方说明该功能会根据原始 IPv6 哈希生成伪 IPv4，供只会处理 IPv4 字段的旧系统使用。若选择“覆盖标头”，`CF-Connecting-IP` 和 `X-Forwarded-For` 会被伪地址替换，原 IPv6 则保存在 `CF-Connecting-IPv6` 中。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 比较三种设置

Pseudo IPv4 默认关闭。选“添加标头”时，Cloudflare 额外给出 `CF-Pseudo-IPv4`，而不以它覆盖原客户端地址标头；选“覆盖标头”时，旧系统习惯读取的字段会看到伪 IPv4，须另读 `CF-Connecting-IPv6` 才能恢复原 IPv6 线索。Class E 地址是实验用途地址，不应拿它推断访客实际拥有可路由的 IPv4 网络连接。

## 排查异常地理定位

若日志或访问控制突然出现大量不寻常 IPv4，先查看 Cloudflare Network 页的 Pseudo IPv4 选项，再对照请求标头，避免把伪地址送入只接受公网 IPv4 的地理定位或封禁逻辑。可以保留一条确定来自 IPv6 客户端的测试请求，分别记录原连接类型、应用读取的 IP 字段和原 IPv6 标头；切换模式后用同一路径重测，确认报表里的变化仅来自字段转换。本站 https://𝒏𝟏𝟏.𝒎𝒚/ 的文章没有证明本站启用了该选项。调整任何日志或风控规则前，应用自己的测试请求核对 IPv6 原值是否可用。

## 常见问题

Q1问：伪 IPv4 是真实访客 IPv4 吗？
A1答：不是，它由原始 IPv6 派生。
Q2问：默认会生成吗？
A2答：Pseudo IPv4 默认关闭。
Q3问：添加标头模式写在哪里？
A3答：写入额外的 `CF-Pseudo-IPv4` 标头。
Q4问：覆盖模式会改哪些字段？
A4答：会覆盖 `CF-Connecting-IP` 与 `X-Forwarded-For`。
Q5问：原 IPv6 到哪里找？
A5答：覆盖模式把它保存在 `CF-Connecting-IPv6`。
Q6问：Class E 地址可当公网地址封禁吗？
A6答：不宜这样解释，先确认伪地址设置。

继续阅读本站网络诊断主题：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《Pseudo IPv4》
更新时间:2026-10-15 23:48:49
