# Class03 教學案設計與開發脈絡全紀錄 (Lesson Plan)

> [!NOTE]
> **作者**：Falo x Force Cheng  
> **發佈日期**：2026/06/08  
> **教案宗旨**：引導學員掌握 Chrome 側邊欄外掛開發，實現網頁 DOM 節點的雙向控制（寫入、擷取、隨機產生、一鍵清空、CSV 備份與還原），並深入理解 Manifest V3 規範、背景腳本（Service Worker）、側邊欄與網頁 Content Script 之間的通訊（Message Passing）底層機制。

---

## 🗺️ 一、教案總體設計地圖

本教案設計為從「體驗注入」到「雙向 DOM 控制」及「資料備份閉環」的實戰演進，其邏輯架構如下：

```mermaid
graph TD
    Start[課前準備/暖身] --> Step1[實作階段 1：基礎外掛 DOM 控制]
    Step1 --> Step2[實作階段 2：雙向控制與 CSV 備份閉環]
    
    subgraph 課前準備/暖身
        Start -->|體驗| IG[IG Video Enhancer v1.0.1]
        IG -->|學習點| DOM_Modify[人藉由外掛「修改」網頁體驗]
    end
    
    subgraph 實作階段 1：基礎外掛 DOM 控制
        Step1 -->|寫入網頁| Write_DOM[外掛 ➔ 網頁：fillField & fillForm]
        Step1 -->|擷取資料| Read_DOM[網頁 ➔ 外掛：readField & readForm]
        Step1 -->|相容性| Reactivity[Dispatch input/change 事件相容 Vue/React]
    end
    
    subgraph 實作階段 2：雙向控制與 CSV 備份閉環
        Step2 -->|隨機與清空| Random_Clear[隨機資料產生與一鍵清空]
        Step2 -->|CSV 備份| CSV_Backup[匯出/匯入 CSV 實現資料閉環]
        Step2 -->|遠端遙控| Remote_Action[側邊欄遙控網頁表單檢核與入庫]
    end
```

---

## 🎨 二、暖身專案：FALO Instagram Video Enhancer

### 1. 暖身專案定位
在進入 ERP 自動化前，先用一個學員日常接觸得到的痛點（IG Reels 無法倒帶、調速）作為起點，建立外掛開發的基礎體感。

*   **暖身專案路徑**：`ig-video-enhancer-extension`
*   **教學核心**：讓學員在 Chrome 開啟開發者模式，載入未封裝項目，直接運行外掛。理解外掛能讀寫瀏覽器的 tab 權限，並「注入」代碼來修改第三方網頁 UI。

### 2. 技術原理說明
*   **Manifest V3**：透過 `content_scripts` 匹配 `https://*.instagram.com/*`，在網頁加載完畢時注入 `content.js` 與 `content.css`。
*   **DOM 修改**：外掛腳本會尋找網頁中的 `<video>` 標籤，動態在下方 append 進度條與速度控制器，並監聽鍵盤事件來實現快捷鍵控制。

---

## ⚙️ 三、實作專案：銀河 ERP 填單助手 (V1.5)

### 1. 教學核心
透過開發一個具備完整功能的 Chrome 側邊欄（Side-panel）填單助手，讓學員理解外掛如何精確定位網頁元素，並實現與網頁 DOM 的雙向互動及通訊。

*   **專案路徑**：`chrome-computer-use/` (發布對照的遠端子目錄為 `class/a01/class3/cases/chrome_extension/`)
*   **主要網頁**：[index.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/index.html) (教學導讀) 與 [erp.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/erp.html) (實體外掛測試網頁)。

### 2. 關鍵技術與程式碼剖析

#### (A) 解決現代前端框架的 Reactivity 填值問題
僅修改 `input.value = "val"` 會導致 React/Vue 雙向資料綁定失效（畫面上變更了，但點擊確認時系統仍判定為空）。我們在 `content.js` 中透過主動 dispatch 觸發 `input` 與 `change` 原生事件：
```javascript
input.dispatchEvent(new Event('input', { bubbles: true }));
input.dispatchEvent(new Event('change', { bubbles: true }));
```

#### (B) 跨視窗/Context 隔離通訊 (Message Passing)
由於側邊欄 `sidepanel.js` 與網頁 `content.js` 屬於不同的 Context，因此必須使用 `chrome.tabs.sendMessage` 向網頁發送指令，網頁端則以 `chrome.runtime.onMessage.addListener` 監聽並執行 DOM 操作：
```javascript
// sidepanel.js 發送
chrome.tabs.sendMessage(tabId, { action: "fillForm", data: { ... } });

// content.js 接收
chrome.runtime.onMessage.addListener((message, sender, sendResponse) => {
  if (message.action === "fillForm") {
    // 執行 DOM 寫入
  }
});
```

