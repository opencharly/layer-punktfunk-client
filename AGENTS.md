# AGENTS.md — layer-punktfunk-client

Standalone candy repo for the `punktfunk-client` layer — the punktfunk streaming
**client** (the `punktfunk-client` package and the headless `punktfunk` CLI),
installed from unom's signed pacman repo on Arch/CachyOS. The candy lives in
`charly.yml` at the repo root: the `distro.arch:` package + repo sections and the
`check:` probes. It carries **no `skill:` entity**.

Canonical files:

- `charly.yml` — the `punktfunk-client:` candy entity (the `distro.arch:`
  package + repo sections and the `check:` probes; no `skill:` entity).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-check:punktfunk` — the family skill: the `punktfunk:` check verb,
  including the client methods that drive the `punktfunk` CLI. Load before
  editing or troubleshooting the candy.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  the `distro:` cascade, package + repo sections, `check:` steps). Load before
  editing any entity field or plan step.
- **Missing owning skill:** this repo carries no `skill:` entity, so no
  repo-owned skill is projected for the candy; the closest family skill is
  `/charly-check:punktfunk` (the client methods of the `punktfunk:` verb). The
  gap is recorded against the named batch
  [opencharly/opencharly#291](https://github.com/opencharly/opencharly/issues/291).

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- `charly box validate` at the repo root checks the manifest parses and
  validates.
- The candy's `plan:` `check:` steps are the functional evidence: the control
  CLI, the package database record, the repo stanza, the trusted release key,
  the renderer binary, its Vulkan linkage, a hardware ICD, and the
  hardware-conditional H.264 decode assertion.
- The H.264 decode check is **runtime-only and hardware-conditional**: on a venue
  with no hardware Vulkan device it prints a visible `N/A` and passes; the
  assertion is still made, and can still fail, wherever the hardware exists.

## Modify this repo

- Keep the repo stanza and key byte-identical to the host candy's; that half is
  already proven by the host beds, so anything that breaks here should be the
  package, not the repo plumbing.
- The renderer's ICD packages (`vulkan-radeon`, `vulkan-intel`,
  `vulkan-nouveau`) are deliberate — a software-only (`lavapipe`) venue
  advertises codec `0x00` and every host refuses the session. Do not drop them.
- New behaviour claims belong in the `plan:` as an observable `check:` step.
- If an owning skill is authored, add the `skill:` entity here and update this
  signpost and the README in the same change.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
