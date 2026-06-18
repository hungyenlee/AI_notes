
我的整理：兩篇其實都不認為「Skill 會完全取代 MCP」，比較接近這個結論：**個人 coding agent 場景，Skill + CLI 會取代很多 MCP；企業、多用戶、跨平台、授權治理場景，MCP 還是有價值。**

## 兩篇文章立場

| 文章 | 核心立場 |
|---|---|
| [愛好 AI 工程：後 MCP 時代](https://blog.aihao.tw/2026/03/12/post-mcp-era-skills-vs-mcp/) | 偏向 Skill。認為在 Claude Code、Codex CLI 這類有 shell / 檔案系統能力的 coding agent 裡，Skills + bash 幾乎能取代大多數 MCP，但 MCP 在 OAuth、有狀態 session、通用標準化整合仍有定位。文章明列 MCP 的 token、server 維護、工具發現成本，也列出 Skills 的非確定性與更新維護問題。 |
| [Shareuhack：MCP 已死？](https://www.shareuhack.com/zh-TW/posts/mcp-vs-skill-vs-cli-guide) | 偏向分層架構。它把 MCP、Skill、CLI 拆成三層：MCP 是「能力層」，Skill 是「流程層」，CLI 是「執行層」。主張三者互補，不是三選一；個人開發者優先 CLI + Skill，企業治理或跨平台分發再用 MCP。 |

## Skill 的優點

| 優點 | 說明 |
|---|---|
| Token 成本低 | Skill 平常只需載入摘要，真正需要時才展開；MCP 常在啟動或連線時把工具 schema 塞進 context。 |
| 維護簡單 | 本質是 Markdown + 可選腳本，不用跑 server、定義 JSON schema、處理 transport。 |
| 很適合教 AI 流程 | 適合放 SOP、code review 標準、工作流、品質規範，也就是「AI 該怎麼做」。 |
| 搭配 CLI 很強 | 如果任務可用 `git`、`gh`、`npm`、`curl`、`psql` 等 CLI 完成，Skill 只要教流程，執行交給 shell。 |
| 適合個人開發者 | 對 side project、個人自動化、coding agent 來說，成本低、上手快、彈性高。 |

## Skill 的缺點

| 缺點 | 說明 |
|---|---|
| 非確定性較高 | Skill 是自然語言指令，Agent 需要自己判斷何時用、怎麼用；同一份 Skill 可能跑出不同路徑。 |
| 失敗模式更多 | MCP 主要是「選錯工具」；Skill 還多了「誤解指令」或「流程推理錯誤」。 |
| 快速變動領域較麻煩 | SDK、API、文件常更新時，Skill 裡的範例與最佳實務要手動同步。 |
| 平台相容性仍不完全一致 | Shareuhack 認為 Skill 目前仍偏 Claude Code 生態；其他平台通常有類似概念，但格式不同。 |
| 不天然解決授權治理 | 多用戶 OAuth、token 保管、租戶隔離、稽核等，Skill 自己不提供標準解。 |

## MCP 的優點

| 優點 | 說明 |
|---|---|
| 標準化工具連接 | MCP 解決的是「AI 能做什麼」：用統一介面連 API、資料庫、雲端服務。 |
| 適合多用戶與企業治理 | OAuth、租戶隔離、權限控管、稽核紀錄，這些是 MCP 的強項。Shareuhack 甚至稱這是 MCP 真正難被取代的場景。 |
| 適合跨平台分發 | 團隊想讓 Cursor、Claude Code、其他 client 都能接同一套工具時，MCP 比各平台各寫一份 prompt 更合理。 |
| 適合無 CLI 的服務 | 像 Notion、Figma、Slack 這類沒有好用 CLI 或 API-only 的服務，現成 MCP server 可能比較省事。 |
| 適合有狀態 session | 互動式 debugger、長連線 session、狀態保存等場景，MCP 抽象比單次 CLI 呼叫自然。 |
| 文件/能力更新可集中管理 | 對快速演進的 SDK 或內部知識庫，MCP 接最新文件或 API，較能維持 single source of truth。 |

## MCP 的缺點

| 缺點 | 說明 |
|---|---|
| Token / schema 開銷大 | 兩篇都提到 MCP 工具 schema 膨脹問題；Shareuhack 引 benchmark 稱 CLI 在 token 效率上可贏 MCP 10-32 倍。 |
| 架 server 與維運成本高 | MCP 要 server process，API 改版、client 相容、連線逾時、部署都會變成成本。 |
| 對個人開發常過度設計 | 很多 MCP 只是包了一層 CLI，對單人本機自動化來說收益不一定抵過複雜度。 |
| 工具發現與管理變複雜 | 工具一多，Agent 要從大量名稱、描述、schema 裡挑對工具，context 也容易被塞滿。 |
| 安全風險更需要治理 | Shareuhack 特別提醒公開 MCP server 的認證不足、供應鏈攻擊、prompt injection 等風險；企業用 MCP 前要做最小權限、來源查驗、獨立驗證。 |

## 一句話結論

如果你是在本機或 coding agent 裡做自己的工作流：**先用 CLI + Skill**。

如果你要做多人、多平台、多租戶、OAuth、企業稽核、無 CLI SaaS 整合：**MCP 還是該上場**。Skill 比較像 SOP 和工作流記憶，MCP 比較像標準化工具插座；它們不是互斥，真正的分界是「流程知識」還是「受治理的工具能力」。

## 參考資料

- [後 MCP 時代：Skills 會取代 MCP 嗎？](https://blog.aihao.tw/2026/03/12/post-mcp-era-skills-vs-mcp/)
- [MCP 已死？MCP vs Skill vs CLI 終極指南](https://www.shareuhack.com/zh-TW/posts/mcp-vs-skill-vs-cli-guide)

## 連結

- [[認識 MCP 與 skill 的分工]]