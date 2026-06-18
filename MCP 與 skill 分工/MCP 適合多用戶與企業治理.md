標籤：#AI #MCP #企業治理

## 一句話

MCP 適合多用戶與企業治理，因為它能把 AI 的工具呼叫放進權限、授權、稽核與租戶隔離的受控邊界。

## 內容

企業場景中的問題通常不是 AI 會不會呼叫 API，而是 AI 代表誰、能看哪些資料、是否能執行危險操作，以及操作紀錄能否被追蹤。若一個 SaaS 產品讓不同客戶用 AI 查 Stripe、Google Drive 或 CRM，每個使用者都有自己的 OAuth token、資料範圍與角色權限，不能只讓 agent 繼承某個本機環境的權限。

MCP server 可以成為 AI client 與外部系統之間的治理層。它集中處理 OAuth、token 保管、租戶隔離、最小權限、rate limit、policy check 與 audit log。這讓 AI 工具能力可以被產品化與服務化，而不是變成一把難以控管的本機鑰匙。

## 連結

- [[認識 MCP 與 skill 的分工]]
- [[Skill 不會完全取代 MCP]]
- [[MCP 讓 agent 取得外部工具與上下文]]
- [[MCP 適合跨平台工具分發]]

## 來源

- [MCP 已死？Skill 和 CLI 取代不了的三個場景](https://www.shareuhack.com/zh-TW/posts/mcp-vs-skill-vs-cli-guide)
- 對話：2026-06-18 關於 MCP 多用戶與企業治理的說明
