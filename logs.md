# 銀河 ERP 內訓課程專案：Falo 變更與決策日誌 (logs.md)

本文件依據 Falo 方法論建立，旨在記錄本專案開發過程中的所有操作、決策與技術變更脈絡，確保教學與維護過程皆有跡可循。

---

## 專案變更歷史

| 時間戳記 | 操作類別 | 描述 | 操作者 | 影響檔案 |
| :--- | :--- | :--- | :--- | :--- |
| 2026-06-08 23:39:00 | 專案更新 | 修正外掛專案教學頁 Tab 2 之「研發背景與二創聲明」描述，改為參考 Chrome Web Store 上的 Progress Bar for Instagram 外掛專案精神，並與 AI Agent 交流後全新改寫實作，避免抽出與反編譯等字眼誤解。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/ig/index.html`, `falo-taiwan/class/a01/class3/ig/falo_extension_tutorial.html` |
| 2026-06-08 23:38:00 | 專案更新 | 於外掛專案教學頁 Tab 2 新增「研發背景與二創聲明」，揭露此專案是基於解構「Progress Bar for Instagram」外掛、以 AI Agent（Antigravity、Claude）抽出程式碼理解後二次創作重構而成，作為 Vibe Coding 教學示範。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/ig/index.html`, `falo-taiwan/class/a01/class3/ig/falo_extension_tutorial.html` |
| 2026-06-08 23:36:00 | 專案更新 | 新增外掛專案教學頁之 Tab 2 專區，深入說明外掛開發的核心技巧與卡頓優化原理（事件冒泡攔截、視區面積定位多影片、儲存適配器與 OLED 更新頻率優化），並將原本的 Chrome 架構與 AI 開發指南移至 Tab 3。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/ig/index.html`, `falo-taiwan/class/a01/class3/ig/falo_extension_tutorial.html` |
| 2026-06-08 23:20:00 | 專案更新 | 解耦外掛專案與 Class 03 教材：移除外掛專案中的返回大綱按鈕以防洩漏 class3，從 falo-taiwan.github.io 刪除 class/a01/class3/ig 目錄，並將 Class 03 大綱主題七連結修改為指向外部獨立專案 https://falo-taiwan.github.io/ig/ (開新視窗)。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `falo-taiwan/class/a01/class3/ig/index.html`, `falo-taiwan/class/a01/class3/ig/falo_extension_tutorial.html`, `sync_and_push.py` |
| 2026-06-08 23:18:00 | 專案更新 | 新增雙分頁 (Tabbed Navigation) 切換介面，將外掛部署實戰與 Chrome 外掛 (Manifest V3) 核心架構、通訊機制與 AI 協同開發指南分離，並推送到 GitHub。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/ig/index.html`, `falo-taiwan/class/a01/class3/ig/falo_extension_tutorial.html` |
| 2026-06-08 23:10:00 | 專案更新 | 修正「GEO」定義為 Generative Engine Optimization (AI 可捕捉 SEO) 中介資料與 JSON-LD 結構化資料，移除非 AI 之地理坐標中介資料後推送到 GitHub。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/ig/index.html`, `falo-taiwan/class/a01/class3/ig/falo_extension_tutorial.html` |
| 2026-06-08 23:08:00 | 專案更新 | 修正主題七外掛配色「一班」錯字為「一般」，移除教學頁之模擬測試區塊，並注入作者、SEO、GEO 與隱藏浮水印後推送到 GitHub。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/ig/index.html`, `falo-taiwan/class/a01/class3/ig/falo_extension_tutorial.html`, `falo-taiwan/class/a01/class3/ig/ig-video-enhancer-extension/content.css`, `falo-taiwan/class/a01/class3/ig/ig-video-enhancer-extension/content.js`, `falo-taiwan/class/a01/class3/ig/FALO_Instagram_Video_Enhancer.zip` |
| 2026-06-08 23:05:00 | 專案匯入 | 只把 ig 專案 clone 過來，變成 class3 下面的單獨專案目錄，並將其整合至 Class 03 課程導航主頁 index.html/md 中。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/ig`, `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md` |
| 2026-06-08 18:52:00 | 檔案更新 | 將 Class 03 大綱主頁重新命名為 index.html/md，修正所有相關連結，並在主題二 agent_tools.html 中補齊返回主頁的按鈕與樣式。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `falo-taiwan/class/a01/class3/agent_tools.html`, `class03_collaboration.html`, `class03_gemini_chrome.html`, `class03_ocr_hitl.html`, `class03_computer_use.html`, `class03_qas.html`, `history.md`, `history.html`, `sync_and_push.py` |
| 2026-06-08 18:15:00 | 檔案更新 | 於主題二與主題五教材中新增其他參考資源，包含電腦王阿達對 Anthropic Academy 的介紹連結。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/agent_tools.md`, `falo-taiwan/class/a01/class3/agent_tools.html`, `falo-taiwan/class/a01/class3/class03_computer_use.md`, `falo-taiwan/class/a01/class3/class03_computer_use.html` |
| 2026-06-08 15:50:00 | 檔案更新 | 在主題五教材中新增實作工具之線上 Live 網址（https://falo-taiwan.github.io/computer-use/）。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/class03_computer_use.md`, `falo-taiwan/class/a01/class3/class03_computer_use.html` |
| 2026-06-08 15:45:00 | 建立檔案 | 建立 Class 03 主題五教材 class03_computer_use.md 與 class03_computer_use.html，整合 LINE 防封鎖工具案例與 Computer Use 示範沙盒。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/class03_computer_use.md`, `falo-taiwan/class/a01/class3/class03_computer_use.html`, `falo-taiwan/class/a01/class3/class03.md`, `falo-taiwan/class/a01/class3/class03.html` |
| 2026-06-08 12:00:00 | 檔案更新 | 將 Class 03 學員提問解答 (QA) 併入歷史彙整與 Class 03 主導航目錄。 | AI (Antigravity) | `history.md`, `history.html`, `falo-taiwan/class/a01/class3/class03.md`, `falo-taiwan/class/a01/class3/class03.html` |
| 2026-06-08 11:58:00 | 建立檔案 | 建立 Class 03 學員課前提問與解答 QA 檔案（包含 md + html 雙軌版本）。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/class03_qas.md`, `falo-taiwan/class/a01/class3/class03_qas.html` |
| 2026-06-07 19:35:00 | 檔案修正 | 修正主題四教材中「某郵局/某郵政」為「台北郵局」，並將「海科大」更正為「海洋大學」，以與原始新聞及學校名稱保持一致。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/class03_ocr_hitl.md`, `falo-taiwan/class/a01/class3/class03_ocr_hitl.html` |
| 2026-06-07 19:30:00 | 建立檔案 | 在主題四教材中新增原始新聞網址（自由時報）與重點內文摘要。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/class03_ocr_hitl.md`, `falo-taiwan/class/a01/class3/class03_ocr_hitl.html` |
| 2026-06-07 19:15:00 | 系統操作 | 解決 Git 推送權限問題（從 force-taiwan 切換為 falo-taiwan），並成功將 Class 03 課件推送至遠端儲存庫。 | AI (Antigravity) | 無 |
| `2026-06-07 18:38:30` | 建立檔案 | 將大宗郵件 OCR 分揀異常與 HITL 分析圖複製並整合至 `class03_ocr_hitl.md` 與 `class03_ocr_hitl.html` 中。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/images/ocr_hitl_flow.jpg`, `class03_ocr_hitl.md`, `class03_ocr_hitl.html` |
| `2026-06-07 16:41:00` | 建立檔案 | 建立 Class 03 主題四教材 `class03_ocr_hitl.md` 與 `class03_ocr_hitl.html`，以郵局分揀辨識延誤為案例解析 OCR 與 HITL 的必要性，並更新 Class 03 主目錄。 | AI (Antigravity) | `class03_ocr_hitl.md`, `class03_ocr_hitl.html`, `class03.md`, `class03.html` |
| `2026-06-07 12:56:00` | 建立檔案 | 建立 Class 03 案例教材 `class03.md` 與 `class03.html`，詳細解構 FALO 六層模型與 Chrome Gemini 解鎖案例。 | AI (Antigravity) | `class03.md`, `class03.html` |
| `2026-06-07 12:55:50` | 建立檔案 | 建立與更新 AI Agent 開發工具比較表 `agent_tools.md` 與 `agent_tools.html`，新增 Gemini Canvas 模式對比。 | AI (Antigravity) | `agent_tools.md`, `agent_tools.html` |
| `2026-06-07 11:39:50` | 建立檔案 | 建立歷史課程彙整網頁 `history.html`，具備 Glassmorphism 現代化視覺設計與 RWD 排版。 | AI (Antigravity) | `history.html` |
| `2026-06-07 11:39:40` | 建立檔案 | 建立歷史課程彙整 Markdown `history.md`，提供 AI 讀取與理解 Class 01、02 的主要概念與原始連結。 | AI (Antigravity) | `history.md` |
| `2026-06-07 11:36:40` | 歸檔檔案 | 從 Google Drive 下載第一堂課 PDF `(完整版v1)銀河-class01.pdf` 並儲存至對應歸檔目錄。 | AI (Antigravity) | `archive/class01/(完整版v1)銀河-class01.pdf` |
| `2026-06-07 11:36:30` | 歸檔檔案 | 從 Google Drive 下載第二堂課 PDF `銀河class02-v101.pdf` 並儲存至對應歸檔目錄。 | AI (Antigravity) | `archive/class02/銀河class02-v101.pdf` |
| `2026-06-07 11:36:20` | 目錄建立 | 建立專案歸檔目錄：`archive/class01`、`archive/class02`、`archive/class03`。 | AI (Antigravity) | `archive/` 及其子目錄 |
| `2026-06-07 11:35:56` | 專案啟動 | 專案初始化，接收老師提供之前兩堂課的 Google Drive 連結與專案基本規範。 | 老師 & AI | 無 |

---

## 專案決策記錄 (Decision Records)

### DR-01：採用 md + html 雙軌並行儲存
* **背景**：老師要求「大部分都要盡量寫 md (ai) + html (人看)」。
* **決策**：專案中的核心內容皆同時提供 `.md` 格式與獨立的 `.html` 網頁檔。
  - `.md`：結構化、純文字，利於大模型 (LLM) 快速解析、編輯與記憶召回。
  - `.html`：採用 Outfit / Inter / Noto Sans TC 字型，搭配深色 Glassmorphism 風格與微互動，便於人類（老師及學員）美觀地瀏覽。
* **狀態**：已執行 (適用於 `history`、`agent_tools` 與 `class03` 等檔案)。

### DR-02：落實 Falo 方法論之軌跡追蹤
* **背景**：課程要求在專案中留下脈絡與軌跡/log觀念。
* **決策**：在專案根目錄中維護 `logs.md` 與 `logs.json` 檔案。
  - `logs.md` 以表格化直觀記錄所有變更事件與決策理由。
  - `logs.json` 記錄機器的時間戳記與結構化後設資料 (Metadata)，方便將來進行自動化脈絡解析或系統檢驗。
* **狀態**：已執行。

### DR-03：收錄經典 FALO 案例與工具自我對比
* **背景**：老師需要編寫三大 AI Agent 程式開發工具的教學，並擴充 Class 03 為 FALO 經典案例 Memo。
* **決策**：建立專屬的工具比較檔 (`agent_tools`) 與 Class 03 案例檔 (`class03`)，並收錄 Chrome Gemini 解鎖及 NotebookLM 知識煉油廠之六層模型分析，作為知識資產化的教材示範。
* **狀態**：已執行。
