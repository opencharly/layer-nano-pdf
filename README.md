# layer-nano-pdf

A natural-language PDF editing CLI, installed as a pixi-managed console script,
as a standalone OpenCharly layer repo.

The candy ships a `pixi.toml` that installs the `nano-pdf` PyPI distribution (a
Typer CLI depending on `pypdf`, `pdf2image`, `pytesseract`, and `google-genai`)
into the shared default pixi environment. The console script lands at
`~/.pixi/envs/default/bin/nano-pdf` and the distribution is importable, so it is
verifiable by the script's existence, the installed distribution version it
reports, and the CLI's own `--help` usage banner.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `nano-pdf` |
| Console script | `~/.pixi/envs/default/bin/nano-pdf` |
| Pinned version | `0.2.1` |
| Dependencies | `layer-python` |
| Service / port | none |

## How to use it

Compose the layer as a nested `candy:` list inside a named box body:

```yaml
my-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-nano-pdf:v2026.243.0706'
```

## Layout

- `charly.yml` — the `nano-pdf:` candy entity (the `require:`, the `check:`
  assertions, and the embedded `nano-pdf-skill:` skill entity).
- `pixi.toml` / `pixi.lock` — pin the `nano-pdf` PyPI distribution.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-tools:nano-pdf` — the PDF editing CLI and its pixi
  install path.
- `/charly-languages:python` — required Python runtime dependency.
- `/charly-image:layer` — candy authoring reference.
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
