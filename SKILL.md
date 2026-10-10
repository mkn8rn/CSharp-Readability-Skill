---
name: csharp-readability
description: "Apply C# Readability when writing, reviewing or refactoring C# code: judge clarity, contracts, architecture fit, async ownership and meaningful verification in libraries, services, desktop apps and games."
---

You have C# Readability. Make intent, contracts, ownership and relevant costs easy
to understand. Stay within the requested change. Prioritize required behavior,
compatibility and performance constraints, then clarity and justified costs.
A known contract failure blocks readiness.

Before editing, inspect affected contracts, callers and tests, repository instructions,
`.editorconfig`/`.globalconfig`, inherited MSBuild policy, SDK/analyzer/language
versions, TFMs and runtime/backend.
Separate requirements from defaults; distinguish owned code from generated/downstream
fixtures. Verify uncertain version-specific behavior against primary documentation.

Reuse project mechanisms, then framework/BCL and installed dependencies. Add state,
coordination or abstractions for a distinct invariant, policy, lifetime or change
boundary; prefer direct transitions and clear owners. Apply the checks below to
affected contracts.

Follow configured naming, nullability, type/`var`, namespace, braces and member-body
style. Prefer supported guard/helper APIs and `nameof`; preserve validation timing and exception contracts.
Do not use null-forgiving assertions or discard results without a verified reason.
Investigate diagnostics at their sites; fix causes while preserving
behavior. Never weaken policy to conceal issues. Suppress only a verified inapplicable
warning, narrowly and with a semantic reason.

Use domain names, cohesive responsibilities, direct control flow and explicit
invariants. Distinguish absence, invalid input and operational failure. Nullability does not validate runtime or
deserialization boundaries. Verify serialized numeric widths, null/default values
and serializer support. Read-only access does not guarantee immutable payloads;
preserve equality/hash consistency and stable dictionary keys. Choose syntax for
the operation and reader. Document caller contracts, limits and non-obvious reasons.

Preserve required observable behavior unless changing it is part of the task.
For simplifications, check evaluation and exception timing, enumeration, ordering,
null/default states, equality, culture, encoding, overflow, mutation and cleanup.
LINQ and iterators may defer or repeat work; materialization changes timing,
memory and source visibility. Preserve required streaming behavior. Check
`IQueryable` provider translation rather than assuming in-memory semantics.

Trace every acquired resource and started operation to an owner, including helpers,
callbacks and synchronization. Identify release/settlement on success, cancellation
and failure. Own work through startup, timeout and shutdown; completion must mean
its promised effects finished. Concurrent repeats of a lifecycle operation must join its promised
completion and failure, including while the first call is unfinished. Returning a task from `using` or removing `async` can
change lifetime or exception delivery. Distinguish expected failures from internal faults; make their
propagation, translation or observation explicit. Prefer `throw;` in the original
catch; capture exceptions when transporting them. Prefer supported asynchronous
calls in async code when callback timing and failure behavior fit. Avoid blocking
waits in async/UI paths; justify required interop.

Verify async contracts for synchronous completion and suspension, including callbacks.
For stateful work, define admission, effect completion and cancellation/fault precedence before
coding. Give each terminal transition one winner; requested cancellation is distinct
from callback/work settlement. Recheck state where the contract commits effects;
passing a token does not establish cancellation behavior or undo effects. Separate shared
work cancellation from a caller's wait; use explicit `CancellationToken.None` when
omission is intentional. Make acquisition and ownership transfer exception-safe:
establish cleanup at acquisition, before another operation or assertion can fail;
dispose only what you own and retain ownership until pending work settles.
Required `async void` handlers must handle failures; composable work must be awaitable.
Guard late publication by state identity/revision. Choose context for every await, including iteration, disposal and test helpers.
Use `ConfigureAwait(false)` consistently in context-independent code; preserve
framework and caller callback affinity. It does not force a thread switch. Respect `ValueTask` consumption, buffer
length/overlap and view/lease lifetimes. Return pooled resources only after reuse
invariants hold. Justify pooling, spans and unsafe code by supported constraints and
measured needs; preserve justified hot paths.

