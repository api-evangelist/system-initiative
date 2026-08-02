---
name: Discover existing infrastructure and import it
description: >-
  Use the System Initiative Public API / MCP server to discover real cloud
  resources and import them into the model as components inside a change set.
api: mcp/system-initiative-mcp.yml
operations: [changeSetCreate, componentDiscover, componentImport, componentList, actionList]
---

# Discover existing infrastructure and import it

System Initiative can build its digital twin from resources that already exist
in your cloud accounts, so you can manage brownfield infrastructure without
recreating it.

## Prerequisites
- Workspace token in `SI_API_TOKEN`, workspace in `SI_WORKSPACE_ID`.
- The relevant provider credential stored as a Secret in the workspace.

## Steps
1. **Create a change set** — `changeSetCreate` to stage the import.
2. **Discover resources** — `componentDiscover` to enumerate existing real
   resources reachable with the stored credential.
3. **Import** — `componentImport` to bring a discovered resource into the model
   as a managed component.
4. **Verify** — `componentList` to confirm the imported components, and
   `actionList` to see any queued refresh/create actions.
5. Apply the change set when the imported model is correct (see the
   model-and-apply skill).

## Rules
- Import into a change set first; review the modeled components before applying.
- Use `componentDiscover` before `componentImport` so you import against real,
  current resource state rather than assumptions.
