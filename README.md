# ActionHud

A lightweight, vanilla-friendly HUD for Fabric that shows your character's
current action - drawing a bow, eating, mining, fishing, and more - as a
small, animated panel above the hotbar. It's built to feel like it could ship
with the game: minimal, quiet when idle, and gone the instant there's
nothing to report.


## Features

- **17 tracked actions** across combat, survival, movement, mining, and
  fishing - see the full list below.
- **Smooth, tasteful animation**: fade and scale transitions, interpolated
  progress bars, and a brief color flash (blue &rarr; green/red) when an
  action finishes or is cancelled.
- **Fully configurable in-game**: press your chosen key (unbound by default -
  set it in *Controls*) to open ActionHud's own settings screen. Adjust HUD
  scale, position, opacity, animation speed, bar thickness, background
  opacity, color theme, and toggle icons/percentages/individual actions -
  all without leaving the game.
- **Content-aware layout**: each entry's panel snugly fits its own label
  instead of a fixed-size box, so "Sleeping" and "Waiting for a Bite" both
  look right.
- **Zero custom mixins.** Every action is detected from stable, public
  client-side API - no hooks into combat/inventory internals. This keeps
  ActionHud's compatibility surface as small as possible (see
  [Compatibility](#compatibility)) and means there is nothing for another
  mod's mixins to conflict with.
- **Real vanilla item icons.** Rather than shipping a custom icon set,
  ActionHud draws the same item icons vanilla itself uses (a bow for
  drawing a bow, a pickaxe for mining, and so on), so it never looks
  "off-brand" next to the rest of the interface.

### Tracked actions

| Category | Actions |
|---|---|
| Combat | Bow, Crossbow, Trident (Riptide), Attack cooldown, Shield disabled |
| Player | Eating, Drinking, Milk, Sleeping, Spyglass |
| Movement | Elytra flying, Firework boosting, Swimming, Crawling, Sneaking *(off by default)* |
| Mining | Block breaking progress |
| Fishing | Casting / Waiting for a bite / Reel in! |

## Installation

1. Install [Fabric Loader](https://fabricmc.net/use/) for Minecraft 1.21.1.
2. Download [Fabric API](https://modrinth.com/mod/fabric-api) for the same version.
3. Drop `actionhud-<version>.jar` into your `mods` folder alongside Fabric API.
4. Launch the game.

## Requirements

- Minecraft 1.21 or 1.21.1
- Fabric Loader 0.16.14+
- Fabric API (matching build for 1.21.1)
- Java 21
- Client-side only - safe to leave off a server, and safe if only some
  players in a server have it installed.

## Configuration

Open *Controls* and bind a key to **"Open ActionHud Settings"** (unbound by
default so it can never collide with another mod's keybind). From that
screen you can adjust every setting listed under [Features](#features);
a second "Edit Actions..." screen lets you turn any of the 17 actions off
individually. Settings are stored as plain JSON at
`config/actionhud.json` if you'd rather edit them by hand.

## Compatibility

ActionHud touches nothing besides the HUD render pass, a client tick event,
and a keybinding - it does not modify world rendering, item rendering, or
any gameplay system. Because it ships with **zero mixins**, there is no
mixin-conflict surface at all, which makes it about as safe a neighbor as a
Fabric mod can be for:

- Sodium / Lithium / FerriteCore / ModernFix / Iris
- Mod Menu (no explicit integration is included yet - see Roadmap - but
  ActionHud does not need it to work, and won't conflict with it)

## Roadmap

- [ ] Mod Menu integration for the settings screen
- [ ] Draggable sliders as an alternative to the click-to-cycle buttons
- [ ] Per-action custom colors
- [ ] A resource-pack-friendly way to override action icons

## Contributing

Issues and pull requests are welcome. The codebase is organized by
responsibility (`action` for detection, `animation` for tweening, `hud` for
layout/rendering, `config` for settings, `render` for drawing primitives) -
adding a new action means adding one small class under `action.detector` and
one line in `ActionManager.createDefault()`; nothing else needs to change.

## Credits

Created by **IAMSOCOOL**.

## License

[MIT](LICENSE) &copy; 2026 IAMSOCOOL

---
