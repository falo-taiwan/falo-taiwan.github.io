# Class03 教學指引：Chrome Extension 填單助手控制實戰

> [!NOTE]
> **作者**：Falo x Force Cheng  
> **發佈日期**：2026/06/08  
> **專案定位**：這堂課的重點是帶領學員開發出一個完整的 Chrome 側邊欄外掛，實現網頁 DOM 節點的讀取與自動填寫，並深入理解瀏覽器擴充功能與網頁之間的雙向通訊與控制機制。

---

## 🎨 課程核心觀念與金句

在進入任何技術實作前，請務必先向學員揭露這套「網頁 DOM 節點控制權」的運作機制。

> [!TIP]
> **Force 老師教學金句**：
> - **寫入網頁 (Write)**：外掛側邊欄發送指令與數據，注入網頁的 content.js 接收並將數值填入對應的 DOM 輸入框。
> - **擷取資料 (Read)**：當外掛點擊擷取，網頁的 content.js 讀取網頁 DOM 欄位值並打包回傳，回填至外掛側邊欄中。

### 🗺️ 控制運作三部曲
1. **傳統手動操作**：人透過滑鼠點擊網頁、手動複製與輸入。
2. **單向控制**：外掛僅能單向寫入資料 (Write DOM) 或是單向擷取網頁內容 (Read DOM)。
3. **雙向控制與資料閉環**：外掛同時實現讀、寫、隨機產生、一鍵清空，並能匯出/匯入 CSV 備份，與網頁進行實時雙向通訊，形成完整的自動化流程。

---

## 📁 專案檔案結構說明

本實作案例採用 **FALO 離線點擊即用（CORS Bypass）** 與 **語意化命名** 規範，結構如下：

- 📝 [index.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/index.html) —— **教學概念導讀首頁**。包含 Force 教學金句、外掛雙向控制觀念、實戰 Prompt 指南，以及實體外掛資源下載連結。
- 🧪 [erp.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/erp.html) —— **實體外掛測試網頁**。提供採購單號、產品代碼、進貨數量、產品效期與進貨部門等欄位，具備欄位檢核、儲存入庫與 CSV 下載等功能。
- 🔌 [chrome-extension/](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/) —— **實體 Chrome 外掛代碼**。包含 manifest.json、background.js、sidepanel.html、sidepanel.js、content.js、content.css 等，學員可真正載入 Chrome 瀏覽器操作。

---

## 🚀 Class03 現場演示 (Showcase) 步驟指南

Force 老師在課堂上可透過以下步驟進行演示：

### 課前暖身：體驗 FALO Instagram Video Enhancer 外掛

在正式進入 ERP 表單自動化演化前，先帶領學員體驗初階的 Chrome 外掛功能，建立基本體感：
1. 讓學員在 Chrome 瀏覽器開啟 `chrome://extensions`「開發者模式」，點擊「載入未封裝項目」，選取本機暖身專案路徑：`ig-video-enhancer-extension`。
2. 導引學員至 Instagram 影片，體驗外掛如何將「自訂影片進度條、音量控制、播放速度選單、快速鍵」直接注入到 IG 中。
3. **觀念轉折**：向學員引導：「這個外掛改善了我們看影片的體驗。那如果我們要自動化完成企業內無聊的 ERP 填單報表呢？這就進到我們的主題 —— 網頁填單助手外掛。」

---

### 步驟一：載入外掛並打開 ERP 測試頁

1. 打開 Chrome 瀏覽器的「擴充功能管理頁面」 (`chrome://extensions`)，開啟右上角 **「開發者模式」**。
2. 點擊 **「載入未封裝項目」**，選取專案目錄中的 [chrome-extension/](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/) 資料夾。
3. 開啟 [erp.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/erp.html)。
4. 點擊 Chrome 工具列的 **FALO ERP Form Helper** 外掛圖示，開啟右側 side panel。

---

### 步驟二：演示外掛的雙向控制功能

1. **隨機產生資料**：在側邊欄點選「隨機產生」，側邊欄欄位自動生成測試數據（單號、產品、數量、效期、部門）。
2. **一鍵全填入**：點擊「一鍵全填入」，外掛將數據發送至 content.js，寫入網頁對應 DOM 輸入框（欄位黃色閃爍提示填值成功）。
3. **網頁手動填寫 ➔ 一鍵全擷取**：在網頁上隨手修改或輸入資料，點擊側邊欄的「一鍵全擷取」，外掛會讀取網頁 DOM 欄位值並同步回外掛欄位。
4. **一鍵清空**：點擊「清空表單」，外掛與網頁欄位同時清空。
5. **CSV 備份與還原**：在側邊欄填入資料後點擊「匯出 CSV」下載備份；清空後，點擊「匯入 CSV」選取剛才的檔案，資料立刻回填至外掛。

> [!IMPORTANT]
> **引導思考**：這時候請問學員：「如果我們明天把網頁上的採購單號輸入框的 `id="po-number"` 改成 `id="po-input"`，這個外掛還動得起來嗎？」➔ 答案是「不行，Selector 找不到，外掛寫入或擷取就會失效！」這就是基於 DOM 操作的網頁自動化之核心特徵。

---

## ⚡ 實戰 Prompt 演化對照表

本課程設計了三套 Prompt 來呈現從一般大眾 (V1.1) 到進階技術 (V1.2) 以及終極完整功能 (V1.5) 的思維深度：

### 💬 V1.1 基礎口語意圖 Prompt (V1-v1)
> 我想要寫一個 Chrome 外掛，當我進入 ERP 網頁時，可以自動幫我把所有的輸入框偵測出來，在必填欄位旁邊加上高亮標示，並且加一個按鈕讓我點一下就能把測試資料填進去。

