# Reel Cover Generator — Agent Skill

Generate professional, branded Instagram Reel cover images (9:16) from a video script. Designed for Arabic and English tech content creators.

**What it does:**
- Reads your reel script and extracts a punchy title (Arabic or English)
- Picks a matching visual theme (AI, cybersecurity, breaking news, etc.)
- Integrates your photo naturally into a cinematic cover
- Outputs a 9:16 portrait image ready to publish

---

## Prerequisites

This skill uses **Gemini image generation** to produce the cover. Make sure the [Gemini MCP server](https://github.com/google-gemini/gemini-cli-mcp) is installed and configured before using the skill.

---

## Installation

### Skills CLI (Claude Code, Cursor, Windsurf, Gemini CLI, and more)

Any agent that supports the Skills CLI can install this skill:

```bash
npx skills add ismail9k/skill-reel-cover-generator
```

Verify it was installed:

```bash
npx skills list
```

---

### Claude Desktop

Claude Desktop doesn't have a Skills CLI, so install manually:

**Step 1 — Open the skill panel**

Go to **Customize → Skills → Create skill → Upload a skill**

![Claude Desktop step 1](img/claude-desktop-step-1.png)

**Step 2 — Upload the skill file**

Upload the skill zip file downloaded from this repo.

![Claude Desktop step 2](img/claude-desktop-step-2.png)

---

## Usage

Once installed, trigger the skill by:

- Dropping a script and asking for a **"reel cover"**
- Or running `/reel-cover-generator`

**The skill will:**
1. Analyze your script and extract a title and visual theme
2. Ask for your photo
3. Generate the cover via Gemini
4. Offer refinements if needed

**Language-aware:** Arabic scripts get Egyptian-dialect Arabic titles; English scripts get punchy English titles. The skill detects the language automatically.

---

## Visual Themes

| Theme | When to use | Visual style |
|-------|-------------|--------------|
| `ai-futuristic` | AI tools, LLMs, future tech | Dark background, glowing neon blue/purple circuits |
| `cybersecurity` | Hacking, data leaks, privacy | Dark red/black, broken shields, code overlays |
| `breaking-news` | Announcements, releases, shocking facts | Bold typography, red accent, high contrast |
| `vs-comparison` | Tool comparisons, A vs B content | Split screen feel, dual tones, versus typography |
| `educational` | Explainers, how-it-works, tutorials | Clean, modern, bright with tech diagrams |
| `opinion-hot-take` | Opinions, controversial takes | Flame/spark aesthetics, bold text, energetic |
| `weekly-recap` | Weekly AI/tech roundups | Magazine-style layout, multiple visual elements |

---

## Example Output Titles

### Arabic

| Script topic | Theme | Title |
|---|---|---|
| Claude usage limits | `ai-futuristic` | "Claude بيقولك لا؟ عرفت ليه" |
| NVIDIA GTC announcement | `breaking-news` | "NVIDIA غيرت قواعد اللعبة" |
| OpenAI vs Gemini | `vs-comparison` | "مين أحسن؟ الحقيقة اللي محدش بيقولها" |
| Cybersecurity breach | `cybersecurity` | "اتهكر بدون ما تعرف 🚨" |
| Weekly AI recap | `weekly-recap` | "أهم أخبار الـAI الأسبوع ده" |

### English

| Script topic | Theme | Title |
|---|---|---|
| Claude usage limits | `ai-futuristic` | "Why Claude Said No To Me" |
| NVIDIA GTC announcement | `breaking-news` | "NVIDIA Just Changed Everything" |
| OpenAI vs Gemini | `vs-comparison` | "The Truth Nobody Tells You" |
| Cybersecurity breach | `cybersecurity` | "You Got Hacked and Don't Know It 🚨" |
| Weekly AI recap | `weekly-recap` | "This Week in AI — Big Moves" |

---

## Customization

The skill is fully editable. Open `SKILL.md` to:

- Change the watermark handle (default: `@ismail9k`)
- Add new themes to the theme reference table
- Adjust the image generation prompt template
- Modify the quality checklist

---

## License

MIT
