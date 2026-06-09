# Class03 教學指引：從 Chrome Extension 到 Computer Use 的控制革命

> [!NOTE]
> **作者**：Falo x Force Cheng  
> **發佈日期**：2026/06/08  
> **專案定位**：這堂課的重點**不是**教如何寫 Chrome 外掛，而是教：**「人如何控制網頁 ➔ AI 如何控制網頁」**。讓學員理解 Chrome Extension、Computer Use 與 AI Agent 是同一條演化路線。

---

## 🎨 課程核心觀念與金句

在進入任何技術實作前，請務必先向學員揭露這套「數位世界控制權」的演變脈絡。

> [!TIP]
> **Force 老師教學金句**：
> - **V1：幫人操作** (透過瀏覽器權限與網頁結構，輔助人類填表單)
> - **V2：AI 幫人操作** (透過大模型看懂螢幕與像素座標，完全自主動滑鼠與鍵盤)

### 🗺️ 控制演化三部曲
1. **傳統人類控制**：人透過滑鼠點擊網頁（DOM 節點）、手動複製貼上。
2. **V1 Chrome Extension (DOM-Based)**：寫入規則與 Selector，在網頁內部進行讀取與修改，但極度依賴前端代碼結構，代碼一改即崩潰。
3. **V2 Computer Use (Vision-Based)**：AI 像人一樣看著螢幕畫面，換算按鈕像素座標點，進行跨軟體的完整自動化流程，實現真正的 **AI Agent 辦公自動化**。

---

## 📁 專案檔案結構說明

本實作案例採用 **FALO 離線點擊即用（CORS Bypass）** 與 **語意化命名** 規範，結構如下：

- 📝 [index.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/index.html) —— **教學概念導讀首頁**。包含 Force 教學金句、演化觀念、雙層 Prompt 對照，以及點擊直接新視窗開啟的互動 SVG 演化路徑圖。
- 🧪 [practice.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/practice.html) —— **模擬操作競技場**。左側為模擬 ERP 系統，右側為 V1 / V2 控制面板與 terminal log，並內建完整的滑鼠與視覺定位動畫。
- 🔌 [chrome-extension/](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/) —— **V1 實體 Chrome 外掛代碼**。包含 manifest.json、content.js 等，學員可真正載入 Chrome 瀏覽器，實地操作任意網頁。

---

## 🚀 Class03 現場演示 (Showcase) 步驟指南

Force 老師在課堂上可透過以下步驟（含課前暖身）進行震撼性展示：

### 課前暖身：體驗 FALO Instagram Video Enhancer 外掛

