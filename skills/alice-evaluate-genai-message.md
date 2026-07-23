---
name: Evaluate a GenAI message with Alice WonderFence
description: Evaluate a prompt or model response in real time for safety and policy violations using the Alice WonderFence guardrail API.
api: openapi/alice-openapi-original.json
operations: [post-genai-evaluate]
---

# Evaluate a GenAI message with Alice WonderFence

Use WonderFence as a runtime guardrail: evaluate every prompt and response in a
live GenAI application before it reaches the model or the user.

## Authentication
Send your API key in the `af-api-key` header.

## Steps
1. Before sending a user prompt to your LLM, call `post-genai-evaluate`
   (`POST /v1/evaluate/message`) with the message.
2. Inspect the returned violations / risk signal; block or allow the message per
   your policy.
3. Repeat on the model's response before returning it to the user.

## Notes
- This is the low-latency inline path — prefer it over the async content
  endpoints for interactive guardrailing.
- Handle `400`, `401`, and `429` per errors/alice-problem-types.yml.
