---
name: Model infrastructure and apply a change set
description: >-
  Use the System Initiative Public API / MCP server to stage infrastructure
  changes in a change set, model a component, and apply it to HEAD.
api: mcp/system-initiative-mcp.yml
operations: [changeSetCreate, componentCreate, componentUpdate, changeSetForceApply]
---

# Model infrastructure and apply a change set

System Initiative models infrastructure as **components** (a digital twin of a
real resource) inside a **change set** (an isolated proposal). You stage work
in a change set, then apply it to HEAD to execute the real actions.

## Prerequisites
- A workspace-scoped API token in `SI_API_TOKEN` and the target `SI_WORKSPACE_ID`.
- All calls send `Authorization: Bearer $SI_API_TOKEN` against `https://api.systeminit.com`.

## Steps
1. **Create a change set** — `changeSetCreate`. Name it for the work you are doing.
2. **Create the component** — `componentCreate`. Pick the schema (resource type)
   and set its attributes.
3. **Refine attributes** — `componentUpdate` as needed until qualifications pass.
4. **Apply** — `changeSetForceApply` to merge the change set to HEAD; enqueued
   actions then execute against the real cloud/API resources.

## Rules
- Never mutate HEAD directly — always work inside a change set so the model can
  be simulated and reviewed before it touches real infrastructure.
- Keep credentials in Secrets; do not inline provider keys into component attributes.
- Watch action status after apply (see the discover/import skill's `actionList`).
