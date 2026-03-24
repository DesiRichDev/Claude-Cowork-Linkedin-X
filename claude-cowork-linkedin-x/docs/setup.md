# Setup Guide

Get Claude Cowork LinkedIn X running for a new brand in under 10 minutes.

---

## Step 1 — Clone the repo

```bash
git clone https://github.com/your-username/linkedin-x-os.git
cd linkedin-x-os
```

---

## Step 2 — Fill in your brand config

Copy the schema template:

```bash
cp schemas/brand-config.json brand-config.json
```

Open `brand-config.json` and fill in:
- `brand` — name, one-line, type, location
- `voice` — tone, POV, what to avoid, reader position
- `audience` — who they are, their pain points, which platforms
- `pillars` — 3-5 content pillars
- `writing_rules` — already set to defaults, adjust if needed
- `platform_tone` — override per platform if your brand differs
- `banned_words` — the default list covers most cases, add brand-specific ones
- `supabase` — your project ID and table name
- `training_posts` — add 5-12 of your best posts so Claude can match your rhythm
- `sources` — URLs and search strategies for the researcher agent

See `examples/brand-config-example.json` for a filled reference.

---

## Step 3 — Add your brand CLAUDE.md

Copy the example:

```bash
cp examples/CLAUDE-brand-example.md CLAUDE.md
```

Edit the brand name references. This file tells Claude Code what project it is working on.

---

## Step 4 — Open in Claude Code

```bash
claude .
```

Or open the folder in Claude Cowork / Cursor.

---

## Step 5 — Run your first post

```
/write-post
```

Optionally pass a URL or topic:

```
/write-post https://techcrunch.com/some-article
/write-post the latest Anthropic revenue numbers
```

---

## Step 6 — Review and approve

```
/review-post
```

Paste the JSON output. The reviewer agent will return APPROVED / NEEDS REVISION / REWRITE with specific issues.

---

## Step 7 — Push to Supabase (optional)

If your Supabase project ID is set in brand-config.json:

```
/push-supabase
```

From there, your n8n workflow picks it up for image generation and scheduling.

---

## Adding a Second Brand

1. Create a new folder: `mkdir my-second-brand`
2. Copy brand-config into it: `cp schemas/brand-config.json my-second-brand/brand-config.json`
3. Fill in the new brand's details
4. Run Claude Code from that folder: `cd my-second-brand && claude .`

All rules, skills, and commands are shared. Only brand-config.json changes per brand.
