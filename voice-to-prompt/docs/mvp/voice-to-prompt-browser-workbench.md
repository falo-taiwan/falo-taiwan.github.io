# Voice-to-Prompt Browser Workbench

版本：v102 (v1.02)
公開識別：Falo x Force Cheng
日期：2026/5/6
語言/地區：zh-Hant / Taiwan

## 1. 專案定位

這是一個教學展示用的 Voice-to-Prompt Workflow MVP。

它的目的不是做完整語音助理，而是讓初學者看懂：

```text
語音 / 音檔
→ 瀏覽器內轉錄
→ 手動選擇文字來源
→ AI 或規則後處理
→ Prompt Template
→ 可執行 Prompt
```

## 2. 核心邊界

這一版採瀏覽器優先：

- Web Speech API：展示零安裝、麥克風即時轉錄。
- Transformers.js Whisper：展示瀏覽器內模型，可處理上傳音檔，也可用 chunk 方式近即時轉錄。
- Chrome Built-in AI：作為地端文字後處理的優先示範選項。
- Ollama：作為本機模型 fallback。
- 本地規則：作為無模型 fallback。

公開展示頁已補入：

- 明文署名：Falo x Force Cheng
- 日期：2026/5/6
- SEO meta：description、keywords、author、creator、publisher、robots
- Social meta：Open Graph / Twitter summary
- Geo meta：Taiwan / Taipei 座標

上方「能力確定區」只負責檢測、模型下載狀態與暖身，不直接決定實際工作流程。

下方「工作區」的按鈕才是真正執行時的選擇。

## 3. 畫面結構

### 0. 能力確定區

用途：

- 檢查 Web Speech API
- 檢查 WebAssembly / WebGPU
- 檢查 Chrome Built-in AI
- 檢測 Chrome Built-in AI 的 Summarizer / Language Detector / Translator / Rewriter / Prompt API availability
- 上方工具列只做 Chrome Built-in AI 狀態檢測
- 各 Chrome Built-in AI 狀態卡才負責透過 `create({ monitor })` 觸發模型下載 / 暖身
- 清理本頁模型暫存狀態：重置本頁記錄，並嘗試清除 Transformers.js / Whisper 相關 Cache Storage 與 IndexedDB
- 檢查 MediaRecorder
- 檢測本頁曾成功下載 / 暖身的 Whisper 模型
- 預下載 / 暖身指定 Whisper 模型
- 檢查 Ollama 是否可用

### Chrome Built-in AI 可用性

這版新增 Chrome Built-in AI 的明確檢測與下載暖身流程。

重點限制：

- Chrome Built-in AI 不是只能用在 Chrome 外掛；官方文件也把它定位為網站 / Web App 可使用的瀏覽器內 AI API。
- 一般網頁能否使用，取決於 Chrome 版本、API 狀態、origin trial / flags、localhost 或 HTTPS、硬體條件、可用儲存空間與地區支援。
- 外掛環境與一般網頁環境不同。外掛 side panel 偵測到 Summarizer、Prompt 或 Translator，不代表 `file://` 或 GitHub Pages 頁面一定能拿到同樣的 `window.Summarizer`、`window.LanguageModel` 或 `window.Translator`。
- Chrome Built-in AI 實體模型由 Chrome 管理；網頁只能建立 / 釋放 session、觸發下載暖身與顯示狀態，不能直接刪除 Chrome 內部模型檔。

能力區會分別顯示：

- Translator API：目標語言不同時，用於翻譯。
- Rewriter API：用於把逐字稿整理成更清楚的文字。
- Prompt API / LanguageModel：用 prompt 方式做文字後處理。
- Summarizer API：可用來確認 Gemini Nano 類內建模型能力，但不作為此 MVP 的預設文字後處理模型。
- Language Detector API：可用來確認瀏覽器內語言偵測能力，但不作為此 MVP 的預設文字後處理模型。

狀態呈現：

