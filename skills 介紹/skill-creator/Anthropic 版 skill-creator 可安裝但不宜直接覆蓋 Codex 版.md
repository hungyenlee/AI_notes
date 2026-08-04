#AI #Codex #skill #知識卡

## 一句話

Anthropic 版 `skill-creator` 技術上可以安裝到 Codex，但它主要對齊 Claude 生態，因此不宜直接覆蓋 Codex 的 `skill-creator`。

## 內容

Anthropic 版 `skill-creator` 也是完整 skill 資料夾，不只是單一 `SKILL.md`。它包含 `agents/`、`assets/`、`eval-viewer/`、`references/`、`scripts/` 等資源，所以技術上可以放進 `~/.codex/skills/`。

但它的內容明顯是為 Claude / Anthropic 工作流設計，會提到 Claude、Claude Code、`claude-with-access-to-the-skill`、Claude 的 skill triggering，以及 Anthropic 的 eval / benchmark 流程。若直接覆蓋 Codex 版，可能讓 Codex 套用不完全適合自己的流程。較好的做法是把它當參考，或改名為 `anthropic-skill-creator`，並修改 frontmatter 的 `name`，避免與 Codex 版撞名。

## 連結

- [[認識 skill-creator]]
- [[Codex 應優先使用 OpenAI 版 skill-creator]]
- [[skill-creator 不一定需要下載]]

## 來源

- [Anthropic skill-creator](https://github.com/anthropics/skills/tree/main/skills/skill-creator)
- [Anthropic skill-creator SKILL.md](https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md)
