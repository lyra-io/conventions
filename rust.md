# Shared Rust Conventions

Use these rules for Lyra-owned Rust APIs and examples across `lyra-io`. Apply them to new APIs and explicitly scoped refactors. Do not automatically rename existing public APIs, upstream code, generated bindings, or methods required by external traits. Non-Rust code follows its language's conventions.

## Method naming

Choose a name that describes the operation and its guarantees:

| Operation | Naming |
| --- | --- |
| Read a local field | `identity()`, `name()` |
| Retrieve a stored record | `fetch_instance()`, `fetch_database()` |
| Enumerate records | `list_components()` |
| Persist a value | `store_*()`—with explicit overwrite/conditional-write semantics |
| Create only if absent | `create_*()` |
| Update an existing record | `update_*()` |
| Lifecycle action | `initialize()`, `register_component()`, `unregister()` |

- `fetch_*` identifies a storage/repository read, not a cheap local-field accessor. Its name does not guarantee that every implementation performs network I/O.
- `store_*` does not implicitly mean upsert, unconditional overwrite, or compare-and-set. Document whether an absent value is created, whether an existing value is overwritten, what condition is required, and how conflicts are reported.
- Keep `create_*`, `update_*`, and lifecycle verbs when those distinctions matter. Do not hide initialization, registration leases, or create-only guarantees behind a generic store name.
- Document absence, backend errors, uncertain writes, and enumeration behavior in the API contract. A naming change must not silently change those semantics.
- For a separately approved rename, update the trait, implementations, callers, tests, and documentation together and review compatibility effects.
- These fetch/store choices are Lyra policy, not a universal Rust requirement. Rust methods use `snake_case`, and simple field getters generally omit `get_`; see the [Rust API naming guidelines](https://rust-lang.github.io/api-guidelines/naming.html).

## Imports

- Import referenced types into scope and use their short names instead of repeating fully qualified paths. For example, prefer `use wal::WalError;` and `WalError::Io` over `crate::wal::WalError::Io`.
- Use an import alias when names genuinely collide rather than obscuring which type is intended.

## Module layout

- Keep `mod.rs` files declarative: module declarations, exports/re-exports, interfaces, shared type declarations, and constants.
- Put operational logic and function implementations in clearly named submodules.
- Place traits after module declarations, exports/re-exports, type aliases, and constants.
- Preserve the existing narrow exception for small segment namespace utilities in `wal/segment/mod.rs`, such as path construction and directory listing/syncing. Do not extend that exception to unrelated modules implicitly.

## Implementation helpers

- Use numbered suffixes for private implementation layers, such as `open0` and `open1`, instead of `open_inner`.
- Use associated `Type::new` functions for constructors.
- Reserve `make_` for free utilities that derive standalone values such as paths, names, or static-like strings, for example `make_segment_path`.
- Keep short, single-use logic inline instead of extracting a helper for only a few straightforward lines.

## Stateful structs

- Group fields in this order: control state, immutable state, mutable state.
- Mark the groups with `// Control state`, `// Immutable state`, and `// Mutable state` comments.
- Within control state, declare an execution/cancellation context first and background task handles immediately after it.
- Follow the same field order in initializers when practical.

Layout example; the application-specific types are illustrative:

```rust
pub struct Service {
    // Control state
    context: CancellationToken,
    tasks: Mutex<Option<JoinSet<()>>>,

    // Immutable state
    request_tx: mpsc::Sender<Request>,
    options: ServiceOptions,

    // Mutable state
    state: Arc<RwLock<State>>,
}
```
