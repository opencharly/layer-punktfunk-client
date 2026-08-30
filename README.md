# layer-punktfunk-client

The punktfunk streaming **client** candy: the `punktfunk-client` package and the headless
`punktfunk` CLI it ships, installed from unom's signed pacman repo on Arch/CachyOS.

Sibling of [`layer-punktfunk`](https://github.com/opencharly/layer-punktfunk) (the host),
and deliberately the *other half* of it. The host candy proves punktfunk installs and
answers; this one exists so a second system can actually pair with a host and pull a
stream — the thing no single-node bed can demonstrate.

| Item | Value |
|---|---|
| Package | `punktfunk-client` |
| Repo | `[punktfunk]`, `SigLevel = Required DatabaseOptional` |
| Key | `E0CA04465C99C936E0B0C6510A317015A34DDD69`, imported and locally signed |
| CLI | `punktfunk` — headless, no display server needed |

## Drive it with the verb, not `command:`

`punktfunk-client` installs the headless CLI documented at
<https://docs.punktfunk.unom.io/docs/clients>. Drive it through
[`plugin-punktfunk`](https://github.com/opencharly/plugin-punktfunk)'s client methods —
`punktfunk: pair`, `punktfunk: speed-test`, `punktfunk: launch` — rather than a `command:`
step. The verb maps the CLI's documented exit codes to distinct verdicts (2 connection
failed, 3 trust rejected, 4 renderer failed, 5 no match, 6 interactive required) and keeps
a pairing PIN on stdin instead of argv.

## No compositor

The GUI client would drag a second Wayland stack into every client venue and prove less
than the headless CLI does. A client venue stays a plain container.
