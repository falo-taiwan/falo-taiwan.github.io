# Shortlink 404 Router

這份文件專門說明 shortlink 的 `404.html` router。

它的角色不是一般內容頁，而是：

- GitHub Pages 的 fallback router
- `/go/<slug>` 的入口中轉頁
- `GAS + Google Sheets` 與 `links.json` 之間的橋接層

一句話理解：

- 使用者打短網址
- `404.html` 接手判斷
- 先問 GAS
- 不行再 fallback `links.json`

## 0. 這次版本的重要發現

這一版最重要的實務發現是：

- shortlink 失敗，不一定代表資料不存在
- 很多時候，真正原因是 `timeout`

這次實測發現：

- GAS 其實有資料
- 但如果 router 等待時間太短
- 使用者仍然會看到找不到或 fallback 失敗

所以目前的設計原則是：

- 只有 `/go/<slug>` 這類 shortlink 路徑才放寬等待時間
- 其他非 shortlink 路徑仍保持快速反應
- 若仍失敗，就用更明確的 error code 告訴使用者發生了什麼

## 1. 這個 404.html 是做什麼的

這份 [404.html](/Users/force/AI-CodeX/tools/shortlink/404.html) 不是單純顯示「找不到頁面」。

在這個 shortlink 專案裡，它負責：

1. 接管 GitHub Pages 上未知路徑
2. 專門處理 `/go/<slug>`
3. 先查 GAS lookup API
4. 若 GAS 沒在時限內回傳可用結果，再 fallback 到 `links.json`
5. 找到目標網址後，立即 redirect

所以它其實是：

- router
- shortlink 入口執行層
- fallback 控制點

## 2. 工作流程

整體流程如下：

1. 使用者打開 `https://your-site/go/demo`
2. GitHub Pages 把這個未知路徑交給網站 root 的 `404.html`
3. `404.html` 解析 slug，也就是 `demo`
4. 先呼叫 GAS lookup
5. 若 GAS 回傳 `status=ok` 且 `target` 合法
   - 直接跳轉
6. 若 GAS timeout、格式錯誤、找不到、或回傳不可用
   - 改查網站 root 的 `links.json`
7. 若 `links.json` 也找不到
   - 顯示 `Shortlink not found`

一句話版：

- GAS 是主資料源
- `links.json` 是 published snapshot / fallback
- `404.html` 是中間的決策層

## 3. 專案中的定位

這份檔案在專案中的定位是：

- 專案內唯一維護來源：
  - [404.html](/Users/force/AI-CodeX/tools/shortlink/404.html)
- 網站上線時的部署位置：
  - 網站 root 的 `/404.html`

也就是說：

- 平常只改 shortlink 專案內這一份
- 要上線時，再手動部署到網站 root

## 4. 為什麼要用 404.html

GitHub Pages 不是完整後端系統，不能像一般 web app 那樣自由做 routing。

但 GitHub Pages 有一個很重要的行為：

- 當路徑不存在時，會回到 `404.html`

所以這個設計的本質是：

- 把 GitHub Pages 的 `404.html`
- 變成 shortlink 的 router

這樣就能在靜態站裡做到：

- `/go/abc`
- `/go/demo`
- `/go/news`

這種看起來像動態 shortlink 的入口。

## 5. 目前支援的 lookup 順序

目前 router 依序做三層判斷：

1. GAS JSONP lookup
2. GAS fetch lookup
3. fallback `links.json`

這樣做的原因是：

- 某些瀏覽器或 App 內建瀏覽器，對跨網域 fetch 比較嚴格
- JSONP 在某些情況下反而更穩
- 若 GAS 仍失敗，還可以退回 published snapshot

## 6. 目前支援的結果畫面

### 成功跳轉

若找到 shortlink，畫面會短暫顯示：

- `Redirecting...`

並顯示：

- slug
- 來源
- target
- router 版本時間

### 找不到

若 GAS 與 fallback 都沒有該 slug，畫面會顯示：

- `Shortlink not found`

### 查詢失敗

