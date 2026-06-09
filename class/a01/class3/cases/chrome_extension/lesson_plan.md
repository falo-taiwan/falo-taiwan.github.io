# Class03 教學案設計與開發脈絡全紀錄 (Lesson Plan)

> [!NOTE]
> **作者**：Falo x Force Cheng  
> **發佈日期**：2026/06/08  
> **教案宗旨**：引導學員跨越「寫外掛」的軟體工程思維，理解從**「人控制網頁 ➔ AI 控制網頁（DOM ➔ 螢幕像素）」**的演化路線，最終導向 **AI Agent 與 Computer Use** 的全新自動化時代。

---

## 🗺️ 一、教案總體設計地圖

本教案設計為三部曲演進，其邏輯架構與技術原理對照如下：

```mermaid
graph TD
    Start[課前準備/暖身] --> Step1[V1：表單輔助器]
    Step1 --> Step2[V2：Computer Use 視覺自動化]
    
    subgraph 課前準備/暖身
        Start -->|體驗| IG[IG Video Enhancer v1.0.1]
        IG -->|學習點| DOM_Modify[人藉由外掛「修改」網頁體驗]
    end
    
    subgraph V1：表單輔助器
        Step1 -->|實作| ERP_Helper[ERP 表單輔助器]
        ERP_Helper -->|讀 DOM| Read_DOM[偵測欄位、顯示 Selector 結構]
        ERP_Helper -->|改 DOM| Write_DOM[一鍵智慧填值]
        ERP_Helper -->|瓶頸| DOM_Break[前端代碼重構即失效]
    end
    
    subgraph V2：Computer Use
        Step2 -->|實作| Screen_Control[視覺與座標操作]
        Screen_Control -->|視覺| Vision[AI 截圖辨識按鈕座標]
        Screen_Control -->|動作| Mouse[動滑鼠、鍵盤鍵入]
        Screen_Control -->|優勢| OS_Cross[跨軟體整合、無視代碼變動]
    end
```

---

## 🎨 二、暖身專案：FALO Instagram Video Enhancer

### 1. 暖身專案定位
在進入 ERP 自動化前，先用一個學員日常接觸得到的痛點（IG Reels 無法倒帶、調速）作為起點。

