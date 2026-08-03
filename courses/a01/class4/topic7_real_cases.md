# 🚀 6. 核心實戰案例展示

以下為 Class 04 重點示範專案，著重於將電腦視覺、OCR 辨識與企業工作流/智慧稽核整合運作的實際落地設計。

### 案例一：IPAS AIAP 模擬考練習字卡 ─ OCR 題庫解析與自動刷題檢測
* **專案精神**：為 IPAS 人工智慧應用專業人員設計的模擬考試練習工具。前三堂課程已引導學員熟習 `ipas-aiap` 線上問答與架構，本堂 Class 04 全新推出 `practice-swiper.html` 互動練習字卡，示範如何結合自動化與 OCR 技術擷取網頁題庫、自動分析作答並檢測推論效能。
* **技術對比與特點**：
  * **OCR 題目抓取與自動判斷**：展示如何透過 OCR 自動擷取螢幕畫面或字卡題目與選項，送入多模態 LLM（如 Gemini Flash）進行語意分析、邏輯推理與自動作答。
  * **答題與效能檢測管線**：打通「截圖 ➔ OCR 辨識 ➔ 答題 ➔ 推論效能與成本對帳」之自動化端到端 ETL 工作流，並精確檢測大批刷題時的 API 延遲與答題精準度。
