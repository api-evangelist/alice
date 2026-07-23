---
name: Moderate content with Alice
description: Analyze text (or image/video/audio) for safety and policy violations using the Alice content-analysis API, synchronously or asynchronously via callback.
api: openapi/alice-openapi-original.json
operations: [post-sync-content-text, post-content-text, post-sync-content-image]
---

# Moderate content with Alice

Use Alice (formerly ActiveFence) to score user or model-generated content for
violations (toxicity, abuse, policy breaches) before it reaches users.

## Authentication
Send your API key in the `af-api-key` request header on every call. Manage keys
with `get-api-keys` / `post-generate-api-key` / `delete-api-key`.

## Synchronous moderation (recommended for real-time flows)
1. Call `post-sync-content-text` with a `content_id` (your platform's id for the
   item) and the `text` to analyze.
2. Read the returned violations, `risk_score`, and `violation_types` inline.
3. For images use `post-sync-content-image`; for batches use
   `post-sync-content-bulk-text`.

## Asynchronous moderation (recommended for large media)
1. Call `post-content-text` (or `post-content-image` / `post-content-video` /
   `post-content-audio`) with `content_id`, the media, a `callback_url`, and a
   `callback_key_name`.
2. Alice returns immediately; when analysis completes it POSTs the
   `analysis.result` payload to your `callback_url`, keyed by `callback_key_name`
   (see asyncapi/alice-webhooks.yml).

## Conventions and error handling
- No idempotency key is supported — dedupe on your own `content_id`.
- Handle `400` (bad payload), `401` (invalid/absent `af-api-key`), and `429`
  (rate limited — back off and retry). See errors/alice-problem-types.yml.
