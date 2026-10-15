# Do not use

| Old | Use instead |
|---|---|
| `NavigationView` | `NavigationStack` / `NavigationSplitView` |
| `NavigationLink(destination:)` in lists | `NavigationLink(value:)` + `navigationDestination(for:)` |
| `ObservableObject` + `@Published` + `@StateObject` / `@ObservedObject` | `@Observable` class + `@State` (owner) or plain property (passed in) |
| `@EnvironmentObject` | `@Environment(MyModel.self)` |
| `.foregroundColor` | `.foregroundStyle` |
| `.cornerRadius` | `.clipShape(.rect(cornerRadius:))` |
| `.animation(.default)` (no value) | `.animation(.default, value:)` |
| `onChange(of:) { newValue in }` single-param | `onChange(of:) { old, new in }` or zero-param |
| `.onAppear { Task { } }` | `.task { }` |
| `DispatchQueue.main.async` | `@MainActor` / `await MainActor.run` |
| `UIScreen.main.bounds` | `containerRelativeFrame` / scoped `GeometryReader` |
| `.navigationBarTitle` | `.navigationTitle` |
| `.navigationBarItems` | `.toolbar { ToolbarItem }` |
| `.accentColor` | `.tint` |
| `Image(systemName:)` as a button with no label | add `.accessibilityLabel` or use `Label` |
| `.sheet(isPresented:)` with manual state for data | `.sheet(item:)` |
| `.fullScreenCover` for routine flows | `NavigationStack` push or `.sheet` |
| `Text(verbatim:)` for user-facing strings | `Text(_ string)` with localisation |
