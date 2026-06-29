# Official NucleScript Language & Preset Ecosystem

> [!TIP]
> 📦 **Official Published Packages:** Install or inspect our standard biological presets directly from the **[Official GitHub Packages Registry (`presets`)](https://github.com/orgs/Nuclescript/packages/npm/package/presets)**.

Welcome to the official **@Nuclescript** GitHub organization — the dedicated home for standard biological presets, community packages, playground modules, and language specification for **NucleScript**.

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

---

## ⚡ Powered by NucleOS

NucleScript programs compile directly down to virtual filesystem (VFS) operations executed by **[NucleOS](https://github.com/VyomKulshrestha/Nucle-OS)** — the software-defined DNA storage engine created by **[Vyom Kulshrestha](https://github.com/VyomKulshrestha)**.

- **Core OS & Storage Engine:** Visit [**VyomKulshrestha/Nucle-OS**](https://github.com/VyomKulshrestha/Nucle-OS) for CLI tools, storage engine binaries, error-correction codecs (Reed-Solomon, Fountain, Yin-Yang), and simulator profiles.
- **Language & Preset Packages:** This organization houses standard library imports, package registry guidelines, and web playground integrations.

---

## Built-in Presets

When importing from `"nuclescript/presets"`, the language compiler resolves standard biological configurations validated against production hardware specs:

| Preset | Target Profile | Redundancy | Description |
| :--- | :--- | :--- | :--- |
| `illumina_recovery` | `Illumina` | `4x` | High-accuracy consensus recovery optimized for Illumina sequencing profiles |
| `nanopore_resilient` | `Nanopore` | `6x` | Heavy Reed-Solomon erasure coding tailored for higher insertion/deletion rates |
| `twist_synthesis` | `Twist` | `3x` | Optimized density and screening for Twist Bioscience silicon pools |

---

## Getting Started

To run or plan a NucleScript source file using the core engine:

```bash
# Install or build the core CLI from VyomKulshrestha/Nucle-OS
$ nucle plan my_pipeline.nsl
$ nucle run my_pipeline.nsl
```

For contributions, package submissions, or language specifications, explore our repositories or connect with the core engine repository.
