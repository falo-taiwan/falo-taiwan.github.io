# Class 03：3小時實戰核心課程大綱 (class03_3hr_core.md)

本文件專為 AI 外部記憶與大模型快速检索所編寫，完整涵蓋 Class 03 內訓的 **3 小時實戰核心精華**：工具教學、痛點排除、開發策略與地雲串接範例。

---

## 1. AI 開發工具教學與模式對比

本章對應 Class 03 三大核心開發代理工具，協助學員掌握 Vibe Coding（意念編程）的工具邊界。

| 工具模式 | 核心定位 | 優勢 | 限制與短板 |
| :--- | :--- | :--- | :--- |
| **Gemini Canvas** | 網頁對話式代碼沙盒 | 適合視覺化調整、快速原型開發，介面直觀。 | 長文本對話後上下文易膨脹、代碼容易被整份蓋掉。 |
| **Antigravity / Codex** | 本機自動化執行與修改代理 | 具備規劃 (Plan) 與驗收 (Verify) 閉環，極精密 Diff 修改。 | 依賴本地權限、需要較高的推理模型支持。 |
| **Claude Code** | CLI 終端機開發代理 | 終端對話、多檔案重構、自動執行本地測試與 Git 提交。 | 無圖形化介面，對非工程師學員門檻稍高。 |

---

## 2. Gemini Canvas 常見困擾與解法

在使用網頁版 Gemini Canvas 或 Claude Artifacts 等對話式代碼沙盒時，學員最常遇到以下三個困擾：

### 困擾一：對話太長導致 Context 膨脹、速度變慢與 Token 耗盡
* **解法**：
  1. **程式碼與對話解耦**：將已穩定的代碼存為本地 `.html` 或 `.js` 檔，並另開新對話。
  2. **中斷上下文傳承**：在新對話中，僅將最新的程式碼以 Markdown 區塊或檔案形式餵給 AI，加上指令：「請僅針對以下代碼的邏輯進行修改，不要保留歷史對話記憶」。

### 困擾二：AI 輸出整份程式碼，直接蓋掉人類手動修改的細節
* **解法**：
  1. **限制輸出長度**：明確指定 Prompt：「請只輸出被修改的函數/區塊，其他部分用 `// ... 保持不變 ...` 代替」。
  2. **採用 Diff 修改法**：請 AI 輸出 Git Diff 格式，或轉用地端工具（如 Antigravity），自動進行精確的行級替換。

### 困擾三：網頁端沙盒無法存取本機環境與檔案
* **解法**：
  1. 搭配**地端橋樑**（Python Local Server 或 ngrok 穿透），讓網頁端發送 HTTP Fetch 請求至 localhost，從而操控地端檔案與 shell 指令。

---

## 3. Markdown 與 HTML 雙軌策略

在企業 AI 導入中，我們倡導 **「AI 讀 md，人類讀 HTML」** 的雙軌策略，藉此最大化降低 Token 成本並提升體驗：

* **Markdown (.md) - AI 專用記憶**：
  * **為什麼？** 純文字、無多餘樣式代碼、語意標籤清晰（#、-、*），最適合 LLM 進行語意搜尋（Semantic Search）與上下文理解。
  * **效益**：省下 60% 以上的 HTML 渲染與排版 Token，讓 AI 能快速「抓取並理解」專案脈絡。
* **HTML (.html) - 人類專用視覺**：
  * **為什麼？** 提供 HSL 漸層、霓虹光暈、微動畫與 RWD 響應式排版，給予學員極佳的閱讀體驗。
  * **效益**：易於上課演示、內建程式碼「一鍵複製」按鈕，實用性極高。

---

## 4. Prompt 工程實戰與部署策略

### 4.1 HTML-based UI 生成提示詞 (一鍵刻出 Premium 介面)
```markdown
【提示詞範例】
請為我建立一個獨立的 HTML 網頁。要求：
1. 採用 dark mode 設計，背景使用暗色放射漸層 (radial-gradient)，主色調為紫色 (#8b5cf6) 與藍色 (#3b82f6)。
2. 卡片設計使用玻璃擬態 (glassmorphism)，包含 border: 1px solid rgba(255,255,255,0.08) 與 backdrop-filter: blur(20px)。
3. 所有程式碼區塊旁需配備一鍵複製按鈕，點擊後會顯示「已複製！」並帶有 200ms 的淡入淡出動畫。
4. 使用 Google Fonts 的 Outfit 與 Noto Sans TC。
```

