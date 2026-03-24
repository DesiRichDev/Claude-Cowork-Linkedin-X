# Claude Cowork LinkedIn X

A Claude Code / Claude Cowork agent harness for LinkedIn and X content.

Research trending signals, write platform-native posts in any brand voice, review output, and push to Supabase — all from your terminal or Cowork.

---

## What It Does

- Researches trending signals with real, verified source URLs
- Writes posts for LinkedIn, X, Instagram, and Facebook in your exact brand voice
- Reviews output against quality gates before it goes out
- Pushes approved posts to Supabase for n8n to pick up and publish
- Works for any brand — just swap the brand config

---

## How It Works

```
/research          → find a trending signal with a real source URL
/write-post        → research + write all four platforms in brand voice
/review-post       → audit the JSON for quality issues
/push-supabase     → insert approved post to Supabase
```

Three agents run the workflow:

- **researcher** — finds signals, returns real URLs only, no fabricated data
- **writer** — writes posts in brand voice, checks all quality gates before outputting
- **reviewer** — audits JSON, returns APPROVED / NEEDS REVISION / REWRITE with specifics

---

## Quick Start

```bash
git clone https://github.com/your-username/linkedin-x-os.git
cd linkedin-x-os

# Fill in your brand
cp schemas/brand-config.json brand-config.json
# edit brand-config.json

# Open in Claude Code
claude .

# Write your first post
/write-post
```

Full setup guide: [docs/setup.md](docs/setup.md)

---

## Folder Structure

```
claude-cowork-linkedin/
├── CLAUDE.md                    ← Claude Code reads this first
├── AGENTS.md                    ← Cross-harness context
├── plan.md                      ← Full repo map
│
├── .claude/
│   ├── settings.json
│   ├── commands/
│   │   ├── write-post.md        ← /write-post
│   │   ├── review-post.md       ← /review-post
│   │   ├── research.md          ← /research
│   │   └── push-supabase.md     ← /push-supabase
│   └── agents/
│       ├── researcher.md
│       ├── writer.md
│       └── reviewer.md
│
├── .claude-plugin/
│   └── plugin.json
│
├── skills/
│   ├── social-content/SKILL.md
│   ├── copywriting/SKILL.md
│   ├── reverse-engineering/SKILL.md
│   ├── content-strategy/SKILL.md
│   └── marketing-psychology/SKILL.md
│
├── rules/
│   ├── common/
│   │   ├── voice.md
│   │   ├── structure.md
│   │   └── image-prompt.md
│   ├── linkedin/linkedin-rules.md
│   └── x/x-rules.md
│
├── schemas/
│   ├── brand-config.json        ← Fill this in per brand
│   └── post-output.json         ← Output schema
│
├── examples/
│   ├── brand-config-example.json
│   ├── post-output-example.json
│   └── CLAUDE-brand-example.md
│
└── docs/
    ├── setup.md
    ├── supabase-integration.md
    └── n8n-integration.md
```

---

## Output Format

Every session produces one JSON:

```json
{
  "brand": "YourBrand",
  "agent_name": "Claude Sonnet 4.6",
  "hook_text": "max 80 chars",
  "linkedin_text": "max 2100 chars",
  "x_text": "max 280 chars",
  "instagram_text": "max 2200 chars + hashtags",
  "facebook_text": "max 1500 chars",
  "image_prompt": "text description for image gen pipeline",
  "url": "source link or null",
  "source": "all research URLs",
  "framework_used": "STORY / LESSON / EDU-TELLING / YOU",
  "check": "YES",
  "agent_message": "notes for human reviewer",
  "rate_yourself": 9
}
```

---

## Adding a New Brand

1. Copy `schemas/brand-config.json` and fill it in
2. Copy `examples/CLAUDE-brand-example.md` as your CLAUDE.md
3. Run Claude Code from that folder
4. All rules, skills, and commands work automatically

---

## Stack

- Claude Code / Claude Cowork — agent harness
- Supabase — post store ([docs/supabase-integration.md](docs/supabase-integration.md))
- n8n — image generation + scheduling ([docs/n8n-integration.md](docs/n8n-integration.md))

---

## License

MIT — use it, fork it, build on it.
