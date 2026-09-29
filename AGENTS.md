# AGENTS.md — layer-nano-pdf

Standalone candy repo for the `nano-pdf` layer — a natural-language PDF editing
CLI installed as a pixi console script. The candy lives in `charly.yml` at the
repo root: the `require:` on `layer-python`, the `check:` assertions, and the
embedded `skill:` entity projected into the marketplace corpus as
`/charly-tools:nano-pdf`. The PyPI pin lives in `pixi.toml` / `pixi.lock`.

Canonical files:

- `charly.yml` — the `nano-pdf:` candy entity and the `nano-pdf-skill:` skill
  entity.
- `pixi.toml` / `pixi.lock` — pin the `nano-pdf` PyPI distribution.
- `CHANGELOG/` — per-CalVer release history; read it before changing baked checks.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-tools:nano-pdf` — the owning skill. The PDF editing CLI and its pixi
  install path. Load before editing or troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package/repo
  sections, and service declarations). Load before editing any entity field or
  plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence; they must stay
  valid on every distro arm they run on. Scope a distro-specific check in the
  command itself — the check runner does not honour runner-level
  `exclude-distro` fields.
- The `check:` steps assert the console script at
  `~/.pixi/envs/default/bin/nano-pdf` and the distribution version `0.2.1`; a
  version bump must update `pixi.toml`, `pixi.lock`, and the `check:` together.

## Modify this repo

- Edit the `nano-pdf:` candy entity AND the `nano-pdf-skill:` skill entity in
  `charly.yml` together. The skill is the projected usage source, so a version or
  behaviour change not mirrored in the skill leaves the corpus stale.
- The PyPI pin lives in `pixi.toml` / `pixi.lock`; keep both and the `check:`
  assertions in sync.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
