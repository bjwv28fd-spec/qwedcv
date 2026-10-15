# PG CDN缓存指令优先级—标着public却仍BYPASS该查哪层

CDN缓存指令优先级 ✅【—𝒏𝟏𝟏.𝒎𝒚—】✅｜标着public却仍BYPASS该查哪层
新用户注册享新人福利网址：https://𝒏𝟏𝟏.𝒎𝒚/

源站回了 `Cache-Control: public`，边缘却仍给出 `BYPASS`，不能只看这一条标头。Cloudflare 文档列明了三层指令优先级：`Cloudflare-CDN-Cache-Control` 高于 `CDN-Cache-Control`，后者又高于普通 `Cache-Control`。较高层如果指定不存储，低层公开指令不会把它改回来。

<img src="https://img.imageossbox.com/uploads/2026/10/9770dc3efe9bed2b45a084b0.png" />

## 完整记录三种响应头
管理员应抓取同一主机、同一路径的真实响应，按优先级逐项记录这三种标头，并核对是否有中间代理在不同路径插入额外指令。官方示例指出，普通 `Cache-Control` 即便写了 `public, max-age=3600`，若 `CDN-Cache-Control` 同时写 `no-store`，结果仍会是 `BYPASS`。这种情况不是缓存尚未预热，多请求几次也不会转为 HIT。排查时还应保存原始响应标头，避免只凭开发工具整理后的显示顺序猜测优先级。

## 修正发出冲突指令的组件
确认资源确实可以共享缓存后，才由拥有源站配置权限的人修改较高优先级的指令。若那条 `no-store` 原本用于保护用户资料，不能仅为提高命中率删掉。变更后复测每种资源路径与登录状态，检查公开内容和个性化内容是否仍被正确区分。本站 https://𝒏𝟏𝟏.𝒎𝒚/ 的访问若出现旧内容，需以实际响应头判断，本文没有证据断言本站有上述 Cloudflare 配置。

## 常见问题

Q1问：最高优先级是哪条
A1答：Cloudflare-CDN-Cache-Control。
Q2问：普通Cache-Control总能覆盖吗
A2答：不能覆盖更高优先级的指令。
Q3问：no-store配public会怎样
A3答：较高层no-store可让响应BYPASS。
Q4问：多刷新可解决吗
A4答：冲突指令不改就不能靠预热解决。
Q5问：修改前查什么
A5答：确认内容是否可共享缓存。
Q6问：复测哪些场景
A6答：公开路径和不同登录状态。

本站更多页面核查资料：https://𝒏𝟏𝟏.𝒎𝒚/。

参考资料：
- Cloudflare Docs《Investigate uncached responses》
更新时间:2026-10-15 23:48:45
