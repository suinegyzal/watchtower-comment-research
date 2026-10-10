# Watchtower Study Comment Research Assistant

**English** | [한국어](README.md)

An AI assistant that researches paragraph-by-paragraph comments for the *Watchtower* Study **using wol.jw.org only**. It organizes them into **Basic / Additional / Research** comments.

> This repository is private and visible only to invited people. Please don't share the link or files publicly.

---

## What it does

- Give it an article link, and it prepares three comments for each paragraph:
  - **Basic comment**: 1–2 sentences that directly answer the study question
  - **Additional comment**: 1–2 sentences from another cited scripture or angle in the same paragraph
  - **Research comment**: a point backed by WOL publications, scripture footnotes, *Insight*, and so on, with the source cited
- It researches the way a person would: it types keywords into the WOL search box, opens the results, reads them, and then writes the comments.
- It shows its research trail in a table (search keyword → number of results → material opened → what was found), so you can retrace and verify every step.
- **It never uses sites other than jw.org / wol.jw.org.** Anything it could not confirm is marked "source not confirmed."

> The skill writes its output in Korean by default. To get English output, ask for it, e.g., "answer in English, using the English WOL". The English WOL search URL is `https://wol.jw.org/en/wol/s/r1/lp-e?q=...`.

## Example output

| # | Keyword | Results | Material opened | Finding |
|---|---|---|---|---|
| 1 | 빛의 천사로 가장 ("disguising himself as an angel of light") | 38 | *Insight*, Vol. 1, "Satan" | Satan approaches while "concealing his identity and purpose" |
| 2 | 의심 바다 물결 ("doubt, wave of the sea") | 33 | *Watchtower*, Feb 2021, pp. 26-31 | Doubt is like rust on the chain that holds the anchor |

**Paragraph 1: What does Satan use to try to turn us away from Jehovah?**
- **Basic**: Satan knows he can't win as long as we stay close to Jehovah. So he tries to make us doubt that Jehovah and Jesus love us, so that we turn away ourselves.
- **Additional**: Satan wants us to believe we are "unworthy of love." But Romans 8:38, 39 says nothing can separate us from God's love. (*Watchtower*, Sept 2019, par. 15)
- **Research**: James 1:6 compares a doubter to a wave of the sea. If our hope is an anchor, our faith is the chain attached to it, and doubts left unresolved rust that chain. (*Watchtower*, Feb 2021, pars. 15-16)

---

## How to use

### Option A. Claude (recommended)

**Claude desktop app or claude.ai**
1. Download [`watchtower-comment-research.skill`](watchtower-comment-research.skill) from this repo. Open the file, then use the download button at the top right.
2. In Claude, go to **Settings → Capabilities → Skills** and upload the file.
   - Menu names may vary slightly by app version.
3. In a new chat, ask:
   ```
   This week's Watchtower article: https://wol.jw.org/ko/wol/d/r8/lp-ko/(article id)
   Please prepare Basic, Additional, and Research comments for paragraphs 1–3.
   ```
4. In the Claude desktop app (Code tab), you can watch the research live in the built-in browser pane.

**Claude Code (terminal)**
```bash
git clone https://github.com/suinegyzal/watchtower-comment-research.git
mkdir -p ~/.claude/skills
cp -R watchtower-comment-research/watchtower-comment-research ~/.claude/skills/
```

### Option B. ChatGPT, Gemini, or other AIs

1. Open [`prompts/파수대-해설-조사-프롬프트.md`](prompts/파수대-해설-조사-프롬프트.md) and copy the "프롬프트 본문" (prompt body) section.
2. Paste it into one of these places:
   - **ChatGPT**: Create a custom GPT → Instructions, or use Project instructions.
   - **Gemini**: Create a Gem → Instructions
   - **Other AIs**: paste it as the first message of the chat.
3. **Turn on web search / browsing.** Without it, the AI can't open wol.jw.org.
4. Send the article link with your request.

> Other AIs may not show the research process on screen. In that case, verify the results using the research table and the cited sources.

---

## Tips

- **Start with 2–3 paragraphs at a time.** Asking for all 18 at once makes the research shallow.
- Places where a personal experience would help are marked `[개인 경험]` (personal experience). Fill those in yourself.
- If a comment is too long, ask for it to be "shorter, under 30 seconds."
- **Always do the final check yourself.** Open each cited source on WOL and confirm the context before using a comment.

## Files

```
README.md                         Korean guide
README.en.md                      English guide (this file)
watchtower-comment-research.skill Claude skill package
watchtower-comment-research/      Skill source (SKILL.md, references/wol.md)
prompts/파수대-해설-조사-프롬프트.md   Shareable prompt for other AIs
```

## Notice

- This is a personal tool to help with meeting preparation. It is not an official tool of Jehovah's Witnesses or the Watch Tower Bible and Tract Society.
- Content on jw.org is copyrighted by the Watch Tower Bible and Tract Society of Pennsylvania. Do not copy and redistribute publication content in bulk.
