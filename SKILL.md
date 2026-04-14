---
name: reel-cover-generator
description: Generate Instagram Reel cover images (9:16 portrait format) from a script. Use this skill whenever the user provides a reel/video script and wants a cover image, thumbnail, or visual for it. Also trigger when the user says "غلاف الريل", "cover للسكريبت", "thumbnail", "reel cover", or asks to generate an image for their content. The skill reads the script, extracts a title and visual theme, asks for the creator's photo, then uses Gemini to generate a polished, branded 9:16 cover image in Arabic/tech style.
---

# Reel Cover Generator

Generate professional, branded Instagram Reel cover images for tech content. The cover must be 9:16 portrait orientation, visually striking, and match the mood/topic of the provided script.

The skill is **language-aware**: it detects the language of the script (or the user's message) and generates titles, captions, and prompts in that language. Arabic scripts get Egyptian-dialect Arabic titles; English scripts get punchy English titles. Mixed-language scripts default to the dominant language.

---

## Workflow (follow in order)

### Step 1 — Analyze the Script

Read the script carefully and extract:

- **Language:** Detect the language of the script (Arabic or English). This determines the title language and messaging in subsequent steps.
- **Title:** A punchy 3-8 word title that captures the core message. Keep it short enough to display prominently on a cover.
  - Arabic scripts: use Egyptian dialect where natural
  - English scripts: use direct, punchy English (e.g. "The AI Nobody Talks About")
- **Subtitle (optional):** A short supporting phrase in English or the detected language (e.g., a tool name, a category label like "AI News", "تحذير أمني", "Deep Dive").
- **Theme/Mood:** Choose ONE from the list below based on the script's topic and tone.

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

### Step 2 — Request Creator Photo

After analyzing the script, ask for the user's photo **in the same language they used**:

- **Arabic:** "عشان أعمل الغلاف، محتاج صورتك! ارفع صورة واضحة بوجه بارز — ممكن portrait أو نص جسم. هي هتتدمج في الغلاف بأسلوب احترافي مع الـvisuals المناسبة للموضوع."
- **English:** "To create the cover I need your photo! Upload a clear shot with a prominent face — portrait or half-body works great. It'll be blended naturally into the scene."

Wait for the user to upload their photo before proceeding.

### Step 3 — Build the Image Generation Prompt

Construct a detailed Gemini image prompt using this template, filling in the dynamic parts:

```
Portrait Instagram Reel cover, 9:16 aspect ratio, ultra high quality.

LAYOUT:
- Top area: [TITLE in Arabic, bold, large font, high contrast against background]
- [SUBTITLE if any, smaller font, English or Arabic]
- Bottom half or right side: real photo of a person integrated naturally into the scene
- Bottom corner: small brand watermark "@ismail9k" in subtle white text

VISUAL THEME: [Insert theme-specific description from Step 1 table above]

PHOTO INTEGRATION:
- The person's photo should appear as if they are part of the scene
- Natural lighting blend with the background
- Professional, confident pose
- The person should look like a tech content creator

TYPOGRAPHY:
- Title: modern, bold, slightly futuristic font feel — [Arabic: right-aligned / English: left or center aligned]
- Text must be sharp and legible against background
- Use white or bright accent color for title text
- Add subtle glow or shadow to make text pop

OVERALL FEEL: Professional tech influencer cover. Cinematic. Eye-catching at thumbnail size. Similar energy to top-tier tech YouTube/Instagram creators.

Do NOT add watermarks, logos, or text other than what's specified.
```

Replace `[TITLE]`, `[SUBTITLE]`, `[VISUAL THEME description]` with actual values for this script.

### Step 4 — Load Image & Generate with Gemini

**Important:** The Gemini MCP server cannot access the container filesystem directly. You must use `gemini:load_image_from_path` first to convert any local file into a usable reference.

1. **Load the user's photo** using `gemini:load_image_from_path` with the uploaded file path (e.g. `/mnt/user-data/uploads/photo.png`). This returns a `filePath` token and `mimeType`.
2. **Call `gemini:edit_image`** using the returned `filePath` (not the original filesystem path):
   - `images`: `[{ "filePath": "<filePath from load_image_from_path>", "mimeType": "<returned mimeType>" }]`
   - `prompt`: the constructed prompt from Step 3
   - `outputPath`: `/mnt/user-data/outputs/reel-cover-[topic-slug].png`

**Do NOT** pass raw `/mnt/...` paths directly to `gemini:edit_image` or `gemini:generate_image` — they will fail. Always go through `load_image_from_path` first.

### Step 5 — Present & Offer Iteration

After generating:
1. Show the generated image
2. Display the title and theme you chose
3. Offer refinements **in the same language as the user**:

- **Arabic:** "إزيك في الغلاف؟ لو عايز أغير حاجة — اللون، العنوان، التأثير البصري — قولي وأعمله تاني 🎨"
- **English:** "How's the cover? If you want to tweak anything — colors, title, visual effect — just say the word and I'll regenerate 🎨"

---

## Quality Checklist

Before presenting the final image:
- [ ] Title is short, punchy, and matches script topic
- [ ] Theme matches the script's mood
- [ ] Photo is naturally integrated (not pasted/floating)
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