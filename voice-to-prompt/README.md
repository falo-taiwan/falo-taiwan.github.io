# Falo_ModelBox

## GitHub Pages 測試入口：Voice-to-Prompt Browser Workbench

公開識別：Falo x Force Cheng  
日期：2026/5/6  
語言/地區：zh-Hant / Taiwan

這次新增一個可直接上 GitHub Pages 測試的 Voice-to-Prompt Workflow MVP。

目前本地版本：`v102 (v1.02)`，尚未推送。

- 預計公開 URL：`https://falo-taiwan.github.io/voice-to-prompt/`
- Pages 首頁入口：[`index.html`](index.html)
- 主工作台：[`content/dish-assets/html/voice-to-prompt-mvp.html`](content/dish-assets/html/voice-to-prompt-mvp.html)
- Single-file HTML 說明頁：[`content/dish-assets/html/voice-to-prompt-browser-workbench-note.html`](content/dish-assets/html/voice-to-prompt-browser-workbench-note.html)
- Markdown 說明：[`docs/mvp/voice-to-prompt-browser-workbench.md`](docs/mvp/voice-to-prompt-browser-workbench.md)

這個 MVP 用來展示：

```text
錄音 / 上傳音檔
→ 瀏覽器內轉錄
→ AI 或本地規則後處理
→ 手動選 Prompt Template
→ 產生可執行 Prompt
```

主頁已補入明文署名、SEO meta、Open Graph / Twitter meta 與 geo meta，方便 GitHub Pages 測試與分享。

Falo_ModelBox 不是一般的程式倉庫。

它的第一用途，是登錄與整理「模型菜」。
它的第二用途，是逐步長成一套可展示、可教學、可查詢、可出版的「模型菜百科全書系統」。

## 1. 專案定位摘要

可以把 Falo_ModelBox 理解成：

一個用來登錄、整理、出版與擴充「模型菜」的百科型知識系統。

更進一步說，它是一套：

多視角可重組的知識圖譜索引。

它像 CM 的近親，但不以「收納」為主要目標，而是以：

- 條目化
- 分類化
- 關聯化
- 展示化
- 教學化
- 出版化

為核心方向。

## 2. 什麼是模型菜

在本專案中，模型菜不是單一 prompt，也不是零碎點子。

它更像是一個已經具有基本成形度的 AI 應用單位，通常具備：

- 明確用途
- 核心流程
- 模組結構
- 人機分工
- 展示與教學價值
- 未來產品化或顧問化的可能

一句話理解：

模型菜是介於點子、知識卡、系統設計、產品雛形之間的結構化單位。

## 3. 關鍵設計原則

Falo_ModelBox 不採用「唯一父節點」的固定樹狀結構。

同一筆條目在不同情境下，可能同時是：

- 某個系統的頂層
- 另一個系統的子模組
- 教學視角下的案例主題
- 產品視角下的方案元件

因此原始資料應優先保存：

- 穩定節點
- 結構化 relations
- perspective 視角

階層只是關係投影出來的結果，不是資料本體。

## 4. 第一階段目標

目前先不做大型平台，先把骨架打穩。

第一階段聚焦在 4 件事：

1. 建立模型菜登錄庫（Registry）
2. 建立模型菜百科條目格式（Entry Schema）
3. 建立模型菜分類系統（Taxonomy）
4. 建立可轉為網站、教材、展示頁的內容底稿

## 5. 建議目錄結構

