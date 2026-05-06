# Voice-to-Prompt PWA Lite 部署說明

版本：v102 (v1.02)  
標注：Falo x Force Cheng｜2026/5/6

## 專案定位

這份 PWA Lite 是 Voice-to-Prompt 的最小可安裝版本。

它的核心功能只有一個：

```text
開啟麥克風
→ Web Speech API 即時轉錄
→ 輸出到文字框
→ 清除 / 複製到剪貼簿
```

它不是完整語音系統，也不是 Chrome Extension；PWA 不會自動解鎖 Chrome Built-in AI 的 Prompt API 或 Rewriter API。

## 公開網址

- PWA 小工具：<https://falo-taiwan.github.io/voice-to-prompt/pwa/>
- PWA 部署案例文件：<https://falo-taiwan.github.io/voice-to-prompt/pwa/deployment-note.html>
- Voice-to-Prompt 主頁：<https://falo-taiwan.github.io/voice-to-prompt/>

## 檔案結構

```text
voice-to-prompt/
├── index.html
├── pwa/
│   ├── index.html
│   ├── deployment-note.html
│   ├── manifest.webmanifest
│   ├── sw.js
│   └── icon.svg
└── docs/
    └── mvp/
        ├── voice-to-prompt-browser-workbench.md
        └── voice-to-prompt-pwa-deployment.md
```

## PWA 三件事

1. `pwa/index.html`
   - PWA 小工具本體。
   - 包含 Web Speech API、安裝提示、Service Worker 註冊。

2. `pwa/manifest.webmanifest`
   - 告訴瀏覽器 App 名稱、啟動路徑、scope、display、theme color 與 icon。

3. `pwa/sw.js`
   - Service Worker。
   - 負責快取 PWA 靜態檔案，提供更像本地 App 的體驗。

## 教學邊界

- PWA 是可安裝的 Web App。
- PWA 不是 Chrome Extension。
- PWA 不保證 Built-in AI 的 `LanguageModel` / `Rewriter` 可用。
- 本案例把核心放在 Web Speech API，因為它最適合做零安裝即時轉錄展示。

## 驗證清單

- 開啟 PWA URL。
- 確認可看到「安裝此 PWA」。
- 確認可看到「開始轉錄 / 停止 / 清除 / 複製到剪貼簿」。
- DevTools Application 可看到 manifest。
- DevTools Application 可看到 service worker。
- 可從 Chrome / Edge 安裝成 App。

