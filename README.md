# new-warp-masque-actions

基于 [byJoey/warp-masque-actions](https://github.com/byJoey/warp-masque-actions) 的 Cloudflare Worker / Pages 单文件部署方案。

通过 Cloudflare WARP（MASQUE）接入 Opera 免费落地节点，自动生成 Clash / Mihomo 订阅。

## 与原项目的区别

| 项目 | 说明 |
|------|------|
| **可修改 SNI** | 管理页支持预设 / 自定义 MASQUE SNI，保存后写入全部节点并重建订阅 |
| **Pages 注册修复** | 修复部署在 Cloudflare Pages 时 WARP 注册失败 / 超时的问题（注册与订阅热路径分离、冷却控制） |
| **精简不可用线路** | 移除 Proton、Windscribe 相关代码（因为不可用） |
| **新增了masque over masque协议** | 使用masque over masque协议，IP固定在美国，可以使用AI服务 |

其余逻辑（Opera 落地、订阅生成、管理密码、KV 缓存等）与原项目一致。

## 功能概览

- 一键注册 Cloudflare WARP（MASQUE）
- 自动拉取 Opera 亚洲 / 欧洲 / 美洲落地
- 生成 Clash Meta / Mihomo 订阅（含分流规则）
- 管理页修改 SNI、订阅路径、密码
- 配置与设备信息持久化到 KV

## 部署

部署方式与 [原项目](https://github.com/byJoey/warp-masque-actions) 相同：

1. 将本仓库_worker.js上传至 Cloudflare **Pages** 或 **Worker**
2. 绑定 KV 命名空间，变量名必须为 `KV`
3. 访问站点设置管理密码
4. 在管理页点击「注册 WARP」，再「刷新 Opera 凭据」
5. 复制订阅链接导入 Clash Verge / Mihomo 等客户端
6. 如果要使用masque over masque协议，就将masqueOvermasque.js改名为_worker.js部署到cloudflare pages，先点击“注册外层warp”，过几分钟再点击“注册内层”，在刷新opera凭据，即可使用masque over masque协议

> 使用 Pages 时请确保已绑定 KV；首次使用需手动注册 WARP，订阅请求不会自动注册。



## 致谢

- 原项目：[byJoey/warp-masque-actions](https://github.com/byJoey/warp-masque-actions)
