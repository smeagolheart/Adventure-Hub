# Adventure Hub

A WeiDU mod for Baldur's Gate II: Enhanced Edition with EET. You come in out of the
rain to an inn where quest givers offer standalone adventures based on your level.
Finish one, come back, and new offers open up. The long-term aim is a toolbox that
other adventures, including mod-added ones, can plug into.

Filename prefix: `S9`.

## Status

Milestone 1 (in progress): the inn and the opening cutscene.

- `S9YARD`: the Friendly Arm Inn's exterior, night and rain, used only in the opening cutscene.
- `S9HUB` and `S9HUB2`: the inn's two floors, emptied of their original cast. The front
  door no longer leads outside.
- `S9CUT01`: the cutscene that walks the party in out of the rain.

Not yet built: the separate campaign entry on the new-game screen (see
`docs/testing.md`), quest givers, and the adventure registry.

## Install

Requires BG2EE with EET installed. Copy `adventurehub/` and a WeiDU executable renamed
to `setup-adventurehub` into the game folder, then run `setup-adventurehub`.

## Layout

```
adventurehub/
  adventurehub.tp2       installer
  lib/s9_area.tpa        area cloning and patching helpers
  hub/areas.tpa          builds the three inn areas
  hub/baf/               area scripts and the opening cutscene
  tra/english/           all player-facing text
docs/testing.md          how to test each milestone in game
```