### 4.2 本地除錯 (Localhost) vs GitHub Pages 線上部署 Prompt 調整
當學員將本地網頁上傳至 GitHub Pages 時，常因為**相對路徑**或**安全協定**出錯。
* **路徑問題**：本地打開檔案時，絕對路徑 `file:///` 會失效。必須引導 AI 使用相對路徑（如 `./css/` 或 `../`）。
* **跨域問題 (CORS)**：本地開發時，若前端直接 fetch 外部 API 可能會被瀏覽器阻擋。
  * *本地解法*：使用地端 Python 伺服器並開啟 CORS 標頭。
  * *部署解法*：將 Python 部署至雲端伺服器，或前端改為 fetch Apps Script (GAS) Web App。

---

## 5. 地端 Server 架設實務 (Python 呼叫本地 shell 指令)

在本地開發中，我們可使用 Python 內建的 `http.server` 模組或 Flask，架設一個輕量級的 API 伺服器，讓前端 HTML 網頁能夠遙控本機。

### Python 3 內建輕量級 API Server (免安裝套件)
建立 `local_server.py`：
```python
import http.server
import json
import subprocess
import urllib.parse

class LocalCommandHandler(http.server.BaseHTTPRequestHandler):
    def end_headers(self):
        # 允許跨域請求 (CORS)，讓網頁端 fetch 能正常運作
        self.send_header('Access-Control-Allow-Origin', '*')
        self.send_header('Access-Control-Allow-Methods', 'GET, POST, OPTIONS')
        self.send_header('Access-Control-Allow-Headers', 'Content-Type')
        super().end_headers()

    def do_OPTIONS(self):
        self.send_response(200)
        self.end_headers()

    def do_POST(self):
        if self.path == '/run-command':
            content_length = int(self.headers['Content-Length'])
            post_data = self.rfile.read(content_length)
            data = json.loads(post_data.decode('utf-8'))
            
            command = data.get('command', '')
            print(f"[Executing] {command}")
            
            try:
                # 執行地端指令並獲取回傳值
                result = subprocess.run(command, shell=True, capture_output=True, text=True, timeout=10)
                response = {
                    "status": "success",
                    "stdout": result.stdout,
                    "stderr": result.stderr,
                    "returncode": result.returncode
                }
            except Exception as e:
                response = {"status": "error", "message": str(e)}
                
            self.send_response(200)
            self.send_header('Content-Type', 'application/json')
            self.end_headers()
            self.wfile.write(json.dumps(response).encode('utf-8'))

if __name__ == '__main__':
    server_address = ('127.0.0.1', 8000)
    httpd = http.server.HTTPServer(server_address, LocalCommandHandler)
    print("Local command server running on http://127.0.0.1:8000")
    httpd.serve_forever()
```

### HTML 前端呼叫範例
```html
<button onclick="runLocalCommand('ls -la')">執行本機 ls 指令</button>

<script>
async function runLocalCommand(cmd) {
    try {
        const response = await fetch('http://127.0.0.1:8000/run-command', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ command: cmd })
        });
        const result = await response.json();
        console.log("地端回傳：", result);
        alert(result.stdout || result.message);
    } catch (err) {
        console.error("連線地端失敗：", err);
    }
}
</script>
```

---

## 6. Apps Script (GAS) 雲端對接範例 (Fetch 寫入試算表與寄信)

利用 Google Apps Script (GAS) 可以秒級架設無伺服器 (Serverless) 的後端，直接將前端網頁的資料儲存至 Google 試算表，或串接 Gmail 發送系統通知。

### 6.1 GAS 後端程式碼 (`Code.gs`)
```javascript
function doPost(e) {
  // 設定 CORS 與回傳標頭
  var headers = {
    "Access-Control-Allow-Origin": "*",
    "Access-Control-Allow-Methods": "POST, OPTIONS",
    "Access-Control-Allow-Headers": "Content-Type"
  };
  
  try {
    var jsonString = e.postData.contents;
    var data = JSON.parse(jsonString);
    
    // 1. 寫入活動試算表的第一個工作表
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    sheet.appendRow([
      new Date(), 
      data.studentName || "未提供姓名", 
      data.email || "未提供 Email", 
      data.feedback || "無內容"
    ]);
    
    // 2. 自動發送 Gmail 通知信給學員與講師
    if (data.email) {
      MailApp.sendEmail({
        to: data.email,
        subject: "【銀河 ERP 內訓】我們已收到您的課後回饋",
        htmlBody: "親愛的 " + data.studentName + " 您好：<br><br>系統已成功記錄您的回饋內容：<br>「" + data.feedback + "」<br><br>祝學習愉快！"
      });
    }
    
    var response = { status: "success", message: "資料已成功儲存並發送確認信！" };
    return ContentService.createTextOutput(JSON.stringify(response))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch(error) {
    var errResponse = { status: "error", message: error.toString() };
    return ContentService.createTextOutput(JSON.stringify(errResponse))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
