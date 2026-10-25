# WorkBuddy2API-Hub（FnDepot 外部源）

把多个 WorkBuddy / CodeBuddy 账号聚合成一个 **OpenAI 兼容 API**，并自带一个 Web 看板（账号导入导出、用量与积分统计、请求流水）。
装到飞牛（fnOS）上以后，可以直接在**应用中心里打开看板，不用再输看板密码**。

> 本仓库是**第三方外部应用源**。外部源由用户自行添加、仅在用户本地客户端生效；FnDepot 不对外部源的应用代码、
> 安装包安全性或运行稳定性做审核、担保或背书。

- 应用名（`appname`）：`workbuddy2api`
- 显示名：`WorkBuddy2API-Hub`
- 平台：`all`（通用包）
- 服务端口：`8788/tcp`
- 安装位置：存储空间（`install_type` 为空）

## 1. 添加这个源

FnDepot 客户端（需要 **v0.0.7 或更高**）→「添加源」，二选一：

1. **GitHub 仓库地址**（推荐）

   ```text
   https://github.com/ccrabit/workbuddy2api-hub
   ```

   客户端读取仓库默认分支根目录的 `fnpack.json`（文件名与大小写都必须完全一致）。

2. **JSON 直链**（仓库地址拉不动时的兜底）

   ```text
   https://raw.githubusercontent.com/ccrabit/workbuddy2api-hub/main/fnpack.json
   ```

   直链不要求文件名叫 `fnpack.json`，只要内容是 V2 结构；仓库默认分支不是 `main` 时，把 `main` 换成实际分支名。

添加后如果列表里看不到本应用，检查源同步状态里的错误详情；仓库模式下最容易被忽略的两点是
「根目录没有 `fnpack.json`」和「用了别的名字/大小写」。

## 2. 安装与打开

1. 在 FnDepot 里找到 **WorkBuddy2API-Hub**，安装（占用存储空间，约几十 MB）。
2. 装完到飞牛**应用中心**点「打开」——看板会内嵌在飞牛界面里打开，
   已经登录飞牛的用户**不需要再输看板密码**（走飞牛统一网关的 socket 免密入口）。
3. 也可以**直连**：`http://<NAS的IP>:8788/`
   这条路径要输看板密码，**默认 `admin`**，首次登录后请在「设置」里改掉。
4. 防火墙：`8788/tcp` 已在应用包内声明；如果路由器/交换机另有一层防火墙，记得放行。

## 3. 首次使用

- **导入账号**：看板「导入账号」选一个 JSON 文件即可，支持本网关导出的文件、账号数组、单个账号对象、
  cockpit tools 导出的 snake_case 写法（`access_token` / `expires_at`）以及桌面客户端的 `{"account":…,"auth":…}`。
- **拿 API 地址**：看板「设置」页顶部的「使用说明」会列出 API 地址、直连地址与应用中心入口，每行都能一键复制。
- **看用量**：看板里有占用/请求流水/积分构成等页面；积分构成直接读 WorkBuddy 的账单接口。

## 4. 数据、升级与卸载

| 用途 | 路径 |
| --- | --- |
| 数据目录（账号、设置、流水、日志、PID） | `/var/apps/workbuddy2api/var/` |
| 程序目录（升级时整体替换） | `/var/apps/workbuddy2api/target/server/` |

- `accounts/`：账号凭证与 `settings.json`（API Key、看板密码）
- `usage/`：请求流水
- `workbuddy2api.log`：服务日志（超过 5 MB 自动轮转一次）

**升级**：在应用中心/FnDepot 里升级即可，账号、密码与用量都留在数据目录里，不受影响。

**卸载**：卸载向导会问你「是否删除数据」——不删除则账号凭证、看板密码与用量流水保留，重装后还能接着用；
选择删除才会清掉数据目录。程序目录不要放自己的东西，升级会整体替换。

## 5. 常见问题

- **看板打不开 / 一直在转**：先看日志 `/var/apps/workbuddy2api/var/workbuddy2api.log`；
  再确认 `8788` 没被别的程序占用、容器/路由器防火墙放行了这个端口。
- **忘了看板密码**：改 `/var/apps/workbuddy2api/var/accounts/settings.json` 里的看板密码字段后重启应用
  （改文件前先停应用，避免被运行中的进程覆盖回去）。
- **应用中心里打开后提示没权限/空白**：确认是从**应用中心**入口进入的；如果浏览器缓存了旧页面，
  强刷一次（Ctrl/Cmd+Shift+R）。
- **源里没有我装的版本**：外部源的版本键由本源作者维护，本仓库当前提供 `1.6.19`；FPK 不入 git，
  从 GitHub Release 资产下载。
- **这个源和应用安全吗**：这是第三方自建源，源码公开在
  [ccrabit/workbuddy2api-hub](https://github.com/ccrabit/workbuddy2api-hub)，可以自己审；FnDepot 不对它背书。

## 6. 关于

- 上游作者（`maintainer`）：[ardeyouxipianyi](https://github.com/ardeyouxipianyi/workbuddy2api-hub)
- 本源发布者（`distributor`）：[ccrabit](https://github.com/ccrabit)
- 问题反馈：[Issues](https://github.com/ccrabit/workbuddy2api-hub/issues)
- 本源只包含应用 `workbuddy2api`；安装包为多架构合一包（`packages.all`）。
