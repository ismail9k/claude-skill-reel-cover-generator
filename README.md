# Reel Cover Generator — Agent Skill

<center><img alt="Claude Desktop step 1" src="img/header.png" width="100%" /></center>

Generate professional, branded Instagram Reel cover images (9:16) from a video script — powered by Claude and Gemini.

Built for Arabic and English tech content creators who want scroll-stopping covers without opening a design tool.

## Table of Contents

- [Features](#features)
- [How It Works](#how-it-works)
- [Installation](#installation)
  - [Claude Code](#claude-code)
  - [Claude Desktop](#claude-desktop)
- [Usage](#usage)
- [Visual Themes](#visual-themes)
- [Customization](#customization)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Script-aware** — reads your reel script, detects its language (Arabic or English), and summarizes it
- **Smart title suggestions** — generates 3 title options in the script's language; pick one or write your own
- **Optional subtitles** — generates 3 subtitle options; pick one, write your own, or skip it entirely
- **Theme matching** — automatically picks a visual theme (AI, cybersecurity, breaking news, etc.) based on your script's topic
- **Prompt preview** — shows the final image prompt before generating, so you can copy it to another tool or continue with Claude
- **Photo integration** — blends your photo naturally into a cinematic 9:16 cover via Gemini
- **Iterative refinement** — tweak colors, titles, or visual effects and regenerate until it's perfect

> **Note:** The skill talks to you in **English**. Only the cover text (title/subtitle) follows the script's language.

## How It Works

```
Script  ──>  Analyze & Summarize  ──>  Pick a Title  ──>  Pick a Subtitle
                                                                │
         Done! <──  Refine if Needed  <──  Generate Cover  <──  Review Prompt
```

1. **Analyze** — the skill reads your script, detects the language, summarizes it, and suggests a visual theme
2. **Title** — you get 3 title suggestions in the script's language; pick one or provide your own
3. **Subtitle** — same for subtitles (or skip this step)
4. **Prompt review** — the full image generation prompt is shown for your approval
5. **Choose your path** — copy the prompt for another tool, or continue with Claude
6. **Generate** — provide your photo, and the skill generates a cinematic 9:16 cover via Gemini
7. **Refine** — ask for tweaks until the cover is exactly right

## Installation

### Prerequisites

To have Claude generate cover images, you need to connect it to Gemini via MCP. This requires a 

**Gemini API key** — get one for free at [Google AI Studio](https://aistudio.google.com/app/apikey).

**Gemini MCP** - check the api here [@houtini/gemini-mcp](https://github.com/houtini/gemini-mcp) to call Gemini's image generation API.

> **Don't want to set up Gemini?** The skill still works — it will generate a ready-to-use image prompt that you can copy into any other image generation tool. You just won't be able to generate the cover directly within Claude.

---

### Claude Code

#### Step 1 — Install the skill

**Option A — via `claude install-skill` (recommended):**

```bash
claude install-skill github.com/ismail9k/skill-reel-cover-generator
```

**Option B — via Skills CLI:**

```bash
npx skills add ismail9k/skill-reel-cover-generator
```

Verify it was installed:

```bash
npx skills list
```

#### Step 2 — Configure Gemini MCP

Add the following to `~/.claude/settings.json` (global) or `.mcp.json` (per-project):

```json
{
  "mcpServers": {
    "gemini": {
      "command": "npx",
      "args": ["-y", "@houtini/gemini-mcp"],
      "env": {
        "GEMINI_API_KEY": "your-gemini-api-key"
      }
    }
  }
}
```

Restart Claude Code after saving so it picks up the new MCP server.

---

### Claude Desktop

#### Step 1 — Install the skill

Claude Desktop doesn't support the Skills CLI, so install manually:

1. Download the skill zip from this repo (or clone it locally)
2. Go to **Customize > Skills > Create skill > Upload a skill**

<center><img alt="Claude Desktop step 1" src="img/claude-desktop-step-1.png" width="600px" /></center>

3. Upload the zip file

<center><img alt="Claude Desktop step 2" src="img/claude-desktop-step-2.png" width="600px" /></center>

#### Step 2 — Configure Gemini MCP

1. Go to **Settings > Developer > Edit Config** to open `claude_desktop_config.json`
2. Add the `mcpServers` block:

```json
{
  "mcpServers": {
    "gemini": {
      "command": "npx",
      "args": ["-y", "@houtini/gemini-mcp"],
      "env": {
        "GEMINI_API_KEY": "your-gemini-api-key"
      }
    }
  }
}
```

3. Save the file and **restart Claude Desktop**

## Usage

Trigger the skill by:

- Dropping a script and asking for a **"reel cover"**
- Or running `/reel-cover-generator`

### Quick example

```
You: Here's my script about Claude's usage limits:
     "كل يوم بستخدم Claude وفجأة بيقولي خلاص..."
     Make me a reel cover.

Skill: Analyzes > suggests 3 titles > suggests 3 subtitles > shows prompt > generates cover
```

### Language handling

| Script language | Conversation | Title/Subtitle |
|-----------------|-------------|----------------|
| Arabic          | English     | Arabic (Egyptian dialect where natural) |
| English         | English     | English |
| Mixed           | English     | Follows dominant language |

## Visual Themes

The skill picks the best theme automatically based on your script's topic. Here's the full palette:

| Theme | Best for | Visual style |
|-------|----------|--------------|
| `ai-futuristic` | AI tools, LLMs, future tech | Dark background, glowing neon blue/purple circuits |
| `cybersecurity` | Hacking, data leaks, privacy | Dark red/black, broken shields, code overlays |
| `breaking-news` | Announcements, releases, shocking facts | Bold typography, red accent, high contrast |
| `vs-comparison` | Tool comparisons, A vs B content | Split screen feel, dual tones, versus typography |
| `educational` | Explainers, how-it-works, tutorials | Clean, modern, bright with tech diagrams |
| `opinion-hot-take` | Opinions, controversial takes | Flame/spark aesthetics, bold text, energetic |
| `weekly-recap` | Weekly AI/tech roundups | Magazine-style layout, multiple visual elements |

### Example titles by theme

<details>
<summary><strong>Arabic examples</strong></summary>

| Script topic | Theme | Title | Subtitle |
|---|---|---|---|
| Claude usage limits | `ai-futuristic` | "Claude بيقولك لا؟ عرفت ليه" | "Usage Limits Explained" |
| NVIDIA GTC announcement | `breaking-news` | "NVIDIA غيرت قواعد اللعبة" | "GTC 2025" |
| OpenAI vs Gemini | `vs-comparison` | "مين أحسن؟ الحقيقة اللي محدش بيقولها" | "OpenAI vs Gemini" |
| Cybersecurity breach | `cybersecurity` | "اتهكر بدون ما تعرف" | "تحذير أمني" |
| Weekly AI recap | `weekly-recap` | "أهم أخبار الـAI الأسبوع ده" | "AI Weekly" |
| How transformers work | `educational` | "الـAI بيفكر إزاي؟ الحقيقة جوا" | "Deep Dive" |
| Controversial AI take | `opinion-hot-take` | "رأيي في الـAI هيزعلك" | "رأي صريح" |

</details>

<details>
<summary><strong>English examples</strong></summary>

| Script topic | Theme | Title | Subtitle |
|---|---|---|---|
| Claude usage limits | `ai-futuristic` | "Why Claude Said No To Me" | "Usage Limits Explained" |
| NVIDIA GTC announcement | `breaking-news` | "NVIDIA Just Changed Everything" | "GTC 2025" |
| OpenAI vs Gemini | `vs-comparison` | "The Truth Nobody Tells You" | "OpenAI vs Gemini" |
| Cybersecurity breach | `cybersecurity` | "You Got Hacked and Don't Know It" | "Security Warning" |
| Weekly AI recap | `weekly-recap` | "This Week in AI — Big Moves" | "AI Weekly" |
| How transformers work | `educational` | "How AI Actually Thinks" | "Deep Dive" |
| Controversial AI take | `opinion-hot-take` | "My AI Take Will Upset You" | "Hot Take" |

</details>

## Customization

The skill is fully editable. Open `SKILL.md` to:

- Change the watermark handle (default: `@ismail9k`)
- Add new themes to the theme reference table
- Adjust the image generation prompt template
- Modify the quality checklist

## Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request if you'd like to:

- Add new visual themes
- Improve prompt templates
- Add support for more languages
- Fix bugs or improve documentation

## License

MIT
