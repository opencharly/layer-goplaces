# goplaces

Google Places API CLI layer for OpenCharly images.

The `goplaces` candy `go install`s
[`github.com/steipete/goplaces`](https://github.com/steipete/goplaces) into the
user's `GOPATH` bin (`~/go/bin/goplaces`), requiring the `golang` toolchain. It
sets `GOPATH=~/go` and appends `~/go/bin` to `PATH`, so the compiled CLI is
directly runnable.

The binary's presence and executable bit are the observable proof the install
step ran; `go install` compiles the CLI from source during the image build.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `goplaces` |
| Requires | `layer-golang` |
| Binary | `${HOME}/go/bin/goplaces` |
| Environment | `GOPATH=~/go`, `PATH` += `~/go/bin` |
| Install files | `charly.yml` (`run:` step) |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-goplaces:v2026.243.0409'
```

After the image is built:

```bash
~/go/bin/goplaces --help
```

The CLI needs a Google Places API key to reach the API — provision it with
`charly secrets` (`/charly-build:secrets`).

## Layout

- `charly.yml` — the `goplaces:` candy entity: the `golang` require, the `env:`
  / `path_append:` wiring, the `run:` install step, the `check:` assertions, and
  the embedded `skill:` entity.
- `CHANGELOG/` — per-CalVer release notes.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-tools:goplaces` — the Google Places API CLI
- Runtime parent: `/charly-coder:golang`
- Sibling Google API CLI: `/charly-tools:gogcli`
- Bundled by: `/charly-openclaw:openclaw-full` (metalayer)
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