* **研究報告與資源下載入口**：
  * [🌐 開啟 IPAS AIAP 模擬考練習字卡](https://falo-taiwan.github.io/ipas-aiap/practice-swiper.html) *(將於新分頁中開啟)*
  * [📥 下載 IPAS AIAP 實戰學習資源包 (ipas_aiap_learning_kit.zip)](backup/ipas_aiap_learning_kit.zip) *(內含實戰模擬考刷題字卡主程式與題庫資源)*

### 案例二：FALO Prompt Manager ─ 企業級提示詞資產管理平台
* **專案精神**：針對企業與 AI 教育訓練設計的本機優先 PWA 提示詞資產管理平台，整合變數動態替換、多模型裝盤教學（Model-Dish）與工作流 Prompt 卡片，解決企業內部提示詞資產混亂、難以複用與培訓銜接的痛點。
* **技術對比與特點**：
  * **動態變數與工作流卡片**：支援雙欄「編輯對照工作台」與即時變數渲染預覽，能將複雜的 AI 任務拆解為時間序列的「工作流 Prompt 卡片（Workflow Strip）」，指導同仁依序執行；支援離線 PWA、語音輸入與高精度 OCR 輔助輸入。
  * **多主題教學與 JSON Connect**：專門針對大型課堂設計「教學大字體主題」與「模型裝盤」示範，支援拖拽式 CSV/JSON 模板批量導入與導出，實現跨團隊提示詞資產無縫同步與 JSON 結構化對接。
* **研究報告與資源下載入口**：
  * [🌐 開啟 FALO Prompt Manager 企業級提示詞資產管理平台](https://falo-taiwan.github.io/prompt-demo/) *(將於新分頁中開啟)*
  * [📥 下載 FALO Prompt Manager 實戰學習資源包 (falo_prompt_manager_learning_pack.zip)](backup/falo_prompt_manager_learning_pack.zip) *(內含提示詞管理工作台主程式與教學範本)*

### 案例三：FALO OCR Workbench ─ 智慧開源 OCR 工作台
* **專案精神**：針對企業與開發者設計的 PWA 智慧開源 OCR 工作台，整合雲端雙模型與瀏覽器原生 AI，打通「圖片上傳 ➔ 智慧 Prompt 模板 ➔ 雙軌比對 ➔ 實時 Token 對帳」的極致資料清洗與轉化 ETL 端到端實踐。
* **技術對比與特點**：
  * **雙軌雲端與地端 Nano 協作**：支援多代 Gemini 雲端模型（3.5 Flash / 3.1 Flash-Lite）並行運作與「雙 OCR 模式」；並深度整合 **Chrome Built-in AI (Gemini Nano)**，在使用者本機進行離線結果比對、校對與摘要提煉，實現零 API 成本與極致隱私保護。
  * **落地經濟學與 PWA 實踐**：內建實時「對帳日誌」，精確計算每一次辨識的 Token 數、延遲（ms）與台幣花費（NT$），落實企業級成本控制意識；採用離線 PWA 技術，打造流暢的桌面級拖拽與浮動縮放交互體驗。
* **研究報告入口**：
  * [🌐 開啟 FALO OCR Workbench 智慧開源 OCR 工作台](https://falo-chinese.github.io/ai-ocr-demo/) *(將於新分頁中開啟)*

### 案例四：雙軌 AI 驅動的公開資料採集助理 (Chrome 外掛)
* **專案精神**：作為 Vibe Coding 與 AI 輔助開發的教學案例，展示如何快速開發出 Chrome 瀏覽器側邊欄外掛，讓使用者透過口語化指令來驅動複雜的政府網站資料採集。
* **雙軌 AI 的運用與特點**：
  * **端雲協同（雲端 Gemini ✕ <span style="color: #4ade80; font-weight: bold;">地端 Chrome built-in AI (Gemini Nano)</span>）**：首創雙軌 AI 架構。日常及高隱私任務可優先調用瀏覽器內置的 **<span style="color: #4ade80; font-weight: bold;">Chrome built-in AI (Gemini Nano)</span>** 進行零延遲、零成本 Graves 級本地語意預處理；面對複雜的多維度查詢時，則無縫調用雲端 Gemini API 進行精確規劃，兼顧隱私與強大推論能力。
  * **人機協作與安全防禦（HITL ✕ <span style="color: #38bdf8; font-weight: bold;">Computer Use</span>）**：導入 **<span style="color: #38bdf8; font-weight: bold;">Computer Use (電腦使用)</span>** 技術 ─ **在解析口語指令後，AI 能主動至指定網頁操作頁面元件以進行自動化資料搜集**。並透過人機協作（HITL）機制，將任務轉化為「可確認、可修正、可輸出」的視覺化工作流與狀態顏色提示（AI 解析呈淡綠、手動覆寫呈淡金），確保執行前二次確認，避免自主運作失控。
  * **極速 Vibe Coding 實踐**：示範在無傳統爬蟲背景下，利用大模型快速生成 Chrome 外掛代碼，打通「網頁 DOM 解析 ➔ 雙軌 AI 語意提取 ➔ ETL 結構化清洗」的完整端到端採集管線。
* **研究報告與資源下載入口**：
  * [🌐 開啟雙軌 AI 公開資料採集助理](https://falo-taiwan.github.io/skyline-class/class2/demo/ai-parser-demo1/index.html) *(將於新分頁中開啟)*


### 案例五：影片內容分析之成本與效能對抗
* **專案精神**：針對多模態影片分析設計的成本與效能對抗指南，深度對比「原生影片直投大模型」與「自適應抽樣故事板拼圖（Storyboard Grid）」兩種架構，協助企業在影片 OCR 與場景理解中極致降低 Token 成本。
* **技術對比與特點**：
  * **自適應抽樣與故事板拼接**：展示如何透過 OpenCV 進行影片畫面自適應抽樣與時間序列幀插值，將影片畫面拼接成單張高解析度的「故事板網格拼圖」，並以單圖方式送入 Qwen2.5-VL 或 Gemini 3.5 Flash。
  * **97% 成本節省與對抗計算機**：對比原生影片高昂的 Video-to-Token 轉換花費，拼圖法能節省高達 97% 的 API Token 成本與時間延遲；並提供互動式「對抗計算機」，讓架構師量化分析不同解析度、幀率下的性能與費用表現。
* **研究報告入口**：
  * [🌐 開啟影片 AI 內容分析之成本與效效能對抗指南](https://falo-taiwan.github.io/video-analysis-optimization/) *(將於新分頁中開啟)*

### 案例六：LINE 防封鎖訊息變體生成器 ─ PWA 雙效混淆與 Agent 沙盒
* **專案精神**：針對社群行銷與大量通知發送場景設計的雙軌訊息防封鎖工具。整合「傳統演算法混淆」與「Gemini AI 語意改寫」，並特別內建 **Computer Use 智能示範沙盒**，展示未來 AI Agent 透過模擬人類游標移動與參數點擊的自動化操作軌跡，防止因內容高度重複而被 LINE 系統判定洗版封帳。
* **技術對比與特點**：
  * **雙效防封鎖混淆管線**：支援「非 AI 演算法混淆」（零寬字元混淆、標點噪聲、同形字替換）與「Gemini 語意無損改寫」雙軌機制，並自動保留原始連結，生成具備唯一 Hash 值的多樣化訊息變體。
  * **Computer Use 模擬沙盒與 PWA**：提供極具視覺衝擊的模擬游標與 Action Terminal HUD 面板，直觀展示 AI Agent 自動點擊、輸入與調節滑桿之執行軌跡；支援響應式主題切換與離線 PWA 運行。
* **研究報告入口**：
  * [🌐 開啟 LINE 防封鎖訊息變體生成器與 Agent 沙盒](https://falo-taiwan.github.io/computer-use/) *(將於新分頁中開啟)*

### 案例七：從故障到能力包 ─ FALO 精神的案例實踐
* **專案精神**：展示 FALO 如何將日常的技術障礙（如「Chrome 內建 Gemini 智慧側邊欄無法啟用」之故障修復），透過範例學習與遷移學習，解構、提煉並沉澱為一套可教學、可複製、可由 AI Agent 自動執行的「能力包（Capability Pack）」之資產化轉化歷程。
* **技術對比與特點**：
  * **故障排查資產化**：不只解決單一 Chrome Gemini 側邊欄啟用故障，更探討如何將零散的排查步驟，標準化為包含故障重現、根因分析、修復步驟與自動化腳本的體系化資產。
  * **能力包與人機協作（HITL）**：示範如何將技術經驗轉化為人機協作（HITL）框架下的「能力包」，打通「人腦經驗 ➔ 結構化文檔 ➔ Agent 執行指令」的知識遷移路徑。
* **研究報告入口**：
  * [🌐 開啟從故障到能力包 ─ FALO 精神的案例實踐](https://falo-taiwan.github.io/gemini_chrome/) *(將於新分頁中開啟)*

### 案例八：銀河ERP - 憑證下載助手 Hub
* **專案精神**：針對企業差旅報銷流程設計的雙版本自主部署解決方案，提供台鐵購票證明的快速查詢、自訂重命名與一鍵下載服務，解決傳統財務手動處理發票憑證的低效痛點。
* **技術對比與特點**：
  * **雙版本靈活部署**：提供輕量前端無伺服器版（Serverless SPA）與企業後端整合版，滿足不同組織的網絡架構與資訊安全治理規範。
  * **憑證自動化管線**：實現非結構化憑證資料的欄位精準提取（如乘車日期、金額、起訖站），支援自訂重命名規則與批量打包下載，極大簡化財務報銷前的審查與歸檔工作。
* **研究報告入口**：
  * [🌐 開啟銀河ERP - 憑證下載助手 Hub](https://falo-taiwan.github.io/ticket-demo/) *(將於新分頁中開啟)*

---