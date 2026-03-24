# Claude Cowork LinkedIn X

A Claude Code / Claude Cowork agent harness for LinkedIn and X content.
Drop this into any project, point it at a brand, and get consistent posts across all platforms.

---

## What It Does

- Research trending signals on LinkedIn and X
- Write platform-native posts in a specific brand voice
- Review and score posts before they go out
- Output paste-ready JSON for Supabase, n8n, or any scheduler

Works with Claude Code CLI, Claude Cowork, Cursor, and any agent harness that reads CLAUDE.md or AGENTS.md.

---

## Folder Map

```
linkedin-x-os/
|
|-- CLAUDE.md                        # Root context — Claude Code reads this first
|-- AGENTS.md                        # Cross-harness context — Codex, Cursor, Cowork
|-- README.md                        # Setup guide for humans
|-- plan.md                          # This file
|-- .gitignore
|
|-- .claude/                         # Claude Code native config
|   |-- settings.json                # Model, hooks, permissions
|   |-- commands/
|   |   |-- write-post.md            # /write-post — research + write all platforms
|   |   |-- review-post.md           # /review-post — audit JSON for quality issues
|   |   |-- research.md              # /research — find trending signal, return URLs
|   |   |-- push-supabase.md         # /push-supabase — insert approved post to DB
|   |
|   |-- agents/
|       |-- researcher.md            # Finds signals, returns real URLs only
|       |-- writer.md                # Writes posts in brand voice
|       |-- reviewer.md              # Audits output before approval
|
|-- .claude-plugin/
|   |-- plugin.json                  # Plugin manifest for /plugin install
|
|-- .agents/                         # Cross-harness skills (Codex / Cowork compatible)
|   |-- skills/
|       |-- social-content/SKILL.md
|       |-- reverse-engineering/SKILL.md
|       |-- copywriting/SKILL.md
|
|-- skills/                          # Skill definitions
|   |-- social-content/SKILL.md      # Platform rules, tone, format, char limits
|   |-- content-strategy/SKILL.md    # Pillar framework, post planning
|   |-- reverse-engineering/SKILL.md # Extract patterns from URLs, transcripts
|   |-- copywriting/SKILL.md         # Hook formulas, CTA patterns, engagement triggers
|   |-- marketing-psychology/SKILL.md # Emotional drivers, psychological triggers
|
|-- commands/                        # Shared slash commands
|   |-- write-post.md
|   |-- review-post.md
|   |-- research.md
|   |-- push-supabase.md
|
|-- rules/                           # Always-follow writing rules
|   |-- common/
|   |   |-- voice.md                 # Tone principles, banned words, anti-hype
|   |   |-- structure.md             # Hook rules, paragraph grouping, char limits
|   |   |-- image-prompt.md          # Image prompt spec + worked example
|   |
|   |-- linkedin/
|   |   |-- linkedin-rules.md        # LinkedIn-specific tone, format, algorithm tips
|   |
|   |-- x/
|       |-- x-rules.md               # X/Twitter-specific rules, thread vs single tweet
|
|-- schemas/
|   |-- post-output.json             # Output JSON schema all agents must follow
|   |-- brand-config.json            # Brand config template (copy + fill per client)
|
|-- hooks/
|   |-- hooks.json                   # Claude Code hook config
|
|-- examples/
|   |-- brand-config-example.json    # Filled brand config example
|   |-- post-output-example.json     # Example post JSON output
|   |-- CLAUDE-brand.md              # Example brand CLAUDE.md override
|
|-- docs/
|   |-- setup.md                     # How to set up for a new brand
|   |-- adding-a-platform.md         # How to add TikTok, Instagram, etc.
|   |-- supabase-integration.md      # Supabase table schema + insert pattern
|   |-- n8n-integration.md           # n8n workflow connection notes
```

---

## How To Use

1. Clone the repo
2. Copy `examples/brand-config-example.json` to `brand-config.json` and fill it in
3. Copy `examples/CLAUDE-brand.md` to `CLAUDE.md` (root) and fill in brand context
4. Run `/write-post` in Claude Code or open in Cowork
5. Review the output JSON, approve or edit
6. Run `/push-supabase` to store — or pipe to n8n for auto-publish

---

## Output Schema

Every post session produces one JSON:

```json
{
  "brand": "brand name",
  "agent_name": "Claude Sonnet 4.6",
  "hook_text": "max 80 chars — for lookup",
  "linkedin_text": "full post, max 2100 chars, no markdown",
  "x_text": "max 280 chars, multiple short lines",
  "instagram_text": "max 2200 chars + hashtags",
  "facebook_text": "max 1500 chars, warm tone",
  "image_prompt": "text description only — passed to image gen",
  "url": "source link or null",
  "source": "all research URLs comma-separated",
  "framework_used": "STORY / LESSON / EDU-TELLING / YOU",
  "check": "YES or NO",
  "agent_message": "notes, flags, questions",
  "rate_yourself": 8
}
```

---

## Add a New Brand

1. Fill `schemas/brand-config.json` with brand details
2. Add a `CLAUDE.md` in your working directory that imports the brand config
3. All rules, skills, and commands apply automatically
4. Brand-specific voice overrides go in the brand CLAUDE.md

---

## Stack

- Claude Code / Claude Cowork — agent harness
- Supabase — post store
- n8n — scheduling and image gen (Nano Banana or equivalent)
- Any LinkedIn/X scheduler — publishing layer
