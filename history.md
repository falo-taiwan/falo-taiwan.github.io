# 銀河 ERP 內訓課程：歷史課程彙整 (Class 01 & Class 02)

本文件彙整了銀河 ERP 內訓課程的前兩堂課內容、原始簡報連結與核心技術概念，供 AI (LLM) 快速檢索並理解本專案的歷史脈絡。

---

## 課程基本資訊

* **課程名稱**：企業 AI 應用與導入策略 | 從概念到落地
* **授課教師**：鄭穎臨 老師
* **上課地點**：台南市安平區育平九街49號 二樓教室

---

## Class 01：企業 AI 應用與導入策略 (完整版v1)

* **上課時間**：2026/05/12 (二) 09:00-12:00
* **原始簡報連結**：[Google Drive (完整版v1)銀河-class01](https://drive.google.com/file/d/1lXezYJhbHxRXl2o-imZDmsQZNj1z8SWF/view?usp=drive_link)
* **本地備份路徑**：`archive/class01/(完整版v1)銀河-class01.pdf`

### 核心技術與概念

#### 1. AI Agent 武器庫與協作模式
課程強調從「個人單兵作戰」轉向「Agentic 協作網路」，並對五大 AI Agent 進行了定位：
* **OpenClaw (龍蝦)**：定位為自動化執行與環境操控。能直接在本地環境執行腳本、修補環境，專為「動手做」設計。
* **Claude Cowork**：定位為協作編排與長文本理解。透過 Artifacts 功能與協作模式，協助專案經理 (PM) 共同編排 ERP 流程。
* **ChatGPT Codex**：定位為邏輯引擎與萬能接口。具備強大的多模態與邏輯推理能力，是自動化流程 (Loop) 中的「大腦」。
* **Perplexity Computer**：定位為實時研究與自動化檢索。能操作電腦進行最新 ERP 協議與技術標準的追蹤，維持系統最新狀態。
* **Hermes Agent**：作為通用型任務代理。

#### 2. Model Context Protocol (MCP) 與外部操作模式
討論了 AI 如何透過不同的接口進行環境控制：
1. **Claude**：使用 Computer Use 模式 / Chrome 外掛 (操控 / MCP)。
2. **ChatGPT**：使用 Atlas (操控 / MCP) / CodeX。
3. **Perplexity**：使用 Computer / Comet (操控 / MCP)。
4. **Smart User 自建外掛**：高度彈性且能大量節省 Token 的自製外掛。

#### 3. 專案記憶與 Markdown
* 強調使用 **Markdown (.md)** 檔案作為 AI 的「外部記憶檔」，藉此建立共通語言，大幅節省 Token 並提升程式產出品質與團隊協作效率。

#### 4. 自動化實施模式
* **AI Computer Mode**
* **AI MCP**
* **RPA (機器人流程自動化)**
* **爬蟲程式**
* **混合模式 (Hybrid Mode)**

### 相關參考連結
* IPAS AIAP 課程網站：`https://forceai0001-commits.github.io/ipas-aiap-2026/`
* IPAS AIAP 歷屆考試資源：`https://forceai0001-commits.github.io/ipas-aiap-exam/`
* Falo 台灣問卷調查：`https://falo-taiwan.github.io/survey/`
* GitHub Superpowers 工具庫：`https://github.com/obra/superpowers`
* 智慧空氣鼓棒展示 (AeroBand PocketDrum 2 Plus)：`https://www.youtube.com/shorts/7deM3U-WraI`

---

## Class 02：企業 AI 應用與導入策略 (學員版)

* **上課時間**：2026/05/22 (五) 09:00-12:00
* **原始簡報連結**：[Google Drive （學員版）銀河class02-v101.pdf](https://drive.google.com/file/d/1B8U9hmc8HIzE9y_yHlS9v_HiVp-A9A0Y/view?usp=sharing)
* **本地備份路徑**：`archive/class02/銀河class02-v101.pdf`

### 實作工具與連結
課程介紹並實作了多項基於 Falo 方法論與 AI 應用的網頁工具：
* **Falo 工具總覽**：`https://falo-taiwan.github.io/tools`
* **Gmail 寄信自動化**：`https://falo-taiwan.github.io/tools/gmail-sent/`
* **ETL 資料轉換 (CSV/Excel)**：`https://falo-taiwan.github.io/tools/etl-csv-excel/`
* **Gemini 程式碼轉 HTML**：`https://falo-taiwan.github.io/tools/gemini-code-to-html/`
* **SVG 教室座位配置工具**：`https://falo-taiwan.github.io/ai-ocr-classroom/`
* **AI OCR 視覺基準測試**：`https://falo-chinese.github.io/ai-ocr-vision-benchmark/`
* **IPAS AIAP 輔導網頁**：`https://falo-taiwan.github.io/ipas-aiap/`
* **AI OCR 專業版工具 (PRO-01)**：`https://falo-chinese.github.io/aiocr-pro01/`
* **AI 防火牆應用**：`https://falo-taiwan.github.io/ai-firewall/`

### 核心實作：PDF 轉換自修題庫 DB (Prompt Engineering)
課程核心練習之一為利用 AI 將 PDF 考卷轉換成結構化的 CSV 題庫。
* **資料欄位**：`"題號","題目","選項A","選項B","選項C","選項D","答案"`
* **提示詞規則 (Prompt Prompting)**：
  1. 每次只批次處理並輸出 10 題。
  2. 嚴格對照 PDF 原文，不跳題、不漏題、不自行新增。
  3. 若無答案則留空。
  4. 欄位皆以雙引號包覆。
  5. 最後一列加上「完成」標記。

### Classroom 資訊
* Google Classroom 課程代碼：`rtvxcb3e`

---

## Class 03：AI Agent 與 Vibe Coding 實戰及知識資產化

* **上課時間**：2026/06/07 (日)
* **核心連結**：[Class 03 課程主題導航](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/index.html)
* **本地主目錄**：`falo-taiwan/class/a01/class3/index.md`

### 核心技術與概念

#### 1. 人與 AI 的共創共生
* 探討 AI 時代的「協作與治理觀念」基礎。理解為什麼我們不是被取代，而是學習與 AI 助理、顧問、副駕駛進行高效人機協作 (HITL) 與放大個人能力。
* [共創共生觀念 (HTML)](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_coexistence.html) | [Markdown](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_coexistence.md)

#### 2. AI Agent 協同討論與即時知識工程化
* 探討「對話即生產」與動態共創筆記模式。讓 AI 在討論中即時進行結構化寫檔與決策軌跡記錄 (Logs)。
* [對話與寫檔實務 (HTML)](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_collaboration.html) | [Markdown](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_collaboration.md)

#### 3. AI Agent & Vibe Coding 工具分析與對比
* 橫向對比四大開發模式（Antigravity、Claude Cowork、ChatGPT Codex、Gemini Canvas 模式），著重探討上下文視窗、本地操作能力、Diff 區塊替換等核心指標。
* [開發工具對比 (HTML)](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/agent_tools.html) | [Markdown](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/agent_tools.md)

#### 4. AI 時代的知識資產化案例實踐 (Gemini Chrome 解鎖)
* 以「Chrome 內建 Gemini 解鎖」為案例，展示如何遵循 FALO 六層模型，將一個真實問題提煉為組織的能力包 (Capability Pack)。
* [案例實作網頁 (HTML)](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_gemini_chrome.html) | [Markdown](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_gemini_chrome.md)

#### 5. OCR 辨識策略與 HITL 人機協作實務 (台北郵局分揀案例)
* 分析台北郵件處理中心 OCR 自動分揀誤判考生成績單事件，解析辨識信賴度、例外判定邏輯與人機協作 (HITL) 審核在 ERP 電子發票與排程系統中的應用。
* [OCR 與 HITL 實務 (HTML)](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_ocr_hitl.html) | [Markdown](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_ocr_hitl.md)

#### 6. LINE 防封鎖工具與 Computer Use 模擬實務
* 解析 LINE 防封鎖工具開發歷程，展示從社群痛點出發、經由 Gemini Canvas PoC、Antigravity 高規進化，再到文件變形輸出與 Computer Use 模擬操作之完整知識工程實踐。
* [Computer Use 與防封鎖 (HTML)](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_computer_use.html) | [Markdown](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_computer_use.md)

#### 7. 學員課前提問與技術解答 (QA)
* 彙整學員提出的 12 個核心技術問題（如 API 效能、AI 命名失控、Token 分配、Docker 環境隔離、安全掃描、PWA APP 開發等）與深度解答。
* [提問解答頁 (HTML)](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_qas.html) | [Markdown](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_qas.md)

#### 8. Chrome 外掛程式載入與部署實戰教學
* 使用 FALO Instagram Video Enhancer v1.0.1 作為範例，手把手學習如何在開發者模式下部署、載入並測試 Chrome 擴充功能，包含智慧遙控器與 5 種色彩主題。
* [外掛部署與教學 (HTML)](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/ig/index.html) | [Markdown (README)](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/ig/README.md)

#### 9. Vibe Coding 實戰武器庫與地雲整合工具清單
* 盤點並分類 Class 03 核心實戰工具，涵蓋 AI 原型開發（Antigravity、Claude Code）、知識提煉（NotebookLM、Perplexity）與地雲整合實作（GAS、地端 Python 伺服器、ngrok 穿透），為 Class 04 系統整合奠定地基。
* [實戰武器庫網頁 (HTML)](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_tools.html) | [Markdown](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_tools.md)

#### 10. 從 ERP 外掛到 AI Agent
* 理清企業自動化演進六階段（人工 ➔ ERP 客製 ➔ RPA ➔ Workflow ➔ AI Agent ➔ Multi-Agent）。立足銀河 ERP 顧問簡化之 Workflow 模式（Event-Rule-Action），探討白箱架構 n8n 在 AI 治理中的全新優勢與 AI Review Workflow 新觀念。
* [從 ERP 外掛到 AI Agent 網頁 (HTML)](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_rpa_to_agent.html) | [Markdown](file:///Users/force/Google_Antigravity/attn-class/falo-taiwan/class/a01/class3/class03_rpa_to_agent.md)


