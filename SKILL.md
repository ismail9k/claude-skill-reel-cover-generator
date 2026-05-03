---
name: reel-cover-generator
description: Generate Instagram Reel cover images (9:16 portrait format) from a script. Use this skill whenever the user provides a reel/video script and wants a cover image, thumbnail, or visual for it. Also trigger when the user says "غلاف الريل", "cover للسكريبت", "thumbnail", "reel cover", or asks to generate an image for their content. The skill reads the script, extracts a title and visual theme, asks for reference image assets, then generates a polished, branded 9:16 cover image in Arabic/tech style.
---

# Reel Cover Generator

Generate professional, branded Instagram Reel cover images for tech content. The cover must be 9:16 portrait orientation, visually striking, and match the mood/topic of the provided script.

**Language rules — important:**
- **All communication with the user is in English.** Every question, confirmation, and status update you write to the user must be English, regardless of the script's language.
- **The generated title/subtitle follow the script's language.** If the script is Arabic, titles are Arabic (Egyptian dialect where natural). If English, titles are English. The *cover text* matches the script; the *conversation* stays in English.

---

## Workflow (follow in order)

### Step 1 — Analyze the Script

Read the provided script carefully and produce:

1. **Detected language** — Arabic, English, or mixed (name the dominant language).
2. **Summary** — a concise 2–3 sentence summary of what the script is about, its angle, and its tone.
3. **Theme/Mood** — choose ONE theme key from the reference table below that best matches the topic and mood.

Present this analysis to the user in English as a compact block, e.g.:

> **Script analysis**
> • Language: Arabic (Egyptian dialect)
> • Summary: A quick explainer about why Claude hits usage limits and how context windows affect cost. Tone: casual, slightly frustrated.
> • Suggested theme: `ai-futuristic` — fits the LLM / usage-limit topic

Then move on to Step 2 (titles).

#### Theme Reference

| Theme | When to use | Visual style |
|-------|-------------|--------------|
| `ai-futuristic` | AI tools, LLMs, future tech | Dark background, glowing neon blue/purple circuits, holographic text |
| `cybersecurity` | Hacking, data leaks, privacy, threats | Dark red/black, broken shields, code overlays, warning aesthetics |
| `breaking-news` | Announcements, releases, shocking facts | Bold typography, red accent, high contrast, urgency feel |
| `vs-comparison` | Tool comparisons, A vs B content | Split screen feel, dual tones, versus typography |
| `educational` | Explainers, how-it-works, tutorials | Clean, modern, bright with tech diagrams |
| `opinion-hot-take` | Opinions, controversial takes, debates | Flame/spark aesthetics, bold text, energetic |
| `weekly-recap` | Weekly AI/tech roundups | Magazine-style layout, multiple visual elements |

### Step 2 — Suggest 3 Titles

Generate **3 distinct title options** based on the script and its detected language. Titles must be in the script's language (Arabic titles for Arabic scripts, English titles for English scripts). Keep each 3–8 words, punchy, and thumbnail-legible.

Present them to the user in English:

> **Pick a title** (or type your own):
> 1. "Claude بيقولك لا؟ عرفت ليه"
> 2. "ليه Claude بيوقفك فجأة"
> 3. "حدود Claude اللي محدش بيقولك عليها"
>
> Reply with a number to pick one, or send your own title.

Wait for the user's choice. Accept either:
- A number (1, 2, or 3) → use that suggestion
- A custom title → use it verbatim

### Step 3 — Suggest 3 Subtitles

Generate **3 subtitle options** aligned with the chosen title and script. Subtitles can be short category labels, tool names, or supporting phrases. They can be in English even when the title is Arabic (mixed is fine and common for tech covers).

Present them to the user in English:

> **Pick a subtitle** (or skip it):
> 1. "Usage Limits Explained"
> 2. "Context Window Deep Dive"
> 3. "AI News"
>
> Reply with a number, send your own, or say "skip" to leave the cover without a subtitle.

Wait for the user's choice. Accept:
- A number (1, 2, or 3)
- A custom subtitle
- "skip" / "no subtitle" / "none" → proceed with no subtitle

### Step 4 — Build the Image Generation Prompt

Construct a detailed image generation prompt using this template, filling in the dynamic parts:

