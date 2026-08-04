#AI #Codex #MCP #知識卡

## 一句話

當任務需要即時資料、外部系統授權或實際執行動作時，MCP 通常比 `AGENTS.md` 或 skill 更適合。

## 內容

`AGENTS.md` 適合放長期規則，例如 repo 慣例、測試要求或回覆偏好。skill 適合封裝可重複的任務流程，例如如何整理試算表、產生簡報或處理 PR review。MCP 則適合處理「agent 必須連到外部世界」的任務。

判斷方式很簡單：如果只是告訴 Codex 怎麼工作，放 `AGENTS.md`；如果是遇到某類任務時要照固定流程做，用 skill；如果需要讀取外部服務、查最新文件、操作瀏覽器、取得私有系統資料，或呼叫第三方 API，就應該考慮 MCP。

MCP 也不一定要單獨存在。plugin 可以打包 MCP server，skill 也可以要求某些 MCP 工具存在。這時候 skill 負責「流程」，MCP 負責「能力」，兩者是互補關係。

## 連結

- [[認識 MCP]]
- [[MCP 讓 agent 取得外部工具與上下文]]
- [[MCP server 是 Codex 可連接的工具端點]]
- [[認識 AGENTS.md]]
- [[認識 skill]]

## 來源

- [Model Context Protocol - Codex | OpenAI Developers](https://developers.openai.com/codex/mcp)
