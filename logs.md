# 銀河 ERP 內訓課程專案：Falo 變更與決策日誌 (logs.md)

本文件依據 Falo 方法論建立，旨在記錄本專案開發過程中的所有操作、決策與技術變更脈絡，確保教學與維護過程皆有跡可循。

---

## 專案變更歷史

| 時間戳記 | 操作類別 | 描述 | 操作者 | 影響檔案 |
| :--- | :--- | :--- | :--- | :--- |
| 2026-06-10 20:46:00 | 本機更新 | 於 Class 03 課程首頁 (index.html) 左側導覽列目錄中，在「實戰專案與進階手冊」下方新增「學員提問與技術解答」連結，並將原本位於側邊欄頁尾之提問按鈕移除，此變更目前僅限本機。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `logs.md`, `logs.json` |
| 2026-06-10 19:56:00 | 本機更新 | 於 Class 03 課程首頁 (index.html/index.md) 的「實戰專案與進階手冊」區塊內新增「學員課前提問解答 (QA)」連結，此變更目前僅限本機。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `logs.md`, `logs.json` |
| 2026-06-10 19:46:00 | 本機更新 | 更新 Class 03 課程首頁 (index.html/index.md) 的 Class 01 與 Class 02 歷史簡報下載連結為 Google Drive 實際網址；並在首頁右上角建立懸浮無障礙工具列，提供切換配色與調整「字體大小 (A+/A-)、版面寬度 (W+/W-)」等 4 個按鈕控制，此變更僅限本機並自動同步推送。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `logs.md`, `logs.json` |
| 2026-06-10 19:42:30 | 本機更新 | 於 Class 03 課程首頁 (index.html/index.md) 歷史回顧區塊，新增「未來將升級為基於 GAS 驗證之高強度保密安全版本」之備註說明，此變更僅限本機並自動同步推送。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `logs.md`, `logs.json` |
| 2026-06-10 19:41:00 | 本機更新 | 為 Class 03 課程首頁 (index.html/index.md) 之「歷史課程回顧」 Class 01 與 Class 02 連結新增密碼保護 (密碼為 attn)，此變更僅限本機並自動同步推送。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `logs.md`, `logs.json` |
| 2026-06-10 19:36:30 | 本機更新 | 將 Class 03 課程首頁 (index.html/index.md) 所有指向 Chrome Extension 與 IPAS ETL 實戰專案之相對連結，統一更換為 falo-taiwan 官方部署之絕對網址，此變更僅限本機。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `logs.md`, `logs.json` |
| 2026-06-10 19:35:00 | 本機更新 | 將全域「Codex / Antigravity」與「Codex/Antigravity」順序交換為「Antigravity / Codex」與「Antigravity/Codex」，將 Google 主導的工具列為首要；並在課程首頁最上方新增「實戰專案與進階手冊」區塊，直接在首頁第一層放置 4 個進階實戰手冊與專案連結，此變更僅限本機。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, 7個教材相關 HTML/MD 檔案, `logs.md`, `logs.json` |
| 2026-06-10 19:31:00 | 本機更新 | 於 Class 03 課程首頁 (index.html/index.md) 最上方新增「歷史課程回顧」區塊，預留 Class 01 與 Class 02 PDF 簡報下載版面，暫時連結至 Google，此變更僅限本機。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `logs.md`, `logs.json` |
| 2026-06-10 19:28:30 | 本機更新 | 隱藏專供教師自用之大綱備忘錄 memo.html 與 memo.md 連結，更新歷史彙整頁 history.html 課程入口，並批量更新 Class 03 旗下 12 個子主題 HTML 課件之返回連結與文字，將其從指向 memo.html (返回主題大綱) 修正回 index.html (返回課程首頁)，此變更僅限本機。 | AI (Antigravity) | `history.html`, 12個 `class03_*.html` 課件, `logs.md`, `logs.json` |
| 2026-06-10 19:27:00 | 本機更新 | 修正去識別化命名，全域還原「銀河軟體/銀河 ERP/Yinhe」名稱，並將 Class 03 課程首頁副標題更新為「銀河軟體 台西分公司 Class03」，此變更僅限本機。 | AI (Antigravity) | 全域 HTML/MD/JSON/Python 檔案 |
| 2026-06-10 19:26:00 | 本機更新 | 優化 Class 03 入口頁面 (index.html) 之深色模式配色，還原高質感深紫微光漸變，並將所有教材與手冊連結更新為以新視窗 (target="_blank") 開啟，僅限本機。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `logs.md`, `logs.json` |
| 2026-06-10 19:24:00 | 本機更新 | 重構 Class 03 首頁入口 (index.html/md)，改版為以 7 大核心教學主軸（包含多人多帳號協作、Canvas、Codex/Antigravity、雙軌文檔、RWD部署、地端Server、GAS自動化）構成的課程地圖，整合雙配色切換與進階實戰手冊連結，僅限本機。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `logs.md`, `logs.json` |
| 2026-06-10 18:11:00 | 本機更新 | 執行去識別化全域修正，將所有教材、歷史頁面與日誌檔案中的「銀河軟體/銀河 ERP/Yinhe」更正為「銀河軟體/銀河 ERP/Yinhe」，以對齊真實「天心 ERP 台南分公司」去識別化為「銀河軟體 台西分公司」之要求，此變更僅限本機。 | AI (Antigravity) | 全域 HTML/MD/JSON/Python 檔案 |
| 2026-06-10 18:10:00 | 本機更新 | 為 Class 03 過渡引導頁 index.html 新增雙配色切換功能，支援預設深色與「清新白」主題，並利用 localStorage 儲存狀態，此變更僅限本機，未同步至遠端。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `logs.md`, `logs.json` |
| 2026-06-10 18:06:00 | 專案重構 | 重構 Class 03 入口頁面，將原大綱 index.html/md 重新命名為 memo.html/md，建立精美 Glassmorphism 過渡期引導首頁，並批量更新所有子主題課件之返回連結指向 memo.html，同步更新歷史彙整頁與部署腳本。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `falo-taiwan/class/a01/class3/memo.html`, `falo-taiwan/class/a01/class3/memo.md`, `history.md`, `history.html`, `logs.md`, `logs.json` |
| 2026-06-10 13:30:00 | 專案更新 | 更新主題九「Vibe Coding 實戰武器庫」，將 Gemini Canvas 困擾與解法、Codex/Antigravity、雙軌文檔策略、本機與 GitHub Pages 部署、地端 Server 與 GAS 範例六大工具教學主線深入融合至教材中，並在主題三、主題九與主題十中置入最新的 Anthropic Claude Fable 5 旗艦模型與 Stripe 實測縮短專案時程的新聞報導。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/agent_tools.md`, `falo-taiwan/class/a01/class3/agent_tools.html`, `falo-taiwan/class/a01/class3/class03_tools.md`, `falo-taiwan/class/a01/class3/class03_tools.html`, `falo-taiwan/class/a01/class3/class03_rpa_to_agent.md`, `falo-taiwan/class/a01/class3/class03_rpa_to_agent.html`, `logs.md`, `logs.json` |
| 2026-06-09 21:55:00 | 建立檔案 | 建立 Class 03 3小時實戰核心速成教材（包含 md + html 雙軌版本），設計玻璃擬態 UI 與一鍵複製代碼功能，並整合至首頁大綱與入口網頁。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/class03_3hr_core.md`, `falo-taiwan/class/a01/class3/class03_3hr_core.html`, `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `logs.md`, `logs.json` |
| 2026-06-09 21:52:00 | 專案更新 | 首頁新增最新線上發佈網址連結，並同步同步與推送所有異動至 GitHub。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `logs.md`, `logs.json` |
| 2026-06-09 16:15:00 | 專案重構 | 將 Google NotebookLM 升級內容與實戰對話 Sine Wave 圖片從主題四剝離，單獨建立主題十二「Google NotebookLM 重磅升級與 Antigravity 實戰」課件，並同步更新大綱主頁、歷史彙整頁及同步腳本。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/class03_notebooklm_upgrade.md`, `falo-taiwan/class/a01/class3/class03_notebooklm_upgrade.html`, `falo-taiwan/class/a01/class3/images/notebooklm_sine_wave.png`, `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `history.md`, `history.html`, `logs.md`, `logs.json`, `sync_and_push.py` |
| 2026-06-09 14:10:00 | 專案重構 | 新增主題十一「WWDC 26 Deep Research 實戰 Prompt 示範」教材，嵌入 WWDC 26 重點觀察圖表與 Prompt 一鍵複製功能，並整合至主大綱首頁、歷史彙整頁與 Git 同步腳本中。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/class03_wwdc_prompt.md`, `falo-taiwan/class/a01/class3/class03_wwdc_prompt.html`, `falo-taiwan/class/a01/class3/images/wwdc26_observe.jpg`, `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `history.md`, `history.html`, `logs.md`, `logs.json`, `sync_and_push.py` |
| 2026-06-09 12:40:00 | 專案更新 | 導入使用者與 Codex 協作的最新版學員 Q&A 課件（class03_qas.html），支援帶有時間戳記與折疊功能之 FAQ 交互面板，並完成去識別化。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/class03_qas.html`, `logs.md`, `logs.json` |
| 2026-06-09 12:35:00 | 專案重構 | 更新主題十「從 ERP 外掛到 AI Agent」教材，對齊銀河 ERP 顧問開發視角，加入 Event-Rule-Action 的 Workflow 模式案例與 6 階段演進，深化 AI 治理白箱優勢。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `falo-taiwan/class/a01/class3/class03_rpa_to_agent.html`, `falo-taiwan/class/a01/class3/class03_rpa_to_agent.md`, `history.md`, `history.html`, `logs.md`, `logs.json` |
| 2026-06-09 12:20:00 | 專案重構 | 新增主題十「從 RPA 到 AI Agent」教材，梳理人工流程到 Multi-Agent 的演進路線與 Workflow 治理觀念，並整合進主頁大綱與歷史彙整頁面。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `falo-taiwan/class/a01/class3/class03_rpa_to_agent.html`, `falo-taiwan/class/a01/class3/class03_rpa_to_agent.md`, `history.md`, `history.html`, `sync_and_push.py` |
| 2026-06-09 11:48:00 | 專案更新 | 於主題一教材最上方新增「常用工具的熟悉重點＋運用技巧」備註區塊（標記為：內容，撰稿中...）。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/class03_coexistence.md`, `falo-taiwan/class/a01/class3/class03_coexistence.html` |
| 2026-06-09 11:20:00 | 專案重構 | 新增主題一「人與 AI 的共創共生」教材，並將其餘主題順延為主題二至主題八。調整相關課件之標題與頁尾，更新 `history.md` 與 `history.html` 彙整列表，並升級 Git 同步腳本。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/index.html`, `falo-taiwan/class/a01/class3/index.md`, `falo-taiwan/class/a01/class3/class03_coexistence.html`, `falo-taiwan/class/a01/class3/class03_coexistence.md`, `falo-taiwan/class/a01/class3/agent_tools.html`, `falo-taiwan/class/a01/class3/class03_gemini_chrome.md`, `falo-taiwan/class/a01/class3/class03_qas.md`, `history.md`, `history.html`, `sync_and_push.py` |
| 2026-06-08 23:40:00 | 專案更新 | 於外掛專案教學頁 Tab 2 新增「致謝與功能重點對照卡片」，列出 Progress Bar for Instagram 外掛之原版核心功能，並將其與 FALO 進化重構版（Tooltip、Hover 音量控制條、懸浮遙控器與 HUD）進行對照與致謝。 | AI (Antigravity) | `falo-taiwan/class/a01/class3/ig/index.html`, `falo-taiwan/class/a01/class3/ig/falo_extension_tutorial.html` |
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
