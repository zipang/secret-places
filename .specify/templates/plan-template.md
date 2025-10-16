# Implementation Plan: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Feature specification from `/specs/[###-feature-name]/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/commands/plan.md` for the execution workflow.

## Summary

[Extract from feature spec: primary requirement + technical approach from research]

## Technical Context

**Language/Version**: TypeScript
**Primary Dependencies**: bun, content-collections, arktype
**Storage**: Local Markdown files (`src/content`)
**Testing**: bun test
**Tooling**: BiomeJS (Linter/Formatter)
**Target Platform**: Evergreen Browsers
**Project Type**: [single/web/mobile - determines source structure]
**Performance Goals**: [domain-specific, e.g., 1000 req/s, 10k lines/sec, 60 fps or NEEDS CLARIFICATION]
**Constraints**: [domain-specific, e.g., <200ms p95, <100MB memory, offline-capable or NEEDS CLARIFICATION]
**Scale/Scope**: [domain-specific, e.g., 10k users, 1M LOC, 50 screens or NEEDS CLARIFICATION]

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- [ ] **Clean Architecture**: Does the plan enforce strict component layering and encapsulation (e.g., only `base` components use the UI library)?
- [ ] **Documented & Readable Code**: Does the plan include tasks for JSDoc and READMEs?
- [ ] **Web Standards First**: Does the plan prioritize standard APIs and avoid libraries with polyfills?
- [ ] **Content as Code**: Is all content managed as Markdown files in `src/content` and loaded via `content-collections`?
- [ ] **Technical Stack**: Does the plan adhere to the mandated technical stack (TypeScript, bun, BiomeJS)?
- [ ] **Mobile-First PWA**: Does the design prioritize a mobile-first experience and function as a PWA?
- [ ] **Performance-Obsessed**: Does the design and technical approach aim for a top Lighthouse performance score?
- [ ] **Holistic Quality**: Are accessibility, best practices, and SEO considered in the design?
- [ ] **KISS**: Is the proposed solution the simplest possible approach?

## Project Structure

### Documentation (this feature)

```
specs/[###-feature]/
├── plan.md              # This file (/speckit.plan command output)
├── research.md          # Phase 0 output (/speckit.plan command)
├── data-model.md        # Phase 1 output (/speckit.plan command)
├── quickstart.md        # Phase 1 output (/speckit.plan command)
├── contracts/           # Phase 1 output (/speckit.plan command)
└── tasks.md             # Phase 2 output (/speckit.tasks command - NOT created by /speckit.plan)
```

### Source Code (repository root)

```
src/
├── components/
│   ├── base/      # Atoms (e.g., Container, Text)
│   └── ui/        # Molecules (e.g., Button, Card)
├── content/     # Static content
├── entities/    # Data models (shared between backend/frontend)
└── routes/      # Page and API routes
```

**Structure Decision**: [Document the selected structure and reference the real
directories captured above]

## Complexity Tracking

*Fill ONLY if Constitution Check has violations that must be justified*

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., 4th project] | [current need] | [why 3 projects insufficient] |
| [e.g., Repository pattern] | [specific problem] | [why direct DB access insufficient] |