- 未檢測：尚未查詢 API。
- 可下載：瀏覽器支援，但模型尚未下載。
- 下載中 / 暖身中：正在建立 session，並顯示 `downloadprogress`。
- 可用：已成功建立 session，可作為文字後處理模型。
- 不可用：此瀏覽器、flags、硬體條件、origin 或 API 版本不支援。

依據 Chrome 官方文件，Built-in AI 模型通常不是網頁自行下載檔案，而是由瀏覽器在第一次 `create()` session 時觸發模型下載；因此本 MVP 把「下載 / 暖身」放在各 API 狀態卡內，不放在上方總工具列。

### Whisper 模型可用性

本 MVP 用「本頁成功暖身紀錄」作為教學展示用的可用模型清單：

- 未下載：灰色，工作區不可選。
- 下載中 / 暖身中：顯示進度，暫時不可選。
- 已下載 / 已暖身：綠色，工作區可選。
- 失敗：提示錯誤，可重新暖身。

瀏覽器實際會使用 cache 加速模型載入，但不同瀏覽器與 Transformers.js 版本不一定能穩定讀出完整 cache 狀態，所以本頁以「成功暖身紀錄」作為可教學、可理解的 MVP 判斷。

### 1. 轉錄工作區

分成兩個清楚區塊：

#### Web Speech API 即時轉錄

特性：

- 零安裝
- 真即時
- 使用瀏覽器原生 `SpeechRecognition`
- 適合麥克風聽寫展示
- 不處理上傳音檔

#### Transformers.js Whisper 轉錄

特性：

- 使用 `@huggingface/transformers`
- 任務為 `automatic-speech-recognition`
- 可轉錄上傳音檔
- 可用 `MediaRecorder` 切 chunk 做近即時轉錄
- 模型管理區提供：
  - `Xenova/whisper-tiny`
  - `Xenova/whisper-base`
  - `Xenova/whisper-small`

MVP 建議先暖身 `Xenova/whisper-tiny` 或 `Xenova/whisper-base`。工作區只允許選擇已暖身完成的模型。

## 4. AI 後處理

使用者手動選擇來源：

- 帶入 Web Speech 文字
- 帶入 Whisper 上傳文字
- 帶入 Whisper 即時文字

再選後處理方式：

- Chrome Built-in AI
- Ollama
- 本地規則

文字後處理模型也採可用性呈現：

- Chrome Built-in AI：預設選擇，環境檢測 / 下載 / 暖身後確認是否可用。
- Ollama：檢查本機 endpoint 與模型清單後，才標示可用。
- 本地規則：永遠可用，作為 demo fallback。

目標語言預設為繁中，表示把逐字稿整理或翻譯成清楚的繁體中文。

這個設計刻意保留人工選擇，避免系統自動猜測哪段文字才是正確來源。

## 5. Prompt DB

目前內建 5 類 Prompt Template：

- 任務拆解
- 會議摘要
- 客戶需求整理
- 教材/文章發想
- 待辦事項產生

每一類都是最小模板，用來示範「整理後文字如何轉成可執行 Prompt」。

## 6. 文字框操作

所有主要文字框都提供兩個操作：

- 清除
- 複製到剪貼簿

包含：

- Web Speech 輸出
- Whisper 上傳檔輸出
- Whisper 近即時輸出
- 待處理原始文字
- 修飾後文字
- 最終 Prompt

## 7. 教學重點

這個頁面可以用來教三個概念：

1. ASR 是把聲音變文字，不等於 AI 助理。
2. 文字後處理可以和 ASR 分工，不必讓同一模型包全部。
3. Prompt Template 是最後一層結構化輸出，不是前面轉錄模型的責任。

## 8. 目前檔案

- 主工作台：`content/dish-assets/html/voice-to-prompt-mvp.html`
- Markdown 說明：`docs/mvp/voice-to-prompt-browser-workbench.md`
- Single-file HTML 說明：`content/dish-assets/html/voice-to-prompt-browser-workbench-note.html`