若查詢過程出錯，畫面會顯示：

- `Shortlink lookup failed`

並附上更明確的 error code。

## 7. Error Code 設計

這份 router 目前已補上較明確的錯誤碼，方便教學、除錯與截圖判讀。

常見類型如下：

### 路徑問題

- `GO_SLUG_MISSING`
  - `/go/` 後面沒有 slug

### GAS JSONP

- `GAS_JSONP_TIMEOUT`
- `GAS_JSONP_SCRIPT_ERROR`
- `GAS_JSONP_INVALID_RESPONSE`
- `GAS_JSONP_NOT_FOUND`
- `GAS_JSONP_ERROR`

### GAS fetch

- `GAS_FETCH_TIMEOUT`
- `GAS_FETCH_403`
- `GAS_FETCH_500`
- `GAS_FETCH_INVALID_RESPONSE`
- `GAS_FETCH_NOT_FOUND`
- `GAS_FETCH_ERROR`

### fallback JSON

- `FALLBACK_NOT_FOUND`
- `FALLBACK_LOAD_ERROR`
- `FALLBACK_ERROR`

### router 本身

- `SHORTLINK_NOT_FOUND`
- `ROUTER_INVALID_JSON`
- `ROUTER_RUNTIME_ERROR`

## 8. 版本確認方式

為了方便確認網站是否已經部署最新版 router，
中轉頁會顯示：

- `Router Updated: YYYY-MM-DD HH:MM TPE`

例如：

- `Router Updated: 2026-03-27 20:13 TPE`

這個時間不是裝飾，而是部署確認點。

如果你線上看到的不是最新時間，
通常代表：

- 網站 root 的 `404.html` 還沒更新
- 或瀏覽器快取還沒刷新

## 9. 部署方式

這份檔案的建議工作方式是：

1. 在本機維護：
   - [404.html](/Users/force/AI-CodeX/tools/shortlink/404.html)
2. 同步更新：
   - [404-readme.md](/Users/force/AI-CodeX/tools/shortlink/404-readme.md)
3. 確認版本時間與邏輯正確
4. 手動上傳到網站 root：
   - `/404.html`
5. 線上重新測試

## 10. 建議測試網址

部署後建議至少測這幾種：

### 正常命中

- `/go/demo`
- `/go/g1`
- `/go/pch3`
- `/go/n1`

### 找不到

- `/go/notfound`

### 非 shortlink 路徑

- `/abc`

## 11. 與其他模組的關係

這份 router 不是孤立存在，它和整個 shortlink 系統的關係如下：

### 主資料源

- Google Sheets
- GAS lookup API

### 備援資料源

- 網站 root 的 `links.json`

### 維護工具

- [falo-shortlink-json-editor-v105.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v105.html)

一句話理解：

- editor 負責維護資料
- GAS 負責提供主查詢
- `404.html` 負責入口跳轉
- `links.json` 負責保底

## 12. 維護原則

這份 router 的維護原則建議如下：

1. 只維護 shortlink 專案內這一份來源檔
2. 每次修改都更新版本時間
3. 每次修改 `404.html`，同步更新 `404-readme.md`
4. 每次部署後都實測 `/go/<slug>`
5. 不把商業邏輯拆太散，先保留 single-file 可維護性
6. 優先讓錯誤可判讀，再追求更複雜功能
7. 每次修改 router timeout、lookup 流程或錯誤文案時，都同步更新這份說明

## 13. 目前檔案位置

- Router source：
  - [404.html](/Users/force/AI-CodeX/tools/shortlink/404.html)
- Router README：
  - [404-readme.md](/Users/force/AI-CodeX/tools/shortlink/404-readme.md)
- Shortlink project README：
  - [README.md](/Users/force/AI-CodeX/tools/shortlink/README.md)
- GAS template：
  - [gas-v2/main.gs](/Users/force/AI-CodeX/tools/shortlink/gas-v2/main.gs)

## 14. 一句話總結

這份 `404.html` 不是「錯誤頁」，
而是 shortlink 系統裡最前面的入口控制器。
