#AI #MCP #原始資料卡

卡片盒版：[[MCP 讓 Agent 透過工具執行外部動作的流程]]

> 註：Google Sheet 只是這份原始整理中的例子，主題其實是 MCP 如何讓 Agent 把外部動作交給工具執行的流程。

## 來源

- 原始整理：MCP 如何讓 Agent 透過工具執行外部動作

## 摘要

這份原始整理用 Google Sheets 寫入資料作為例子，說明 MCP 在 Agent、MCP client、MCP server 與外部 API 之間扮演的工具呼叫橋梁。它適合作為理解 MCP tool call 流程的來源材料。

## 可沉澱的知識卡

- [[認識 MCP]]
- [[MCP 讓 Agent 透過工具執行外部動作的流程]]
- [[MCP server 是 Codex 可連接的工具端點]]

## 核心概念

MCP 不是讓 Agent 自己直接操作 Google Sheet。

比較精準地說：

> Agent 透過 MCP server，把「新增一行」這類動作交給有 Google Sheets 權限的工具去執行。

## 範例任務

使用者說：

```text
請在 Google Sheet「銷售報表」的「訂單」分頁新增一行：
2026-06-16, Leo, 1200
```

這句話一開始只是自然語言，不是 API call。

## 執行流程

```text
User
  ↓
Agent / Codex
  ↓
MCP Client
  ↓
Google Sheets MCP Server
  ↓
Google Sheets API
  ↓
你的試算表
```

簡化後的流程：

```text
你提出需求
→ Agent 理解任務
→ Agent 判斷需要 Google Sheet 工具
→ Agent 選擇 append row 類工具
→ Agent 把自然語言轉成結構化參數
→ MCP Client 把 tool call 送給 MCP Server
→ MCP Server 呼叫 Google Sheets API
→ Google Sheet 被寫入資料
→ 結果回傳給 Agent
→ Agent 用人話回覆你
```

## Agent 做什麼

Agent 負責理解任務與決策。

它會判斷：

- 這不是單純文字回答。
- 需要操作 Google Sheet。
- 應該使用新增資料的工具。
- 如果沒有 spreadsheet ID，要先搜尋檔案。

可能會先找：

```text
銷售報表
```

找到 spreadsheet ID 後，再新增資料。

## Tool Call 長什麼樣

Agent 會把自然語言轉成類似這樣的結構化參數：

```json
{
  "spreadsheet_id": "abc123...",
  "sheet_name": "訂單",
  "range": "訂單!A:C",
  "values": [
    ["2026-06-16", "Leo", 1200]
  ]
}
```

如果是「新增到最後一行」，通常會用 append 類工具。

如果是「插入第 5 行」，就可能需要 insert rows 或 update values 類工具。

## MCP Client 做什麼

MCP Client 是 Agent 和 MCP Server 中間的通訊層。

它負責把 Agent 決定好的 tool call，用 MCP 協定送給對應的 MCP Server。

可以把它想成：

```text
Agent 決定要做什麼
MCP Client 負責把這個請求送出去
```

## MCP Server 做什麼

Google Sheets MCP Server 負責真正執行工具能力。

它通常會做：

- 檢查參數。
- 檢查授權。
- 呼叫 Google Sheets API。
- 處理錯誤。
- 整理回傳結果。

真正寫入 Google Sheet 的不是 Agent，而是 MCP Server 透過 Google Sheets API 執行。

## Google Sheets API 做什麼

Google Sheets API 是最後真正修改試算表的服務。

新增一行時，概念上會呼叫：

```text
spreadsheets.values.append
```

成功後可能回傳：

```json
{
  "updatedRange": "訂單!A42:C42",
  "updatedRows": 1,
  "updatedCells": 3
}
```

Agent 最後再把這個結果整理成自然語言：

```text
已新增一行到「銷售報表」的「訂單」分頁，位置是 A42:C42。
```

## 角色分工

| 角色 | 負責的事 |
|---|---|
| User | 用自然語言提出需求 |
| Agent / Codex | 理解任務、選工具、組參數 |
| MCP Client | 用 MCP 協定送出 tool call |
| MCP Server | 驗證授權、執行工具、處理 API 回應 |
| Google Sheets API | 真正修改試算表 |

## 最重要的理解

Agent 不是自己直接連 Google Sheet。

Agent 的工作是：

```text
判斷要做什麼
選擇哪個工具
準備工具參數
理解回傳結果
```

MCP Server 的工作是：

```text
真正連到 Google
處理授權
呼叫 API
執行修改
回傳結果
```

一句話記：

> Agent 負責決策，MCP 負責把決策交給工具執行。