#### (C) 資料 CSV 備份與還原閉環
在側邊欄中提供將當前欄位值匯出為 CSV 檔案下載的備份功能（為防止中文亂碼，加上了 UTF-8 BOM `\uFEFF`），並使用 `FileReader` 讀取並還原上傳的 CSV 資料。

---

## ⚡ 四、實戰 Prompt 演化對照表

本教案設計了三套 Prompt，引導學員從口語意圖的描述，升級到進階技術控制，再到能夠一鍵生成完整外掛的終極 Prompt：

*   💬 **V1.1 基礎口語意圖 Prompt**：
    > 我想要寫一個 Chrome 外掛，當我進入 ERP 網頁時，可以自動幫我把所有的輸入框偵測出來，在必填欄位旁邊加上高亮標示，並且加一個按鈕讓我點一下就能把測試資料填進去。
*   ⚡ **V1.2 進階技術控制 Prompt**：
    > 請建立一個 Manifest V3 規格的 Chrome 外掛。編寫 content.js，在網頁加載時以 document.querySelectorAll 篩選所有未隱藏的 input, select, textarea。在 required 的欄位加上 glows-pink 的 CSS border highlighters。在網頁右上角動態 inject 一個玻璃質感的 sidebar 面板，列出偵測到的所有欄位標籤與其唯一 CSS selector，並提供 'Focus' 與 'Smart Fill' 觸發事件。
*   🚀 **V1.5 終極完整功能 Prompt**：
    > (請參閱教學首頁 `#promptText` 中提供的一鍵生成 Prompt，其包含完整的 5 欄位雙向讀寫、隨機、清空、CSV匯出匯入、下拉部門選項對齊以及 Vue/React 事件相容性與黃色填值閃爍反饋設計。)

---

## 🚀 五、Class03 課堂引導腳本設計 (教案執行流程)

| 階段 | 教學時間 | 教師操作步驟 | 學員互動與思考引導 |
| :--- | :--- | :--- | :--- |
| **暖身體驗** | 10 mins | 1. 載入 `ig-video-enhancer-extension`<br>2. 開啟 IG reels 頁面並播放。<br>3. 調整播放速度，展示進度條。 | **引導問答**：「大家常用的外掛都是為了解決什麼問題？（如去廣告、下載）外掛是怎麼做到的？答案是：因為外掛有權限可以改動網頁代碼。」 |
| **載入外掛** | 15 mins | 1. 在 Chrome 中開啟開發者模式，載入 `chrome-extension/` 外掛資料夾。<br>2. 開啟 [erp.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/erp.html) 並點擊外掛 Icon 滑出側邊欄。 | **思考點**：「外掛側邊欄的 HTML/JS 和原本的網頁 DOM 是互相隔離的，他們要怎麼溝通？➔ 透過 Chrome API 進行跨宇宙通訊。」 |
| **功能實戰** | 20 mins | 1. 演示「隨機產生資料」及「一鍵全填入」（黃色閃爍反饋）。<br>2. 演示「一鍵全擷取」將網頁欄位同步回側邊欄。<br>3. 演示「匯出 CSV」與「匯入 CSV」的資料備份閉環。<br>4. 演示「檢核表單」與「確認入庫」遙控動作。 | **核心震撼點**：「為什麼外掛填完值後，Vue/React 能讀到新資料？因為 content.js 派發了 input/change 事件，這解決了現代前端框架的 Reactivity 狀態同步問題。」 |
| **總結** | 10 mins | 1. 切換回 [index.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/index.html)。<br>2. 導讀雙向控制觀念。<br>3. 引導思考 DOM 控制的侷限性（Selector 變更即失效）。 | **總結性反思**：「外掛是利用 `CSS Selector` 精確讀寫 DOM 欄位。只要網頁結構改變（如 po-number 變為 po-id），外掛就需要重新維護。這就是 DOM 控制自動化的必經之路。」 |

---

## 🛡️ 六、教材開發規範對照 (Developer Guide Compliance)

本專案之開發完全落實 `developer_guide.md` 所要求的高品質標準：
- [x] **Tutorial as Entrypoint**：根目錄 `index.html` 為概念教學導讀，測試頁面與實作分開。
- [x] **CORS Bypass**：完全使用本機/靜態網頁邏輯，離線雙擊即可執行與測試。
- [x] **SEO & Schema**：在 HTML 結構中宣告 JSON-LD `TechArticle` / `WebPage`，標明作者 `Falo x Force Cheng`。
- [x] **Watercolor Aesthetic**：介面全面採用 Outfit 字體、Pastel 漸層及半透明玻璃磨砂設計，確保視覺體驗高階。
