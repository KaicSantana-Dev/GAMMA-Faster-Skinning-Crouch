# Dorn's Faster Skinning

Speeds up mutant skinning/looting in **S.T.A.L.K.E.R. G.A.M.M.A.** without touching any animation files.

## The problem

The vanilla "Well Dressed" achievement (500 mutant kills, or 250 field dressings) is meant to
swap the slow default skinning/looting animation for a much faster one. See
`ui_mutant_loot.script`'s `UIMutantLoot:Loot()`, and, if FDDA Redone's mutant skinning is
installed, `liz_fdda_redone_mutant_skinning.script`'s `get_mutant_skin_speed()`. Both key off
`game_achievements.has_achievement("well_dressed")`. In practice that takes hours of grinding to
earn, so almost nobody ever sees the speed-up it's supposed to grant.

## What this mod does

- Patches `game_achievements.has_achievement` so a query for `"well_dressed"` specifically
  always returns true, applying the skinning speed-up the achievement already grants, by
  default, without editing or replacing any animation
- Works with both the stock skinning/looting camera effect and FDDA Redone's mutant skinning
  animation, since both already check the same achievement
- Equipping an actual Hunting Kit still stacks on top for the fastest tier, same as vanilla;
  this mod only removes the grind, it doesn't change that part of the balance
- If FDDA Redone's mutant skinning is installed, also patches its animation queue (`lam2`) to
  drop the extra "tucking the part away" animation that plays right after the knife-cut. The
  part is already in your inventory by the time that animation would start -
  `ui_mutant_loot.script` adds it before FDDA ever queues the animation - so skipping it costs
  nothing and removes what was often as much dead time as the cut itself
- We deliberately don't touch the knife-cut animation's own playback speed. The sound played
  during it is an engine-level sound baked into the animation/motion itself, not a scriptable
  `sound_object` we could pitch-shift to match - so speeding up the visual animation desyncs
  it from its audio. Skipping the (silent) pickup animation avoids that problem entirely
- MCM toggle to disable if you'd rather keep vanilla pacing, plus a debug log option

## Installation

1. Install with Mod Organizer 2 like any other mod
2. Place below any mod that changes mutant skinning/looting logic if you see conflicts

Releases: https://github.com/JoshuaCarter/GAMMA-Faster-Skinning/releases

## Files

- `gamedata/scripts/dorn_faster_skinning_main.script` — patches `game_achievements.has_achievement`
- `gamedata/scripts/dorn_faster_skinning_mcm.script` — MCM options
