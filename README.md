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
- If FDDA Redone's mutant skinning is installed, also applies FDDA body search's height-based
  auto-crouch on the knife-cut (honors FDDA Redone MCM -> Body Search -> "Auto crouch")
- Optional (off by default): a slider to also speed up the knife-cut animation itself, for
  players who want to push past what the achievement/hunting kit bonuses give. Above 1x we
  swap in our own cut sound pitched to match the new speed (since the vanilla one can't be
  sped up to match) and skip all camera motion tied to the cut (lam2's cam effector, the
  actor look-at tilt, and the hud fov zoom). Leave the slider at 1x for the original,
  unmodified pacing, sound, and camera motion
- MCM toggle to disable if you'd rather keep vanilla pacing, plus a debug log option

## Installation

1. Install with Mod Organizer 2 like any other mod
2. Place below any mod that changes mutant skinning/looting logic if you see conflicts

Releases: https://github.com/JoshuaCarter/GAMMA-Faster-Skinning/releases

## Files

- `gamedata/scripts/dorn_faster_skinning_main.script` — patches `game_achievements.has_achievement`
- `gamedata/scripts/dorn_faster_skinning_mcm.script` — MCM options
