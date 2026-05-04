# pokefirered-et — Translation File Reference

---

## 1. Map dialogue and scripts

Each map folder under `data/maps/` contains up to three relevant files:

- `scripts.inc` — event script logic (msgbox calls, conditionals, item/flag triggers)
- `text.inc` — the actual dialogue strings for that map
- `events.inc` — NPC and trigger placement (rarely needs text changes, but trainer names live here)

There are roughly **350+ maps** with a `text.inc`. Prioritize story-critical locations first:

| Priority | Maps |
|---|---|
| High | `PalletTown*`, `PalletTown_ProfessorOaksLab`, `ViridianCity*`, `PewterCity*`, `CeruleanCity*`, `SaffronCity*`, `VermilionCity*`, `LavenderTown*`, `CeladonCity*`, `FuchsiaCity*`, `CinnabarIsland*` |
| High | `PokemonLeague_*` (all Elite Four / Champion rooms) |
| High | `SilphCo_*` (all floors) |
| Medium | `Route*` buildings and entrances with `text.inc` |
| Medium | `OneIsland*` through `SevenIsland*` (Sevii Islands story) |
| Low | Generic rest houses, duplicate layouts, unused maps |

---

## 2. Global / shared text files

These are not tied to a single map and cover system-wide strings.

### `data/text/`
| File | Contents |
|---|---|
| ~~aide.inc~~ | ~~Professor's Aide dialogue~~ |
| ~~berries.inc~~ | ~~Berry descriptions and names~~ |
| `braille.inc` | Braille puzzle text (Sealed Chamber etc.) |
| ~~competitive_brothers.inc~~ | ~~Move tutor brothers dialogue~~ |
| `day_care.inc` | Day-care couple dialogue |
| `eon_ticket.inc` | Eon Ticket event text |
| `fame_checker.inc` | Fame Checker entries |
| `flavor_text.inc` | Item flavor descriptions |
| ~~help_system.inc~~ | ~~In-game help menu text~~ |
| ~~ingame_trade.inc~~ | ~~In-game trade NPC dialogue~~ |
| ~~itemfinder.inc~~ | ~~Itemfinder responses~~ |
| ~~new_game_intro.inc~~ | ~~Oak's intro monologue~~ |
| ~~obtain_item.inc~~ | ~~Item-receive messages~~ |
| ~~pc.inc~~ | ~~PC system text~~ |
| ~~pc_transfer.inc~~ | ~~PC transfer messages~~ |
| `pokedex_rating.inc` | Oak's Pokédex rating dialogue |
| `pokedude.inc` | Teachy TV Pokédude dialogue |
| ~~poke_mart.inc~~ | ~~Poké Mart clerk dialogue~~ |
| ~~route23.inc~~ | ~~Victory Road gate guard dialogue~~ |
| `safari_zone.inc` | Safari Zone warden/entry text |
| ~~save.inc~~ | ~~Save system messages~~ |
| `seagallop.inc` | Seagallop ferry dialogue |
| `sign_lady.inc` | Sign and notice board text |
| ~~surf.inc~~ | ~~Surf-related field messages~~ |
| `trainer_card.inc` | Trainer card labels |
| `trainers.inc` | Trainer pre/post battle dialogue |
| ~~white_out.inc~~ | ~~Blacking out messages~~ |

### `data/scripts/`
These contain shared script logic with embedded text or msgbox references. Some have translatable strings baked in.

| File | Notes |
|---|---|
| `bag_full.inc` | "Bag is full" message |
| `field_moves.inc` | HM use prompts (Cut, Surf, etc.) |
| `flash.inc` | Flash HM prompt |
| `hole.inc` | Hole fall text |
| `move_tutors.inc` | Move tutor offer/decline strings |
| `mystery_event_club.inc` | Mystery Gift club text |
| `obtain_item.inc` | Shared item-obtain logic |
| `pkmn_center_nurse.inc` | Nurse Joy healing dialogue |
| `pokemon_league.inc` | League gate guard text |
| `pokemon_mansion.inc` | Mansion journal entries |
| `repel.inc` | Repel wore-off message |
| `safari_zone.inc` | Safari Zone entry/exit |

---

## 3. Pokémon and species data

### `src/data/text/`
| File | Contents |
|---|---|
| `species_names.h` | All 386 Pokémon names |
| `move_names.h` | All move names |
| `abilities.h` | All ability names |
| `nature_names.h` | Nature names (Hardy, Lonely, etc.) |
| `trainer_class_names.h` | Trainer class names (Bug Catcher, Lass, etc.) |
| `quest_log.h` | Quest log entry strings |
| `teachy_tv.h` | Teachy TV show text |

### `src/data/pokemon/`
| File | Contents |
|---|---|
| `pokedex_entries.h` | Pokédex entry flavor text for all species |
| `pokedex_categories.h` | Species category names (e.g. "Seed Pokémon") |
| `pokedex_text.h` | FireRed Pokédex text strings |
| `pokedex_text_fr.h` | FireRed-specific alternate Pokédex text |

---

## 4. Item data

### `src/data/`
| File | Contents |
|---|---|
| `items.h` | Item names and descriptions for all items |

### `data/text/flavor_text.inc`
Item flavor text (longer descriptions shown in bag).

---

## 5. Battle messages

### `src/` (C source — string literals or string ID references)
| File | Notes |
|---|---|
| `battle_message.c` | Most in-battle message strings; heavy translation burden |
| `strings.c` | General game strings (level up, evolution, etc.) |

These files use the game's custom string encoding. Strings are defined with `_()` macros and compiled via `preproc`. Edit the `.c` source; do not edit `.o` build artifacts.

---

## 6. UI and menus

| File | Contents |
|---|---|
| `src/data/text/quest_log.h` | Quest log UI labels |
| `src/data/easy_chat/easy_chat_group_*.h` | Easy Chat word lists (all groups) |
| `src/data/easy_chat/easy_chat_groups.h` | Easy Chat group names |
| `data/text/help_system.inc` | Help system entries |

---

## 7. Fonts and character encoding

| File | Notes |
|---|---|
| ~~charmap.txt~~ | ~~Character encoding table — **must be extended** for Estonian characters (ä, ö, ü, õ, š, ž)~~ |
| `graphics/fonts/latin_normal.latfont` | Main Latin font bitmap |
| `graphics/fonts/latin_male.latfont` | Male protagonist font |
| `graphics/fonts/latin_female.latfont` | Female protagonist font |
| `graphics/fonts/latin_small.latfont` | Small font variant |

Extending `charmap.txt` and the `.latfont` bitmaps is a prerequisite for any characters outside the base Latin set.

---

## 8. Localization notes file

| File | Notes |
|---|---|
| `TÕLKED.md` | Existing translation notes in the repo root — keep updated as conventions are established |

---

## Suggested edit order

1. `charmap.txt` + `graphics/fonts/*.latfont` — unblock Estonian characters first
2. `src/data/text/species_names.h`, `move_names.h`, `abilities.h` — core terminology
3. `src/data/pokemon/pokedex_entries.h` + `pokedex_categories.h` — Pokédex
4. `src/data/items.h` + `data/text/flavor_text.inc` — items
5. `data/text/new_game_intro.inc` + `PalletTown*` / `PalletTown_ProfessorOaksLab` — opening sequence
6. All remaining `data/maps/*/text.inc` in story order
7. `src/battle_message.c` + `src/strings.c` — battle and system strings
8. `src/data/easy_chat/` — Easy Chat (lowest gameplay priority)