在正式進入 ERP 表單自動化演化前，先帶領學員體驗初階的 Chrome 外掛功能，建立基本體感：
1. 讓學員在 Chrome 瀏覽器開啟 `chrome://extensions`「開發者模式」，點擊「載入未封裝項目」，選取本機暖身專案路徑：`[ig-video-enhancer-extension](file:///Users/force/Google_Antigravity/test-case/ig-video-enhancer-extension)`。
2. 導引學員至 [Instagram 官網](https://www.instagram.com/)、線上介紹頁 [https://falo-taiwan.github.io/ig/](https://falo-taiwan.github.io/ig/)，或直接雙擊開啟該目錄下的本地網頁 `mock_instagram.html`。
3. 實地體驗外掛如何將「自訂影片進度條、音量控制、播放速度選單、快速鍵」直接注入到 IG 的 Reels 影片中，藉此感受**外掛如何透過注入代碼，在前端改善第三方網站的體驗**。
4. **觀念轉折**：向學員引導：「這個 IG 外掛改善了我們看影片的日常體驗。那如果我們不是要優化看影片，而是要自動化完成內部無聊的 ERP 報表表單呢？這就進到我們的主題 —— V1 表單輔助器。」

---

### 步驟一：展示 V1 外掛「讀網頁」與「改網頁」

1. 打開 Chrome 瀏覽器的「擴充功能管理頁面」 (`chrome://extensions`)，開啟右上角 **「開發者模式」**。
2. 點擊 **「載入未封裝項目」**，選取專案目錄中的 [chrome-extension/](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/) 資料夾。
3. 打開 [practice.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/practice.html)。
4. 點擊 Chrome 工具列的 **FALO ERP Form Helper** 外掛圖示：
   - 點選 **「開啟網頁元素偵測」** ➔ 畫面上的帳號、密碼輸入框立刻亮起粉紅色光暈，並在網頁右上角彈出 DOM Inspector 側邊欄，顯示所有 input 的 CSS Selector（讀網頁 DOM 結構）。
   - 點選 **「一鍵填入測試資料」** ➔ 帳號密碼立刻被自動填寫完成（改網頁 DOM 數值）。

> [!IMPORTANT]
> **引導思考**：這時候請問學員：「如果我們明天把帳號輸入框的 `id="username"` 改成 `id="account-input"`，這個外掛還動得起來嗎？」➔ 答案是「不行，Selector 找不到，外掛立刻失效！」這就是 V1 的技術侷限。

---

### 步驟二：切換 V2 啟動 Computer Use 模擬

1. 在 [practice.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/practice.html) 右側控制台，點選 **「啟動 V2 電腦操作模擬」**。
2. 學員將會看到以下極具震撼感的視覺動畫：
   - 一個 **虛擬粉紅色光點（滑鼠游標）** 出現在螢幕中央，並開始平滑移動。
   - 當滑鼠移至「帳號」時，該輸入框四周亮起 **「AI Vision 偵測虛線框 (Bounding Box)」**。
   - 控制台的 Terminal Log 即時以中英文印出 AI 內心的想法：`[AI Vision] 定位帳號輸入框：(X: 200, Y: 155)`。
   - 滑鼠點擊（產生漣漪動畫），隨後字元一個個自動鍵入。
   - 登入成功後，介面自動切換至資料中心，滑鼠繼續移動到「關鍵字輸入框」輸入 `ERP_REPORT_2026`。
   - 滑鼠移至「匯出 Excel」並點擊 ➔ 畫面彈出下載成功提示。
   - 滑鼠移至「Email 收件人」輸入 `force@falo.tw` ➔ 點擊「發送 Email」 ➔ 寄送成功。

---

### 步驟三：總結 Agent 時代的數位控制權

1. 請 Force 老師指出，在 V2 的模擬中，AI **完全沒有**讀取網頁原始碼的 CSS Selector。
2. AI 是像人類一樣「看著螢幕截圖（Vision）」➔「判斷按鈕在第幾個像素（Coordinates）」➔「送出 Click 與 Type 訊號」。
3. 這樣的能力，讓 AI 可以跨出瀏覽器。只要把這套 API 接上作業系統，AI 就能在 Mac 桌面打開 Excel、把資料拷貝到 LINE 寄出，實現跨軟體的完整運作。
4. **結論**：AI 不只會聊天。AI 可以藉由視覺與 OS API，操作整個數位世界。

---

## ⚡ 實戰 Prompt 雙層對照表

本課程設計了兩套 Prompt 來呈現一般大眾 (v1) 與專業 AI 開發者 (v2) 的思維深度：

### 1. V1 階段：Chrome Extension 表單輔助器
- 💬 **基礎版 Prompt (一般 User - v1)**：
  > 我想要寫一個 Chrome 外掛，當我進入 ERP 網頁時，可以自動幫我把所有的輸入框偵測出來，在必填欄位旁邊加上高亮標示，並且加一個按鈕讓我點一下就能把測試資料填進去。
- ⚡ **高級版 Prompt (專業開發者 - v2)**：
  > 請建立一個 Manifest V3 規格的 Chrome 外掛。編寫 content.js，在網頁加載時以 document.querySelectorAll 篩選所有未隱藏的 input, select, textarea。在 required 的欄位加上 glows-pink 的 CSS border highlighters。在網頁右上角動態 inject 一個玻璃質感的 sidebar 面板，列出偵測到的所有欄位標籤與其唯一 CSS selector，並提供 'Focus' 與 'Smart Fill' 觸發事件。

### 2. V2 階段：Computer Use 流程自動化
- 💬 **基礎版 Prompt (一般 User - v1)**：
  > 幫我登入銀河軟體，把單號 PO-2026-9918 的商品 FALO-R1 辦理進貨入庫，數量是 120 件，效期寫 2027-06-09，填完就點確認。
- ⚡ **高級版 Prompt (專業開發者 - v2)**：
  > 請啟動 OSWorld 環境與 Vision Agent。
  > 步驟 1：在 Chrome 瀏覽器截圖中尋找 '銀河軟體' 登入按鈕，定位座標並輸入帳密。
  > 步驟 2：偵測並定位進貨登錄欄位，填入採購單號『PO-2026-9918』、產品代碼『FALO-R1』、進貨數量『120』與效期『2027-06-09』。
  > 步驟 3：定位並點擊『驗證並確認入庫』按鈕，確認彈出入庫成功對話框。

---

## 📖 📝 V1 擴充功能分檔逐行教學指引 (逐檔剖析)

為了讓您在課堂上面對學員時，能夠將外掛目錄中的 **6 個檔案** 當作教材順暢講授，以下為您整理各檔案的「核心目的」與「逐行解析教案」：

### 📄 1. 身份宣告檔：[manifest.json](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/manifest.json)
*   **教學目標**：理解 Manifest V3 擴充功能的配置規範。
*   **核心程式碼解析**：
    - `"manifest_version": 3`：告訴瀏覽器這使用的是現代 V3 規範（V2 已廢棄）。
    - `"background": { "service_worker": "background.js" }`：註冊後台背景線程，負責監聽擴充功能級別的事件。
    - `"side_panel": { "default_path": "sidepanel.html" }`：宣告我們的外掛是「側邊欄」形式，並指定其預設畫面。
    - `"permissions": ["activeTab", "sidePanel"]`：要求安全權限，`activeTab` 代表僅允許讀寫當前開啟的分頁，`sidePanel` 允許使用側邊欄 API。
    - `"content_scripts": [...]`：定義「當使用者打開任何網頁時，自動將 `content.js` 與 `content.css` 注入該網頁」。

---

### 📄 2. 背景服務：[background.js](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/background.js)
*   **教學目標**：理解事件驅動的背景處理（Event-driven Service Worker）。
*   **核心程式碼解析**：
    - `chrome.sidePanel.setPanelBehavior({ openPanelOnActionClick: true })`：這行程式碼非常關鍵！它告訴瀏覽器：「當使用者用滑鼠點擊瀏覽器右上角的外掛圖示時，請直接滑出我們的 `sidepanel.html` 側邊欄，而不是彈出傳統的小 Popup 視窗。」

---

### 📄 3. 側邊欄介面：[sidepanel.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/sidepanel.html)
*   **教學目標**：外掛側邊欄的視覺結構，使用純 HTML。
*   **核心程式碼解析**：
    - 本質上就是一個普通的 HTML 網頁。
    - 定義了 3 個進貨明細卡片按鈕（`#btn-fill-a`, `#btn-fill-b`, `#btn-fill-c`）與 1 個高亮按鈕（`#btn-toggle-highlight`）。
    - 在最底部以 `<script src="sidepanel.js"></script>` 載入側邊欄的控制邏輯。

---

### 📄 4. 側邊欄控制：[sidepanel.js](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/sidepanel.js)
*   **教學目標**：掌握**「Context 隔離宇宙」**與**「跨宇宙通訊 (Message Passing)」**。
*   **核心程式碼解析**：
    - `chrome.tabs.query({ active: true, currentWindow: true }, (tabs) => { ... })`：這是 Chrome 擴充功能最常用的 API，用來查詢「目前使用者正在瀏覽的 Active 分頁資訊」。
    - `chrome.tabs.sendMessage(tabs[0].id, { action: "fillForm", data: { ... } })`：因為側邊欄的 JS 摸不到網頁 DOM，因此它向當前分頁（`tabs[0].id`）發送一封「通訊信件」，信件內容包含動作（`action`）與要填寫的資料物件（`data`）。
    - 這體現了外掛與網頁的「跨宇宙通訊」。

---

### 📄 5. 網頁注入邏輯：[content.js](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/content.js)
*   **教學目標**：理解「接收信件並控制主網頁 DOM」的底層原理。
*   **核心程式碼解析**：
    - `chrome.runtime.onMessage.addListener((message) => { ... })`：在網頁宇宙中註冊一個「收信箱」，用來監聽剛才 `sidepanel.js` 寄過來的信件。
    - `document.querySelectorAll('#po-number...')`：一旦收到高亮信件，用網頁最原生的 `querySelectorAll` 取得欄位，並加上 `falo-highlighted-field` CSS 類別。
    - `document.querySelector(selector).value = value`：一旦收到填值信件，取得輸入框並直接賦予 value。
    - `input.dispatchEvent(new Event('input', { bubbles: true }))`：**（教學亮點）**告訴學員如果網頁是用 React/Vue 寫的，僅改 value 會無效，必須主動派發一個 `input` 與 `change` 事件，通知前端框架進行雙向綁定更新。

---

### 📄 6. 注入樣式：[content.css](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/chrome-extension/content.css)
*   **教學目標**：外掛如何修改第三方網頁的 CSS 樣式。
*   **核心程式碼解析**：
    - 當外掛執行高亮時，網頁輸入框會被套用 `.falo-highlighted-field` 樣式。
    - 使用了 `box-shadow` 與 `border: 2px solid #ec4899`，在輸入框四周渲染出粉紅色的發光邊框。
    - 註明 `!important` 確保該樣式能覆蓋原有 ERP 網頁本身的 border 樣式。
