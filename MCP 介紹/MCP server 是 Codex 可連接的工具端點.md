#AI #Codex #MCP #知識卡

## 一句話

MCP server 是把某個外部能力暴露給 Codex 的端點，Codex 透過設定檔知道要如何連上它。

## 內容

在 Codex 裡，MCP server 通常透過 `config.toml` 註冊。每個 server 會有自己的 `[mcp_servers.<server-name>]` 設定，可以是本機命令啟動的 server，也可以是遠端 HTTP server。設定中也能控制啟用狀態、逾時、允許或停用哪些工具，以及工具呼叫時的 approval mode。

這代表 MCP 不是「把一段說明塞進 prompt」，而是讓 Codex 多了一組可呼叫工具。舉例來說，OpenAI Docs MCP 可以搜尋與讀取官方文件；Playwright 或 Chrome DevTools MCP 可以讓 Codex 檢查瀏覽器；GitHub MCP 則能處理超出 `git` 本身的 GitHub 工作。

## 連結

- [[認識 MCP]]
- [[MCP 讓 agent 取得外部工具與上下文]]
- [[MCP 適合需要即時外部資料或動作的任務]]

## 來源

- [Model Context Protocol - Codex | OpenAI Developers](https://developers.openai.com/codex/mcp)
