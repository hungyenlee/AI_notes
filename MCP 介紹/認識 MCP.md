標籤：#AI #Codex #MCP #索引筆記

## 核心問題

MCP 是什麼？它如何讓 Codex 連接外部工具、資料源與執行環境？

## 相關卡片

- [[MCP 讓 agent 取得外部工具與上下文]]
- [[MCP server 是 Codex 可連接的工具端點]]
- [[MCP 適合需要即時外部資料或動作的任務]]
- [[MCP 讓 Agent 透過工具執行外部動作的流程]]
- [[認識 MCP 與 skill 的分工]]
- [[MCP 適合多用戶與企業治理]]
- [[MCP 適合跨平台工具分發]]
- [[AGENTS.md 會先組成指令鏈而 skill 會按需讀取]]
- [[認識 skill]]

## 初步理解

MCP 是 Model Context Protocol，重點是讓 agent 不只依靠 prompt 和本地檔案，而能透過標準協定連到外部工具與上下文。對 Codex 來說，MCP server 可以提供搜尋文件、讀取設計稿、操作瀏覽器、查 GitHub issue、讀 Sentry log 等能力。它和 `AGENTS.md`、skill 的差異在於：`AGENTS.md` 提供長期規則，skill 提供可重複流程，MCP 則提供可被呼叫的外部能力。

## 來源

- [Model Context Protocol - Codex | OpenAI Developers](https://developers.openai.com/codex/mcp)
