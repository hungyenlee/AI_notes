標籤：#AI #MCP #工具整合

## 一句話

MCP 適合跨平台工具分發，因為同一個 MCP server 可以被多個支援 MCP 的 AI client 共用。

## 內容

若公司想讓 Claude Code、Cursor、VS Code agent、內部 agent 都能查同一套內部 wiki、CRM 或資料庫，不使用 MCP 時往往要為每個平台各自寫一份整合方式。Claude Code 可能用 skill，Cursor 可能用 rules，Copilot 或內部 agent 又有自己的 tool schema。這會造成多份邏輯、多份文件與多份維護成本。

MCP 的價值在於提供共同插座。公司可以維護一個 Internal Wiki MCP Server，讓不同 client 透過同一套協議使用它。skill 仍可負責各平台上的工作流程與品質規範，但外部工具能力本身可以由 MCP 統一提供。

## 連結

- [[認識 MCP 與 skill 的分工]]
- [[Skill 適合流程知識而 MCP 適合工具能力]]
- [[MCP 適合多用戶與企業治理]]
- [[MCP server 是 Codex 可連接的工具端點]]

## 來源

- [MCP 已死？Skill 和 CLI 取代不了的三個場景](https://www.shareuhack.com/zh-TW/posts/mcp-vs-skill-vs-cli-guide)
- 對話：2026-06-18 關於 MCP 跨平台分發的說明
