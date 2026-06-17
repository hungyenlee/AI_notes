標籤：#AI #AI-agent #Claude-Code #索引筆記

## 核心問題

Claude Code 術語文章裡提到的概念，哪些可以幫助理解通用 AI agent，哪些只是 Claude Code 的產品實作名稱？

## 相關卡片

- [[認識 prompt、context、memory]]
- [[context 太長時會因壓縮而流失細節]]
- [[認識 MCP]]
- [[認識 skill]]
- [[AI agent 工具概念]]
- [[認識 harness]]

## 初步理解

這篇 HackMD 雖然以 Claude Code 為主題，但裡面許多術語其實能幫助理解 Codex 和其他 coding agent，例如 prompt、context window、tool use、agentic loop、MCP、skill、hook、subagent、compaction 等。

閱讀時要分清楚兩層：第一層是通用概念，也就是 AI agent 為了完成任務，會讀上下文、使用工具、連接外部資料、拆分任務並在過程中壓縮資訊；第二層是產品名稱，例如 `CLAUDE.md`、`.claude/rules/`、Claude Code 的 slash commands、allowedTools、checkpoint 或 Agent Teams。這些在 Codex 裡可能有相似功能，但不一定用同一個檔名、設定方式或操作流程。

所以這篇適合當成「AI agent 術語入口」，而不是只當 Claude Code 教學。整理時應優先吸收可跨工具通用的概念，再另外標註 Claude Code 與 Codex 的對應差異。

## 離線整理版

以下是原文重點的改寫整理，不是逐字備份。目標是讓原連結失效時，仍能看懂這篇文章主要介紹了哪些概念。

### AI 基礎概念

| 術語 | 白話理解 | 通用性 |
|---|---|---|
| LLM | 大型語言模型，是 AI agent 推理、理解文字、產生回覆的核心模型。 | 通用 |
| Token | AI 處理文字時使用的基本單位，也常是 API 計費與 context 長度計算的單位。中文、英文、符號轉成 token 的方式不完全一樣。 | 通用 |
| Prompt | 使用者這次給 AI 的問題、指令或任務要求。 | 通用，對應 [[prompt 是使用者這次給 AI 的任務指令]] |
| System Prompt | 在使用者輸入之前就給模型的高優先權指令，用來設定角色、限制、行為準則或產品規則。 | 通用，但每個產品呈現方式不同 |
| Context Window | 模型一次回答時能看到的資訊上限。對話、文件、工具結果、系統規則都會佔用 context。 | 通用，對應 [[context 是 AI 當下能參考的資料包]] |
| Agentic Loop / ReAct Pattern | Agent 常用的工作循環：先思考下一步，呼叫工具或採取行動，觀察結果，再決定下一步。 | 通用 |
| Tool Use / Function Calling | 模型不只產生文字，還能呼叫工具，例如讀檔、搜尋、查資料庫、執行命令或修改檔案。 | 通用 |

### Claude Code 產品層概念

| 術語 | 白話理解 | Codex 對應或注意 |
|---|---|---|
| Claude Code | Anthropic 的命令列 coding agent，可以在專案中讀檔、寫程式、跑命令、管理 Git。 | Codex 是 OpenAI 的 coding agent，概念相近但產品不同 |
| `CLAUDE.md` | Claude Code 的專案指令檔，用來記錄專案慣例、風格、測試方式與偏好。 | Codex 對應概念是 `AGENTS.md` |
| Rules | Claude Code 中可拆分管理的規則檔，讓指令不必全部塞在單一 `CLAUDE.md`。 | Codex 有 `AGENTS.md`、rules、config 等相近機制，但路徑與規則不同 |
| Slash Commands | 用 `/` 觸發的快捷命令，例如清理、切換模式、提交或自訂流程。 | Codex 也有 slash commands，但命令名稱與功能不完全相同 |
| Permissions / allowedTools | 控制 agent 可以自動做什麼、哪些動作要先問使用者，例如執行命令或改檔案。 | Codex 對應 sandbox、approval policy、permissions |
| Statusline | Claude Code 底部顯示狀態的資訊欄，例如模型、token、context 使用量等。 | Codex 也會呈現狀態資訊，但 UI 不同 |
| Auto-compact / Compaction | 當 context 太長時，把舊內容摘要成較短版本，讓 thread 可以繼續。 | 通用概念，對應 [[context 太長時會因壓縮而流失細節]] |
| Checkpoint | 在重要修改前建立可回復的狀態，方便出錯時回到先前版本。 | Codex 有 Git/worktree/patch 等工作流，但不是同名功能 |

### 擴展機制

| 術語 | 白話理解 | 通用性 |
|---|---|---|
| MCP | Model Context Protocol，讓 agent 用標準方式連接外部工具、資料源和服務。 | 通用，對應 [[認識 MCP]] |
| Skills | 可重複使用的任務能力包，包含指令、流程、參考資料或腳本。 | 通用概念；Claude Code 與 Codex 的資料夾位置和 metadata 規則不同 |
| Hooks | 在特定事件前後自動執行的確定性腳本，例如改檔後格式化、命令前做檢查。 | 通用概念；各產品設定方式不同 |
| Plugins | 把 skills、hooks、commands、MCP 等能力打包，方便安裝與分享。 | 通用概念；Codex 也有 plugin |
| Subagent | 從主 agent 拆出去的子任務執行者，有自己的 context，做完後回傳摘要或結果。 | 通用概念；Codex 也支援 subagent 工作流 |

