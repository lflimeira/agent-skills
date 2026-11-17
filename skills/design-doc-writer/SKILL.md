---
name: design-doc-writer
description: Use when the user wants to write, draft, review or improve a technical design doc, RFC or proposal, or an implementation doc, for a new feature, system change or tech implementation.
---

# Design Doc Writer

Help the user produce a short, clear Design Doc that proposes a feature or technical implementation and gets a team to a decision, and, when the user wants it, a separate Implementation Doc with the technical details for the engineers who will build it.

**Core principle: straight to the point.** People don't read long docs. Every sentence in the Design Doc must help a reviewer understand the proposal or make a decision. If it doesn't, cut it or move it to the Implementation Doc.

## Workflow overview

1. Gather context
2. Write the Design Doc
3. Write the Implementation Doc (if the user wants one)
4. Link both docs and deliver

The user can also start at step 3: if they already have a Design Doc (theirs or one made earlier), read it and generate only the Implementation Doc from it.

## Step 1. Gather context

A doc is only as accurate as the context behind it. Before writing, collect real material about the system.

### 1a. Ask for context artifacts

Ask what source material the user can share. Offer this checklist:

- **Code**: repositories, specific services/modules, or relevant files
- **Microservices / architecture**: services involved, how they communicate (REST, gRPC, events/queues), existing diagrams
- **Existing documentation**: READMEs, previous design docs, ADRs, wiki/Confluence/Notion pages, runbooks
- **Contracts and data**: OpenAPI/Swagger specs, protobufs, event schemas, database schemas/migrations
- **Product input**: PRD, tickets/epics (Jira, Linear), user stories, acceptance criteria
- **Operational data**: dashboards, current metrics, recent incidents or postmortems
- **Infrastructure**: cloud provider, Kubernetes/Docker setup, IaC, CI/CD
- **Team conventions**: company doc templates, coding standards, approved technologies

Also ask: "Is there anything you already know you DON'T want, or a decision that's already been made?"

### 1b. Look for context yourself

Check what you can reach: attached files, connected folders, connected apps (Google Drive, Confluence, Notion, GitHub, Jira) and accessible repositories (READMEs, API definitions, config and dependency files). Tell the user briefly which sources you used. If a useful source probably exists but you can't reach it, ask for it.

### 1c. Summarize your understanding

Send a short summary (5-10 bullets): current architecture, services involved, constraints and the problem. Ask the user to confirm or correct it. Skip only if the user asked for a fast draft.

### 1d. Fill the remaining gaps

Ask only for what is still missing, in one short batch:

- **Problem**: what is broken, missing or costly today? Who feels it?
- **Goals**: what must this change achieve? How will we measure success?
- **Non-goals**: what is explicitly out of scope, even if a reader might expect it?
- **Constraints**: deadlines, team size, existing stack, compliance, legacy systems
- **Audience**: who reviews and approves this doc?
- **Implementation Doc**: "Do you also want a separate Implementation Doc with the code and technical details? The Design Doc would keep only the context, main idea, trade-offs and risks." Recommend it for medium and large changes. Remember the answer: it decides whether Step 3 runs.

Always ask about goals and non-goals explicitly unless they are already clear. If the user isn't sure, propose 3-5 candidates of each and let them confirm, edit or remove.

If the user wants a fast first draft, make reasonable assumptions, list them, and continue.

## Step 2. Write the Design Doc

### Length budget

Pick a size and say which one in one line:

- **Lightweight**: small feature, single service, low risk -> **max ~1 page**. Sections 1-5 and 8 only.
- **Standard**: new service, cross-team change, migration, security- or money-sensitive flows -> **max ~2-3 pages**. Full template, skipping sections that don't apply.

If the draft goes over budget, cut it or move detail to the Implementation Doc.

### Design Doc template

```
# <Title>

Author(s): | Reviewers: | Status: Draft / In review / Approved | Date:
Implementation Doc: <link, or "not planned">

## 1. TL;DR
2-4 sentences: problem, proposed solution, main trade-off, decision needed.

## 2. Context and problem
A few bullets: current state, pain, evidence (numbers, incidents). Why now?

## 3. Goals / Non-goals
- Goals (measurable)
- Non-goals

## 4. Proposal
- The main idea in a few bullets.
- ONE architecture or sequence diagram (Mermaid) if it helps more than text.
- Only the key decisions (e.g. "async via queue", "new table X"), not full contracts or code.
- If there is an Implementation Doc: "Details: see Implementation Doc, section X."

## 5. Alternatives considered
Comparison table: option | pros | cons | why not. Include "do nothing".

## 6. Rollout and observability
Bullets: feature flag / phases, rollback plan, the 2-3 metrics that show it works.

## 7. Security / privacy (only if relevant)
Bullets: sensitive data, auth, compliance (e.g. LGPD).

## 8. Risks and open questions
- Risk -> mitigation (one line each)
- Open questions for reviewers

## 9. Milestones (optional)
Phases with rough effort.
```

