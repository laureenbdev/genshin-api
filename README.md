# Genshin API

## Description

A public GitHub raw API providing comprehensive game data for Genshin Impact.
This API may contain errors and/or missing contents. Feel free to contact me or open a pull request.

**Use Cases:**
- Build character and weapon databases for web applications
- Create team composition calculators and build optimizers
- Develop farming guides and resource planners
- Power fan websites, wikis, and community tools
- Integrate Genshin Impact data into Discord bots or other applications

**Important Note:** This is a raw JSON API hosted on GitHub. Since it's a static file service, you cannot apply filters or query parameters directly in the request. You must retrieve the complete dataset and implement filtering logic in your application code.

## Credits

This API is made by Mei, a french web developer.

**GitHub:** [@meihwg](https://github.com/meihwg)

**Portfolio:** [https://meihwg.github.io/](https://meihwg.github.io/)

This API was made for my website (under construction) La Taverne de Jade.

**Link:** [https://meihwg.github.io/genshin/](https://meihwg.github.io/taverne-de-jade/)

**Discord:** [https://discord.gg/Urwmqt9jgK](https://discord.gg/Urwmqt9jgK)

## API Endpoints

### Base URL

All data endpoints use the following base URL:
```
https://raw.githubusercontent.com/meihwg/genshin-api/main/
```

### Data Files

#### Game Data
**Endpoint:** `game-data.json`

Contains comprehensive ascension cost data for the game:
- **Character Level Ascension**: Material requirements and Mora costs for each phase (1-6)
- **Talent Leveling**: Costs and materials needed for talent levels 2-10
- **Weapon Ascension**: Material requirements for weapon ascension phases 1-6

**Example:**
```
https://raw.githubusercontent.com/meihwg/genshin-api/main/game-data.json
```

#### Characters
**Endpoint:** `characters.json`

Provides detailed information about all playable characters including:
- Character ID, name, and rarity (4★ or 5★)
- Element type (Anemo, Geo, Electro, Dendro, Hydro, Pyro, Cryo)
- Weapon type (Sword, Claymore, Polearm, Catalyst, Bow)
- Region of origin
- Ascension materials types required (boss drops, local specialties, common enemy drops, talent books, weekly boss drops)

**Example:**
```
https://raw.githubusercontent.com/meihwg/genshin-api/main/characters.json
```

#### Weapons
**Endpoint:** `weapons.json`

Contains comprehensive weapon data including:
- Weapon ID, name, and type
- Rarity (1★ to 5★)
- Base attack values at level 1 and level 90
- Secondary stat values at level 1 and level 90
- Passive ability name and description
- Ascension materials types required (weapon materials, common enemy drops, elite enemy drops)

**Example:**
```
https://raw.githubusercontent.com/meihwg/genshin-api/main/weapons.json
```

#### Materials
**Endpoint:** `materials.json`

Farmable resources used by the planner. Each item has a name, rarity, family (the same label as in `characters.json` / `weapons.json`), a source (`domain`, `boss`, `weekly`, `leyline` or `overworld`), the weekday rotation when it comes from a domain, a resin cost, and an image path.

The file also lists character EXP between ascension levels, and the World Level 8 yields used to estimate the minimum resin (60 000 Mora or 5 Hero's Wit per ley line, 2 Philosophies per talent run, 1 highest weapon stone per forgery run, 3 world-boss drops, 2 weekly-boss drops).

**Example:**
```
https://raw.githubusercontent.com/meihwg/genshin-api/main/materials.json
```

#### Artifacts
**Endpoint:** `artifacts.json`

Artifact sets with rarity, source (`domain` or `boss`) and an image path.

**Example:**
```
https://raw.githubusercontent.com/meihwg/genshin-api/main/artifacts.json
```

#### Achievements
**Endpoint:** `achievements.json`

Every achievement, grouped by the in-game series. Each series has an English name, a French name and an icon. Each achievement has a name and description in both languages, the count required to complete it, the primogem reward and the version that added it. Tiers of the same achievement share a `chain` id. `rewardImage` is the primogem icon.

**Example:**
```
https://raw.githubusercontent.com/meihwg/genshin-api/main/achievements.json
```

#### Quests
**Endpoint:** `quests.json`

Quests grouped the way the quest menu does: Archon quests, story quests, hangouts, world quests, commissions and event quests. Each chapter has an English and French name, the act label when there is one, the region or character it belongs to, and the chapter icon. Each quest inside it has a name, a description and, when the game grants them, primogems, Mora and adventure experience. `rewardImage` is the primogem icon.

**Example:**
```
https://raw.githubusercontent.com/meihwg/genshin-api/main/quests.json
```

#### Viewpoints
**Endpoint:** `viewpoints.json`

Every viewpoint in the Archive, grouped by nation and then by region. Each nation has an English name, a French name and its chapter icon. Each region does the same. A viewpoint has a name, a description and, when the spot is more precise than the region, a place, all in English and French. `image` is the in-game scenery photo.

**Example:**
```
https://raw.githubusercontent.com/meihwg/genshin-api/main/viewpoints.json
```

### Images

**Base URL for Images:**
```
https://raw.githubusercontent.com/Eticeo/genshin-api/main/images/
```

#### Character Images
**Format:** `characters/[characterId].png`

Get character portrait images using the character's ID from the characters.json file.

**Example:**
```
https://raw.githubusercontent.com/Eticeo/genshin-api/main/images/characters/albedo.png
https://raw.githubusercontent.com/Eticeo/genshin-api/main/images/characters/raiden_shogun.png
```

Other images use the path stored on each entry:

```
https://raw.githubusercontent.com/meihwg/genshin-api/main/images/materials/philosophies_of_ballad.png
https://raw.githubusercontent.com/meihwg/genshin-api/main/images/artifacts/gladiators_finale.png
https://raw.githubusercontent.com/meihwg/genshin-api/main/images/achievements/wonders_of_the_world.png
https://raw.githubusercontent.com/meihwg/genshin-api/main/images/achievements/primogem.png
https://raw.githubusercontent.com/meihwg/genshin-api/main/images/quests/mengde.png
https://raw.githubusercontent.com/meihwg/genshin-api/main/images/quests/primogem.png
https://raw.githubusercontent.com/meihwg/genshin-api/main/images/viewpoints/mondstadt.png
https://raw.githubusercontent.com/meihwg/genshin-api/main/images/viewpoints/the_city_of_wind.png
```

## Usage Examples

### Fetching Character Data
```javascript
// Fetch all characters
const response = await fetch('https://raw.githubusercontent.com/meihwg/genshin-api/main/characters.json');
const characters = await response.json();

// Filter by element
const pyroCharacters = characters.filter(char => char.element === 'pyro');

// Find specific character
const albedo = characters.find(char => char.id === 'albedo');
```

### Fetching Weapon Data
```javascript
// Fetch all weapons
const response = await fetch('https://raw.githubusercontent.com/meihwg/genshin-api/main/weapons.json');
const weapons = await response.json();

// Filter by type
const swords = weapons.filter(weapon => weapon.type === 'sword');

// Filter by rarity
const fiveStarWeapons = weapons.filter(weapon => weapon.rarity === 5);
```

### Fetching Game Data
```javascript
// Fetch game data
const response = await fetch('https://raw.githubusercontent.com/meihwg/genshin-api/main/game-data.json');
const gameData = await response.json();

// Access character level ascension costs
const characterAscension = gameData[0].ascension_values.character_level;

// Access talent leveling costs
const talentCosts = gameData[0].ascension_values.talents;

// Access weapon ascension costs
const weaponAscension = gameData[0].ascension_values.weapons;
```




