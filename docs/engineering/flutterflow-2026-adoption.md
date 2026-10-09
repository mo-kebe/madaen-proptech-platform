# MADAEN × FlutterFlow: Evidence-led Adoption Playbook

**Prepared:** 2026-10-09  
**Scope:** engineering guidance only; no FlutterFlow/Supabase production change  
**Source status:** The user-referenced [FlutterFlow X post](https://x.com/flutterflow/status/2108260730940313821) could not be independently retrieved. Do **not** attribute the following claims to that post. The guidance below is grounded in the linked **official FlutterFlow changelogs/docs** and MADAEN's public product scope.

## Principle

Learn capabilities from FlutterFlow, but teach MADAEN through **reproducible engineering decisions, verified UI behavior, and contracts**—not screenshots, isolated prompts, or untested visual duplication. Protect organization/branch isolation, server-side authorization, and existing workflows.

## Verified lessons and how MADAEN applies them

| FlutterFlow capability | MADAEN application | Acceptance evidence |
| --- | --- | --- |
| **Storyboard** with navigation triggers (2026-09-24) | Map Property list → Property details → Create/edit; Incoming requests → Assignment → Follow-up/Task; Dashboard → actionable work. Capture the actual triggering widget and expected destination/parameter. | Navigation map, no unreachable critical screen, correct back/refresh behavior. |
| **Data Type folders**, find/replace and theme tokens (2026-09-24) | Organize client models into Property, Lead, Request, Assignment, Task, Employee, Shared. Consolidate repeated color/typography bindings via reviewed edits. This is *editor organization*, not permission to rename database schemas. | Reused types/components, previewed diffs, compile checks, untouched RPC and RLS contracts. |
| **Try / Catch / Finally** and debug logging (2026-09-02) | All network mutations (create property, assignment, status change, follow-up) show saving, success, recoverable failure; `Finally` releases UI busy state. Errors should be actionable, never silently swallowed. | Success/error/offline/retry tests; no endless spinners or duplicate writes. |
| **Supabase RPC with typed action outputs**, Upsert, Full-Text Search (2026-08-13) | Bind to **existing, approved** server contracts rather than recreating policy in client actions. Use typed outputs where integration benefits. Evaluate search and pagination only with branch/role filtering intact. | Negative authorization tests, typed payload checks, pagination/filter tests, verified contract diff. |
| **Responsive AI screenshots** in desktop agent (2026-09-24) | Screenshot Arabic RTL screens at phone/tablet/desktop and their loading, empty, error, long-content states. Test visual density, table overflow, tap targets and navigation. | Actual captured screenshots, defect list, fixes reviewed visually; code-only PASS is insufficient. |
| **Designer prompting and global Theme** | Specify users, page purpose, actions, key states, reference styles; compare at least 2 visual directions, then reuse tokens and existing components. Avoid generating standalone pages disconnected from product flows. | Design intent, source/reference, comparison, component map, visual review. |

## Execution sequence — one vertical slice at a time

1. **READ** the current project, active FlutterFlow branch, design system, affected pages, existing Supabase RPC signatures and RLS guarantees. Label historical snapshots as historical.
2. **MAP** the end-to-end user journey in Storyboard; record roles and parameters. Include direct navigation/deep-link and auth-loss return behavior.
3. **DESIGN** reusable screen patterns (headers, filter bars, result rows/cards, status/priority badges, actionable footers). Reuse property/task conventions before inventing new UI.
4. **IMPLEMENT** in a non-production branch with exact source/contract pins. Keep business decisions on the server; never bypass RLS or broaden access through client filters.
5. **VERIFY** compiled code + contract/permission tests + local run + responsive RTL screenshots. Test Initial, Empty, Filtered-empty, Loading, Error, Save-success, Save-error, Offline, Session-loss, Unsaved-changes cases as applicable.
6. **REVIEW / SHIP** only when before/after evidence, branch identity, user-visible results, and a rollback path are recorded. Otherwise report `NOT_VERIFIED` and do not publish.

## Suggested first implementation slice

**Incoming Requests → Assignment → Task Follow-up**

- User sees assigned/unassigned requests appropriate to their **authorized** role and organization/branch.
- Request details and assignment routes preserve the selected request ID.
- Assignment action displays pending/success/failure and refreshes only after server confirmation.
- Concurrent or repeated taps do not create duplicate effects; permissions are enforced server-side.
- User can continue to the linked task, with accurate status and due date.
- Phone RTL and desktop screenshots show no clipping or unreachable actions.

Then expand the same verified patterns to **Property Workspace**, **Dashboard**, and **Employees**, rather than redesigning each independently.

## Explicit non-goals / guardrails

- No assumption that a new feature is enabled in the currently running FlutterFlow workspace.
- No unsupported claim that the referenced X post announced any particular feature.
- No backend migration, RLS change, RPC replacement, mass theme replace, remote push, publish, or customer-data write from this document.
- No adoption of RevenueCat or GenUI Chat just because they appear in a changelog; require a real product need, deployment/cost/security review.
- No screenshots or test results marked PASS before observing the actual target.

## References (primary sources)

- [FlutterFlow changelog — 2026-09-24: Storyboard, Data Type folders, responsive AI screenshots](https://flutterflow.io/changelog/storyboard-revenuecat-find-and-replace)
- [FlutterFlow changelog — 2026-09-02: Try/Catch/Finally, grouped query filters, agent validation](https://flutterflow.io/changelog/project-search-try-catch-modern-calendar)
- [FlutterFlow changelog — 2026-08-13: typed Supabase RPC, Upsert, full-text search](https://www.flutterflow.io/changelog/supabase-upsert-rpc-full-text-search)
- [FlutterFlow Designer — prompting and global Theme](https://docs.flutterflow.io/designer/prompting/)
- [FlutterFlow 7.0 — MCP, Live Sessions and Test Pilot](https://flutterflow.io/changelog/flutterflow-7-0)

## Project integration status

This is a reviewable knowledge artifact in a **documentation-only branch of the public demo repository**. It is **not** an update to MADAEN Engineering's persistent plugin memory, the FlutterFlow project, or the production database. Integrate with the engineering agent only after its live connection and project identity are verified.