### MCP 細項

| 術語 | 白話理解 | 備註 |
|---|---|---|
| MCP Server | 實作 MCP 的服務端，負責把某個外部能力暴露給 agent。 | 例如 GitHub、文件搜尋、資料庫、瀏覽器、設計工具 |
| MCP Tool | MCP server 提供的可呼叫功能，例如建立 issue、查詢資料、抓取文件。 | agent 會依任務判斷是否呼叫 |
| MCP Resource | MCP server 提供的可讀資料，例如檔案、schema、設定或應用狀態。 | 偏向「讀取資料」而不是「執行動作」 |
| MCP Prompt | MCP server 提供的提示模板，讓使用者或 agent 快速啟動某類任務。 | 有些 client 會把它呈現成快捷命令 |
| JSON-RPC | MCP 底層使用的訊息格式之一，定義 client 和 server 如何交換請求與回應。 | 一般使用者不一定需要深入 |

### Agent 系統

| 術語 | 白話理解 | Codex 對應或注意 |
|---|---|---|
| Agent | 不只是回答問題，而是能規劃、用工具、觀察結果並完成任務的 AI 系統。 | 通用 |
| Subagent Types | Claude Code 中不同任務類型的子代理人，例如探索、規劃、一般任務、命令執行、程式碼審查。 | Codex 也可以有不同 agent 角色，但名稱與設定不同 |
| Agent Teams | 多個 Claude Code 實例協作，各自有 context，可以互相溝通與分工。 | 偏 Claude Code 特定功能；Codex 有 subagents、多執行緒、worktree 等相近工作流 |
| Task | 用來啟動子代理人或分派任務的工具。 | 通用概念，但產品介面不同 |
| Plan Mode | 先探索與規劃，暫時不直接修改檔案或執行高風險動作。 | 通用工作模式；Codex 也有規劃導向流程 |
| TaskList / TaskCreate / TaskUpdate | 用任務清單追蹤多步驟工作的進度。 | Codex 裡常見對應是 plan / task list 類工具 |

### 進階功能

| 術語 | 白話理解 | 注意 |
|---|---|---|
| Fast Mode | 讓回覆速度更快的模式。原文把它描述成同模型的快速輸出策略。 | 這類產品功能會變，需查 Claude 官方文件 |
| Extended Thinking | 讓模型在回答前投入更多推理資源，通常適合複雜 debug、架構設計或長任務。 | 通用概念；不同模型和產品名稱不同 |
| Adaptive Thinking | 依問題難度自動調整推理深度。 | 偏 Claude / Anthropic 模型功能，需查官方最新文件 |
| Worktree | Git 的隔離工作目錄，讓多個任務可以在同一 repo 的不同工作樹中並行。 | 通用 Git 概念；Codex app 也常用 worktree |
| Headless Mode | 沒有互動 UI，透過指令、SDK 或自動化流程在背景執行 agent。 | 通用自動化概念 |
| Auto Memory | 跨對話保存偏好或專案知識的記憶功能。 | 通用產品概念；Codex 對應 [[Codex memory 預設不會自動永久記錄]] |
| Model Selection | 在不同能力、速度、成本的模型之間切換。 | 通用；具體模型名稱、價格與可用性會變 |

## 三個容易混淆的選擇

### Skills、Hooks、MCP 怎麼分？

- Hooks 適合確定性的自動動作，例如每次改檔後格式化。
- Skills 適合可重複的工作方法，例如固定格式的文件產生流程。
- MCP 適合連接外部系統，例如查 GitHub、Jira、資料庫、瀏覽器或內部文件。

簡單記法：Hooks 偏自動化事件，Skills 偏任務流程，MCP 偏外部能力。

### Subagent 和 Agent Teams 怎麼分？

Subagent 比較像把一個明確子任務交出去，做完回傳結果；Agent Teams 比較像多個常駐 agent 分工協作，適合更複雜、需要持續溝通的任務。前者比較輕，後者成本與協調複雜度較高。

### Context window 滿了怎麼辦？

常見方法包括：主動壓縮、開新對話、把研究型工作交給 subagent、把穩定規則寫進指令檔，以及在重要節點保留可回復狀態。對 Codex 來說，也要注意 thread compaction 後細節可能流失。

## 對 Codex 的翻譯表

| Claude Code 名詞 | Codex 中可類比的概念 |
|---|---|
| `CLAUDE.md` | `AGENTS.md` |
| `.claude/rules/` | Codex rules / `AGENTS.md` 分層 / config |
| allowedTools / Permissions | sandbox、approval policy、permissions |
| Skills | Codex skills |
| Hooks | Codex hooks |
| MCP Server | Codex MCP server / connector / app |
| Plan Mode | 規劃階段、Plan mode、只讀探索流程 |
| Auto Memory | Codex Memories |
| Worktree | Codex worktree / Git worktree |

## 需要日後查證的部分

原文中提到的模型名稱、價格、token 數、Fast Mode、Adaptive Thinking、Agent Teams 狀態等，都屬於會隨產品更新而變動的資訊。若要做決策或教學，應再查 Claude / Anthropic 或 Codex 官方文件。

## 來源

- [Claude Code 術語大全：Agent、MCP、Skills、Hooks，一篇搞懂 38 個 AI 開發關鍵詞](https://hackmd.io/@BASHCAT/Hk5IjaLdbg)

## 其他相關網站
- https://codelove.tw/@tony/post/anNeea