Libraries: preserve source, binary and behavioral compatibility, including
parameter names, failures, enumeration, callbacks and ownership. Check supported
TFMs, dependencies and packaging.

Services: expose business invariants, read/write authorization, transaction and
retry boundaries. Account for duplicate or ambiguous external effects; acceptance
is not completion. Query filters alone do not establish authorization. Match DI
lifetimes to scopes and give background work a shutdown owner.
When using ambient context, validate it against the retained scope; `AsyncLocal`
flow alone does not establish lifetime or authority.

Desktop: preserve workflows, binding/notifications, undo and persistence. Respect
actual UI affinity, keep interactions responsive, and own work, late completions
and subscriptions across view/document closure. Choose separation for real
responsibilities; consider startup, interaction latency and long-session memory.

Games: respect engine/backend capabilities, serialization, scene/resource
lifetimes, simulation order and required determinism. Mutable state and direct
loops can be appropriate. Check engine API thread rules and frame/allocation
budgets on target hardware; verify affected gameplay and target builds.

Look for whole-input copying/parsing and static allocations. Measure representative
cold and steady-state costs, including setup/cleanup, before claiming improvement.
Preserve required output bits and behavior.

Before finishing, try to falsify each material contract with an observable
counterexample. Use controlled gates/clocks for races; assert forbidden effects did
not occur. `Task.WhenAll` joins existing tasks; it does not prove operations overlapped.
Trace interrupted exits against that ownership inventory, including test
helpers. Prove resources/gates are released and all started work settles on failure;
a cleanup wrapper alone is not proof. A cleanup timeout is failed verification.
Derive each assertion from required observable behavior; ask whether another valid implementation would pass. Require identity, exact diagnostics or representation only when contracted.
Before choosing formatter/linter checks and analyzer-enabled builds, read effective
rules, severities and project/TFM scope, including tests and demos. Use available
quality and style checks; confirm the intended files are inspected.
Whitespace-only formatting does not cover diagnostics.
With `dotnet format`, include `style` and `analyzers`; `--severity info` includes
suggestions. Read the output and address relevant unfixed findings. Formatter
success proves only that its selected fixers found no changes; identify remaining
coverage gaps and choose suitable supplementary checks. Compare baseline debt and resolve introduced diagnostics without
weakening rules. Recheck relevant changes; report actual output, scope, unverified
behavior and remaining diagnostics by rule, location, severity and consequence.

Review concrete triggers, locations, consequences and practical corrections. Mark
preferences optional, accept sound code and bound findings to inspected evidence.

Optional documentation: [C# conventions](https://github.com/dotnet/docs/blob/67daa56878f432b8eb01c6c02f904dfbcb9836b4/docs/csharp/fundamentals/coding-style/coding-conventions.md),
[nullability](https://github.com/dotnet/docs/blob/67daa56878f432b8eb01c6c02f904dfbcb9836b4/docs/csharp/fundamentals/null-safety/nullable-reference-types.md),
[library compatibility](https://github.com/dotnet/docs/blob/67daa56878f432b8eb01c6c02f904dfbcb9836b4/docs/standard/library-guidance/breaking-changes.md),
[ConfigureAwait](https://devblogs.microsoft.com/dotnet/configureawait-faq/),
[WPF threading](https://github.com/dotnet/docs-desktop/blob/25b6309575e6c047c8e7dc49a42a1d03293f9f2e/dotnet-desktop-guide/wpf/advanced/threading-model.md),
[Godot threading](https://github.com/godotengine/godot-docs/blob/0acd581bed9f6793a66f37dd7e8bb4b72bbd6bcb/tutorials/performance/thread_safe_apis.rst),
[analyzer configuration](https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/configuration-options),
[formatter verification](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-format).
