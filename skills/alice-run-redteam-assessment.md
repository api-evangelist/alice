---
name: Run an Alice red-team assessment
description: List, run, and clone adversarial red-team assessments against an AI model or application with Alice WonderBuild.
api: openapi/alice-openapi-original.json
operations: [get-assessments, run-assessment, clone-and-run-assessment, run-assessment-preset]
---

# Run an Alice red-team assessment

Use Alice WonderBuild to stress-test an AI system with adversarial red-team
assessments before or after launch.

## Authentication
Send your API key in the `af-api-key` header on every request.

## Steps
1. Call `get-assessments` to list existing assessments (supports `page`,
   `limit`, `sort`, `order`, `search`, `status`, and date filters).
2. Run one by id with `run-assessment` (`POST /redteam/assessments/run/{id}`).
3. To iterate without mutating the original, use `clone-and-run-assessment`
   (`POST /redteam/assessments/cloneAndRun/{id}`).
4. To launch from a canned scenario, use `run-assessment-preset`
   (`POST /redteam/assessments/runFromPreset`).

## Notes
- Assessment endpoints live under `/redteam/` (unversioned).
- Handle `401` (bad `af-api-key`) and `429` (rate limit) as in
  errors/alice-problem-types.yml.
