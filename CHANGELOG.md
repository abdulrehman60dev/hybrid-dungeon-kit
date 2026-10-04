# Changelog

All notable changes to Hybrid Dungeon Kit are documented here.
This project follows [Semantic Versioning](https://semver.org/).

## [1.0.0] — Unreleased

First release.

### Features
- Hybrid procedural dungeon generator (BSP partitioning + WFC-inspired room
  modules + MST-style corridors) with guaranteed connectivity.
- Branded custom Inspector: Initialize / Generate / Clear / Regenerate buttons,
  quick size presets, collapsible settings sections, and a live result readout.
- One-click setup: **Tools → Hybrid Dungeon Kit** menu to create a wired
  generator or a clean demo scene.
- Boss rooms: configurable count; the exit/boss room is always the farthest
  single-entrance dead-end from the start.
- Layout Mode: Single Line (one path start to end), Branches (tree, no loops),
  or Loops (branches + circular paths).
- Swappable `DungeonTheme` assets and per-cell tile overrides.
- Two sample themes (Dungeon pixel art + Colors flat) built by the theme builder.
- Dungeon Theme Switcher component to switch/cycle themes at runtime or in the
  editor, re-skinning the current dungeon without regenerating it.
- Placeholder colour tiles so a dungeon is visible on import before art is added.
- Optional multi-level run controller with per-level room/boss/theme scaling and
  UnityEvents.
- Scene-view gizmos highlighting room, start, and boss rooms.
- Dungeon Camera Framer: auto-fits an orthographic camera to the whole dungeon
  after each generation (used by the demo scene).
- Wall collision: the wall tilemap gets a Tilemap/Composite collider after each
  render, so generated walls are solid out of the box.
- Room data API: DungeonRoom objects with index, rect, type (Normal/Start/Boss),
  exit flag, connected rooms, doorways and centre; plus GetRoom, GetRoomAtCell,
  GetRoomAtWorld, StartRoom, ExitRoom and TryGetRandomWalkableCell.
- Dungeon Spawner: rule-based placement of enemies, loot and props by room type,
  keeping spawns clear of walls and doorways.
- Dungeon Room Tracker: fires OnRoomEntered / OnRoomExited / OnRoomFirstEntered
  as the player moves between rooms.
- Treasure and shop rooms: configurable counts, smart placement (treasure in
  dead-ends deep in the dungeon, shops mid-run on the main route), their own
  tiles in both sample themes, gizmo colours, and spawner filters.
- Start and exit markers: the start room is painted with the Start tile and an
  Exit pad marks the centre of the exit room.
- DungeonRoom.DistanceFromStart and generator.GetRoomsOfType().
- Corridor Width setting (1-3 cells) with matching doorways.
- Dungeon Minimap: zero-setup on-screen minimap with player marker, optional fog
  of war (rooms reveal on entry, corridors around the player), and a texture you
  can show in your own UI.
- Bake to Prefab: save the current dungeon (tilemaps, colliders, bosses, spawns)
  as a standalone prefab from the inspector or the Tools menu.
- Async generation: GenerateAsync() spreads layout attempts and tile drawing over
  several frames, with OnGenerationStarted / OnGenerationProgress events and an
  IsGenerating flag.
- Faster rendering using batched Tilemap.SetTiles calls.
- Save / load layouts: export the exact dungeon (grid, rooms, roles, corridors)
  as compact JSON, load it back from the inspector, from code, or automatically
  on start via a Saved Layout asset.
- Dungeon Fog Of War: in-world fog with unexplored / explored / visible states,
  reveal radius, room reveal on entry, and an event the minimap can follow.
- Rule Tile support documented, plus a renderer option to draw corridors on the
  floor tilemap so floor Rule Tiles connect seamlessly.
- Playable demo scene (Examples/HybridDungeonKit_Demo) showing every feature,
  plus a Tools menu item that rebuilds it.
- Sample scripts: Player Spawner (walkable placeholder player), Exit Trigger,
  Player Controller, Camera Follow, Demo HUD, and an input wrapper that supports
  both the new Input System and the legacy Input Manager.
- PDF manual.
- Self-contained assembly definitions and the `HybridDungeonKit` namespace.

### Fixes
- Sample theme wall tiles now have a Grid collider; previously they had none, so
  wall collision did not stop the player. Re-run Build Sample Theme to update
  existing themes. The renderer warns about wall tiles without a collider.
- The sample Player Spawner tags its placeholder player "Player", so the minimap
  and fog of war find it automatically.
- Room bumps can no longer be carved onto the grid's outer edge, which could
  leave a gap in the outer wall.
- Spawning, doorway detection and walkability now treat boss, start, exit,
  treasure and shop floors as walkable (boss rooms were previously skipped).
- No obsolete-API warnings on Unity 2023.1+ / Unity 6 (composite collider and
  scene search calls are version-guarded).

### Notes
- Requires Unity 6 (6000.0) or newer and the 2D Tilemap package.
