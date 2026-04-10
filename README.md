# Python 服务（各自独立仓库 / Render）

路径：`c:\Users\Administrator\Desktop\Publishing\render_service\python`

本 Expo 仓库**不内置**你的 Python 源码；此处按**职责**分子目录说明部署契约，便于与 Node 代理、主应用 env 对齐。

| 子目录 | 说明 |
|--------|------|
| `audio-analyze-api/` | 你运行在 `:8000` 的 Django/FastAPI 等：`POST …/api/v1/audio/analyze`（multipart `file`），由 `node/web-api-proxy` 经 `AUDIO_API_UPSTREAM_URL` 转发 |
| `soundgen-local-server/` | 可选：仓库根目录若存在 `soundgen_server.py`，由 `npm run soundgen:local` 启动的本地声学服务；可单独打成 Docker/Render **Background Worker** 或 Web Service |

每个 Python 项目在 Render 上应是 **单独一条服务**（单独 `requirements.txt` / `Dockerfile` / `render.yaml`），不要和 Node 目录混在一个 Root Directory 里。
