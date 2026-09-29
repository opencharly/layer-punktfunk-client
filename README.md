# punktfunk-client

The **client** half of the [punktfunk](https://git.unom.io/unom/punktfunk)
streaming stack for OpenCharly images — the `punktfunk-client` package and the
headless `punktfunk` CLI it ships, installed from unom's signed pacman repository
on Arch/CachyOS.

The sibling [`layer-punktfunk`](https://github.com/opencharly/layer-punktfunk)
repo proves a host installs and answers; this candy exists so a second system can
actually **pair with a host and pull a stream** — the thing no single-node bed
can demonstrate.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `punktfunk-client` |
| Package | `punktfunk-client` |
| Repo | `[punktfunk]` in `/etc/pacman.conf`, `SigLevel = Required DatabaseOptional` |
| Key | fetched + `pacman-key --lsign-key`'d; fingerprint `E0CA04465C99C936E0B0C6510A317015A34DDD69` |
| CLI | `punktfunk` (control), `punktfunk-client` (renderer) |
| Distros | Arch **and** CachyOS (one `distro.arch:` section) |

The package ships three binaries, and they are not interchangeable:

| Binary | Role |
|---|---|
| `punktfunk` | control CLI (links nothing but libc/libm/libgcc) |
| `punktfunk-client` | the decoder/renderer (Wayland + Vulkan) |
| `punktfunk-session` | session host |

`pair`, `hosts list`, `library`, `reachable`, and `wake` run on the control
binary and need no display. `launch` and `open` **spawn the renderer**, which
needs both a compositor and a hardware Vulkan ICD with `VK_KHR_video_decode_h264`.

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list, then drive it
through the `punktfunk:` check verb's client methods:

```bash
punktfunk hosts list --probe
punktfunk pair
punktfunk launch
```

## Layout

- `charly.yml` — the `punktfunk-client:` candy entity (the `distro.arch:` package
  + repo sections and the `check:` probes). It carries **no `skill:` entity**.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning family skill: `/charly-check:punktfunk` (the `punktfunk:` verb,
  including the client methods)
- Host sibling: [`layer-punktfunk`](https://github.com/opencharly/layer-punktfunk)
  — owning skill `/charly-punktfunk:punktfunk-host`
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
