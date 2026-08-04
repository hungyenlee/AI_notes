#AI #Codex #skill #原始資料卡

## 來源

- AI 對話原始整理
- grill-with-docs / domain-modeling 相關 skill 說明

## 摘要

這份原始資料整理 `grill-me`、`grill-with-docs` 與 `domain-modeling` 的演化關係。它說明追問流程如何從通用計畫盤問，逐步拆分成能維護專案共同語言與文件的工作流。

## 可沉澱的知識卡

- [[認識 grill-with-docs]]
- [[grill-with-docs 讓追問結果沉澱成 CONTEXT.md 與 ADR.md]]
- [[domain-modeling 負責維護專案共同語言與架構決策]]
- [[grill-me 到 domain-modeling 的演化是追問流程與文件化能力拆分]]

## 原始整理

`grill-me` 沒有被完全取代；它是被「拆分、專門化」了。在 codebase 或工程情境裡，`grill-with-docs` 更適合；但一般人生計畫、產品想法、寫作、學習規劃，`grill-me` 還是適合。

## 使用時機

| Skill | 適合使用時機 | 不太適合 |
|---|---|---|
| `grill-me` | 想壓力測試一個計畫、設計、產品想法、學習路線、人生決策 | 已經有 codebase，需要沉澱專案術語與架構決策 |
| `grill-with-docs` | 有 codebase，要邊釐清功能設計，邊更新 `CONTEXT.md`、glossary、ADR | 單純聊天、非工程決策、沒有需要留下文件的討論 |
| `domain-modeling` | 要釐清專案中的 domain terms、ubiquitous language、概念邊界、關係與 ADR | 只是想被追問計畫，不需要建立或修改專案語言 |

## grill-me 為什麼在 codebase 情境被 grill-with-docs 取代

`grill-me` 的核心能力是「追問」。它會一題一題問，直到計畫或設計被釐清。問題是，在真實 codebase 裡，只追問不夠。

Matt Pocock 在 `grill-with-docs` 文章裡提到幾個痛點：

1. AI 會變得囉嗦，因為它不知道專案裡已經有某些既定名詞。
2. 討論中產生了很好的共同語言，但沒有被記錄下來。
3. 每次新 session 都要重新解釋 codebase 和 domain 裡不顯而易見的事情。
4. 他原本同時用 `grill-me` 和 `ubiquitous-language`，但兩個 skill 並行很沒效率。

所以 `grill-with-docs` 的改進是：保留 `grill-me` 的追問流程，但同時把結果寫成文件。它會找或建立 `CONTEXT.md`，釐清 glossary，必要時建立 ADR。這讓 AI 下次可以從專案文件接續理解，而不是每次從零開始。

## 演化脈絡

```text
grill-me
  ↓
grill-me + ubiquitous-language
  ↓
grill-with-docs
  ↓
grilling + domain-modeling
```

更細一點：

1. `grill-me`
   最早是通用的 relentless interview：把你的計畫問到清楚。現在 repo 裡它已經變成很薄的一層：只負責跑 `/grilling`。

2. `ubiquitous-language`
   早期用來整理 DDD 的共同語言，輸出 `UBIQUITOUS_LANGUAGE.md`。後來 deprecated，合併進 `grill-with-docs`。

3. `grill-with-docs`
   把「追問」和「文件化」合在一起。它適合 codebase，會處理 `CONTEXT.md`、bounded context、glossary、ADR。

4. `grilling`
   後來被抽成獨立的核心追問 loop。也就是原本 `grill-me` 的精神被拆出來，變成可重用的底層 skill。

5. `domain-modeling`
   後來被抽成獨立 skill，專門負責建立與維護 domain model：挑戰模糊詞、釐清概念關係、更新 `CONTEXT.md`、必要時寫 ADR。

所以目前比較準確的理解是：

```text
grill-me = 通用追問入口
grilling = 追問流程本體
domain-modeling = 專案語言與決策文件化能力
grill-with-docs = grilling + domain-modeling 的工程版入口
```

## 時間線

| 時間 | 事件 |
|---|---|
| 2026-04-28 | GitHub history 中出現 `grill-me`、`ubiquitous-language`、`grill-with-docs` 相關檔案 |
| 2026-04-30 | AI Hero changelog 說 `ubiquitous-language` 被併入 `grill-with-docs` |
| 2026-05-05 | `grill-with-docs: Align Before You Build` 文章更新或發布 |
| 2026-05-31 | `grilling` 與 `domain-modeling` 被抽成獨立 skill，`grill-with-docs` 變薄 |

## 一句話記法

`grill-me` 是「把想法問清楚」。

`grill-with-docs` 是「把 codebase 裡的想法問清楚，並寫進文件」。

`domain-modeling` 是「維護專案共同語言與架構決策的核心能力」。

## 來源

- [grill-with-docs 文章](https://www.aihero.dev/grill-with-docs.md)
- [常見誤用文章](https://www.aihero.dev/things-people-get-wrong-with-grill-me-and-grill-with-docs.md)
- [Ubiquitous Language -> grill-with-docs changelog](https://www.aihero.dev/skills-changelog-ubiquitous-language-grill-with-docs.md)
- [v1 changelog](https://www.aihero.dev/skills/skills-changelog-v1-announcement)
- [mattpocock/skills repo](https://github.com/mattpocock/skills)
- https://www.aihero.dev/grill-with-docs
