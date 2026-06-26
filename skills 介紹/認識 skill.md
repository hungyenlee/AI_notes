標籤：#AI #Codex #skill #卡片盒

這是一張關於 Codex skill 的索引筆記。它不試圖一次說完所有內容，而是把「認識 skill」拆成幾張可以彼此連結、日後擴充的卡片。

## 核心問題

skill 是什麼？它如何讓 AI agent 在特定任務中取得可重複使用的工作方法？

## 相關卡片

- [[skill 是 AI agent 的可重複任務能力]]
- [[建立 skill 需要先定義觸發情境]]
- [[AI agent 先看 skill 描述 再按需讀取內容]]
- [[AGENTS.md 會先組成指令鏈而 skill 會按需讀取]]
- [[skill 檔案由 SKILL.md 和輔助資源組成]]
- [[SKILL.md 的資料夾結構與撰寫模板]]
- [[認識 grill-me]]
- [[認識 skill-creator]]
- [[自己寫 skill、請 AI 寫 skill 與用 skill-creator 寫 skill 的差異]]
- [[認識 MCP 與 skill 的分工]]
- [[Skill 不會完全取代 MCP]]
- [[Skill 適合流程知識而 MCP 適合工具能力]]

## 初步理解

如果 `AGENTS.md` 比較像「這個專案裡的長期工作規則」，那 skill 比較像「遇到某一類任務時可以拿出來用的作業手冊」。

skill 通常不是單純的說明文件，而是 agent 在需要時會讀取並遵循的任務流程。它的價值不在於把所有知識塞進 context，而是讓 agent 先根據 metadata 判斷是否需要使用，等任務真的符合時，再讀取完整流程、參考資料、腳本或模板。
