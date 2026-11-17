# linux-daw-utilities
Several convenience scripts for apps and plugins aimed at digital music production under a wine environment. Notable features include but are not limited to: support for browser login roundtrips (e.g. Native Instruments Logins) and better program launching and closing behavior under wineprefix managers like bottles.

## Installation

Clone the repository and link the scripts into a directory on your `PATH`, such as
`~/.local/bin`. Use symbolic links rather than copies: the links always point at the
clone, so an update only needs a `git pull`.

```bash
git clone https://github.com/Mosen333/linux-daw-utilities.git ~/linux-daw-utilities
mkdir -p ~/.local/bin
for script in wine-bottle-guard wine-url-register install-vcrun kontakt-register; do
    ln -sfn ~/linux-daw-utilities/utilities/$script ~/.local/bin/$script
done
```

Shortcuts and systemd units that the scripts write (e.g. `wine-bottle-guard shortcuts`
or `service`) call the script by the path you ran it from. Run it through the link in
`~/.local/bin`, so that they keep working if you move the clone.

## Updating

If you haven't changed the scripts yourself, one pull updates all of them:

```bash
git -C ~/linux-daw-utilities pull
```

A `wine-bottle-guard watch` service that is already running keeps the old version
until it restarts, so restart it once after the pull:

```bash
systemctl --user restart wine-bottle-guard-<bottle>.service   # e.g. wine-bottle-guard-fl-studio.service
```

Everything else (`launch` from a shortcut, `status`, the other scripts) starts fresh on
every call and uses the new version right away. Existing shortcuts and units don't need
to be written again. If you copied the scripts instead of linking them, copy them again
after the pull, or replace the copies with links as shown above.
