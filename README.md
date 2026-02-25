# Agentic Frontend Workflow

A collection of **GitHub Copilot agent files** (`.github/agents/`) designed to support a structured, AI-assisted React frontend development workflow — from initial requirements discovery through to verified, production-ready code.

Each agent has a focused role and is invoked at the right stage of the development lifecycle. Together they form a complete pipeline that keeps work organized, consistent and high quality.

---

## How It Works

The agents are organized into four groups that map to the natural phases of building a feature:

```
Requirements → Epics → Stories → Story Detail → Development → Code Review → Done
                                      ↑                ↑
                               Design & Architecture   Specialists (on demand)
```

See [`workflows/agent-workflow.md`](workflows/agent-workflow.md) for the full Mermaid diagram and detailed tables.

---

## Agent Reference

### Planning Pipeline

Run these agents **in sequence** at the start of any new feature or project phase.

| Agent                        | File                                                                                | Purpose                                                                                                          |
| ---------------------------- | ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Requirements Gathering Agent | [`requirements-gathering.agent.md`](.github/agents/requirements-gathering.agent.md) | Leads structured discovery conversations to produce a complete requirements document                             |
| Epics Agent                  | [`epics.agent.md`](.github/agents/epics.agent.md)                                   | Breaks the requirements document into meaningful, well-scoped epics                                              |
| Stories Agent                | [`stories.agent.md`](.github/agents/stories.agent.md)                               | Decomposes epics into clearly defined, independently deliverable user stories                                    |
| FE Story Detail Agent        | [`fe-story-detail.agent.md`](.github/agents/fe-story-detail.agent.md)               | Refines each story with technical sub-tasks, component breakdowns, complexity estimates and implementation notes |
| Implementation Planner       | [`implementation-planner.agent.md`](.github/agents/implementation-planner.agent.md) | Creates detailed markdown implementation plans saved to `research/plans/`                                        |

---

### Change Management Pipeline

Use these agents when adding or changing requirements against an **existing SPA**. Run them in sequence — the output of each feeds into the next.

| Agent                   | File                                                                                  | Purpose                                                                                                                                |
| ----------------------- | ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Change Impact Analyst   | [`change-impact-analyst.agent.md`](.github/agents/change-impact-analyst.agent.md)     | Analyses new requirements against the existing codebase and produces a structured impact analysis document                             |
| Story Writer            | [`story-writer.agent.md`](.github/agents/story-writer.agent.md)                       | Transforms the impact analysis into well-defined user stories following the INVEST principle                                           |
| FE Refinement Developer | [`fe-refinement-developer.agent.md`](.github/agents/fe-refinement-developer.agent.md) | Runs an interactive refinement session — works through stories one by one, asks clarifying questions and writes technical descriptions |

---

### Design & Architecture

Consulted **during refinement**, before development starts on a story.

| Agent                        | File                                                                                | Purpose                                                                                                    |
| ---------------------------- | ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| UX/UI Design Advisor         | [`ux-ui-design-advisor.agent.md`](.github/agents/ux-ui-design-advisor.agent.md)     | Defines screen layouts, user flows and interaction patterns                                                |
| Component Architecture Agent | [`component-architecture.agent.md`](.github/agents/component-architecture.agent.md) | Designs the component tree, folder structure and boundaries between shared and feature-specific components |

---

### Development

The agent that writes the code based on the refined plan.

| Agent                     | File                                                                          | Purpose                                                                                      |
| ------------------------- | ----------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| Senior FE Developer Agent | [`senior-fe-developer.agent.md`](.github/agents/senior-fe-developer.agent.md) | Implements user stories — components, state, data fetching, routing and Supabase integration |

---

### Specialists — consulted on demand

Brought in during development whenever specific expertise is needed. Not part of the main sequence.

| Agent                              | File                                                                                                  | When to use                                                                |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Zustand Specialist                 | [`zustand-specialist.agent.md`](.github/agents/zustand-specialist.agent.md)                           | Designing or reviewing Zustand store structure                             |
| TanStack Query Specialist          | [`tanstack-query-specialist.agent.md`](.github/agents/tanstack-query-specialist.agent.md)             | Designing or reviewing data fetching and caching hooks                     |
| React Router v6 Specialist         | [`router-specialist.agent.md`](.github/agents/router-specialist.agent.md)                             | Routing structure, nested layouts, protected routes, URL state             |
| shadcn/ui Specialist               | [`shadcn-ui-specialist.agent.md`](.github/agents/shadcn-ui-specialist.agent.md)                       | Choosing, composing and customizing shadcn/ui components                   |
| Tailwind CSS Advisor               | [`tailwind-css-advisor.agent.md`](.github/agents/tailwind-css-advisor.agent.md)                       | Styling decisions, responsive design, theming, design consistency          |
| React Hook Form & Validation Agent | [`react-hook-form-validation.agent.md`](.github/agents/react-hook-form-validation.agent.md)           | Form logic, Zod schemas, validation, error handling, multi-step forms      |
| Supabase Integration Specialist    | [`supabase-integration-specialist.agent.md`](.github/agents/supabase-integration-specialist.agent.md) | Database queries, realtime subscriptions, Supabase Storage                 |
| Supabase Auth Flow Agent           | [`supabase-auth-flow.agent.md`](.github/agents/supabase-auth-flow.agent.md)                           | Auth flows, session management, OAuth, protected routes                    |
| React Patterns Agent               | [`react-patterns.agent.md`](.github/agents/react-patterns.agent.md)                                   | Choosing the right React pattern — hooks, composition, context vs. Zustand |
| FE Mentor Agent                    | [`fe-mentor.agent.md`](.github/agents/fe-mentor.agent.md)                                             | Learning concepts, getting unstuck, understanding trade-offs               |

---

### Quality & Verification

Used **after implementation** to ensure the story is genuinely complete.

| Agent                    | File                                                                              | When to use                                                                |
| ------------------------ | --------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Accessibility Advisor    | [`accessibility-advisor.agent.md`](.github/agents/accessibility-advisor.agent.md) | Reviewing WCAG compliance, ARIA usage, keyboard nav, focus management      |
| Code Review Agent        | [`code-review.agent.md`](.github/agents/code-review.agent.md)                     | Reviewing completed code for correctness, quality and convention adherence |
| Testing Strategy Agent   | [`testing-strategy.agent.md`](.github/agents/testing-strategy.agent.md)           | Defining and reviewing unit, integration and e2e tests                     |
| Definition of Done Agent | [`definition-of-done.agent.md`](.github/agents/definition-of-done.agent.md)       | Final pass/fail verification before marking a story as done                |

---

## Tech Stack Covered

These agents are tuned for a modern React frontend stack:

- **React** — components, hooks, patterns
- **TypeScript** — type safety throughout
- **Zustand** — client state management
- **TanStack Query** — server state, caching, data fetching
- **React Router v6** — routing, nested layouts, protected routes
- **shadcn/ui** — accessible, composable UI components
- **Tailwind CSS** — utility-first styling and theming
- **React Hook Form + Zod** — form management and validation
- **Supabase** — database, auth, realtime and storage

---

## Repository Structure

```
.github/
  agents/                  # All Copilot agent definition files
workflows/
  agent-workflow.md        # Full workflow diagram and agent group descriptions
README.md
```

---

## Getting Started

1. Open this folder in VS Code with the [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) extension installed.
2. Open GitHub Copilot Chat and switch to **Agent mode**.
3. Select the agent appropriate for your current phase (e.g. start with `Requirements Gathering Agent` for a new project).
4. Follow the planning pipeline in sequence, then bring in specialists as needed during development.
5. Use the quality agents before marking any story as done.
