# Template setup

Complete this checklist before implementation.

**Item 3 is the one that gets skipped.** On 2026-08-26 eight repositories in the
estate were still called `xmip-template` — including two carrying more than
seven hundred lines of working code. Two crates with the same name cannot
coexist in one dependency graph, so nothing that depended on both could build,
and the cause was invisible because each repository compiled fine on its own.

1. Choose the final repository name. The grammar of a name is
   `doc/architecture/repository-model.md` section 2 in the estate, and the
   manifest path is the name.
2. Declare the repository in `architecture.toml` in the same change as the
   models and records it affects: `doc/governance/architectural-change-permission.md`,
   *Estate changes are atomic*.
3. **Replace `xmip-template-rust` in `Cargo.toml`** — the package name, the
   description and the repository URL. The package name must equal the
   repository name.
4. Replace the template title and instructions in `README.md`.
5. Complete `ARCHITECTURE.md`: classification, maturity, owning capability,
   responsibility, public contracts, dependencies and non-responsibilities.
6. Keep the full AGPL-3.0 license in `LICENSE` and `license.workspace =
   true` in `Cargo.toml`, the estate root's AGPL-3.0-or-later.
7. Add verification that proves the repository's accepted responsibility and
   contracts.
8. Inherit the shared governance defaults as `README.md`, *Shared governance*,
   says; an override is a reviewed change.
9. Leave `.github/workflows/verify.yml` as generated: it is this template's,
   manual-only (`README.md`, *Verification*) as `automaticVerification` in
   `architecture.toml` says for the estate, and the estate writes it into
   every module and holds each identical to it.
10. Add no `rust-toolchain.toml`, and no version, edition, publish setting
    or lint that the estate's root `Cargo.toml` already holds: the module
    builds only inside the estate and takes them from there (`README.md`,
    *Building*).
11. Remove this setup file after every item is complete.

## Depending on another Xmip module

By path, through the estate root's `[workspace.dependencies]`, under the key
the root holds for it: `doc/architecture/repository-model.md` section 6 in
the estate says how a new key is written (ADR-0005, amendment 2026-11-28).
The package name is the repository name, and the key is an alias so the
import stays short:

```toml
[dependencies]
xmip-context = { workspace = true }
```

```rust
use xmip_context::MessageContext;
```

## This is a snapshot

Template repositories do not propagate. A change made here after a repository is
generated does not reach that repository, which is why `Sync-XmipEstate` checks
these invariants rather than trusting that the template established them. One
file is written from here into every module again: the workflow,
`Sync-XmipEstate -Workflow`.
