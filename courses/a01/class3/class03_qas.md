# 主題七：學員課前提問與技術解答 (QA) (class03_qas.md)

本文件整理了學員在 Class 03 期間提出的 12 個核心技術與專案開發疑問，並由 AI (Antigravity) 提供系統化的專業解答，作為知識庫儲存以供 AI 檢索。

---

## Q1. API 效能要怎麼寫比較快? 架構說明

### 💡 核心答覆
API 的效能瓶頸通常在於 **I/O 阻塞（特別是資料庫查詢）**。要寫出高效能 API，需遵循以下架構與優化原則：

1. **資料庫優化（80% 效能來源）**：
   * **索引 (Index)**：針對常出現在 `WHERE`、`JOIN`、`ORDER BY` 的欄位建立索引。
   * **避免 N+1 查詢**：多表關聯時，使用 `JOIN` 或 Eager Loading 一次查出，不要在迴圈中重複查詢資料庫。
   * **連線池 (Connection Pool)**：重用資料庫連線，避免每次請求都重新 Handshake。
2. **快取機制 (Cache)**：
   * 將不常變動但常讀取的資料（如系統參數、下拉選單、權限設定）存入 **Redis**。
3. **非同步與佇列 (Message Queue)**：
   * 寄信、產報表等耗時工作，應丟入佇列（如 BullMQ / RabbitMQ）由背景 Worker 處理，API 立刻回傳 `202 Accepted`。
4. **非阻塞事件驅動架構**：
   * 使用 Go、Node.js (V8) 或 FastAPI 等高併發框架，適合處理大量的網路 I/O。

### 📊 高效能 API 典型架構
`Client -> Load Balancer (Nginx) -> API Gateway -> API Servers -> Redis (快取) / MySQL (資料庫) / MQ (訊息佇列) -> Background Worker`

---

## Q2. AI 可以自己創建資料表與欄位名稱，但那是他的邏輯，系統變大後真的能有效管理嗎?

### 💡 核心答覆
**完全不行。如果放任 AI 自由設計，系統變大後必然會失控。**

AI 缺乏全域視角，它在不同模組可能會把同一概念命名為 `members`、`user_info` 或 `member_table`，甚至選用不一致的資料型態（`INT` vs `BIGINT`，`VARCHAR(50)` vs `TEXT`）。

### 🛡️ 管理對策
1. **鎖定 Schema（Schema-First）**：
   * 系統的 DDL (Data Definition Language) 必須由人類工程師（架構師/DBA）審查並簽核。
   * 提供 AI 現有的 `schema.sql`，並下達指令：「**你只能使用這些既有的資料表，未經批准，禁止擅自修改結構或新增欄位**」。
2. **制定命名契約 (Naming Convention)**：
   * 明定全域規則（例如：一律用 `snake_case`、主鍵必為 `id` 且型態為 `UUID` 或 `BIGINT AUTO_INCREMENT`、時間欄位統一用 `created_at` 等）。
3. **資料字典 (Data Dictionary)**：
   * 維護一份欄位對照字典，讓 AI 與開發團隊遵循統一的業務語意（Ubiquitous Language）。

---

## Q3. Codex 就算付費也有用量限制，要怎麼有效分配？

### 💡 核心答覆
AI 限制通常為 **Token 限制（Context Window）** 與 **速率限制（RPM/TPM）**。高效分配策略如下：

1. **精準餵食（減少無效 Context）**：
   * 不要一次把整個專案的程式碼塞給 AI。
   * 只餵入與目前工作相關的檔案。如需調用外部 API，只給 API 定義（Interface/Type），不給其實作細節。
2. **任務原子化（Task Chunking）**：
   * 將大需求拆解為單一職責的小函數。
   * 例如：不要問「幫我寫出整個購物車系統」，而是問「請幫我寫一個計算購物車內『特定折價券扣抵額』的 Function」。
3. **大小模型分流 (Hybrid LLM Pipeline)**：
   * **日常小事**：代碼補全（Inline Completion）、修復小語法錯誤，交給本地輕量模型（如 Ollama 跑 Llama 3 或 Gemini Flash）。
   * **關鍵大事**：架構重構、複雜邏輯設計、安全審查，才交給 Codex、Gemini Pro 或 Claude 3.5 Sonnet 等付費大型模型。

---

## Q4. Antigravity 2.0 真的不能中文介面嗎? 他對話框命名都英文? 我還要自己重新命名才容易找。

### 💡 核心答覆
Antigravity 2.0 作為 Google DeepMind 開發的進階 AI 寫碼系統，其底層與介面元件（如 Chat history title 產生器）為了相容於各國開發者的 OS 環境與 Git 相容性，預設會使用英文命名。

### 💡 實務技巧
1. **中文溝通無阻**：它完全能理解您的繁體中文指令並以繁體中文回答。
2. **主動指令命名**：在開啟對話的第一步，可以直接打上：「*請用繁體中文回答，並在本次對話的標題或開頭，為我生成一個簡短的中文主題名稱，例如：『修復登入邏輯』*」，這能幫您更方便地在對話框列表中快速識別。

