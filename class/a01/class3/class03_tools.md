# 主題九：Vibe Coding 實戰武器庫與地雲整合工具清單 (class03_tools.md)

本文件盤點並詳細解析 Class 03 核心實戰教學工具與核心方法論，做為學員進行 Vibe Coding、地雲整合與 AI 協同開發時的「武器指南」，為 Class 04 的系統整合打下深厚的技術地基。

> **版權所有與智財防禦**：`Falo x Force Cheng 2026/6/8`

---

## 1. AI 程式開發與原型代理 (Coding & Prototyping)

這組工具用於快速生成代碼、設計前端 UI 原型以及進行地端程式庫的直接操作與重構：

### A. Codex / Antigravity (主動式 AI 代理)
* **定位**：地端自動寫檔、編譯與終端操作代理人。
* **開發技巧與實務重點**：
  * **主動決策閉環**：掌握規劃（Plan）、任務拆解（Task）與驗收（Verify）的自動化三部曲。
  * **精確檔案修改**：避免頻繁重新生成整份長檔案，應命令 AI 善用 `replace_file_content` 與 `multi_replace_file_content` 進行精準的 Diff 局部修改，大幅節省 Token 並降低出錯率。
  * **環境掌控能力**：利用本地 terminal 控制能力執行編譯與測試，即時修補環境。

### B. Gemini Canvas 模式 (常見困擾與解法)
* **定位**：網頁端雙向側邊欄編輯與文案編排。
* **困擾與解法分析**：
  * **困擾 1：對話框命名均為英文，專案多了之後難以檢索與管理**。
    * *解法*：在對話開始時，以系統提示詞（System Instructions）明確規定對話框格式；或者在生成程式碼後，立即手動將對話框重新命名為包含「中文模組與功能名稱」的標籤（例如：`[Class 03-Topic 08] Chrome外掛實作`）。
  * **困擾 2：AI 思考過程為英文，回覆的註解也是英文，對非英語系學員造成負擔**。
    * *解法*：在對話一開頭注入 Grounding Prompt，強制要求：「**後續所有計畫書、思考過程與代碼註解，均必須以繁體中文 (zh-TW) 進行與撰寫**」。若是對英文吃力，亦可直接使用 ChatGPT Codex 或 Claude Code 做為轉譯中介。
  * **困擾 3：程式碼調整時容易整檔覆寫或無法精準控制**。
    * *解法*：善用 Canvas 的側邊欄雙向編輯器，選取特定行數進行行內修改 (Inline Edit)，避免將大段 code 丟回對話框。

