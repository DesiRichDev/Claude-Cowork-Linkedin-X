# Claude Cowork LinkedIn X — Agent Context

Social content harness for LinkedIn and X. Writes platform-native posts in a specific brand voice.

## Agents

### researcher
Finds trending signals. Returns real URLs only — no search queries, no fabricated numbers.
Reads: `schemas/brand-config.json`, `rules/common/voice.md`

### writer
Writes posts across LinkedIn, X, Instagram, Facebook.
Reads: all rules files, brand config, training examples in brand config.
Output: JSON matching `schemas/post-output.json`

### reviewer
Audits post JSON before approval.
Checks: hook word count, banned words, char limits per platform, source integrity, structure.
Returns: pass/fail with specific issues listed.

## Skills Available
- social-content — platform rules, tone, format
- reverse-engineering — extract patterns from URLs and transcripts
- copywriting — hooks, CTAs, engagement triggers
- content-strategy — pillars, frameworks, planning
- marketing-psychology — emotional drivers, psychological triggers

## Output Format
Always one JSON object. No prose before or after. See `schemas/post-output.json`.