```text
Falo_ModelBox/
├─ README.md
├─ docs/
│  ├─ architecture/
│  │  └─ project-positioning.md
│  ├─ schema/
│  │  ├─ model-dish-entry.schema.yaml
│  │  ├─ model-dish-entry-template.md
│  │  ├─ relation-types.md
│  │  ├─ perspectives.md
│  │  ├─ entry-writing-guidelines.md
│  │  └─ golden-entry-guidelines.md
│  └─ mvp/
│     └─ mvp-direction.md
├─ taxonomy/
│  └─ model-dish-taxonomy.yaml
└─ content/
   ├─ dish-assets/
   │  ├─ progress-index.md
   │  ├─ workflow-log.md
   │  ├─ markdown/
   │  └─ html/
   ├─ registry/
   │  └─ model-dishes.yaml
   └─ model-dishes/
      ├─ examples/
      │  ├─ falo-capture-board.md
      │  ├─ agent-coach-workbench.md
      │  └─ knowledge-to-course-engine.md
      ├─ golden/
      │  ├─ ai-logging-shell.md
      │  └─ local-data-hub.md
      └─ real/
         ├─ news-exploration-knowledge-flow-system.md
         ├─ ai-logging-shell.md
         ├─ local-data-hub.md
         ├─ prompt-asset-manager.md
         └─ trusted-session-governance.md
```

## 6. 目錄用途

- `docs/architecture/`
  放專案定位、設計原則、系統邊界。
- `docs/schema/`
  放條目欄位規格與模板。
- `docs/mvp/`
  放第一階段 MVP 的範圍與取捨。
- `taxonomy/`
  放分類法、主題樹、標籤規則。
- `content/registry/`
  放總索引，類似目錄表。
- `content/model-dishes/`
  放每一筆模型菜條目本體。
- `content/dish-assets/`
  放模型菜內容資產、Markdown 主記憶、Single-file HTML 展示版與工作紀錄。
  這裡不是 DB，也不是 docs；它是未來可接 Falo Web / CMS 的內容資產層。

## 7. 最小可行版本（MVP）方向

第一版先做「內容系統 MVP」，不是「平台 MVP」。

最小可行版本只需要能做到：

1. 新增一筆模型菜條目
2. 用固定 schema 描述它
3. 依分類與標籤進行整理
4. 用 relations + perspective 描述它和其他節點的關係
5. 在 registry 中建立索引
6. 讓條目可直接轉為 README、網頁文案或教材草稿

也就是先把「知識底稿」做對，再決定之後要不要接網站、搜尋、前端展示。

## 8. 下一步建議

如果要繼續往下做，建議順序是：

1. 先確認 schema 與 taxonomy 是否符合你的教學語境
2. 再挑 3 到 10 道真實模型菜進來試填
3. 試著用不同 perspective 生成不同目錄
4. 從試填結果修正欄位、分類與 relation types
5. 最後再決定要不要加上靜態網站、搜尋頁或展示頁

## 9. 目前已建立的起始文件

- [專案定位文件](/Users/force/AI-CodeX/Falo_ModelBox/docs/architecture/project-positioning.md)
- [Relation-First 資料模型](/Users/force/AI-CodeX/Falo_ModelBox/docs/architecture/relation-first-model.md)
- [模型菜條目 Schema 草案](/Users/force/AI-CodeX/Falo_ModelBox/docs/schema/model-dish-entry.schema.yaml)
- [模型菜條目模板](/Users/force/AI-CodeX/Falo_ModelBox/docs/schema/model-dish-entry-template.md)
- [Relation Types 字典](/Users/force/AI-CodeX/Falo_ModelBox/docs/schema/relation-types.md)
- [Perspectives 字典](/Users/force/AI-CodeX/Falo_ModelBox/docs/schema/perspectives.md)
- [條目寫作規範](/Users/force/AI-CodeX/Falo_ModelBox/docs/schema/entry-writing-guidelines.md)
- [Golden Entry 指南](/Users/force/AI-CodeX/Falo_ModelBox/docs/schema/golden-entry-guidelines.md)
- [MVP 方向文件](/Users/force/AI-CodeX/Falo_ModelBox/docs/mvp/mvp-direction.md)
- [分類系統草案](/Users/force/AI-CodeX/Falo_ModelBox/taxonomy/model-dish-taxonomy.yaml)
- [模型菜登錄索引](/Users/force/AI-CodeX/Falo_ModelBox/content/registry/model-dishes.yaml)