---

## Q5. 各開發工具的優缺點列示，目前主流好用的開發工具?

### 💡 核心答覆
目前開發界已進入 AI 原生編輯器與傳統 IDE 插件共存的時代：

* **Cursor (AI 原生編輯器)**：
  * *優點*：與 AI 結合極深，Composer 功能能同時修改多個檔案，Tab 自動補全強大。
  * *缺點*：需額外訂閱，屬閉源修改版 VS Code，有資安稽核疑慮。
* **Windsurf (AI 原生編輯器)**：
  * *優點*：具備強大 Agent 代理模式（能自己跑指令、除錯、測試），Flow 體驗流暢。
  * *缺點*：社群資源與生態系較新，需付費。
* **VS Code + AI 插件 (如 GitHub Copilot, Gemini in IDE)**：
  * *優點*：完全免費（編輯器本體），生態系最龐大，企業資安控管首選。
  * *缺點*：AI 功能以側邊欄或補全視窗單點式協作，缺乏多檔案協同修改的體驗不如 Cursor/Windsurf。
* **JetBrains 系列 (IntelliJ, WebStorm)**：
  * *優點*：傳統靜態語法分析與安全重構（Refactoring）地表最強。
  * *缺點*：耗記憶體、開專案慢、費用高。

---

## Q6. 資深工程師是如何看待這些工具? 他們運用方式跟我們有一樣嗎?

### 💡 核心答覆
資深工程師將 AI 定位為**「極有效率的助理（Super Intern）」**而非「替代者」。他們的用法在於「**決策在人，執行在 AI**」：

1. **思維差異**：
   * *初學者*：「請幫我寫一個登入系統。」（直接複製貼上 AI 的程式碼，常不知其所以然）。
   * *資深者*：先規劃好登入流程的安全標準（JWT, Refresh Token），寫好 Interface 定義，然後要求 AI：「請幫我實作這個 Interface，並寫出能應對邊界異常（如資料庫連線中斷）的單元測試。」
2. **AI 代勞髒活 (Boilerplate)**：
   * 拿 AI 來產生繁瑣重複的程式（如 DTO 轉換、資料驗證、設定檔）。
3. **驗證與測試**：
   * 寫完程式後，把代碼丟給 AI 扮演「黑客」：「請幫我審查這段程式碼是否有 XSS 或 SQL Injection 漏洞？請提供 5 個能讓它 Crash 的極端測試資料。」

---

## Q7. Codex 編寫程式很強但美術直；Gemini Canvas 美術不錯但程式架構不嚴謹且不受控。要怎麼搭配使用?

### 💡 核心答覆
這需要實施「**視覺與邏輯分流工作流**」：

```
[Gemini Canvas] 產出 CSS/設計概念/排版 -> [人工過濾與抽離] -> [Antigravity/Codex] 模組化與架構化 -> 最終嚴謹代碼
```

1. **視覺設計期（Gemini Canvas / Figma）**：
   * 用 Gemini Canvas 來生成美觀的網頁佈局、色彩配對（使用 CSS Variables）、動畫效果與 RWD 樣式。
2. **邏輯工程化（Antigravity / Codex）**：
   * 將 Canvas 產生的 HTML/CSS 複製到 AI 編輯器中，對 Antigravity 下指令：
     > 「這是我在 Canvas 產生的前端靜態畫面。請幫我將這段 HTML/CSS 進行模組化，將邏輯（JavaScript）與樣式分離，並改為符合原生 ES Modules 的架構，確保程式碼結構嚴謹。」
3. **串接與安全檢查**：
   * 最後由 Antigravity / Codex 負責資料驗證（Validation）、錯誤處理（Error Handling）與 API 的整合串接。

---

## Q8. 我們電腦開發環境要怎麼做才是乾淨的? 移動到其他電腦安裝才能確保我們軟體沒問題?

### 💡 核心答覆
要確保「在我的電腦可以跑，在其他台也一定可以」，有三大核心工具：

1. **容器化 (Docker) — 黃金標準**：
   * 將資料庫 (MySQL/PostgreSQL/Redis) 與後端環境用 Docker 封裝。
   * 新電腦只需安裝 Docker，執行 `docker compose up -d` 便可一秒複製一模一樣的執行環境。
2. **版本管理器 (Version Managers)**：
   * 絕不在 OS 全域直接安裝 Node.js 或 Python。
   * 使用 `nvm` / `fnm` (Node) 或 `pyenv` (Python) 在不同專案間隔離執行版本。
3. **CI/CD（持續整合/部署）**：
   * 將專案上傳至 Git，並配置 GitHub Actions 或 GitLab CI。
   * 每次 Push 程式碼時，雲端的乾淨虛擬主機（Runner）會自動下載相依套件、建置專案並跑測試。**只要 CI 通過，就代表該專案的建置環境是乾淨、可移植的。**

---

## Q9. 我要怎麼做程式碼掃描? 檢視邏輯、資安漏洞 (例如: sql injection) 相關問題?

### 💡 核心答覆
必須建立**自動化靜態代碼分析 (SAST)** 機制，並遵循安全開發守則：

