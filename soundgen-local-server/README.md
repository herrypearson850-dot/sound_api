# 本地 Soundgen 兼容服务（Python，可选）

主仓库脚本：`scripts/start-soundgen-server.mjs` 会在**仓库根目录**查找 `soundgen_server.py` 并用 `python soundgen_server.py` 启动。

## 与 Render 的关系

若你把同一套 Python 部署到公网：

1. 在 Render 创建 **Web Service**（或 Docker），暴露你实现的 HTTP 端口。
2. 在客户端通过 **`EXPO_PUBLIC_SOUNDGEN_BASE_URL`** 或统一代理里的 Soundgen 上游环境变量指向该地址（视你实际路由而定）。

本目录仅作文档占位；**请把你的 `soundgen_server.py` 及依赖放在你自己的 Python 仓库或本仓库根目录**（与现有脚本一致），Render 上指向该代码根目录部署。
