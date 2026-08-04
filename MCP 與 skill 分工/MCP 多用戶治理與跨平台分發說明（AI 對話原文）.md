#AI #MCP #對話原文 #原始資料卡

## 來源

- Codex 對話：2026-06-18

## 摘要

這份對話原文說明 MCP 在多用戶、企業治理與跨平台分發情境中的價值。它的核心不是 MCP 比 skill 更聰明，而是 MCP 能把工具能力放在可授權、可稽核、可分發的受控邊界裡。

## 可沉澱的知識卡

- [[認識 MCP 與 skill 的分工]]
- [[MCP 適合多用戶與企業治理]]
- [[MCP 適合跨平台工具分發]]

## 說明

以下保存 2026-06-18 對話中，針對「MCP 的多用戶與企業治理、跨平台分發」所做的說明原文。這份檔案不是原子卡，而是依照要求保留的對話材料。

## 原文

可以。這兩個優點其實都不是「MCP 比 Skill 聰明」，而是 **MCP 比較像一個可治理、可分發的工具介面標準**。它的價值在組織尺度出現，個人本機使用時反而常顯得笨重。

**1. 適合多用戶與企業治理**

假設你做一個 SaaS 產品，讓每個客戶可以對 AI 說：

> 幫我查這個客戶在 Stripe 的付款狀態  
> 幫我整理我 Google Drive 裡這個專案的文件  
> 幫我查公司 CRM 裡某個 deal 的進度

這時問題不是「AI 會不會查 API」，而是：

- 這次操作代表哪一位使用者？
- 這位使用者有沒有權限看這筆資料？
- OAuth token 放在哪裡？
- token 過期怎麼刷新？
- 這次查詢要不要留下 audit log？
- 如果 AI 想刪資料，誰負責擋？
- 不同租戶的資料如何隔離？
- 公司資安政策如何統一套用？

這些就是「企業治理」。

如果只用 Skill + CLI，通常比較像：

> Agent 繼承目前執行環境的權限，照 Skill 裡的流程跑指令。

這對個人很方便，但對企業很危險。因為企業不希望 AI 只是「拿到一把本機鑰匙後到處跑」，而是希望所有工具呼叫都經過可控的邊界。

MCP server 可以扮演這個邊界：

```text
AI Client
  ↓
MCP Server
  ↓
權限檢查 / OAuth / audit log / policy / rate limit
  ↓
Stripe / Google Drive / Salesforce / internal DB
```

所以 MCP 的優點不是「比較省 token」，而是它能把工具能力包成一個受控服務。企業可以集中管理誰能用、能用哪些工具、能讀哪些資料、哪些操作要審核。

一個具體例子：

你做一個「AI 財務助理」，每個客戶都要連自己的 Stripe。  
如果用 Skill + CLI，你很難安全地替每個使用者保管 OAuth token，也很難保證 A 公司不會讀到 B 公司的資料。  
如果用 MCP，MCP server 可以幫每個使用者維護授權狀態，工具呼叫時帶著正確的使用者身份，並在 server 端做租戶隔離與紀錄。

所以「多用戶與企業治理」的重點是：**MCP 適合把 AI 工具能力產品化、服務化、權限化。**

**2. 適合跨平台分發**

跨平台分發指的是：你寫一次工具整合，很多不同 AI client 都能用。

例如公司想做一個內部知識庫工具，讓 AI 可以查：

- Confluence
- Notion
- Google Drive
- GitHub issues
- 內部 PostgreSQL
- 公司自建 API

如果不用 MCP，你可能要為不同平台各寫一套：

```text
Claude Code: 寫 Skill
Cursor: 寫 .cursorrules 或 extension
GitHub Copilot: 寫 copilot instructions / extension
ChatGPT: 寫 connector 或 actions
內部 agent: 寫自家 tool schema
```

這會變成多份整合邏輯、多份文件、多份維護成本。

MCP 的想法是：

```text
同一個 Internal Wiki MCP Server
  ├─ Claude Code 可接
  ├─ Cursor 可接
  ├─ VS Code agent 可接
  ├─ 內部 agent 可接
  └─ 其他支援 MCP 的 client 可接
```

也就是「工具寫一次，給多個 AI client 用」。

這就是為什麼文章說 MCP 像 USB-C。你不需要替每台裝置設計不同插頭，而是大家約定一個介面。

Skill 在這裡的問題是：Skill 比較像「某個 agent 怎麼工作的說明書」。它常常跟平台能力綁在一起，例如 Claude Code 的 Skill、Cursor 的 rules、Copilot 的 instructions。概念類似，但格式、觸發方式、工具能力、檔案結構不一定相同。

所以跨平台場景下：

- **Skill** 適合傳遞流程與規範：例如「查資料時先看內部 wiki，再看 GitHub，再整理成摘要」。
- **MCP** 適合提供共同工具能力：例如「查內部 wiki」「查 CRM」「讀資料庫」這些能力本身。

**簡單對比**

| 問題 | Skill / CLI 比較適合 | MCP 比較適合 |
|---|---|---|
| 我自己在本機開發，要自動化流程 | 是 | 通常太重 |
| 我要教 AI 遵守團隊 code review 流程 | 是 | 不必要 |
| 我要讓 AI 用 `git`、`gh`、`npm` | 是 | 多半多此一舉 |
| 我要讓 500 個員工用 AI 查內部系統 | 不太適合 | 是 |
| 我要保管每個使用者的 OAuth token | 不太適合 | 是 |
| 我要限制不同角色能查不同資料 | 不太適合 | 是 |
| 我要讓 Claude、Cursor、內部 agent 都用同一套工具 | 麻煩 | 是 |
| 我要留下工具呼叫紀錄與稽核軌跡 | 要自己補很多 | 是 |

**更白話的判斷**

如果你是在問：

> AI 要怎麼做這件事？

那通常是 Skill 的領域。

如果你是在問：

> AI 可以安全地代表誰、用什麼權限、透過哪個標準介面去操作外部系統？

那就比較像 MCP 的領域。

所以那兩個優點其實都指向同一件事：**MCP 的價值不在個人效率，而在組織級工具治理與標準化分發。**
