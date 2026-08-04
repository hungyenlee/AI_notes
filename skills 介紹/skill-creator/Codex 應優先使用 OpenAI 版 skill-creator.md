#AI #Codex #skill #知識卡

## 一句話

在 Codex 裡建立 skill 時，應優先使用 OpenAI 版 `skill-creator`，因為它的流程與術語直接對齊 Codex。

## 內容

OpenAI 版 `skill-creator` 明確描述 skill 如何擴充 Codex 能力，並強調 `SKILL.md` frontmatter 中的 `name` 與 `description` 是 Codex 判斷是否觸發 skill 的核心。它也包含 Codex 取向的建立與驗證流程，例如使用 `init_skill.py` 初始化 skill、使用 `quick_validate.py` 檢查格式，並建議包含 `agents/openai.yaml` 作為 UI metadata。

因此，若目標是在 Codex 中使用，OpenAI 版不是只「技術上可裝」，而是語境最匹配的版本。它更適合作為正式安裝來源，而 Anthropic 版則比較適合作為參考或另存為不同名稱的變體。

## 連結

- [[認識 skill-creator]]
- [[skill-creator 不一定需要下載]]
- [[Anthropic 版 skill-creator 可安裝但不宜直接覆蓋 Codex 版]]
- [[skill 檔案由 SKILL.md 和輔助資源組成]]

## 來源

- [OpenAI skill-creator](https://github.com/openai/skills/tree/main/skills/.system/skill-creator)
- [OpenAI skill-creator SKILL.md](https://raw.githubusercontent.com/openai/skills/main/skills/.system/skill-creator/SKILL.md)
