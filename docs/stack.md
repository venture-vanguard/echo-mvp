# Echo Stack Handbook (one-pager)

Decision crib for dev agents. Each tool: purpose, when to use, gotchas, integrate, docs.

## Databases
### Turso (libSQL, edge SQLite)
- **Use:** Edge reads, small TX data, configs, feature flags.
- **When:** Global low-latency reads, modest write contention.
- **Gotchas:** Single-writer pattern; not for heavy analytics.
- **Integrate:** libsql client; migrations in repo; seed via CLI.
- **Docs:** https://turso.tech/docs

### Supabase (Postgres + RLS)
- **Use:** Core relational data, audit trails, realtime, REST.
- **When:** SQL + integrity + RLS needed.
- **Gotchas:** Default-deny RLS; align Clerk `user_id`; long funcs.
- **Integrate:** Prisma/SQL migrations; map JWT → `auth.uid()`; storage for light blobs; heavy media → Cloudinary/S3.
- **Docs:** https://supabase.com/docs

### Zapier Tables
- **Use:** Lightweight ops tables glued to Zaps.
- **When:** Ops needs CRUD without backend changes.
- **Gotchas:** JSON explodes to fields when referenced (your note).
  - **Workarounds:** base64 JSON; store S3/DB pointer; “Storage by Zapier” for blobs; pass only IDs through Zaps.
- **Integrate:** Gate writes via “Code by Zapier” for encode/validate.
- **Docs:** https://zapier.com/help/create/tables

## Orchestration
### Zapier (Pro) — primary
- **Use:** External webhooks, quick glue, user-facing ops.
- **Pattern:** Webhook → validate → idempotency (Storage KV) → actions → log.
- **Gotchas:** Rate limits, silent retries, JSON coercion.
- **Integrate:** Central secrets; version Zaps; DLQ via Slack/Logtail.
- **Docs:** https://platform.zapier.com

### Inngest — for scale
- **Use:** Durable workflows, retries, fan-out/fan-in, cron.
- **When:** Need stronger guarantees than Zapier.
- **Gotchas:** Idempotency at event and step; DLQ metrics.
- **Integrate:** Node/TS SDK; large payloads to S3.
- **Docs:** https://www.inngest.com/docs

### SST (on AWS) — CI/CD + IaC
- **Use:** Deploy Lambda/API GW/EventBridge/SQS/S3.
- **Pattern:** Stages (dev/stage/prod); env vars in SSM; GH Actions → `sst deploy`.
- **Gotchas:** Region `ap-southeast-2`; least-priv IAM; tag resources.
- **Docs:** https://sst.dev

### Clerk (Auth)
- **Use:** Accounts, SSO, sessions, JWT.
- **Pattern:** Verify JWT server-side; map to DB user; minimal claims.
- **Gotchas:** PII minimisation; RLS alignment.
- **Docs:** https://clerk.com/docs

### AWS (account active)
- **Use:** S3, CloudFront, Lambda, SES/SNS/SQS, EventBridge, Secrets/SSM.
- **Guardrails:** MFA on root; budgets; logging; SCPs.
- **Docs:** https://docs.aws.amazon.com

### Mem0 (memory layer)
- **Use:** Per-user conversational memory and statful interactions.
- **Pattern:** Store pointers/summaries, not raw content; tenant namespaces; TTL.
- **Docs:** https://docs.mem0.ai/introduction 

### GitHub (current repo)
- **Use:** Code, Actions, issues, environments.
- **Pattern:** Trunk-based; PR checks; CODEOWNERS; conventional commits.
- **Docs:** https://docs.github.com

## Domain / Web
### Squarespace DNS (current)
- **Records:** `www` CNAME → `cname.vercel-dns.com`; apex A → `76.76.21.21` (Vercel). Keep MX for Google.
- **Gotchas:** No apex CNAME; remove stale AAAA.
- **Docs:** https://support.squarespace.com

### Route 53 (optional)
- **Use:** ALIAS at apex, health checks, IaC DNS.
- **When:** Tighter AWS integration needed.
- **Docs:** https://docs.aws.amazon.com/route53

## Apps
### Bland.ai
- **Use:** AI phone calls; transcripts via webhooks.
- **Gotchas:** Answer detection variance; webhook retries; consent prompts.
- **Integrate:** Zapier or Inngest to send calls (POST) or GET transcripts. 
- **Docs:** https://docs.bland.ai

### Google Workspace
- **Use:** Gmail/Calendar/Drive APIs.
- **Pattern:** OAuth2; least scopes; push channels.
- **Docs:** https://developers.google.com/workspace

### Cloudinary
- **Use:** Media storage + transforms.
- **Pattern:** Signed uploads; public transforms; originals/private → S3.
- **Docs:** https://cloudinary.com/documentation

### Calendly (paid)
- **Use:** Booking + reminders.
- **Integrate:** Webhooks `invitee.created`; sync to Google; pass context params.
- **Docs:** https://developer.calendly.com

### Tally (Pro)
- **Use:** Forms with webhooks.
- **Gotchas:** PII; fetch detail server-side by ID.
- **Docs:** https://help.tally.so/category/developers

### 2Chat (WhatsApp, Pro)
- **Use:** WhatsApp send/receive with templates.
- **Gotchas:** Template approval; rate limits; SMS fallback.
- **Docs:** https://developers.2chat.co/docs/intro 

### ClickSend (SMS)
- **Use:** SMS fallback/notifications.
- **Integrate:** Capture inbound to same thread.
- **Docs:** https://developers.clicksend.com/docs 

### ElevenLabs (TTS)
- **Use:** Generate voice files.
- **Gotchas:** Consent for clones; cache; usage caps.
- **Docs:** https://docs.elevenlabs.io

### Hume.ai
- **Use:** Affect analysis; Twilio calling alt to Bland.
- **Gotchas:** Latency; retention; anonymised IDs.
- **Docs:** https://dev.hume.ai

## LLM Providers
### OpenAI — primary
- **Use:** Reasoning, tool use, function calling.
- **Gotchas:** Rate limits; redact identifiers; batch.
- **Docs:** https://platform.openai.com/docs

### xAI — active
- **Use:** Outputs where profanity must pass.
- **Gotchas:** Safety variance; gate upstream.
- **Docs:** https://docs.x.ai

### Anthropic — planned
- **Use:** Long-context, cautious gen.
- **Next:** Open dev account; mirror tool schema.
- **Docs:** https://docs.anthropic.com

## Other
### Expo (React Native)
- **Use:** Managed RN apps, OTA via EAS Update, builds via EAS Build.
- **Gotchas:** Native telephony may require Bare/Dev Client; plan push tokens.
- **Docs:** https://docs.expo.dev

## Cross-cutting guardrails
- **Privacy by design:** Cohort analytics only; no raw voice to managers; narrow, auditable exceptions; export/delete supported.
- **Data residency:** Pin regions; encrypt at rest/in transit; access logs.
- **Idempotency:** Keys on all webhooks and steps; retries with backoff; DLQs.
- **Observability:** Structured logs, correlation IDs, metrics, alerts.
- **PII minimisation:** Store pointers/derived features where possible.

## Default choices
- **DB:** Supabase Postgres + RLS. Edge read-heavy: Turso.
- **Orchestration:** Zapier first; Inngest for scale/guarantees.
- **Auth:** Clerk.
- **Media:** Cloudinary (public) + S3 (originals/private).
- **Deploys/IaC:** SST on AWS `ap-southeast-2`.
- **Messaging:** WhatsApp (2Chat) with SMS fallback (ClickSend).
