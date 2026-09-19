# new-warp-masque-actions

基于 [byJoey/warp-masque-actions](https://github.com/byJoey/warp-masque-actions) 的 Cloudflare Worker / Pages 单文件部署方案。

通过 Cloudflare WARP（MASQUE）接入 Opera 免费落地节点，自动生成 Clash / Mihomo 订阅。

## 与原项目的区别

| 项目 | 说明 |
|------|------|
| **可修改 SNI** | 管理页支持预设 / 自定义 MASQUE SNI，保存后写入全部节点并重建订阅 |
| **Pages 注册修复** | 修复部署在 Cloudflare Pages 时 WARP 注册失败 / 超时的问题（注册与订阅热路径分离、冷却控制） |
| **精简不可用线路** | 移除 Proton、Windscribe 相关代码（因为不可用） |

其余逻辑（Opera 落地、订阅生成、管理密码、KV 缓存等）与原项目一致。

## 功能概览

- 一键注册 Cloudflare WARP（MASQUE）
- 自动拉取 Opera 亚洲 / 欧洲 / 美洲落地
- 生成 Clash Meta / Mihomo 订阅（含分流规则）
- 管理页修改 SNI、订阅路径、密码
- 配置与设备信息持久化到 KV

## 部署

部署方式与 [原项目](https://github.com/byJoey/warp-masque-actions) 相同：

1. 将本仓库根目录文件上传至 Cloudflare **Pages** 或 **Worker**
2. 绑定 KV 命名空间，变量名必须为 `KV`
3. 访问站点设置管理密码
4. 在管理页点击「注册 WARP」，再「刷新 Opera 凭据」
5. 复制订阅链接导入 Clash Verge / Mihomo 等客户端

> 使用 Pages 时请确保已绑定 KV；首次使用需手动注册 WARP，订阅请求不会自动注册。

## 使用说明

1. 打开管理页 → **注册 WARP**
2. **刷新 Opera 凭据**（生成订阅）
3. 按需在 **MASQUE SNI** 中选择或自定义 SNI → 保存并重建
4. 将订阅链接导入客户端并更新

## 致谢

- 原项目：[byJoey/warp-masque-actions](https://github.com/byJoey/warp-masque-actions)
