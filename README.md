# Reel Cover Generator — Agent Skill

Generate professional, branded Instagram Reel cover images (9:16) from a video script. Designed for Arabic and English tech content creators.

**What it does:**
- Reads your reel script, detects its language, and summarizes it
- Suggests **3 title options** (in the script's language) — pick one or write your own
- Suggests **3 subtitle options** — pick one, write your own, or skip it
- Picks a matching visual theme (AI, cybersecurity, breaking news, etc.)
- Shows you the **final image prompt** for review — copy it into another tool, or let Claude continue
- If you continue with Claude: asks for your photo, then generates a cinematic 9:16 cover via Gemini

> **Note:** All conversation with you happens in **English**. Only the cover text (title/subtitle) follows the script's language.

## Prerequisites

This skill uses **Gemini image generation** to produce the cover. Make sure the [@houtini/gemini-mcp](https://github.com/houtini/gemini-mcp) server is installed and configured before using the skill.

## Installation

### Using Skills CMD

Any agent that supports the Skills CLI can install this skill:

```bash
npx skills add ismail9k/claude-skill-reel-cover-generator
```

Verify it was installed:

```bash
npx skills list
```

### Manually (no command line)

If you're not comfortable with the terminal, you can install the skill by copying the files into Claude's skills folder:

1. **Download the skill**
   - Go to [https://github.com/ismail9k/skill-reel-cover-generator](https://github.com/ismail9k/skill-reel-cover-generator)
   - Click the green **Code** button → **Download ZIP**
   - Unzip the downloaded file — you'll get a folder named `skill-reel-cover-generator`

2. **Open the Claude skills folder**
   - **macOS:** Open Finder, press `Cmd + Shift + G`, paste `~/.claude/skills` and press Enter
   - **Windows:** Open File Explorer, paste `%USERPROFILE%\.claude\skills` in the address bar and press Enter
   - If the `skills` folder doesn't exist yet, create it

3. **Move the skill into place**
   - Drag the unzipped `skill-reel-cover-generator` folder into the `skills` folder
   - The final path should look like: `~/.claude/skills/skill-reel-cover-generator/SKILL.md`

4. **Restart Claude**
   - Close and reopen Claude Code (or your Claude client) so it picks up the new skill

That's it — you can now use the skill by asking for a "reel cover" or running `/reel-cover-generator`.


## Usage

Once installed, trigger the skill by:

- Dropping a script and asking for a **"reel cover"**
- Or running `/reel-cover-generator`

**The skill will:**
1. Analyze your script — detect the language, summarize it, suggest a theme
2. Offer **3 title suggestions** — pick one or provide a custom title
3. Offer **3 subtitle suggestions** — pick one, provide a custom one, or skip it
4. Build the final image generation prompt and show it to you for review
5. Let you choose: **copy the prompt** to use elsewhere, or **continue with Claude**
6. If continuing: ask for your photo, generate the cover via Gemini, and offer refinements

**Language handling:** The skill talks to you in English. The cover text itself follows the script's language — Arabic scripts get Egyptian-dialect Arabic titles, English scripts get punchy English titles.

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

## Customization

The skill is fully editable. Open `SKILL.md` to:

- Change the watermark handle (default: `@ismail9k`)
- Add new themes to the theme reference table
- Adjust the image generation prompt template
- Modify the quality checklist

## License

MIT
