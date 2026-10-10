# WorkBuddy2API-Hub · FnDepot 外部源

把多个 WorkBuddy / CodeBuddy 账号聚合成一个 **OpenAI 兼容 API**，并自带 Web 看板（账号导入导出、用量与积分统计）。装到飞牛（fnOS）后可以直接在应用中心里打开看板。

> 第三方外部源，由用户自行添加、仅在本机客户端生效；FnDepot 不审核、不担保本应用的代码安全与运行稳定性。

## 安装与打开

1. 在 FnDepot 里添加本源并安装 **WorkBuddy2API-Hub**（占用存储空间，约几十 MB）。
2. 到飞牛**应用中心**点「打开」：看板内嵌在飞牛界面里，已登录飞牛的用户**不用再输看板密码**（走统一网关的 socket 免密入口）。
3. 也可以直连 `http://<NAS的IP>:8788/`；这条路径要输看板密码，**默认 `admin`**，请首次登录后在「设置」里改掉。
4. 端口 `8788/tcp` 已随包声明；若路由器另有防火墙，记得放行。

## 导入账号

看板「导入账号」选 JSON 文件即可，支持本网关导出的文件、账号数组、单个账号对象、cockpit tools 的 snake_case 写法（`access_token` / `expires_at`）以及桌面客户端的 `{"account":…,"auth":…}`。导入后到「设置 → 使用说明」一键复制 API 地址与直连地址。

## 常见问题

- **看板打不开**：先看日志 `/var/apps/workbuddy2api/var/workbuddy2api.log`，再确认 `8788` 没被占用、防火墙已放行。
- **忘了看板密码**：停掉应用后改 `/var/apps/workbuddy2api/var/accounts/settings.json`，再启动（运行中改会被覆盖回去）。
- **升级/卸载会丢数据吗**：不会。账号凭证、看板密码、用量流水都在 `/var/apps/workbuddy2api/var/`；卸载向导选「保留数据」即可留着，重装接着用。程序目录升级时整体替换，别往里放东西。
- **源里只有 `1.6.19`**：外部源的版本键由本源维护，当前提供 `1.6.19`；FPK 不入 git，从 [Releases](https://github.com/ccrabit/workbuddy2api-hub/releases) 资产下载。

源码与问题反馈：[ccrabit/workbuddy2api-hub](https://github.com/ccrabit/workbuddy2api-hub)（应用维护者 ardeyouxipianyi）。
