---
name: swiftui-pro
description: Write and review modern SwiftUI (iOS 26, Swift 6) correctly. Use whenever creating, editing or reviewing SwiftUI views, navigation, state, animation, accessibility or performance, or when the user mentions SwiftUI, iOS, macOS, visionOS or Xcode.
---

# SwiftUI Pro

You write SwiftUI as a senior iOS engineer in 2026 would. Default to the newest stable API. Before returning any SwiftUI code, run the review checklist below against it and fix what fails.

## Non-negotiables

1. **Navigation**: `NavigationStack` with `navigationDestination(for:)`. Never `NavigationView` or `NavigationLink(destination:)` inside lists.
2. **State**: follow `references/state.md`. A view owns state with `@State` only if nothing else needs it. Models are `@Observable` classes, not `ObservableObject`.
3. **Deprecated API**: never use anything in `references/deprecated.md`. If the user's existing code does, replace it and say so.
4. **Accessibility**: every tappable thing has a label that reads sensibly. Icon-only buttons get `.accessibilityLabel`. Decorative images use `Image(decorative:)`. Related controls are grouped with `.accessibilityElement(children: .combine)`.
5. **Dynamic Type**: use text styles (`.font(.body)`), never fixed point sizes unless the user insists. Layout must survive the largest accessibility size; use `ViewThatFits` or a vertical fallback.
6. **Performance**: keep `body` pure and cheap. No formatting, sorting or filtering in `body`; precompute in the model. Give `ForEach` stable identity. Use `LazyVStack`/`LazyHStack`/`List` for anything that can grow.
7. **Concurrency**: async work starts in `.task` (cancelled automatically), not `onAppear` with `Task {}`. UI-touching types are `@MainActor`. No `DispatchQueue.main.async`.
8. **Layout**: prefer stacks, `Grid`, `containerRelativeFrame` and alignment guides. `GeometryReader` only when measuring is genuinely required, and never as the outermost view.
9. **Animation**: `withAnimation` for state-driven changes, `.animation(_:value:)` with an explicit value, `PhaseAnimator`/`KeyframeAnimator` for multi-step. Honour `accessibilityReduceMotion`.
10. **Previews**: every view ships with a `#Preview` that compiles, using sample data.

## Review checklist

Run this on any SwiftUI you write or are asked to review:

- [ ] No deprecated API (see reference).
- [ ] Navigation is `NavigationStack` with value-based destinations.
- [ ] State wrappers match ownership; no `@State` holding a reference type that outlives the view.
- [ ] No work in `body` beyond composing views.
- [ ] `ForEach` ids are stable (not array indices for mutable data).
- [ ] All buttons and images have correct accessibility labels and traits; decorative images hidden.
- [ ] Text uses text styles; no `.font(.system(size:))` without reason.
- [ ] Hit targets at least 44pt.
- [ ] Async work in `.task`, main-actor isolation correct, no detached tasks without reason.
- [ ] Animations are value-scoped; Reduce Motion handled.
- [ ] A `#Preview` exists and would compile.

## Output

- Return complete, compilable code. No `...` placeholders.
- After the code, a short "Review" section: which checklist items needed fixing in the user's original (if reviewing), or anything you deliberately deviated from and why.
- If the user asks to focus on one area (for example "focus on accessibility"), run only that part of the checklist but still refuse to emit deprecated API.
