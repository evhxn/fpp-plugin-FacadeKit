# FacadeKit Projectors (FPP plugin)

A [Falcon Player](https://github.com/FalconChristmas/fpp) (FPP 10.4+) plugin that switches
**PJLink class 1** projectors on and off from FPP Commands, playlists and the scheduler,
shows their state, and lists the projection shows [FacadeKit](https://github.com/evhxn/facadekit)
sent to the player. It is optional: FacadeKit can send and play shows without it.

- PHP and shell only; installs nothing from the network.
- Several projectors at once, each switched in parallel; waits for warm-up or cool-down only
  when a projector itself reports it (laser projectors normally need none).
- Optional automatic power on at show start and off at show stop, and a fault guard. Both are
  off until you turn them on.
- A small token-protected REST API for FacadeKit (`/api/plugin/fpp-plugin-FacadeKit/...`),
  answering the local network only.

See [docs/USER-GUIDE.md](docs/USER-GUIDE.md) for setup. Licensed under the GNU GPL v3 (see
[LICENSE](LICENSE)).

## Install

On the player (FPP 10.4 or newer), as the `fpp` user:

```bash
cd /home/fpp/media/plugins
git clone https://github.com/evhxn/fpp-plugin-FacadeKit.git fpp-plugin-FacadeKit
sudo FPPDIR=/opt/fpp fpp-plugin-FacadeKit/scripts/fpp_install.sh
curl -X POST http://localhost/api/fppd/plugin/fpp-plugin-FacadeKit/load
```

Then open **Status/Control > FacadeKit Projectors**. To update, run `git pull` in the plugin
folder, then the install script and the `load` call again.

Remove it from **Content Setup > Plugin Manager > FacadeKit Projectors > Uninstall**, or with
`sudo /opt/fpp/scripts/uninstall_plugin fpp-plugin-FacadeKit`. That deletes the projector
list, the pairing token and the plugin's log from the player.

## Status

Tested on FPP 10.4 (Raspberry Pi 4) against fake PJLink projectors. Behaviour with specific
real projector models is reported in the issue tracker as people try it.
