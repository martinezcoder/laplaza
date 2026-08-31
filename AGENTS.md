# AGENTS.md — LaPlaza

Guide for agents (human and AI) working in this repository.

> ⛔ **No commits or pushes without explicit human approval.**

## Project description

**LaPlaza** is a mobile app that centralizes the events (sports, cultural, music, etc.)
of a location, so people can find out what is happening in their town or neighborhood.
Today this information is scattered across Facebook and Instagram.

We start **with a small town in Spain** as the pilot location.

## Source of truth

The `docs/` folder is the source of truth for product and architectural decisions.

- `docs/product/` defines what LaPlaza should do and why.
- `docs/architecture/` defines significant technical and architectural decisions.

When documentation and code disagree, do not silently assume which one is correct.
For product or architectural conflicts, surface the discrepancy to the human owner
and reconcile the documentation when appropriate.

For implementation details and technical versions, the existing code and dependency
manifests are the source of truth. Documentation must never duplicate concrete
version numbers (see **Versions** below).

## Project structure

LaPlaza is a monorepo.

```text
laplaza/
├── AGENTS.md
├── .gitignore
├── apps/
│   ├── mobile/          # React Native mobile application
│   └── api/             # Rails backend and GraphQL API
└── docs/
    ├── product/
    └── architecture/
```

## Target stack

- **Mobile frontend:** React Native (iOS + Android).
- **Backend:** Ruby on Rails with a **GraphQL API** (occasional REST where it adds value).
- **Structure:** monorepo.

Name the stack, not the versions. Concrete versions belong only in project code
and configuration files (see **Versions** below).

## Documentation

The `docs/` folder contains the project's product and architecture documentation.

### Versions

Never include concrete version numbers of tools, runtimes, languages, frameworks,
databases, or dependencies in documentation: `AGENTS.md`, `docs/**`, READMEs, and
any other product or architecture markdown.

Naming the stack is fine (Rails, PostgreSQL, React Native). Versions live only in
the project's code and configuration (`Dockerfile`, `docker-compose.yml`,
`Gemfile`, lockfiles, `package.json`, and similar). Do not invent a version
inventory in docs.

### Product

`docs/product/` contains product requirements and decisions.

Relevant documents include:

- `docs/product/vision.md` — problem, users, and value proposition.
- `docs/product/mvp-scope.md` — MVP scope and what is out.
- `docs/roadmap.md` — phases and milestones.

Read the relevant product documentation before implementing product functionality.

### Architecture

`docs/architecture/` contains important technical decisions and architectural
documentation.

Relevant documents include:

- `docs/architecture/overview.md` — system architecture.
- `docs/architecture/data-model.md` — data model.

Read the relevant architecture documentation before making significant technical
or architectural changes.

Documentation should reflect important decisions and remain consistent with the
implementation. It should not unnecessarily block development.

## Development

When given a sufficiently clear task:

1. Understand the relevant product requirements and existing implementation.
2. Inspect the existing code before making changes.
3. Choose a reasonable implementation based on the existing architecture and conventions.
4. Implement the change.
5. Add or update tests where appropriate.
6. Run the relevant tests and checks.
7. Summarize what changed and any relevant decisions.

Prefer working software over unnecessary planning.

Do not create, refine, split, or rewrite tickets unless explicitly asked.

Do not ask for clarification when a reasonable implementation can be inferred.
Ask only when an ambiguity would materially affect the product or implementation.

Keep changes small and focused.

## Product decisions

Do not unilaterally change product scope or requirements.

If an important product decision is not covered by the existing documentation and
cannot reasonably be inferred, surface it to the human owner before proceeding.

## Technical decisions

Use the existing architecture and conventions unless there is a good reason to
change them.

Technical implementation decisions belong to the development agent.

For significant architectural changes:

- consider the trade-offs before implementing them;
- explain the decision to the human owner;
- update the relevant documentation in `docs/architecture/`.

Do not introduce dependencies, abstractions, or infrastructure without a clear reason.

## Language

- **Code, code comments, documentation, issues, PRs, and commit messages:** English.
- **User-facing application copy:** Spanish.
- User-facing strings must be localization-ready.

## Git

### Approval before commits

- Do not commit or push without explicit prior approval from the human owner.
- After implementing a change, show or summarize the relevant diff and wait for
  explicit approval before running `git commit`.
- If it is unclear whether approval was given, ask before committing.
- This applies to both human-directed and AI-assisted development.

### Commits

Use Conventional Commits:

`type(scope): summary`

Examples:

- `feat(api): add Event GraphQL type`
- `fix(mobile): correct event ordering`
- `docs: update architecture overview`

Common types include:

`feat`, `fix`, `docs`, `chore`, `refactor`, `test`, `build`, `ci`.

Keep commits focused and meaningful.

## Pull Requests

When a PR resolves a GitHub issue, its description should include the appropriate
closing keyword, such as:

`Closes #123`

Keep PRs small and reviewable. The description should explain the purpose and
impact of the change, not merely repeat the implementation details.