*   **專案路徑**：`/Users/force/Google_Antigravity/test-case/ig-video-enhancer-extension`
*   **線上展示**：[https://falo-taiwan.github.io/ig/](https://falo-taiwan.github.io/ig/)
*   **教學核心**：讓學員在 Chrome 開啟開發者模式，載入未封裝項目，直接運行外掛。理解外掛能讀寫瀏覽器的 tab 權限，並「注入」代碼來修改網頁 UI。

### 2. 技術原理說明
*   **Manifest V3**：透過 `content_scripts` 匹配 `https://*.instagram.com/*`，在網頁加載完畢（`document_end`）時注入 `content.js` 與 `content.css`。
*   **DOM 修改**：外掛腳本會遍歷網頁中的 `<video>` 標籤，動態在下方 append 進度條與速度控制器，並監聽鍵盤事件來實現快捷鍵控制。

---

## ⚙️ 三、V1 實作：ERP 表單輔助器 (幫人操作)

### 1. 教學核心
透過表單輔助器，讓學員理解外掛如何精確定位網頁元素。這是**自動化控制數位世界的第一步：DOM 控制**。

*   **專案路徑**：`/Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/`
*   **入口引導**：雙擊開啟 [index.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/index.html) ➔ 進入 [practice.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/practice.html)。

### 2. V1 代碼架構與關鍵技術

#### (A) 欄位高亮與 CSS Selector 定位器 (content.js)
外掛必須能精確指出「欄位在哪裡」。我們編寫了唯一的 CSS Selector 尋讀演算法，將元素的 Tag、ID、Name 與 nth-of-type 階層做字串拼接：
```javascript
function getCSSSelector(el) {
  if (el.id) return `#${el.id}`;
  let path = el.tagName.toLowerCase();
  if (el.name) return `${path}[name="${el.name}"]`;
  
  const parent = el.parentElement;
  if (parent) {
    const siblings = Array.from(parent.children).filter(c => c.tagName === el.tagName);
    if (siblings.length > 1) {
      const idx = siblings.indexOf(el) + 1;
      path += `:nth-of-type(${idx})`;
    }
    if (parent.id) path = `#${parent.id} > ${path}`;
  }
  return path;
}
```

#### (B) 解決現代前端框架的 Reactivity 填值問題
僅修改 `input.value = "val"` 會導致 React/Vue 雙向綁定失效（畫面上變更了，但點擊登入時系統仍判定為空）。我們透過 dispatch 觸發 `input` 與 `change` 原生事件：
```javascript
field.value = val;
field.dispatchEvent(new Event('input', { bubbles: true }));
field.dispatchEvent(new Event('change', { bubbles: true }));
```

### 3. V1 實戰 Prompt 雙層對照集
*   💬 **基礎版 Prompt (一般 User - v1)**：
    > 我想要寫一個 Chrome 外掛，當我進入 ERP 網頁時，可以自動幫我把所有的輸入框偵測出來，在必填欄位旁邊加上高亮標示，並且加一個按鈕讓我點一下就能把測試資料填進去。
*   ⚡ **高級版 Prompt (專業開發者 - v2)**：
    > 請建立一個 Manifest V3 規格的 Chrome 外掛。編寫 content.js，在網頁加載時以 document.querySelectorAll 篩選所有未隱藏的 input, select, textarea。在 required 的欄位加上 glows-pink 的 CSS border highlighters。在網頁右上角動態 inject 一個玻璃質感的 sidebar 面板，列出偵測到的所有欄位標籤與其唯一 CSS selector，並提供 'Focus' 與 'Smart Fill' 觸發事件。

---

## 🤖 四、V2 實作：OSWorld Computer Use (AI 幫人操作)

### 1. 教學核心
當我們問學員：「如果連『滑鼠』都不需要人類點擊了呢？」這時就進入了 **V2：Computer Use**。AI 像人一樣有眼睛（視覺模型），它看著螢幕截圖直接操作。

### 2. V2 技術原理與模擬機制 (practice.html)
我們在網頁中實作了高模擬度的視覺動畫，用以展示 Anthropic OSWorld / Computer Use 的核心運作機制：
*   **視覺識別 (Vision Bounding Box)**：模擬 Vision 模型在畫面上標註檢測框。當滑鼠移動前，目標輸入框會閃爍 dashed border，並在 Log 輸出 `[AI Vision] 偵測輸入框位置：座標 (X, Y)`。
*   **虛擬游標運動 (Virtual Cursor)**：建立一個圓形的虛擬 pointer 標籤，利用 CSS 貝氏曲線（cubic-bezier）進行平滑過渡，移動到目標元素的中心座標。
*   **模擬物理敲擊 (Type Simulation)**：利用 async/await 與隨機 delay，一個字元接一個字元填入值，並觸發 `change` 事件。
*   **系統狀態變更**：當 AI 填滿所有採購單號、產品代碼、進貨數量與效期後，點擊「驗證並確認入庫」會觸發完成入庫的 Toast 提示，展示倉庫進貨核對與實體寫入資料庫的完整流程。

### 3. V2 實戰 Prompt 雙層對照集
*   💬 **基礎版 Prompt (一般 User - v1)**：
    > 幫我登入銀河軟體，把單號 PO-2026-9918 的商品 FALO-R1 辦理進貨入庫，數量是 120 件，效期寫 2027-06-09，填完就點確認。
*   ⚡ **高級版 Prompt (專業開發者 - v2)**：
    > 請啟動 OSWorld 環境與 Vision Agent。
    > 步驟 1：在 Chrome 瀏覽器截圖中尋找 '銀河軟體' 登入按鈕，定位座標並輸入帳密。
    > 步驟 2：偵測並定位進貨登錄欄位，填入採購單號『PO-2026-9918』、產品代碼『FALO-R1』、進貨數量『120』與效期『2027-06-09』。
    > 步驟 3：定位並點擊『驗證並確認入庫』按鈕，確認彈出入庫成功對話框。

---

## 🚀 五、Class03 課堂引導腳本設計 (教案執行流程)

| 階段 | 教學時間 | 教師操作步驟 | 學員互動與思考引導 |
| :--- | :--- | :--- | :--- |
| **暖身體驗** | 10 mins | 1. 載入 `ig-video-enhancer-extension`<br>2. 開啟 IG reels 頁面並播放。<br>3. 調整播放速度，展示進度條。 | **引導問答**：「大家常用的外掛都是為了解決什麼問題？（如去廣告、下載）外掛是怎麼做到的？答案是：因為外掛有權限可以改動網頁代碼。」 |
| **進入 V1** | 15 mins | 1. 開啟 [practice.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/practice.html)。<br>2. 開啟 V1 模擬器（或運行 real extension）。<br>3. 顯示 DOM Selector 側邊欄。<br>4. 點擊自動填值。 | **思考點**：「外掛是利用 `CSS Selector` 找到輸入框。但如果 ERP 系統明天重構了，帳號的 ID 從 `username` 改成 `user-id`，會發生什麼事？」➔ 外掛立刻失效崩潰。 |
| **躍升 V2** | 20 mins | 1. 在控制台點選「啟動 V2 電腦操作模擬」。<br>2. 觀察虛擬粉紅滑鼠移動軌跡。<br>3. 觀察 Bounding Box 的閃爍。<br>4. 閱讀 terminal 顯示的 AI 視覺日誌。 | **核心震撼點**：「大家有發現嗎？AI 這時候完全沒有去看網頁代碼！它是像人類一樣看著螢幕畫面，認出那是個輸入框，認出那是個按鈕，然後計算座標、把滑鼠移過去點擊。」 |
| **總結** | 10 mins | 1. 切換回 [index.html](file:///Users/force/Google_Antigravity/attn-class3-demo/chrome-computer-use/index.html)。<br>2. 導讀雙路徑流程圖。<br>3. 重申 Force 金句：「V1 幫人操作 ➔ V2 AI 幫人操作」。 | **總結性反思**：「一旦 AI 具備了 Computer Use 操作電腦的能力，它就不僅僅能控制網頁，它能控制 Excel、LINE、Outlook。這就是 AI Agent 時代數位控制權的革命。」 |

---

## 🛡️ 六、教材開發規範對照 (Developer Guide Compliance)

本專案之開發完全落實 `developer_guide.md` 所要求的高品質標準：
- [x] **Tutorial as Entrypoint**：根目錄 `index.html` 為純概念教學，實作放置於 `practice.html`。
- [x] **CORS Bypass**：完全使用本地 `questions.js` 或本地邏輯，離線雙擊即用。
- [x] **GEO JSON-LD**：在 HTML 結構中宣告 `TechArticle` / `WebPage`，標明作者 `Falo x Force Cheng`。
- [x] **Watercolor Aesthetic**：全系統介面採用 Outfit 字體、Pastel 漸層及半透明玻璃磨砂設計。
