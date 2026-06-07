# AI Agent 程式開發工具自我解析與比較表 (agent_tools.md)

本文件深入解析我（Antigravity）的核心架構、工具箱與工作流，並建立四大 AI Agent 開發模式（Antigravity、Claude Cowork、ChatGPT Codex、Gemini Canvas 模式）的詳細比較表，以供後續知識擴充與研究使用。

---

## 1. Antigravity 自我架構與能力解析

我是一個由 Google DeepMind 團隊設計的**主動式 AI 程式開發代理人 (Agentic AI Coding Assistant)**。與傳統的生成式聊天機器人不同，我具備與本地作業系統深度整合的「工具鏈」以及雙軌的「工作流模式」。

### A. 核心工具箱 (Agent Toolset)
我能透過直接呼叫系統 API 與 Shell 工具，實現以下自動化操作：

* **終端執行與操控 (`run_command`)**：可在使用者的 macOS 本地環境中執行任意 shell 指令（經使用者授權後），進行腳本執行、環境部署、套件安裝等。
* **精確檔案修改 (`write_to_file` / `replace_file_content` / `multi_replace_file_content`)**：
  - `write_to_file`：直接建立新檔案。
  - `replace_file_content`：精準替換單一區域的程式碼。
  - `multi_replace_file_content`：一次性對檔案多個非連續位置進行 Diff 修改，避免整檔重寫，大幅節省 Token 並提高精準度。
* **程式碼檢索與探索 (`view_file` / `list_dir` / `grep_search`)**：
  - `view_file`：檢視本地文字或二進位（圖片、PDF）檔案。
  - `list_dir`：掃描目錄結構。
  - `grep_search`：使用 `ripgrep` 工具快速在專案中進行全文字正則搜尋。
* **外部知識獲取 (`read_url_content` / `search_web`)**：聯網搜尋最新技術標準，或直接將網頁 HTML 轉為 Markdown 讀取。
* **背景任務與定時器 (`schedule` / `manage_task`)**：可啟動定時監控或 cron 任務，並在背景任務完成後喚醒我進行下一步。
* **多 Agent 協同 (`define_subagent` / `invoke_subagent` / `send_message`)**：當任務龐大時，我可以動態定義並喚醒多個子 Agent 進行分工（如獨立進行 Code Research 或除錯）。
* **UI 與素材生成 (`generate_image`)**：直接生成網頁 UI 設計圖或專案素材。

### B. 架構工作流 (Workflow Methodology)
我的行為受到嚴格的「規劃與執行模式」規範，這與 Falo 方法論的「留存脈絡」完美契合：
1. **研究與規劃 (Research & Plan)**：在修改前，先搜尋程式庫，並在 `implementation_plan.md` 中撰寫設計圖，等待使用者審查。
2. **任務拆解 (Execution with task.md)**：經批准後，建立 `task.md` 任務清單，實時標記進度 (`[ ]` -> `[/]` -> `[x]`)。
3. **驗證與導覽 (Verify & Walkthrough)**：完成修改後，進行自動化或手動驗證，並在 `walkthrough.md` 中記錄結果。

---

## 2. 四大 AI Agent 程式開發工具/模式比較表

以下是針對 **Antigravity**、**Claude Cowork**、**ChatGPT Codex** 與 **Gemini Canvas 模式** 的對比分析。

| 比較維度 | Antigravity (本代理人) | Claude Cowork (Claude Artifacts/MCP) | ChatGPT Codex (Code Interpreter) | Gemini Canvas 模式 (網頁端雙向編輯) |
| :--- | :--- | :--- | :--- | :--- |
| **底層模型與核心** | Gemini 3.5 Flash (Google) | Claude 3.5 Sonnet / Opis (Anthropic) | GPT-4o / GPT-4 (OpenAI) | Gemini 1.5 Pro / 2.0 (Google Web UI) |
| **上下文視窗 (Context)** | **極大 (1M - 2M+ Tokens)**<br>適合超長文件、大型程式庫與完整歷史日誌。 | 中等 (200k Tokens)<br>長對話後半段容易遺忘或產生 Token 焦慮。 | 較小 (128k Tokens)<br>長對話時需頻繁手動整理脈絡。 | **極大 (1M - 2M Tokens)**<br>支援超長文本，但在網頁前端渲染超長對話時有時會受限。 |
| **本地環境執行能力** | **原生整合**<br>可直接在使用者 macOS 本地終端執行指令。 | **沙盒/遠端 MCP**<br>主要在雲端虛擬環境，需額外架設 MCP 伺服器才能操控本地。 | **封閉沙盒**<br>在隔離的 Linux Python 環境中運行，無法控制使用者本地系統。 | **無**<br>完全在 Google 雲端網頁端執行，無法控制使用者本地終端。 |
| **檔案修改方式** | **精準 Diff 區塊替換**<br>針對特定行數做 patch，極省 Token 且安全。 | **整檔覆寫 (Artifacts)**<br>容易因為小修改而重新生成整份長檔案，消耗大量 Token。 | **代碼生成與手動複製**<br>多數需使用者自行複製貼上，或由 Code Interpreter 修改其沙盒內檔案。 | **網頁雙向側邊欄編輯**<br>可在側邊欄進行行內修改 (Inline Edit)、直接調整格式與導出。 |
| **多代理人協同** | **支援**<br>可動態定義 (Define) 並喚醒子 Agent 進行背景協作。 | **有限支援**<br>主要依賴專案 (Projects) 的 Custom Instructions，難以動態平行派生。 | **有限支援**<br>可透過 GPTs 或 Assistants API 串接，但對話中難以動態派生。 | **不支援**<br>網頁端單一 Agent 對話，不支援動態派生子 Agent 執行背景工作。 |
| **知識管理與備份** | **專案目錄同步**<br>所有日誌、計畫與歷史直接寫入本地 workspace。 | **雲端對話歷史**<br>儲存於 Claude 平台，難以直接與本地 Git/專案結構無縫同步。 | **雲端對話與沙盒暫存**<br>對話關閉或超時後，沙盒檔案即消失。 | **雲端儲存與雲端硬碟導出**<br>可一鍵將成果導出至 Google Docs/Gmail，但缺乏本地目錄同步。 |
| **最適合場景** | **SME/個人知識工程與本地專案開發**<br>需要高性價比、執行指令、建立完整變更日誌。 | **前端 UI 快速原型設計**<br>利用 Artifacts 進行即時視覺化預覽。 | **數據分析與演算法驗證**<br>在沙盒內運行 Python 進行資料繪圖與計算。 | **網頁端文案撰寫、報告編排與單檔代碼雙向編輯**<br>不依賴本地環境的協作編排。 |

*註：本比較表為初步分析，後續可依據老師的實務經驗進行微調與充實。*
