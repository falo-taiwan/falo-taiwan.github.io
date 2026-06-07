# 銀河 ERP 內訓課程專案：Falo 變更與決策日誌 (logs.md)

本文件依據 Falo 方法論建立，旨在記錄本專案開發過程中的所有操作、決策與技術變更脈絡，確保教學與維護過程皆有跡可循。

---

## 專案變更歷史

| 時間戳記 | 操作類別 | 描述 | 操作者 | 影響檔案 |
| :--- | :--- | :--- | :--- | :--- |
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
