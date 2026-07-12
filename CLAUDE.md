# OneCart

## Concept
Multiple users log in under one shared SwiggyOne membership account to access
membership benefits (delivery, discounts, etc.), but order-building and payment
happen in a distributed way — each participant builds/pays for their own portion
rather than one person owning the whole cart and expense.

## Status
Pre-architecture. Repo is a fresh scaffold — no stack decisions locked yet.

## Constraints from the signed Swiggy Integration Agreement (09-Jul-2026)
These apply to every implementation decision, not just legal review:

- **MCP-only integration.** All Swiggy order/search/discovery interaction goes
  through the Swiggy MCP server (https://www.mcp.swiggy.com). No independent
  scraping of Swiggy surfaces.
- **Prior written consent required before deployment** (Clause 2.1(v)). Once the
  build is functional, full technical specs must go to Swiggy in writing and get
  sign-off before going live — do not ship silently.
- **Branding**: every screen touching the MCP integration must display "Powered
  by Swiggy" per Swiggy's prescribed style (Clause 3.4).
- **No competing product logic.** Nothing in this build should double as
  competitive intelligence gathering or a multi-platform comparison tool
  (Clause 4(iv)) — this is Swiggy-only by design, which OneCart already is.
- **Exclusivity**: no parallel build of a similar concept for another
  food-delivery/quick-commerce platform during the agreement term (1 year from
  09-Jul-2026).
- **Customer data**: any customer data obtained via the integration is subject to
  DPDP Act 2023 handling rules — no marketing use, no storage of failed/abandoned
  transaction data, 24-hour breach notification to Swiggy.
- **Rate limits / throttling**: respect whatever limits Swiggy notifies via the
  MCP; no circumventing throttling or auth controls.

## Open questions to resolve in plan mode before scaffolding
- [ ] Stack: backend framework, DB, auth provider
- [ ] How "distributed payment" actually settles — split at order time vs.
      reconciliation after
- [ ] Auth model: one SwiggyOne login, multiple app-level user identities mapped
      to it — session/permission design
- [ ] Where MCP calls happen: server-side only, or does each participant's client
      need direct MCP access
- [ ] Deployment target: web app, desktop (Electron), mobile

## Notes
- Solo project, individual developer agreement (not a registered business entity
  yet — flagged as a placeholder gap in the signed agreement, worth resolving
  before scaling).
