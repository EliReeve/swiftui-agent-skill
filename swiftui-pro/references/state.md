# State ownership

| Situation | Use |
|---|---|
| Simple value this view alone creates and mutates | `@State private var` |
| Value owned by a parent, this view reads and writes it | `@Binding` |
| Reference-type model this view creates and keeps alive | `@State private var model = Model()` (model is `@Observable`) |
| Reference-type model passed from a parent | plain `let model: Model` (or `@Bindable var` if it needs bindings) |
| Shared across the app | inject with `.environment(model)`, read with `@Environment(Model.self)` |
| Persisted small preferences | `@AppStorage` |
| Scene-level persistence | `@SceneStorage` |
| Derived value | computed property on the model, never stored twice |

Rules:
- The owner creates it. Everything below receives it.
- Never put a reference type in `@State` that something outside the view also needs; it dies with the view.
- `@Observable` tracks only properties that `body` actually reads, so keep hot properties separate from large data to minimise invalidation.
- Views that only need a slice of a model should receive the slice, not the model.
