# Official NucleScript Language & Preset Ecosystem

> [!TIP]
> 🧩 **[VS Code extension](https://marketplace.visualstudio.com/items?itemName=nuclescript.nuclescript):** syntax highlighting, live diagnostics, formatting, and a one-click ▷ **Run File** button — install it and write/run a `.nsl` program with nothing else to set up (both `nucle-lsp` and `nucle-cli` download themselves on first use).
> 📦 **Official Published Packages:** Browse or install official language presets and modules directly from our **[Packages Registry](https://github.com/orgs/Nuclescript/packages)**.
> 🧪 **[Try it live in your browser](https://nuclescript.github.io/playground/)** — no install, no download. The same Write & Run editor, Benchmark Explorer, and Pipeline Visualizer, compiled to WebAssembly and running entirely client-side. Prefer a native binary? `cargo run -p nucle_playground`, or grab a prebuilt one from the [**Releases**](https://github.com/Nuclescript/playground/releases) page.

Welcome to the official **Nuclescript** GitHub organization — the dedicated home for standard biological presets, the interactive playground, and the package registry for **NucleScript**.

---

## What is NucleScript?

NucleScript (`.nsl`) is a declarative domain-specific programming language designed for software-defined DNA data storage pools. It provides a clean operations and biological computation layer over molecular storage pools, enforcing chemistry constraints (GC balance, homopolymer limits, hairpin avoidance) and probabilistic error budgets at compile time.

```nuclescript
import { illumina_recovery } from "nuclescript/presets"

pool archive: DnaPool {
    codec: Ternary,
    redundancy: 3x,
    profile: Illumina
}

store "critical_records.tar" into archive {
    redundancy: 4x,
    tag: ["medical", "genomics", "2026"]
}
```

Functions are reusable, effect-checked units — calling one that touches
hardware or destroys data requires the same confirmation a literal operation
would, even through the call:

```nuclescript
fn archive_with_guarantee(data: File, target: Pool<Illumina>, guarantee: Recovery) returns DnaFile {
    let plan: DnaFile = protect data for guarantee
    store plan into target
}
```

---

## ⚡ Powered by NucleOS

NucleScript programs compile directly down to virtual filesystem (VFS) operations executed by **[NucleOS](https://github.com/VyomKulshrestha/Nucle-OS)** — the software-defined DNA storage engine created by **[Vyom Kulshrestha](https://github.com/VyomKulshrestha)**.

- **Core OS & Storage Engine:** Visit [**VyomKulshrestha/Nucle-OS**](https://github.com/VyomKulshrestha/Nucle-OS) — tagged at [**v0.1.0**](https://github.com/VyomKulshrestha/Nucle-OS/releases/tag/v0.1.0) — for the CLI, storage engine source, error-correction codecs (Reed-Solomon, Fountain, Ternary, Yin-Yang), and simulator profiles.
- **Playground:** **[Live in your browser](https://nuclescript.github.io/playground/)** — compiled to WebAssembly, no server, redeployed automatically on every push. [**Nuclescript/playground**](https://github.com/Nuclescript/playground) is the source: a self-contained mirror of the engine plus an interactive web UI with three tabs — Write & Run (paste a `.nsl` program, see diagnostics/simulation/optimizer notes), Benchmark Explorer (live codec/profile/redundancy comparisons), and Pipeline Visualizer (animated encode → noise → recovery on real input). Prebuilt native binaries are on its [Releases](https://github.com/Nuclescript/playground/releases) page for anyone without `cargo`.
- **Packages:** This organization's [package registry](https://github.com/orgs/Nuclescript/packages) hosts the official `@nuclescript` scope.

---

## Official Packages

Four packages are published today, each versioned independently of NucleOS itself:

| Package | Import source | Purpose |
| :--- | :--- | :--- |
| [`@nuclescript/presets`](https://github.com/orgs/Nuclescript/packages/npm/package/presets) | `nuclescript/presets` | Baseline archive pool schemas, a reliable-store pipeline, and an `archive_with_guarantee` function |
| [`@nuclescript/profiles`](https://github.com/orgs/Nuclescript/packages/npm/package/profiles) | `nuclescript/profiles` | Illumina/Nanopore/Twist pool presets at optimizer-recommended redundancy, plus per-profile simulate functions |
| [`@nuclescript/benchmarks`](https://github.com/orgs/Nuclescript/packages/npm/package/benchmarks) | `nuclescript/benchmarks` | Pool schemas and pipelines matching the core repo's standard fixture set |
| [`@nuclescript/recovery`](https://github.com/orgs/Nuclescript/packages/npm/package/recovery) | `nuclescript/recovery` | Consensus/recovery pool bindings and a `recover_with_consensus` function |

Every package is compiler-validated before publish (`nucle package verify`)
and every exported symbol carries a `kind` (pool schema, pipeline, recovery
profile, or function) plus a description — see each package's own README
under [`VyomKulshrestha/Nucle-OS/packages/`](https://github.com/VyomKulshrestha/Nucle-OS/tree/main/packages)
for its exact exports.

---

## Getting Started

**Using VS Code?** Install the [**NucleScript extension**](https://marketplace.visualstudio.com/items?itemName=nuclescript.nuclescript)
and you're done — highlighting, live diagnostics, hover, formatting, and a
▷ **Run File** button that actually executes a program, all with nothing
to build or download by hand.

Prefer the terminal? Install/build the core CLI from [VyomKulshrestha/Nucle-OS](https://github.com/VyomKulshrestha/Nucle-OS), then:

```bash
# Compile-only validation — no hardware, no execution
nucle check my_pipeline.nsl

# Explain what a program does and why the optimizer changed anything
nucle explain my_pipeline.nsl

# Preview a no-hardware simulation plan, or actually run it
nucle plan my_pipeline.nsl
nucle run my_pipeline.nsl

# Inspect or install an official package
nucle package inspect "@nuclescript/presets"
nucle package install "@nuclescript/presets"

# Environment and integrity diagnostics
nucle doctor
```

Or skip installation entirely: **[try it live in your browser](https://nuclescript.github.io/playground/)**, or grab a prebuilt binary from the playground's [**Releases**](https://github.com/Nuclescript/playground/releases) page and try it locally with zero setup.

For contributions, package submissions, or language specification questions, open an issue against [VyomKulshrestha/Nucle-OS](https://github.com/VyomKulshrestha/Nucle-OS) — that's the engine's source of truth.
