# HttpsAudio2Esp32

这是一个可直接部署到 GitHub Pages 的静态项目，用来托管拆分后的 `raw PCM` 音频分片。

当前资源位于：

- `docs/manifest.json`
- `docs/audio/Audio_1/*.raw`

建议的音频格式：

- `raw PCM`
- `16-bit signed little-endian`
- `mono`
- `24000 Hz`

## 目录结构

```text
HttpsAudio2Esp32/
  data/Audio_1/           本地原始分片
  docs/
    index.html            浏览器测试页
    manifest.json         分片清单
    audio/Audio_1/*.raw   GitHub Pages 实际托管文件
```

## 部署到 GitHub Pages

1. 在 GitHub 新建一个仓库，例如 `HttpsAudio2Esp32`
2. 把当前目录内容推到仓库
3. 进入仓库 `Settings -> Pages`
4. 在 `Build and deployment` 中选择：
   - `Source: Deploy from a branch`
   - `Branch: main`
   - `Folder: /docs`
5. 保存后等待 GitHub Pages 发布

发布后的地址一般类似：

```text
https://<你的用户名>.github.io/HttpsAudio2Esp32/
```

清单地址类似：

```text
https://<你的用户名>.github.io/HttpsAudio2Esp32/manifest.json
```

首个音频分片地址类似：

```text
https://<你的用户名>.github.io/HttpsAudio2Esp32/audio/Audio_1/Audio_001.raw
```

## 本地验证

部署完成后打开：

- `https://<你的用户名>.github.io/HttpsAudio2Esp32/`

页面可以：

- 加载 `manifest.json`
- 在浏览器中顺序播放所有 `raw PCM` 分片
- 输出调试日志

## 后续给 ESP32 使用

板端后续只需要支持：

1. 下载 `manifest.json`
2. 顺序读取 `chunks[*].file`
3. 按 `24000Hz / 16-bit / mono raw PCM` 直接送入 I2S

这样就不需要把完整大音频放进板载存储。
