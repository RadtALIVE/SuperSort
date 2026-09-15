<p align="center">
  <img src="./assets/supersort-banner.svg" alt="SuperSort banner" width="100%" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/release-v1.0.0-blue" alt="release v1.0.0" />
  <img src="https://img.shields.io/badge/BepInEx-IL2CPP-orange" alt="BepInEx IL2CPP" />
  <img src="https://img.shields.io/badge/license-MIT-blue" alt="license MIT" />
</p>

# <img src="./assets/supersort-logo.svg" width="32" align="top" /> SuperSort

A BepInEx mod for Supermarket Simulator that automatically labels empty, compatible shelf slots for unassigned products. It only handles the assignment — your restockers still do all the actual stocking, exactly as before. Toggle on/off anytime with F6.

> ⚠️ **Please back up your save before using SuperSort.** This mod is currently in **BETA** — it writes label/assignment state to display slots at runtime, and while it's designed to avoid touching anything else, it hasn't been tested across the full range of saves, shelf types, and game versions yet. Unexpected interactions are possible, especially early on. Keeping a backup means you can always roll back if something looks off, with zero risk to your progress. This warning will be relaxed once SuperSort has had more testing and reports come back clean.

## Why

Supermarket Simulator's restockers are good at their job — once a shelf slot is labeled for a product, they'll find it in storage or off the delivery truck and carry it over themselves, no help needed. The tedious part isn't the restocking. It's clicking through every empty slot yourself to tell the game what belongs where before any of that can even start.

SuperSort skips that one click. Everything downstream — sourcing stock, choosing storage over a fresh delivery, carrying the box, stocking the shelf — stays exactly as it was. **Your restockers keep doing their actual job; SuperSort just stops making you do theirs.**

## Features

- **Automatic shelf labeling** — scans for products without a display assignment and labels a compatible empty slot for them, on a configurable interval.
- **Real compatibility checks** — reuses the game's own slot-compatibility logic instead of guessing which products belong where.
- **Duplicate-safe** — never assigns a product that already has a pending or active display slot, and never overwrites an existing label.
- **Assignment only** — doesn't spawn, move, or place a single product. Storage vs. delivery-truck sourcing, box carrying, and shelf stocking are entirely up to the game's normal restocker AI.
- **F6 toggle** — off by default. Press F6 in-game to turn assignment on or off at any time; toggling off never undoes labels you already have.

## Installation

1. Install [BepInEx](https://github.com/BepInEx/BepInEx) (IL2CPP build) for Supermarket Simulator, if you haven't already.
2. Download `SuperSort.dll` from the [Releases](../../releases) page.
3. Copy it to:

   ```
   Supermarket Simulator\BepInEx\plugins\SuperSort\SuperSort.dll
   ```

4. Launch the game and load a save.

## Usage

1. Press **F6** to enable SuperSort. You'll see a confirmation in the BepInEx log.
2. That's it — SuperSort scans in the background and labels empty, compatible slots for unassigned products as it finds them.
3. Press **F6** again any time to pause new assignments. Slots it already labeled stay labeled.

## Configuration

A config file is generated on first run at `BepInEx\config\boi.supersort.cfg`:

| Setting | Default | Description |
|---|---|---|
| `ScanIntervalSeconds` | `1.0` | How often SuperSort checks for unassigned products. |
| `VerboseLogging` | `false` | Log every individual assignment decision. |

## What SuperSort does not do

- Does not move, spawn, or place products.
- Does not touch storage, delivery, or restocker AI in any way.
- Does not modify save files.
- Does not require a bundled .NET runtime — it's a normal framework-dependent BepInEx plugin.

## Building from source

```
dotnet build -c Release -p:GameDir="path\to\Supermarket Simulator"
```

Requires the .NET 8 SDK. Output: `bin\Release\net8.0\SuperSort.dll`.

## License

MIT. See [LICENSE](./LICENSE).
