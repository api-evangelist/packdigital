---
name: Create, review, and publish a storefront page
description: Build a Pack CMS page from sections and publish it to a Shopify Hydrogen storefront, using a content release for review-then-ship.
api: https://app.packdigital.com/graphql
operations: [pageCreate, pageUpdate, pageAddSectionsBulk, pagePublish]
source: https://docs.packdigital.com/api-reference/content-management-api
---

# Create, review, and publish a storefront page

Use the Pack Content Management GraphQL API at `https://app.packdigital.com/graphql`.

## Auth
Send `Authorization: <PACK_ACCESS_TOKEN>` on every request. Use a **secret** token
(read-write) for the mutations below; a public token is read-only and will fail on writes.

## Optional: scope to a content release
To stage changes for review before they go live, send the `X-Pack-Release-Id` header on
every mutation so the edits land in that release rather than publishing immediately.

## Steps
1. **`pageCreate`** — create the page (title, handle). Capture the returned page `id`.
2. **`pageAddSectionsBulk`** — attach the section blocks that make up the page body.
3. **`pageUpdate`** — adjust page fields/section content as needed. The page stays in
   `draft` state until published.
4. Preview the draft (create a preview URL) and review.
5. **`pagePublish`** — publish the page (or publish the content release) to move it from
   `draft` to `published`.

## Rules
- Content has `draft` and `published` states; mutations operate on the draft until you publish.
- Every content type has history/`*Restore` mutations — you can roll a page back to a prior revision.
- Errors come back in the GraphQL `errors[]` array (see `errors/packdigital-problem-types.yml`).
- There is no idempotency-key header; pages are addressed by `id`, so re-running `pageUpdate`
  on the same id is the safe retry.
