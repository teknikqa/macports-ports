# macports-ports

A self-hosted [MacPorts](https://www.macports.org) port repository for [teknikqa](https://github.com/teknikqa)'s apps, currently [upkeep](https://github.com/teknikqa/upkeep). MacPorts has no "tap" concept like Homebrew, so this is a plain Portfile repo that you add as a local source.

## Install

1. Clone this repo somewhere permanent:

   ```bash
   git clone https://github.com/teknikqa/macports-ports.git ~/.macports-ports
   ```

2. Add it to `/opt/local/etc/macports/sources.conf`, **above** the `[default]` line:

   ```
   file:///Users/<you>/.macports-ports
   rsync://rsync.macports.org/macports/release/tarballs/ports.tar [default]
   ```

3. Install:

   ```bash
   sudo port install upkeep
   ```

## Updating

```bash
cd ~/.macports-ports && git pull
sudo port upgrade upkeep
```

The `PortIndex` in this repo is regenerated automatically by CI whenever a `Portfile` changes, so a `git pull` is all you need locally — no manual `portindex` step.

## Troubleshooting

**`Failed to open statefile for upkeep: ... Permission denied`** — MacPorts drops root privileges to an unprivileged build user for fetch/build/destroot, which can't read a source tree outside `/opt/local`. Add this to `/opt/local/etc/macports/macports.conf`:

```
macportsuser root
```

## Maintenance

Each `Portfile`'s `version` and `checksums` are updated automatically by its app's release workflow whenever a new tag is pushed.
