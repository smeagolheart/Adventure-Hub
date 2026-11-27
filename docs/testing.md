# Testing

Nothing here has been run in a real game yet. The installer was parse-checked with
WeiDU 249 and its area patching was run against stand-in area files, not EET's.

## Milestone 1: the inn and the opening

1. Install component 0 on a BG2EE + EET game.
2. The install log prints the points it read from the Friendly Arm Inn, for example
   `inn door at [x.y], outside [x.y], inside [x.y]`. Note them.
3. Start or load any game, open the console (enable `Debug Mode=1` in `Baldur.lua`,
   then Ctrl+Space) and run:

   ```
   C:MoveToArea("S9YARD")
   ```

   Arriving in the yard plays the opening cutscene once. To watch it again, run
   `C:Eval('SetGlobal("S9_OPENING_STARTED","GLOBAL",0)')` and move to the yard again.

4. Check:
   - [ ] The yard is dark and raining.
   - [ ] The party is placed just outside the inn door, with the camera on Player1.
   - [ ] The narration line shows, the party takes a few steps toward the door, and the screen fades.
   - [ ] The party ends up inside `S9HUB` with no original inn characters.
   - [ ] The stairs go to `S9HUB2` and back.
   - [ ] Clicking the front door shows the rain message and does not leave.

Things most likely to need fixing:

- `DayNight(MIDNIGHT)` and `Weather(RAIN)` in `S9CUT01.baf`: if they fail to compile,
  check `TIMEODAY.IDS` and `WEATHER.IDS` for the right values.
- The area names. `S9_BG1_AREA` assumes EET renamed `AR2300`/`AR2301`/`AR2302` to
  `BG2300`/`BG2301`/`BG2302`. If the install fails to find them, look up the Friendly Arm
  Inn's names in Near Infinity.
- The start point: the party starts at the yard entrance the inn's front exit uses and
  walks at most 60 pixels toward the door. If it starts in the wrong place, send the
  `Adventure Hub: inn door at ...` line from `setup-adventurehub.debug`.

## Still to build in milestone 1: the campaign entry

A new campaign on EET needs more than a `CAMPAIGN.2DA` row. The new-game screen is
driven by EET's Lua campaign table, so the mod must also add a campaign record there
(title, description, logo and icon frames), a start-area 2DA for its own start point,
and the art for its button. Research notes:
https://www.gibberlings3.net/forums/topic/28824-adding-new-campaigns/