### ⚡ V1.2 進階技術控制 Prompt (V1-v2)
> 請建立一個 Manifest V3 規格的 Chrome 外掛。
> 編寫 content.js，在網頁加載時以 document.querySelectorAll 篩選所有未隱藏的 input, select, textarea。
> 在 required 的欄位加上 glows-pink 的 CSS border highlighters。
> 在網頁右上角動態 inject 一個玻璃質感的 sidebar 面板，列出偵測到的所有欄位標籤與其唯一 CSS selector，並提供 'Focus' 與 'Smart Fill' 觸發事件。

### 🚀 V1.5 終極完整功能 Prompt (V1-v3)
> 請複製以下結構化提示詞，並直接貼給 AI 編輯器或 Agent 終端機，它將會自動讀取並解析線上網頁結構，在你的工作區生成整個 Chrome 外掛：
> (Prompt 內容包含 Manifest V3 側邊欄配置、background.js 開啟側邊欄、sidepanel.html 控制項、sidepanel.js 跨分頁通訊/CSV匯入匯出/遠端遙控，以及 content.js 的原生 DOM 讀寫與事件派遣、黃色填值閃爍視覺反饋)

---

## 📖 V1 擴充功能分檔逐行教學指引 (逐檔剖析)

為了讓您在課堂上面對學員時，能夠將外掛目錄中的 **6 個檔案** 當作教材順暢講授，以下為您整理各檔案的「核心目的」與「逐行解析教案」：

### 📄 1. 身份宣告檔：[manifest.json](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/manifest.json)
*   **教學目標**：理解 Manifest V3 擴充功能的配置規範。
*   **核心配置解析**：
    - `"manifest_version": 3`：告訴瀏覽器這使用的是現代 V3 規範（V2 已廢棄）。
    - `"background": { "service_worker": "background.js" }`：註冊後台背景線程，負責監聽外掛級別事件。
    - `"side_panel": { "default_path": "sidepanel.html" }`：宣告我們的外掛是「側邊欄」形式，並指定其預設畫面。
    - `"permissions": ["activeTab", "sidePanel"]`：要求安全權限，`activeTab` 代表僅允許讀寫當前開啟的分頁，`sidePanel` 允許使用側邊欄 API。
    - `"content_scripts": [...]`：定義「當使用者打開任何網頁時，自動將 `content.js` 與 `content.css` 注入該網頁」。

---

### 📄 2. 背景服務：[background.js](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/background.js)
*   **教學目標**：理解事件驅動的背景處理（Event-driven Service Worker）。
*   **核心代碼解析**：
    - `chrome.sidePanel.setPanelBehavior({ openPanelOnActionClick: true })`：這行程式碼非常關鍵！它告訴瀏覽器：「當使用者用滑鼠點擊瀏覽器右上角的外掛圖示時，請直接滑出我們的 `sidepanel.html` 側邊欄，而不是彈出傳統的小 Popup 視窗。」

---

### 📄 3. 側邊欄介面：[sidepanel.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/sidepanel.html)
*   **教學目標**：外掛側邊欄的視覺結構，使用純 HTML。
*   **核心內容解析**：
    - 提供了與 ERP 表單對應的 5 個輸入控制項（採購單號、產品代碼、進貨部門下拉、進貨數量、產品效期）與系統流水號的唯讀框。
    - 每個控制項旁皆有獨立的「填入」與「擷取」按鈕。
    - 提供了「隨機產生資料」、「清空表單」、「匯出 CSV」、「匯入 CSV」、「一鍵全填入」、「一鍵全擷取」、「檢核表單」、「確認入庫」等豐富的功能按鈕。

---

### 📄 4. 側邊欄控制：[sidepanel.js](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/sidepanel.js)
*   **教學目標**：掌握**「Context 隔離宇宙」**與**「跨宇宙通訊 (Message Passing)」**。
*   **核心代碼解析**：
    - `chrome.tabs.query({ active: true, currentWindow: true }, (tabs) => { ... })`：這是 Chrome 擴充功能最常用的 API，用來查詢當前使用者的 Active 分頁資訊。
    - `chrome.tabs.sendMessage(...)`：向 content.js 發送訊息信件，通知其操作網頁 DOM 元素。
    - 實作了 CSV 格式的生成（加入 UTF-8 BOM `\uFEFF` 防止 Excel 開啟亂碼）與下載，並以 `FileReader` 讀取並還原上傳的 CSV 資料。

---

### 📄 5. 網頁注入邏輯：[content.js](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/content.js)
*   **教學目標**：理解「接收信件並控制主網頁 DOM」的底層原理。
*   **核心代碼解析**：
    - `chrome.runtime.onMessage.addListener((message, sender, sendResponse) => { ... })`：在網頁宇宙中註冊一個「收信箱」，用來監聽側邊欄發過來的訊息。
    - `input.dispatchEvent(new Event('input', { bubbles: true }))`：告訴學員如果網頁是用 React/Vue 寫的，僅修改 `.value` 無法讓框架感知，必須主動派發 `input` 與 `change` 事件，通知前端框架進行資料更新。
    - 輔助填值函式在寫入值後會對 DOM 元素進行短暫的背景黃色閃爍（`#fef08a`）視覺反饋，提示學員填值已生效。

---

### 📄 6. 注入樣式：[content.css](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/content.css)
*   **教學目標**：了解外掛如何透過注入樣式來客製化目標網頁的視覺呈現。
