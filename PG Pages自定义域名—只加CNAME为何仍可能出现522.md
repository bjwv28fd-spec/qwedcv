# PG Pages自定义域名—只加CNAME为何仍可能出现522

Pages自定义域名 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜只加CNAME为何仍可能出现522
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

把子域名 CNAME 指向项目的 `pages.dev` 地址，并不等于已经把该域名接入 Cloudflare Pages。官方要求先在 Pages 项目的 Custom domains 流程里关联域名；只手工添加 CNAME、未完成项目内关联，可能出现 522。应先看项目自带地址是否已有成功部署，再核对自定义域名是否在项目中激活，最后查看 DNS 记录。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 子域名与根域名的条件不同

使用外部 DNS 服务时，Pages 自定义子域名可以通过 CNAME 指向项目的 `pages.dev` 主机名；但自定义根域名要把该域名作为 Cloudflare 区域，并将名称服务器指向 Cloudflare。若 DNS 本就在 Cloudflare，完成项目的域名设置后，系统通常会自动创建所需 CNAME。不能把“DNS 查到记录”当作 Pages 项目已认可这个主机名的证据。

## 按接入顺序排查

先在 Workers & Pages 找到目标项目，查看 Custom domains 中的域名和激活状态，再对照项目地址与 CNAME 指向。若域名曾改指其他源站，之后又改回 Pages，官方提示其状态可能变为不活跃，需要等重新激活，不能只改回记录就立即视为恢复。本站 https://𝒏𝟏𝟏.𝒎𝒚/ 的阅读入口不能证明本站用 Pages 托管；本文只供采用该产品的网站负责人核对接入链路。

## 常见问题

Q1问：只加 CNAME 就能完成 Pages 绑定吗？
A1答：不能，还须在 Pages 项目里添加自定义域名。
Q2问：外部 DNS 能用子域名吗？
A2答：可以，按官方流程关联后再配置指向项目地址的 CNAME。
Q3问：根域名也能保持外部名称服务器吗？
A3答：Pages 自定义根域名要求区域及名称服务器按官方条件配置。
Q4问：已有 DNS 答案为何仍会报 522？
A4答：可能缺少项目内的自定义域名关联。
Q5问：改回原 CNAME 会立即恢复吗？
A5答：未必，域名可能需重新变为活动状态。
Q6问：先查哪两个后台位置？
A6答：核对 Pages 项目自定义域名状态和 DNS 记录。

继续阅读本站建站专题：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《Custom domains》
更新时间:2026-10-15 23:48:48
