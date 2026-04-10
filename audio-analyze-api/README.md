# 音频分析上游（Python / Django）

本仓库**不包含**你运行在 `http://127.0.0.1:8000/api/v1/audio/analyze` 的实现；它只是 **Node 统一代理**（`render_service/node/web-api-proxy`）的转发目标。

## 与主项目的关系

- 代理读取环境变量 **`AUDIO_API_UPSTREAM_URL`**，将 `POST …/proxy/audio-analyze` 的 body（含 multipart 与客户端一致）转发到该 URL。
- 客户端优先使用 **`EXPO_PUBLIC_AUDIO_API_URL`**（指向代理路径 `/proxy/audio-analyze`），逻辑见 `services/soundgen-client.ts` 的 `getSoundgenAnalyzeUrl()`。

## 部署到 Render

1. 将你的 Django/FastAPI 项目作为 **Web Service** 或 **Docker** 部署（需能接收 **POST**、`multipart/form-data` 字段名与现网一致，一般为 `file`）。
2. 部署完成后得到公网 URL，例如 `https://dog-audio-xxxx.onrender.com`。
3. 在 **代理服务** 的环境变量中设置：

```text
AUDIO_API_UPSTREAM_URL=https://dog-audio-xxxx.onrender.com/api/v1/audio/analyze
```

（路径以你真实路由为准。）

4. 主应用 `.env` 仍只改 **`EXPO_PUBLIC_WEB_API_PROXY`** 与 **`EXPO_PUBLIC_AUDIO_API_URL`**（指向代理），**不要**把 `AUDIO_API_UPSTREAM_URL` 写进 Expo（该变量仅服务端代理使用）。

## 本地

保持现有：

```text
AUDIO_API_UPSTREAM_URL=http://127.0.0.1:8000/api/v1/audio/analyze
```

并确保 Django 在 8000 监听。
