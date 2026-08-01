---
name: Schedule content to go live
description: Create a Pack schedule, add content to it, and publish it so storefront content goes live at a specified time.
api: https://app.packdigital.com/graphql
operations: [scheduleCreate, scheduleAddContent, schedulePublish]
source: https://docs.packdigital.com/api-reference/content-management-api
---

# Schedule content to go live

Use the Pack Content Management GraphQL API at `https://app.packdigital.com/graphql` with a
**secret** access token in the `Authorization` header.

## Steps
1. **`scheduleCreate`** — create a schedule with the target publish (and optional unpublish)
   time. Capture the schedule `id`.
2. **`scheduleAddContent`** — add the content items (page/article/section ids) to that
   schedule by id.
3. **`schedulePublish`** — activate the schedule so the added content publishes at the
   scheduled time.

## Verify
- Query **`schedules`** (cursor-paginated) or **`schedulesByContentId`** to confirm the
  content is attached to a schedule.

## Rules
- List queries are cursor-paginated (`first`/`after`, `edges`/`node`/`pageInfo`).
- Use `scheduleUpdate` to change timing and `scheduleDelete` to cancel.
- Errors are in the GraphQL `errors[]` array.