1. **自動掃描工具 (SAST)**：
   * **SonarQube / SonarCloud**：檢查代碼品質、壞味道（Code Smells）、邏輯錯誤與一般漏洞。
   * **Snyk**：掃描專案第三方套件（dependencies）是否有已知的漏洞。
   * **GitHub Advanced Security (CodeQL)**：每次 PR 時自動語意掃描 SQL 注入與 XSS。
2. **如何防範 SQL Injection（結構性做法）**：
   * **參數化查詢（Prepared Statements）**：嚴禁直接拼接字串組成 SQL 指令。
   * **使用 ORM**：使用 Prisma、Sequelize 等現代 ORM 工具，其底層已預設採用參數化查詢，阻絕 SQL 注入。
3. **語法與邏輯檢查 (Linter)**：
   * 專案內必須設定 `ESLint`（程式碼靜態語法分析）與 `Prettier`（格式化），在開發當下就將潛在邏輯錯誤（如未定義的變數、Null 指標異常）消滅。

---

## Q10. 一開始指定 HTML5+CSS+JS 開發，系統變大後 AI 會不會自行亂加其他程式語言？怎麼讓他保證順？移交工程師難度變很高？

### 💡 核心答覆
**會。如果沒有明確限制，AI 很容易因為網路資料的多樣性，在遇到難題時偷偷引入 React/Vue 的語法，或是 TypeScript、Python 等。**

### 🛡️ 解決方案
1. **設定 `.clinerules` / `.cursorrules`**：
   * 在專案根目錄建立規則檔，限制 AI：
     > 「本專案僅允許使用原生 HTML5、CSS3 與原生 ES Modules JavaScript。禁止使用任何建置工具 (Vite, Webpack) 或外部編譯語系 (TypeScript)。所有 JS 模組化必須使用瀏覽器原生的 import/export。」
2. **模組化分層架構（Vanilla JS 的系統化寫法）**：
   * 即使只用原生 JS，也要有清晰的目錄結構：
     * `/css` - 存放 CSS 變數與元件樣式。
     * `/js` - 拆分為 `main.js` (入口)、`/services` (專門處理 API 請求)、`/components` (UI 元件邏輯)。
3. **人類的 Code Review 控制**：
   * 工程師在接受 AI 的變更前，必須透過 `git diff` 仔細審查，確保沒有不屬於 Vanilla JS 的套件被偷偷打包進來。

---

## Q11. 日後維護一定會陸續增加很多功能，到底要怎麼樣有系統性維護??

### 💡 核心答覆
系統性維護不能光靠口頭約定，必須依靠 **Git 分支管理、自動化測試與架構重構**：

1. **Git 分支策略（Branching Strategy）**：
   * `main`：永遠保持穩定、可部署的生產環境狀態。
   * `dev`：開發整合測試環境。
   * `feature/xxx`：每次要加新功能，必須切新分支，經 Review 測試後才能併入 `dev`。
2. **撰寫單元測試 (Unit Tests)**：
   * 當功能變多，只靠人工測試絕對會漏。
   * 寫好單元測試（如使用 Vitest 或 Jest），在每次合併程式前自動執行。確保新增 A 功能時，沒有改壞既有的 B 功能。
3. **定期重構與還技術債**：
   * 當某個 JS 檔超過 500 行，就應強制要求 AI：「請幫我把這個模組重構成多個職責單一的小檔案」。

---

## Q12. 我們開發 APP 對於我們銀河軟體真的好維護嗎? 上平台驗證與付費？手機規格、不同 OS 的受限程度有多高?

### 💡 核心答覆
針對於去識別化的**銀河 ERP** 這種企業內部 / 協同工作為主的系統，**非常不推薦開發「原生 App（Native App）」**，因為這會帶來極高的維護與平台上架負擔。

### 🚨 App 開發痛點
* **平台年費與審查**：Apple App Store 年費 99 美元，Google Play 一次性 25 美元。每一次修改 App 都需要送審（Apple 通常需 1-3 天），且 App 內如果包含交易，會被平台強行抽取 15% - 30% 的「蘋果/安卓稅」。
* **OS 與手機規格碎片化**：Android 手機成千上萬種螢幕大小，且各家（三星、小米）對後台背景處理與相機的權限控管大相漸庭，維護成本是 Web 的三倍以上。

### 💡 推薦替代路徑

#### 方案 A：PWA (Progressive Web App) —— 首選（低成本、極好維護）
* PWA 本質上是高性能的響應式網頁，但用戶能「加入手機主畫面」像一般 App 一樣開啟，並支援手機離線存取與推播通知。
* **優點**：**完全免上架、免審查、免年費**。後端程式碼一更新，用戶重新打開即是最新版，直接繞過 App Store 的審查枷鎖。

#### 方案 B：跨平台框架 (Flutter 或 React Native / Expo) —— 若一定要上架
* 若因客戶要求一定要上 App Store，請用單一語言編譯雙系統的框架，並搭配 **Expo** 的 OTA (Over-The-Air) 熱更新技術，可以在不送審的情況下更新 App 內的 UI 邏輯。