If there will be no Implementation Doc, still keep the Design Doc short: put only essential technical details in a short appendix.

After delivering the Design Doc, if the user wants an Implementation Doc, ask: "Do you want to adjust the Design Doc first, or should I write the Implementation Doc now?" The Implementation Doc must follow the final version of the Design Doc, so apply any changes before Step 3.

## Step 3. Write the Implementation Doc (if the user wants one)

This document is for the engineers who will build the solution. Here detail is welcome, but it must stay consistent with the Design Doc.

### How to build it

1. Use the final Design Doc as the source of truth: every key decision in the Proposal must appear here with its technical details. Don't introduce new decisions that contradict it. If you find a problem with the design while detailing it, stop and flag it to the user instead of silently changing the approach.
2. Go back to the collected context (code, schemas, specs) to use real names: existing services, packages, files, tables, endpoints, conventions and the team's language/framework.
3. If important technical details are missing (e.g. which database, which queue, code style), ask in one short batch before writing.
4. Don't repeat context, goals, trade-offs or risks from the Design Doc. Link to it instead.

### Implementation Doc template

```
# <Title> - Implementation Doc

Design Doc: <link> | Author(s): | Status: | Date:

## 1. Overview
2-3 sentences summarizing what will be built, plus the link to the Design Doc.

## 2. Components and changes per service
For each service/module: what changes, new files/classes/packages, new dependencies.

## 3. API contracts
Endpoints/events with request/response examples, error codes, versioning.

## 4. Data model
Schemas, migrations, indexes, backfill scripts, retention.

## 5. Key code and logic
Code snippets or pseudo-code for the core parts, business rules, algorithms.

## 6. Failure handling
Retries, idempotency, timeouts, fallbacks, edge cases.

## 7. Configuration and infra
Env vars, feature flags, Kubernetes/IaC changes, alerts and dashboards.

## 8. Testing plan
Unit, integration, contract and load tests, with specific test cases.

## 9. Task breakdown
Ordered list of tasks / PRs with rough estimates and dependencies between them.
```

Skip sections that don't apply. Code snippets should be short and focused on the non-obvious parts, not full files.

## Step 4. Link both docs and deliver

- Deliver each document separately, as something the user can edit and share (a doc, or Markdown if they ask).
- Link both ways: the Design Doc header has the Implementation Doc link, and the Implementation Doc header has the Design Doc link. Also add section-level references where useful (e.g. Proposal -> "see Implementation Doc, section 3").
- If the docs live somewhere links aren't possible yet (e.g. not published), use a clear placeholder like `<link to Implementation Doc>` and tell the user to replace it after publishing.
- End with a short list of assumptions and open questions to confirm before review.

## Writing rules (both docs)

- **Lead with the decision**: the TL;DR alone should explain the proposal.
- **Bullets over paragraphs**, tables over long comparisons, one diagram over three paragraphs.
- **No filler**: no generic intros, no textbook explanations, no repeating the same point in several sections or across the two docs.
- **Skip sections that don't apply.**
- **No code in the Design Doc**, except a tiny example when a contract is the key decision.
- **Be concrete**: real names, numbers, mechanisms. No vague "fast", "scalable", "robust".
- **Honest trade-offs**: the chosen option has cons too.
- **Ground claims in the collected context** and list sources in a short "References" line. Never invent details about the existing system. Mark guesses with `[ASSUMPTION]` and unresolved points with `[OPEN QUESTION]`.
- Write in the language the user asks for (default: the language of the request).

## Review pass before delivering

Design Doc:
- [ ] Within the length budget; every section earns its place
- [ ] TL;DR matches the rest of the doc
- [ ] Problem has evidence; goals are measurable; non-goals are confirmed
- [ ] The proposal serves every goal and doesn't quietly include a non-goal
- [ ] At least two alternatives (including "do nothing")
- [ ] Rollback and success metrics are clear
- [ ] Risks and open questions are explicit
- [ ] No implementation detail that belongs in the Implementation Doc

Implementation Doc:
- [ ] Every key decision from the Design Doc is covered, and nothing contradicts it
- [ ] Uses real names from the codebase/artifacts; guesses are marked
- [ ] Doesn't repeat Design Doc content; links to it instead
- [ ] Task breakdown is ordered and buildable

Both:
- [ ] Linked to each other in the header (and in sections where useful)

## Reviewing existing docs

Gather context first (Step 1), then return: (1) overall verdict, (2) the top 3-5 issues (including verbosity and missing goals/non-goals), (3) what to cut or move between the Design Doc and the Implementation Doc, (4) questions a senior reviewer would ask.
