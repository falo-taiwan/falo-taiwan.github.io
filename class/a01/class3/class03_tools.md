# 主題九：Vibe Coding 實戰武器庫與地雲整合工具清單 (class03_tools.md)

本文件盤點並分類 Class 03 所涉及的核心實戰工具，作為學員進行 Vibe Coding、地雲整合與 AI 協同開發時的「武器清單」，並為 Class 04 的系統整合打下工具基礎。

---

## 1. AI 程式開發與原型代理 (Coding & Prototyping)

這組工具用於快速生成代碼、設計前端 UI 原型以及進行地端程式庫的直接操作與重構：

* **Antigravity / ChatGPT Codex**：
  * *定位*：地端自動寫檔、編譯與終端操作代理人。
  * *重點*：掌握規劃（Plan）、任務拆解（Task）與驗收（Verify）的自動化閉環，透過精準 Diff 修改檔案。
* **Claude Code**：
  * *定位*：終端機 CLI 開發代理人。
  * *重點*：直接在終端機與本地代碼庫進行多檔案重構、執行測試與自動生成 Git Commit。
* **Claude Artifacts / v0.dev**：
  * *定位*：前端視覺化原型設計工具。
  * *重點*：一鍵生成 HTML 靜態原型或 React UI 元件，提供直觀的視覺驗收。

---

## 2. 知識工程與即時研究 (Knowledge & Research)

這組工具用於在開發前進行需求整理、資料分析以及系統規格研究：

* **NotebookLM**：
  * *定位*：專案知識庫與知識煉油廠。
  * *重點*：將 legacy 程式碼、SQL DDL、ERP 手冊等「原油」丟入，提煉出 FAQ、中文心智圖與背景規格。
* **Perplexity**：
  * *定位*：AI 搜尋引擎與技術瀏覽器。
  * *重點*：即時查閱最新的 API 規格、第三方套件改版資訊與故障排除偏方。

---

## 3. 地雲整合與通信橋樑 (Integration & Bridging)

這組工具用於連接前端網頁、雲端服務以及地端作業系統，實現完整的前後端數據通信：

* **Google Apps Script (GAS) & HTML + GAS**：
  * *定位*：輕量級雲端 Serverless 後端。
  * *重點*：利用 HTML 發送 Fetch API，直接將網頁資料寫入 Google 試算表，或串接 Gmail 自動寄信，實現地雲對接。
* **地端 HTML Server & Python 呼叫**：
  * *定位*：本地 full-stack 控制架構。
  * *重點*：使用 HTML 前端作為 UI 控制面板，呼叫本地 Python 伺服器（如 Flask/FastAPI）執行本機的 shell 指令、檔案批次處理或 OCR 辨識。
* **ngrok / LocalTunnel**：
  * *定位*：地端測試與 Webhook 穿透工具。
  * *重點*：將地端的 `localhost` 連接埠映射為公開的 HTTPS 網址，以便接收 LINE Bot 訊息或外部 ERP 系統的 Webhook 回傳通知。
