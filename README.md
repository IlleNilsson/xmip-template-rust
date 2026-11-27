# Xmip repository template — Rust

This repository is the starter snapshot for a Rust Xmip module repository. It is
not an Xmip runtime capability.

For a .NET 11 surface — the PowerShell module, the MAUI desktop GUI or the
Blazor web GUI — use
[xmip-template-dotnet](https://github.com/IlleNilsson/xmip-template-dotnet)
instead. ADR-0014: those surfaces are .NET 11 over the C ABI; the command
line is Rust, on the runtime's traits (amendments 2026-10-12 and
2026-11-17).

A repository generated from this template has independent history. Later
template changes do not rewrite generated repositories, but for one file:
`.github/workflows/verify.yml`, which `Sync-XmipEstate -Workflow` writes from
here into every module, and `test/Workflow.Test.ps1` in the estate holds the
same.

## Before implementation

Follow [TEMPLATE_SETUP.md](TEMPLATE_SETUP.md), and item 3 first. The new
repository must be classified and declared in the authoritative Xmip
architecture manifest before its responsibility or dependencies are treated as
accepted architecture.

## Building

A module builds only inside the Xmip estate. Mounted there, it is a member of
the estate's one Cargo workspace and takes its version, edition, license,
publish setting and lints from the estate's root `Cargo.toml`, and its
toolchain from the root's `rust-toolchain.toml` (ADR-0016, amendment
2026-11-27); it writes its own only where it differs.

## Shared governance

Repository-specific licensing remains explicit in [LICENSE](LICENSE).
Contribution, security, support, issue and pull-request defaults are inherited
from [IlleNilsson/.github](https://github.com/IlleNilsson/.github) when they are
not overridden locally.

## Verification

The included workflow is manual-only and calls the versioned shared workflow at
`IlleNilsson/.github@v1`. It does not run on pushes, pull requests or a
schedule.

The ordered stages are formatting, semantic analysis, linting, compilation and
linking, and test execution. Packaging and publishing are not configured.
