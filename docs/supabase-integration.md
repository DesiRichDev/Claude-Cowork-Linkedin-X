# Supabase Integration

How to set up the posts table and connect it to the agent.

---

## Table Schema

Run this SQL in your Supabase project to create the posts table:

```sql
create table posts (
  id bigint generated always as identity primary key,
  created_at timestamptz default now(),
  modified_at timestamptz default now(),
  brand text,
  agent_name text,
  hook_text text,
  linkedin_text text,
  x_text text,
  instagram_text text,
  facebook_text text,
  image_prompt text,
  url text,
  source text,
  framework_used text,
  "check" text,
  agent_message text,
  rate_yourself integer,
  status text default 'draft'
);
```

---

## Insert Pattern

The `/push-supabase` command uses `Supabase:execute_sql` directly. The key rules:

- `"check"` must always be quoted — it is a reserved SQL keyword
- All text as plain string values — no markdown, no JSON wrapping
- Empty result `[]` from execute_sql = success on INSERT
- `status` defaults to `draft` — change to `approved` or `published` manually or via n8n

---

## Status Flow

```
draft → approved → published
```

- Agent inserts as `draft`
- You or n8n updates to `approved` after human review
- n8n updates to `published` after posting

---

## Connecting brand-config.json

Set your project ID and table in brand-config.json:

```json
"supabase": {
  "project_id": "your-project-id-here",
  "table": "posts",
  "columns": ["brand", "agent_name", "hook_text", ...]
}
```

The agent reads this before every push — no hardcoded credentials anywhere in the repo.

---

## Multiple Brands, One Table

Use the `brand` column to filter. All brands can share one Supabase project.

```sql
select * from posts where brand = 'MillionaireCopy' order by created_at desc limit 10;
```

---

## Checking for Duplicate Topics

Before writing, the researcher agent can query recent posts:

```sql
select hook_text from posts where brand = 'YourBrand' order by created_at desc limit 10;
```

This prevents repeating a topic or angle already covered.
