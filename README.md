# withlang.org

The website for **With** — an ergonomics-first systems language. Served at
<https://withlang.org> via GitHub Pages (custom domain in `CNAME`).

The language itself lives at
[withlang-dev/with](https://github.com/withlang-dev/with).

## What's here

| Path | Purpose |
|---|---|
| `index.html` | The landing page. One self-contained file: inline CSS + vanilla JS, no build step. |
| `installer/install.sh` | Unix (macOS / Linux) installer — the primary install path. |
| `installer/install.ps1` | Windows PowerShell installer. |
| `installer/install.cmd` | Windows `cmd.exe` wrapper (fetches and runs `install.ps1`). |
| `assets/` | Images (founder headshot). |
| `.github/workflows/installer-uat.yml` | Installer UAT — see below. |
| `CNAME` | `withlang.org`. |

The installer scripts are copies of the canonical ones in
[`withlang-dev/with/scripts/`](https://github.com/withlang-dev/with/tree/main/scripts).
They download a single self-contained compiler binary from the latest GitHub
release and place it in `~/.local/bin` (override with `WITH_INSTALL_DIR`).

## Install a user runs

```sh
# macOS / Linux
curl -fsSL https://withlang.org/installer/install.sh | sh
```
```powershell
# Windows (PowerShell)
irm https://withlang.org/installer/install.ps1 | iex
```

## Installer UAT

`.github/workflows/installer-uat.yml` guards the primary install path so it
can't silently break:

- **release-asset** (every push + daily): the checked-in scripts install the
  latest release binary on macOS, Linux, and Windows, then run
  `with -e 'print(...)'` to prove the result is a working compiler.
- **hosted** (daily + manual): the exact command the site tells users to run,
  fetched from the live `withlang.org`, end to end on all three OSes.

## Develop

No build tools. Open `index.html` in a browser. Edit and refresh. Keep the
single-file, dependency-free structure.
