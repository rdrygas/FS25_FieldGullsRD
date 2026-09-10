# FS25 Field Gulls

Field Gulls adds animated gull flocks that follow working field implements and feed on freshly worked ground in Farming Simulator 25.

> This repository is a fork of the original [FS25_FieldGulls project by sprkem](https://github.com/sprkem/FS25_FieldGulls). The fork is maintained at [rdrygas/FS25_FieldGulls](https://github.com/rdrygas/FS25_FieldGulls) and contains additional fixes and behavior changes described below.

## Description

The mod makes fieldwork feel more alive by attracting gulls to plows, cultivators, and sowing machines. Birds approach gradually, search the area worked by their associated implement, land to feed, and take flight when a vehicle gets too close.

Gulls are active only in daylight and dry weather. Starting work at night or during rain, snow, or hail does not activate a flock. If night falls or precipitation begins while a flock is active, no more birds spawn and the existing delayed, gradual departure sequence starts.

## Assumptions

- Farming Simulator 25 on PC/Mac.
- The mod applies generally to vehicles and implements using the standard plow, cultivator, or sowing-machine specializations.
- No map-specific configuration or external dependency is required.
- Bird behavior is visual and does not change field yield, crop growth, soil state, or operating costs.
- Multiplayer is declared as supported in `modDesc.xml`; see [Compatibility](#compatibility) for the current verification status.

## Features

- Animated gulls with approach, diving, feeding, searching, fleeing, and departure behavior.
- Support for plows, cultivators, and sowing machines using standard FS25 work areas.
- Per-tool feeding zones, so gulls feed only on ground worked by their associated implement.
- Collision-aware fleeing from nearby vehicles.
- Gradual spawning and departure instead of an entire flock appearing or disappearing at once.
- Continuous daylight and precipitation checks.
- Configurable flock size, appearance chance, sound volume, and number of simultaneous active tools.
- English, Polish, German, and French localization for the settings menu.
- Settings saved locally in `modSettings/FieldGulls.xml`.

## How it works

When a supported implement begins working, the mod records its freshly processed work area. If the environment is suitable, the active-tool limit has not been reached, and the appearance roll succeeds, a flock containing 50–100% of the configured maximum number of birds begins to arrive.

Each flock remains associated with its implement. Birds select feeding targets from that tool's recent work area and flee when a vehicle approaches their position. When work stops, the tool disappears, night begins, or precipitation starts, the flock uses the existing delayed departure sequence and birds leave one by one.

| Condition | Result |
|---|---|
| A supported implement works during daylight in dry weather | The mod may activate a flock, subject to chance and the active-tool limit. |
| The appearance roll succeeds | A random flock of 50–100% of the configured maximum begins spawning gradually. |
| The appearance roll fails | That implement cannot roll for another flock for 30 real-time minutes, independently of game time. |
| Work begins at night or during rain, snow, or hail | No flock is activated and no random-failure timeout is applied. |
| Night or precipitation begins while birds are active | Further spawning stops and the delayed, gradual departure mechanism starts. |
| Work stops | The flock begins its normal departure sequence after a 15-second delay. |
| Work resumes during the delay in suitable conditions | The pending departure is cancelled and the flock remains active. |
| A vehicle approaches a feeding bird | The bird abandons its ground target and takes flight. |
| Several supported tools work simultaneously | Each flock uses only the feeding area belonging to its own tool, up to the configured active-tool limit. |

## Installation

1. Download the released `FS25_FieldGulls.zip` archive.
2. Copy it without unpacking to the Farming Simulator 25 `mods` directory.
3. Enable **Field Gulls** when loading or creating a savegame.

Typical Windows directory:

```text
%USERPROFILE%\Documents\My Games\FarmingSimulator2025\mods
```

The ZIP must contain `modDesc.xml` at its root. Do not place all mod files inside an additional directory within the archive.

## Configuration

Open the in-game settings menu and find the **Field Gulls** section. Changes are saved immediately and reused in later sessions.

| Setting | Default | Available values | Description |
|---|---:|---|---|
| Bird Sound Volume | 100% | 0–200% in 20% steps | Controls flock sound volume. Set it to 0% to disable bird sounds. |
| Maximum Birds | 80 | 10–100 in steps of 10, then 120–200 in steps of 20 | Upper limit for one flock. The actual flock contains 50–100% of this value. |
| Chance of Birds | 70% | 10–100% in 10% steps | Chance that a flock is selected when eligible work begins. |
| Max Active Tools | 2 | 1–10 or Unlimited | Limits how many tools may have active flocks at the same time. |

The settings file is stored in the Farming Simulator 25 user profile:

```text
modSettings/FieldGulls.xml
```

## Compatibility

- Game: Farming Simulator 25 (`descVersion` 107).
- Supported work types: standard plowing, cultivating, and sowing work areas.
- Existing savegames: compatible; no new savegame is required.
- Multiplayer: declared as supported by the mod metadata, but this fork does not add explicit network synchronization. Bird simulation and settings run client-side and multiplayer behavior has not been verified.
- Known mod conflicts: none documented. Mods that replace the same specialization callbacks may affect compatibility.

## Known limitations

- Only implements exposing the standard `Plow`, `Cultivator`, or `SowingMachine` specializations are detected.
- Appearance chance is evaluated when work changes from inactive to active. If work starts in unsuitable conditions and continues without interruption, a flock is not activated merely because daylight or dry weather later returns.
- A failed appearance roll uses a 30-minute timeout, although the current in-game tooltip says one hour.
- Environmental departure retains the normal 15-second delay, so birds already present do not vanish immediately when night or precipitation begins.
- Very large flock limits and many simultaneous active tools can reduce performance.
- Multiplayer behavior is not currently verified.

## Troubleshooting

If the mod does not work:

1. Confirm that `FS25_FieldGulls.zip` is directly inside the game's `mods` directory.
2. Open the ZIP and verify that `modDesc.xml` is at its root.
3. Confirm that the mod is enabled for the current savegame.
4. Test with a standard plow, cultivator, or sowing machine during daylight and dry weather.
5. Temporarily set **Chance of Birds** to 100% and check that the **Max Active Tools** limit has not been reached.
6. Review `log.txt` for entries containing `[FieldGulls]`, Lua errors, or mod-loading errors.

Typical Windows log location:

```text
%USERPROFILE%\Documents\My Games\FarmingSimulator2025\log.txt
```

When reporting a problem, include the game version, mod version, affected implement, weather and time-of-day conditions, reproduction steps, and the relevant section of `log.txt`.

## Changelog

### Fork changes after 1.0.0.1

- Restricted flock activation to daylight and dry weather.
- Added continuous environment checks while a flock is active.
- Reused the gradual departure mechanism when night or precipitation begins.
- Prevented environmental restrictions from starting the random-failure timeout.

### 1.0.0.1 (upstream)

- Restricted each flock to ground worked by its associated tool.
- Added the maximum-active-tools setting.
- Added Polish localization.

## Fork and credits

- Original mod author: **Ozz**.
- Original repository: [sprkem/FS25_FieldGulls](https://github.com/sprkem/FS25_FieldGulls).
- Fork repository and maintenance: [rdrygas/FS25_FieldGulls](https://github.com/rdrygas/FS25_FieldGulls).
- Polish translation credits recorded by the upstream project: **KITT3000** in `modDesc.xml` and **Ziuta** in the Polish localization file.

This fork is not presented as the original upstream release. Please report fork-specific problems to the fork repository.

## AI disclosure

Parts of the fork's code and documentation were prepared with assistance from OpenAI ChatGPT/Codex. The maintainer remains responsible for reviewing, testing, distributing, and licensing the project.

## License

No license file is currently included in this repository. The original author's rights therefore remain reserved unless the upstream project or another authoritative source states otherwise.
