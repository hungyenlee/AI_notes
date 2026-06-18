標籤：#AI #CLI #skill

## 一句話

個人開發者若只是自動化自己的工作，通常應先考慮 CLI 加 skill，而不是先架 MCP。

## 內容

個人使用 coding agent 時，很多任務本來就可以用本機 CLI 完成，例如 `git`、`gh`、`npm`、`curl`、`psql` 或檔案系統操作。這時 skill 只需要提供流程、規範與判斷標準，執行層交給 agent 呼叫既有命令即可。

這種做法的優點是上下文成本低、維護簡單，也不需要額外維運 server。MCP 在這裡常顯得太重，尤其當 MCP 只是把 CLI 指令包成工具 schema 時，收益不一定抵得過 token、安裝、連線與工具發現成本。

## 連結

- [[認識 MCP 與 skill 的分工]]
- [[Skill 不會完全取代 MCP]]
- [[Skill 適合流程知識而 MCP 適合工具能力]]

## 來源

- [後 MCP 時代: Skill 取代 MCP 嗎?](https://blog.aihao.tw/2026/03/12/post-mcp-era-skills-vs-mcp/)
- [MCP 已死？Skill 和 CLI 取代不了的三個場景](https://www.shareuhack.com/zh-TW/posts/mcp-vs-skill-vs-cli-guide)
