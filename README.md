# SwiftUI Agent Skill

An agent skill that stops AI coding assistants writing bad SwiftUI. Models trained on years of old tutorials reach for deprecated APIs, forget VoiceOver, over-use `@State`, and rebuild views on every frame. This skill gives the agent a modern rulebook (iOS 26, Swift 6) and a review checklist it applies before it hands code back.

Works with Claude Code, Cursor, Codex and any tool that supports the Agent Skills format.

## What it covers

- **Navigation**: `NavigationStack` and typed destinations, never `NavigationView`.
- **State**: which wrapper to use and when (`@State`, `@Binding`, `@Observable`, `@Environment`), and the ownership rules that keep views cheap.
- **Layout**: stacks, grids, `ViewThatFits`, `containerRelativeFrame`, safe areas, and why `GeometryReader` is usually wrong.
- **Animation**: implicit vs explicit, `PhaseAnimator`, `KeyframeAnimator`, transitions, Reduce Motion.
- **Accessibility**: labels, traits, grouping, Dynamic Type, and the invisible-button problem.
- **Performance**: identity, lazy containers, keeping `body` pure.
- **Concurrency**: `.task`, `@MainActor`, structured cancellation.
- **Deprecated API**: a kill list the agent must not use and what replaces each one.

## Install

```bash
npx skills add EliReeve/swiftui-agent-skill
```

Or clone into `~/.claude/skills/` or a project's `.claude/skills/`.

## Use

Trigger it with `/swiftui-pro` in Claude Code, or just ask:

```
Build a settings screen with a toggle for notifications and a picker for theme.
Review this view for performance problems.
Make this list accessible.
```

## Structure

```
swiftui-pro/
  SKILL.md             rules, review checklist, output format
  references/
    deprecated.md      do-not-use list with replacements
    state.md           state ownership decision table
```

## Licence

MIT. Swift, SwiftUI and iOS are trademarks of Apple Inc. This project is independent.
