#AI #Codex #MCP #工具調用 #知識卡

## 一句話

MCP 的執行流程，是讓 Agent 把「我要做某件外部動作」轉成結構化 tool call，再交給有權限的 MCP server 去執行。

## 內容

Agent 接到自然語言任務時，會先判斷這是單純回答，還是需要外部工具。如果任務需要操作外部系統，MCP 的執行流程通常是：Agent 選擇合適工具，將使用者意圖整理成結構化參數，再透過 MCP Client 送給對應的 MCP Server。

以「在 Google Sheet 新增一行」為例，Google Sheet 不是核心主題，只是一個外部動作的例子。真正的重點是：Agent 不直接修改試算表，而是準備 spreadsheet ID、分頁名稱、range、values 等參數，交給 Google Sheets MCP Server，再由 server 呼叫 Google Sheets API 完成寫入。

所以這篇筆記關注的是 MCP tool call 的執行流程：Agent 負責理解任務、選工具與組參數；MCP Server 負責授權、檢查參數、呼叫外部 API 與回傳結果。這讓 Agent 可以用同一種模式操作不同外部系統，例如試算表、文件、瀏覽器、GitHub 或內部服務。

## 連結

- [[認識 MCP]]
- [[MCP server 是 Codex 可連接的工具端點]]
- [[MCP 讓 agent 取得外部工具與上下文]]
- [[MCP 適合需要即時外部資料或動作的任務]]

## 來源

- [[MCP 讓 Agent 透過工具執行外部動作的流程（原始整理）]]
