# n8n Integration

How n8n connects to Supabase and handles image generation + scheduling.

---

## Overview

```
Agent writes post JSON
    → /push-supabase inserts as status: draft
        → n8n polls Supabase for draft posts
            → triggers image generation (Nano Banana or equivalent)
                → updates status to approved
                    → schedules and publishes to platforms
                        → updates status to published
```

---

## Supabase Trigger Node

Poll for new draft posts every X minutes:

```sql
select * from posts where status = 'draft' order by created_at asc limit 1;
```

After processing, update status:

```sql
update posts set status = 'approved', modified_at = now() where id = {{ $json.id }};
```

---

## Image Generation Node

Pass `image_prompt` from the post row to your image gen service (Nano Banana, Midjourney API, DALL-E, etc.).

The `image_prompt` field is a plain text description — no special formatting needed.

Store the generated image URL back in the row:

```sql
update posts set image_url = '{{ generatedUrl }}', modified_at = now() where id = {{ $json.id }};
```

Add `image_url` to your posts table if not already there:

```sql
alter table posts add column image_url text;
```

---

## Publishing Nodes

Connect to your LinkedIn / X / Instagram / Facebook publishing nodes.

Map fields:
- LinkedIn: `linkedin_text` + `image_url`
- X: `x_text`
- Instagram: `instagram_text` + `image_url`
- Facebook: `facebook_text` + `image_url`

After publishing, update status:

```sql
update posts set status = 'published', modified_at = now() where id = {{ $json.id }};
```

---

## Scheduling

Set your n8n schedule node to run at your optimal posting times.

LinkedIn B2B: Tuesday-Thursday, 7-9am local time
X: varies — test and find your audience's peak
Sunday morning also performs well for LinkedIn decision-makers

---

## Error Handling

If image generation fails — set status to `image_error` and alert.
If publishing fails — set status to `publish_error` and alert.
Never silently drop a post.
