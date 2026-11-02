# Strata / Global Mapping — Playbook

Permanent location: midnghtsapphire/revvel-hail/docs/strata-mapping/

Follows revvel-standards OWNER RULES (AGENTS.md): never delete, never wholesale rewrite, additions only, everything committed, conventional commits, draft PRs for review.

## Permanent priority
Global mapping is the permanent layer and the actual product of play. Every other goal (grave verification, residual noticing, SAR sampling, predictive locations) sits on top of it and uses it. They do not replace it.

## Sequential order (finish one before opening the next)
1. Streamed topography foundation  
   Done when a player can move across one real-world patch from public data only.

2. Mapping driver + gap fill  
   Done when a gap becomes navigable after the driver pass and the player can ignore the driver.

3. First residual site  
   Done when a single site (clandestine-grave or equivalent) can be spotted, marked, and resolved.

4. Noticing threshold on the residual  
   Done when a player who was not looking still registers the mismatch.

5. Global layer stays current  
   Done when the driver or tile stream advances while the player is only doing the residual.

## Noticing factor
Entry point is ordinary noticing, not chemistry. One plant that looks wrong (taller, denser, different color, growing where nothing else does) is enough to stop. Optional deeper reading (decomposition signature, nitrate plume) is available later. Same pattern for oversized patches, darker soil after rain, mismatched smell or sound.

## Loop style
Short and farm-like: walk the area, spot the odd plant or oversized patch, mark or clear it, move on. Completing one improves the local navigable view and leaves the player free to move to the next. No 10-year grind. Mapping driver and streamed topography keep filling the rest of the planet in the background. Player contribution is optional refinement, not the job of building the map.

## Data sources
Elevation/terrain: public DEMs (SRTM, Copernicus, or equivalent). Surface/roads: OpenStreetMap. Imagery/3D: public photogrammetry or 3D tiles where available. Procedural Street View fallback from the same stack where official coverage is missing.

## Testable now
Self-contained HTML viewers in viewers/. Open index.html or the individual files. No install. GitHub Pages path (once enabled): https://midnghtsapphire.github.io/revvel-hail/docs/strata-mapping/

## Daily automation
Strata Sequential Build (09:00 America/Denver) advances only the earliest unfinished step, commits concrete files here, and emails the status (Expected today / What got done / Needs completion / Next day).

## Rules reminder
One step finished before the next opens. Basic first. Entertainment and ordinary movement first. Science optional. Everything lands in this directory.