```
Portrait Instagram Reel cover, 9:16 aspect ratio, ultra high quality.

LAYOUT:
- Top area: [TITLE in <language>, bold, large font, high contrast against background]
- [SUBTITLE if any, smaller font, English or Arabic]
- Lower half: if a person image is provided, the person's face/upper body anchors the composition — large, prominent, centered or slightly offset to one side to leave room for the title
- If a non-person base image is provided, use it as the main scene/product/context reference and build the cover around it

VISUAL THEME: [Insert theme-specific description from Step 1 table above]

REFERENCE IMAGE INTEGRATION:
- If a person photo is provided, make the person appear naturally part of the scene
- If a base image is provided, preserve its important details and use it to guide the cover composition
- Include relevant extra assets such as screenshots, logos, product images, UI captures, charts, or visual references when provided
- Natural lighting and color blend with the background
- Do not make assets look pasted or floating

TYPOGRAPHY:
- Title: modern, bold, slightly futuristic font feel — [ALIGNMENT]
- Text must be sharp and legible against background
- Use white or bright accent color for title text
- Add subtle glow or shadow to make text pop

OVERALL FEEL: Professional tech influencer cover. Cinematic. Eye-catching at thumbnail size. Similar energy to top-tier tech YouTube/Instagram creators.

Do NOT add watermarks, logos, or text other than what's specified.
```

Replace `[TITLE]`, `[SUBTITLE]`, `[VISUAL THEME description]`, `<language>`, and `[ALIGNMENT]` with actual values for this script:

- `<language>` → the language detected in Step 1 (e.g. `Arabic` or `English`).
- `[ALIGNMENT]` → `right-aligned` for Arabic titles, `left or center aligned` for English titles.

If the user skipped the subtitle in Step 3, remove the subtitle line entirely from the LAYOUT section — do not leave a placeholder.

### Step 5 — Present the Final Prompt for Review

**Do not generate the image yet.** Show the fully constructed prompt to the user inside a fenced code block so it's easy to copy, and ask how they want to proceed:

> **Here's the final prompt:**
>
> ```
> <full constructed prompt>
> ```
>
> You can either:
> 1. **Copy this prompt** and use it with another image generation agent/tool
> 2. **Continue with me** — I'll generate the cover for you
>
> Which would you like?

Wait for the user's response.
- If they choose option 1 (copy / use elsewhere) → acknowledge and stop. Do not call any generation tool.
- If they choose option 2 (continue here) → proceed to Step 6.

### Step 6 — Request Required Assets

Only enter this step if the user chose to continue here in Step 5.

Ask for at least one reference image. The user can provide either a person image or another base image. Extra assets are optional but recommended.

**If working in Codex:** the user can paste, copy, upload, or attach the image directly in the chat. They can also provide absolute file paths if that is easier.

**If working in Claude with Gemini MCP:** ask for absolute file paths to the reference assets — every run, no caching, no auto-pickup, no inline uploads. `gemini:generate_image` needs real `filePath` values on disk.

Prompt the user in English, adapting the first line to the current environment:

Codex:

> Great! Before I generate, send at least one reference image. You can paste or attach it directly here, or send an absolute file path if you prefer:
>
> - **Person image:** a clear portrait or half-body photo if you want a person in the cover
> - **Base image:** a screenshot, product image, app UI, or scene you want the cover to build around
>
> You can also add extra assets, like logos, screenshots, device mockups, charts, or UI captures. The more relevant assets you provide, the better I can include them in the cover and produce a stronger result.

Claude/Gemini:

> Great! Before I generate, send the **absolute file path** to at least one reference image:
>
> - **Person image:** a clear portrait or half-body photo if you want a person in the cover
> - **Base image:** a screenshot, product image, app UI, or scene you want the cover to build around
>
> You can also send extra asset paths, like logos, screenshots, device mockups, charts, or UI captures. The more relevant assets you provide, the better I can include them in the cover and produce a stronger result.
>
> 💡 **Tip — copy a file's path quickly:**
> - **macOS:** select the file in Finder, then press **Cmd + Option + C**
> - **Windows:** select the file in Explorer, then press **Ctrl + Shift + C**
>
> Paste the path or paths here and I'll take it from there.

Wait for the user to provide at least one reference image before proceeding to Step 7.

- In Codex, accept pasted/copied/uploaded/attached images directly, or accept absolute file paths.
- In Claude/Gemini, do **not** accept inline image uploads for generation. If they attach an image inline, ask them to save it locally and send the absolute path. If they point to a folder instead of a file, ask them to pick specific images. Do not proceed until at least one path is in hand.

### Step 7 — Generate the Cover

#### Codex

