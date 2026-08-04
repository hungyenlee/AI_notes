#AI #Codex #MCP #知識卡

## 一句話

MCP 讓 AI agent 能透過標準協定取得外部工具與上下文，而不是只依靠模型內部知識或當前 prompt。

## 內容

沒有 MCP 時，agent 的工作主要受限於已放進 context 的資訊、工作區檔案，以及目前可用的內建工具。MCP 的用途，是把外部系統包裝成 agent 可以理解與呼叫的能力，例如文件搜尋、瀏覽器控制、設計稿讀取、錯誤監控、GitHub PR 或 issue 操作。

因此 MCP 比較像「能力連接層」，不是單純的筆記、規則或工作流程。它讓 agent 可以在需要時向外部 server 要資料、執行工具，或取得更貼近當下狀態的上下文。這也解釋了為什麼 MCP 適合處理會變動、需要授權、或必須呼叫外部服務的任務。

## 連結

- [[認識 MCP]]
- [[MCP server 是 Codex 可連接的工具端點]]
- [[MCP 適合需要即時外部資料或動作的任務]]

## 來源

- [Model Context Protocol - Codex | OpenAI Developers](https://developers.openai.com/codex/mcp)