### C. Claude Code (終端 CLI 代理) & Claude Fable 5
* **定位**：終端機 CLI 開發代理人與最新旗艦大模型。
* **開發技巧**：
  * **最新進展**：搭配 Anthropic 最新發布的 [Claude Fable 5](https://tw.stock.yahoo.com/news/anthropic%E5%85%AC%E9%96%8B%E6%9C%80%E5%BC%B7ai%E6%A8%A1%E5%9E%8B-claude-fable-5%E7%9E%84%E6%BA%96%E5%B7%A5%E7%A8%8B%E8%88%87%E7%A7%91%E7%A0%94%E5%B8%82%E5%A0%B4-025700532.html)（首度向企業公開 Mythos 級技術），在軟體開發、科學研究與因果推理上取得爆炸性突破。Stripe 實測顯示原本需數月的工程專案，利用 Fable 5 能在數天內完成初步建置與驗證。
  * **實務重點**：直接在本地終端機以對話方式命令 AI 進行跨檔案重構、執行單元測試，並自動生成規範的 Git Commit，大幅加速 Vibe Coding 的閉環。

---

## 2. 雙軌文檔策略與部署 Prompt (Doc Strategy & Deployment)

### A. md / html 策略 (AI 與人類的雙軌並行)
為了同時滿足「AI 高效檢索」與「人類視覺享受」，本課程全面採用雙軌文件架構：
* **AI 專用文件 (.md)**：
  * *目的*：做為 AI Agent 的**外部記憶體 (External Memory)**。
  * *重點*：摒棄冗餘的裝飾性 HTML/CSS，以結構化的 Markdown 語法精確記錄專案結構、變更日誌 (`logs.md`) 與規則，大幅節省 AI 的 Token 消耗，並避免 AI 產生幻覺。
* **人類專用網頁 (.html)**：
  * *目的*：做為人類學員學習的精美講義。
  * *重點*：採用 Glassmorphism (毛玻璃風格)、響應式設計 (RWD)、Outfit/Inter 字型與亮暗色主題切換 (Style Switcher)，提供 wow-effect 頂級視覺體驗。

### B. 本機與 GitHub Pages 部署的 Prompt 策略
* **本機測試 Prompt**：
  * *策略*：在引導 AI 開發本地網頁時，Prompt 必須要求使用本地路徑（如絕對路徑 `file:///Users/force/` 或相對路徑 `../../../../`），並且使用 `localStorage` 作為 `chrome.storage.sync` 的降級備用適配（如 Topic 08 的 Chrome 外掛本地測試頁 `mock_instagram.html`）。
* **GitHub Pages 部署 Prompt**：
  * *策略*：當專案準備 push 上線時，Prompt 必須指示 AI 執行連結轉換（例如將連結的 `../../../../` 統一替換為相對於 GitHub Pages 根目錄的 `../../../`），並在頁面中注入防偽浮水印（`Falo x Force Cheng 2026/6/8`）以及 GEO/SEO 後設標記（LD-JSON 結構化數據），以便 AI 搜尋引擎檢索（Generative Engine Optimization, GEO）。

---

## 3. 地雲整合與通信橋樑 (Integration & Bridging)

這組工具用於連接前端網頁、雲端服務以及地端作業系統，實現完整的前後端數據通信：

### A. 地端 Server (Python 呼叫與 CLI 控制)
* **定位**：本地 Full-Stack 自動化控制架構。
* **開發技巧與實務重點**：
  * **前後端分離通訊**：前端使用 HTML + Vanilla JS 提供精美控制按鈕，當使用者點擊時，利用 JavaScript 的 `fetch()` API 向本地運行的 Python 伺服器（如 Flask/FastAPI 運作於 `http://localhost:5000`）發送 HTTP 請求。
  * **地端執行**：Python 接收到請求後，調用 `subprocess` 執行本機的 shell 指令、進行大宗檔案批次命名、或是呼叫本地 AI OCR 引擎進行分揀，最後將結果回傳給網頁顯示，完美融合網頁視覺與地端操作。

### B. Google Apps Script (GAS) 範例與 HTML 對接
* **定位**：輕量級雲端 Serverless 後端。
* **開發技巧與實務重點**：
  * **零代價地雲對接**：前端 HTML 可以直接發送 HTTP POST/GET 請求到 GAS 部署好的 Web App 網址（透過 `doPost(e)` 或 `doGet(e)` 處理函數）。
  * **GAS 範例應用**：
    * *自動寫入試算表*：網頁前端發送含有表單 JSON 的 Fetch 請求，GAS 接收後使用 `SpreadsheetApp.openById().appendRow()` 將數據追加寫入 Google Sheet。
    * *自動寄信與排程*：串接 `MailApp.sendEmail()` 自動寄送通知信，或使用 `CalendarApp.createEvent()` 自動新增行事曆，無需架設複雜的地端伺服器與資料庫即可完成地雲對接。

### C. ngrok / LocalTunnel (穿透調試)
* **定位**：地端測試與外部 Webhook 的公網橋樑。
* **實務重點**：
  * 將地端運行的本地埠（如 `http://localhost:5000`）映射為公網可存取的 HTTPS 網址。
  * 在調試 LINE Bot、Slack Bot 或接收外部 ERP 系統的即時 Webhook 通知時，不需要部署到雲端，在本地即可完成即時中斷點除錯。