Use Codex's image generation/editing capability with the final prompt and the user-provided reference image assets. If the user pasted or attached images directly, use those images as references; do not ask for file paths again.

#### Claude/Gemini

Use `gemini:generate_image`, NOT `gemini:edit_image`. This is critical:

- `generate_image` supports `aspectRatio: "9:16"` — required for Reels.
- `edit_image` has **no** `aspectRatio` parameter; its output ratio follows the input reference image, which breaks the 9:16 requirement when the user uploads a square or landscape asset.

The person photo, base image, and any extra assets go in as **reference images** to guide the generation, while the prompt + aspect ratio fully control composition.

#### Call

```
gemini:generate_image
  prompt:       <constructed prompt from Step 4>
  aspectRatio:  "9:16"
  images:       [{ "filePath": "<real absolute path to reference image>" }, { "filePath": "<optional extra asset path>" }]
  outputPath:   "<real absolute path>/reel-cover-<topic-slug>.png"   # optional
```

Notes on the `images` parameter:
- The schema accepts `filePath` directly — the server reads the file itself, bypassing the MCP transport limit. You do **not** need to base64-encode or call `load_image_from_path` first.
- `mimeType` is auto-detected from `filePath`, so you can omit it.
- If an asset path is very large or transient, base64 `data` + `mimeType` also works but is subject to MCP transport size limits.

If `outputPath` is omitted the server saves to its configured `GEMINI_IMAGE_OUTPUT_DIR` (or its built-in default) with an auto-generated name — providing an explicit path keeps the file findable.

#### Iteration / refinement turns

When the user asks for tweaks ("make the title red", "different background"), regenerate with an updated prompt and the **same reference image assets** unless the user provides replacements.

- In Codex, use the same pasted/attached images or file-path references from the previous generation.
- In Claude/Gemini, call `gemini:generate_image` again. Do not switch to `edit_image` for refinements — the 9:16 ratio must be preserved.

### Step 8 — Present & Offer Iteration

After generating:
1. Show the generated image
2. Display the final title, subtitle, and theme used
3. Offer refinements **in English**:

> How's the cover? If you want to tweak anything — colors, title, visual effect, person placement, or asset placement — just say the word and I'll regenerate.

---

## Quality Checklist

Before presenting the final image:
- [ ] Title is short, punchy, and matches script topic
- [ ] Theme matches the script's mood
- [ ] Person image, base image, and extra assets are naturally integrated where provided
- [ ] 9:16 portrait ratio
- [ ] Text is legible at small sizes

---

## Example Titles by Theme

### Arabic

| Script topic | Theme | Generated title | Subtitle |
|---|---|---|---|
| Claude usage limits | `ai-futuristic` | "Claude بيقولك لا؟ عرفت ليه" | "Usage Limits Explained" |
| NVIDIA GTC announcement | `breaking-news` | "NVIDIA غيرت قواعد اللعبة" | "GTC 2025" |
| OpenAI vs Gemini | `vs-comparison` | "مين أحسن؟ الحقيقة اللي محدش بيقولها" | "OpenAI vs Gemini" |
| Cybersecurity breach | `cybersecurity` | "اتهكر بدون ما تعرف 🚨" | "تحذير أمني" |
| Weekly AI recap | `weekly-recap` | "أهم أخبار الـAI الأسبوع ده" | "AI Weekly" |
| How transformers work | `educational` | "الـAI بيفكر إزاي؟ الحقيقة جوا" | "Deep Dive" |
| Controversial AI take | `opinion-hot-take` | "رأيي في الـAI هيزعلك" | "رأي صريح" |

### English

| Script topic | Theme | Generated title | Subtitle |
|---|---|---|---|
| Claude usage limits | `ai-futuristic` | "Why Claude Said No To Me" | "Usage Limits Explained" |
| NVIDIA GTC announcement | `breaking-news` | "NVIDIA Just Changed Everything" | "GTC 2025" |
| OpenAI vs Gemini | `vs-comparison` | "The Truth Nobody Tells You" | "OpenAI vs Gemini" |
| Cybersecurity breach | `cybersecurity` | "You Got Hacked and Don't Know It 🚨" | "Security Warning" |
| Weekly AI recap | `weekly-recap` | "This Week in AI — Big Moves" | "AI Weekly" |
| How transformers work | `educational` | "How AI Actually Thinks" | "Deep Dive" |
| Controversial AI take | `opinion-hot-take` | "My AI Take Will Upset You" | "Hot Take" |
