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
   C:Eval('StartCutSceneMode()')
   C:Eval('StartCutScene("S9CUT01")')
   ```

4. Check:
   - [ ] The party appears outside the inn at night, in the rain.
   - [ ] The narration line shows, the party walks to the inn door, and the screen fades.
   - [ ] The party ends up inside `S9HUB` with no original inn characters.
   - [ ] The stairs go to `S9HUB2` and back.
   - [ ] Clicking the front door shows the rain message and does not leave.

Things most likely to need fixing:

- `DayNight(MIDNIGHT)` and `Weather(RAIN)` in `S9CUT01.baf`: if they fail to compile,
  check `TIMEODAY.IDS` and `WEATHER.IDS` for the right values.
- The area names. `S9_BG1_AREA` assumes EET renamed `AR2300`/`AR2301`/`AR2302` to
  `BG2300`/`BG2301`/`BG2302`. If the install fails to find them, look up the Friendly Arm
  Inn's names in Near Infinity.
- The walk to the door: the door point is the centre of the exterior travel region,
  which might be awkward to path to.

## Still to build in milestone 1: the campaign entry

A new campaign on EET needs more than a `CAMPAIGN.2DA` row. The new-game screen is
driven by EET's Lua campaign table, so the mod must also add a campaign record there
(title, description, logo and icon frames), a start-area 2DA for its own start point,
and the art for its button. Research notes:
https://www.gibberlings3.net/forums/topic/28824-adding-new-campaigns/
