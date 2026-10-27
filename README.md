# NES Co-op Mods

> **NO ROMS INCLUDED.** These are patches, not games. Each one needs your own copy of the
> original NES game and turns it into the mod. A patch holds only the mod's changes: the
> original game's code and graphics come from your ROM.

Experimental, unofficial fan mods that add co-op and multiplayer play to ten NES games, as BPS
patches: Super Mario Bros. for up to four players, Metroid, Castlevania, Zelda II and Kid Icarus
for two at once, and more, 14 mods in all. Not made or endorsed by Nintendo, Konami or The Tetris
Company.

These are experiments, and each one has rough edges: every mod's section lists its known issues.
Please report problems on the [Issues](https://github.com/benj-edwards/NESCoopMods/issues) page, with the mod and
its version, the emulator or flash cart, and where in the game it happened.

## The mods

| Mod | Players | Made from | Version |
|---|---|---|---|
| [Super Duper Mario Bros. 4P](#super-duper-mario-bros-4p) | 1-4 at once (Four Score) | Super Mario Bros. | v45 |
| [Super Mario Bros. Co-op](#super-mario-bros-co-op) | 1-2 at once | Super Mario Bros. | v45 |
| [Super Mario Bros. Zapper](#super-mario-bros-zapper) | 1-2 at once, plus a Zapper | Super Mario Bros. | v45 |
| [Super Mario Bros. 3 Co-op](#super-mario-bros-3-co-op) | 1-2 at once | Super Mario Bros. 3 | v9 |
| [Mario Bros. Extra](#mario-bros-extra) | 1-2 at once | Super Mario Bros. 3 | v5 |
| [Wrecking Crew Co-op](#wrecking-crew-co-op) | 1-4 at once (Four Score) | Wrecking Crew | v2 |
| [Excitebike 4-Player](#excitebike-4-player) | 1-4 at once (Four Score) | Excitebike | v2 |
| [Metroid Co-op](#metroid-co-op) | 1-2 at once | Metroid | v2.6 |
| [Castlevania Co-op](#castlevania-co-op) | 1-2 at once | Castlevania | v6 |
| [Zelda II Co-op](#zelda-ii-co-op) | 1-2 at once | Zelda II: The Adventure of Link | v5 |
| [Kid Icarus Co-op](#kid-icarus-co-op) | 1-2 at once | Kid Icarus | v1.1 |
| [Punch-Out!! Vs](#punch-out-vs) | 2 (player 2 is the opponent) | Mike Tyson's Punch-Out!! | v3 |
| [Punch-Out!! Two Macs](#punch-out-two-macs) | 1-2 at once | Mike Tyson's Punch-Out!! | v3 |
| [Co-op Tetris](#co-op-tetris) | 1-2 at once | Tetris | v4 |

## Applying a patch

1. Find your mod's section below, and the row of its patch table that matches your ROM file
   (its CRC32 or SHA-1). `shasum "file.nes"` (Mac) or `sha1sum "file.nes"` (Linux) prints the
   SHA-1; RomPatcher.js and most ROM managers show the CRC32.
2. Apply the patch with any BPS patcher:
   - **RomPatcher.js** (in a web browser): <https://www.marcrobledo.com/RomPatcher.js/>. Pick
     your ROM and the `.bps` file, then *Apply patch*.
   - **Floating IPS** (Windows, Linux): *Apply Patch*, the `.bps`, then your ROM.
   - On the command line (Floating IPS):

     ```
     flips --apply SuperMarioBrosCoop-v45.bps "Super Mario Bros. (World).nes" "Super Mario Bros Co-op.nes"
     ```
3. The section gives the result's size, CRC32 and SHA-1, to check it.

**Headers.** An NES ROM file starts with a 16-byte header, and copies of the same game come with
different ones. Each table has a patch for the file with an iNES header and, where there is one,
for the same data with the NES 2.0 header of the newer ROM sets. Every patch writes the mod's
whole header itself and never reads yours, so if only the header differs (the data after the
first 16 bytes matches the checksums under the table), the result is the same:

- RomPatcher.js warns that the checksum doesn't match, and *Apply patch* still makes the right
  ROM.
- Floating IPS refuses. Give it `--ignore-checksum`, or put the table's header in the first 16
  bytes with a hex editor first.
- Don't use RomPatcher.js's option to remove the header: it puts your old header back on, and
  the ROM won't work.

If the data after the header doesn't match either, your copy is another revision or dump of the
game, and the patch won't make a working ROM from it.

## Playing them

- Each section names the board (mapper) the patched ROM uses. Emulators and flash carts that
  have that board load it like any other NES ROM.
- Super Mario Bros. 3 Co-op uses the MMC5 mapper: see its section.
- The four-player mods need the Four Score turned on, and Super Mario Bros. Zapper needs a
  Zapper in controller port 2 (see its section).

### Three or four players (NES Four Score)

Super Duper Mario Bros. 4P, Wrecking Crew Co-op and Excitebike 4-Player take up to four players.

- **On an NES,** players 3 and 4 plug into an **NES Four Score** or **NES Satellite** with its
  switch on 4 players. On a Famicom, controllers in the expansion port are players 3 and 4.
- **In an emulator,** turn the Four Score (or 4-player adapter) on in the input settings.
  Emulators turn it on by themselves only for the commercial four-player games in their
  databases, so without it, players 3 and 4 do nothing.
  - Mesen, FCEUX, Nestopia UE: the Four Score in the controller settings.
  - RetroArch, FCEUmm core: Quick Menu > Controls > Port 3 Controls > Device Type > Gamepad,
    the same for Port 4, then Manage Remap Files > Save Core Remap File.
  - RetroArch, Nestopia core: Quick Menu > Core Options > 4 Player Adapter > NTSC, then ports 3
    and 4 as for FCEUmm.
  - MAME:

    ```
    mame nes -cart "Super Duper Mario Bros 4P.nes" -ctrl1 4score_p1p3 -ctrl2 4score_p2p4
    ```
  - OpenEmu gives players 1 and 2 only.

## Super Duper Mario Bros. 4P

Super Mario Bros. for **up to four players at once**, on one screen, as **Mario, Luigi, Toad or Princess Peach**. Version v45, an unofficial fan mod of Super Mario Bros.

**What it does**

- **1 to 4 players at once** with an NES Four Score (or NES Satellite). Players 1 and 2 work without one.
- **Pick a character** on the title screen with left/right on your own controller: Mario, Luigi, Toad or Princess Peach (no two players the same; Peach floats as in Super Mario Bros. 2). Each has a fire form.
- **Join at any time:** a controller without a player presses Start to come in; a player out of lives presses Start to continue.
- **One shared screen:** a stuck player is brought along, a player who loses a life comes back next to a partner (with a life from the partner who has the most, if their own are gone), and the level starts over only when everyone is down.
- **An item for every player** in every power-up block.
- **Bounce** off each other's heads.
- **Bubbles:** press Select to float safely in a bubble behind a teammate; Select again pops you out next to them.
- **Infinite lives mode** on the title screen.
- The status bar shows every player's score and coins; the castle says THANK YOU EVERYONE!
- In the 8-4 ending, with a Peach playing, the princess in the castle is Rosalina.
- 1 PLAYER GAME with Mario is the original game.

**How to play**

- **Title screen:** Select steps through 1, 2, 3 and 4 PLAYER GAME, then the same with INFINITE LIVES; left/right on each controller picks that player's character; Start begins.
- **In play:** Select goes into a bubble or out of it; Start on a controller without a player joins or continues; Start on any controller pauses.
- Players 3 and 4 need the Four Score: see [Three or four players](#three-or-four-players-nes-four-score).

**Known issues**

- **Flicker:** the NES draws at most 8 sprites on a line, and a big character is 8 sprites, so with four players and enemies on the same lines, sprites flicker.
- **Slowdown:** with four players, busy scenes slow down; four players running through 11 busy levels ran at 92-100% of full speed.
- **Colors:** Peach has red hair and a white dress (the sprite palettes have no pink or yellow), and with Luigi in a water, underground or castle level, some enemies show their above-ground colors.
- The purple flower (the giant) and walking back are in Super Mario Bros. Co-op only.

**Patches.** No ROM included: you need your own copy of Super Mario Bros. Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Super Mario Bros. (World), iNES header | 40,976 bytes | `3337EC46` | `ea343f4e445a9050d4b4fbac2c77d0693b1d0922` | [`SuperDuperMarioBros4P-v45.bps`](patches/SuperDuperMarioBros4P/SuperDuperMarioBros4P-v45.bps) |
| Super Mario Bros. (World), NES 2.0 header | 40,976 bytes | `393A432F` | `33d23c2f2cfa4c9efec87f7bc1321ce3ce6c89bd` | [`SuperDuperMarioBros4P-v45-nes2header.bps`](patches/SuperDuperMarioBros4P/SuperDuperMarioBros4P-v45-nes2header.bps) |

The game data after the 16-byte header: Super Mario Bros. (World): CRC32 `D445F698`, SHA-1 `facee9c577a5262dbe33ac4930bb0b58c8c037f7`.

The result: 262,160 bytes, CRC32 `878E5C3D`, SHA-1 `187c0c195aff620016f76dd6f8183ae5e82cc872`. MMC3 (mapper 4), 256 KB PRG ROM, 8 KB CHR RAM, 8 KB work RAM, NES 2.0 header. Four players have played it on a real NES with an NES Four Score.

## Super Mario Bros. Co-op

Super Mario Bros. for **two players at once**, on one screen, as Mario, Luigi, Toad or Princess Peach, with a giant power-up, bubbles and walking back. Version v45, an unofficial fan mod of Super Mario Bros.

**What it does**

- Two players on one screen, each on their own controller. Players can't hurt or block each other.
- **Pick a character** each: Mario, Luigi, Toad or Peach (no two the same; Peach floats as in Super Mario Bros. 2). Fire Luigi has his own colors.
- **The screen** follows the leader but doesn't leave the other player behind: after 2 seconds of pushing at the edge, the partner pops up beside you.
- **Two items in each power-up block,** one per hit, each matched to the size of the player who hits it.
- A player who loses a life comes back beside the partner (with their own life or the partner's); the level starts over only when both are down.
- **Join and continue:** player 2 presses Start at any time to come in; a player out of lives continues with 3 lives (score and coins back to 0).
- **The purple flower:** a power-up block hit while fiery gives a purple flower, which makes you a **giant** for 5 seconds: twice the size, smashing blocks and knocking out enemies.
- **Bubbles:** Select floats you safely behind your partner, through pipes, vines and restarts and onto the flagpole; Select again to come out.
- **Walking back:** the screen scrolls left, back to the start of the area, past pipes and the halfway point.
- **Infinite lives mode** on the title screen.
- 1 PLAYER GAME with Mario is the original game, frame for frame.

**How to play**

- **Title screen:** Select picks 1 or 2 PLAYER GAME (each also with INFINITE LIVES); left/right on each controller picks the character; Start begins.
- **In play:** Select goes into a bubble or out of it; Start on controller 2 joins or continues (left/right to pick a character, then A or Start); Start pauses.

**Known issues**

- A little slowdown in the busiest levels.
- Underground blue Koopas and Piranha Plants look green when Luigi plays.
- The giant has no recharge meter and throws no giant fireballs.
- While a purple flower is out, things drawn with the white of the second sprite palette (red Koopas, fireballs) turn purple.

**Patches.** No ROM included: you need your own copy of Super Mario Bros. Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Super Mario Bros. (World), iNES header | 40,976 bytes | `3337EC46` | `ea343f4e445a9050d4b4fbac2c77d0693b1d0922` | [`SuperMarioBrosCoop-v45.bps`](patches/SuperMarioBrosCoop/SuperMarioBrosCoop-v45.bps) |
| Super Mario Bros. (World), NES 2.0 header | 40,976 bytes | `393A432F` | `33d23c2f2cfa4c9efec87f7bc1321ce3ce6c89bd` | [`SuperMarioBrosCoop-v45-nes2header.bps`](patches/SuperMarioBrosCoop/SuperMarioBrosCoop-v45-nes2header.bps) |

The game data after the 16-byte header: Super Mario Bros. (World): CRC32 `D445F698`, SHA-1 `facee9c577a5262dbe33ac4930bb0b58c8c037f7`.

The result: 262,160 bytes, CRC32 `5E06B1F9`, SHA-1 `9fc49680f445066c4f54ab87e63893110a5eb6d0`. MMC3 (mapper 4), 128 KB PRG ROM, 128 KB CHR ROM, 8 KB work RAM, NES 2.0 header.

## Super Mario Bros. Zapper

Super Mario Bros. Co-op plus an **NES Zapper**: a helper with the light gun shoots enemies, blocks, coins and scenery, and can make a player a giant. Or **SHOOTING CRUISE**, where the game plays Mario through all 32 levels and the gunner keeps him alive. Version v45, an unofficial fan mod of Super Mario Bros.

**What it does**

- **The Zapper in controller port 2:** a shot knocks out an enemy as a fireball would (also Buzzy Beetles and Bullet Bills; Bowser takes five).
- **Six bullets** in the bottom right corner, each back 2 seconds after it's fired; shoot the corner to load all six; each coin a shot collects puts a bullet back. With none left, a pull of the trigger only makes a failure sound.
- **Bricks and ? blocks** that are shot get bumped as by big Mario's head (bricks break, ? blocks give their coin or power-up).
- **Shoot a player** to make them a giant for 5 seconds.
- **1-ups:** shoot a Podoboo, or the star flag that rises on the castle at a level's end (once a level). Hits in a row climb like stomps in a row (100, 200, 400 ... 8000, then 1-ups).
- **Nearly everything on the screen reacts:** Koopas pull into their shells, Paratroopas lose their wings, Bullet Bills burst like fireworks, mushrooms turn around, coins are collected, hammers and Bowser's fire are knocked out of the air, fire bars go out for 3 seconds, cannons jam, and shooting the axe drops Bowser. A bush that is shot floats up into the sky as a cloud, a cloud drops and lands as a bush, every pipe holds a coin, and one pipe, bush or cloud in each level hides a 1-up.
- **Without a controller:** shoot the title's menu line to choose and start; a shot at GAME OVER continues.
- **SHOOTING CRUISE** (on the title screen): the computer plays Mario from 1-1 to 8-4, in order, from routes planned ahead of time and stored in the ROM, while the gunner clears the way. Three lives as usual; 1-ups count.
- Without a Zapper it plays as Super Mario Bros. Co-op.

**How to play**

- **On an NES** the Zapper goes in controller port 2, so it's one player plus the gunner. Two players and a gunner need a Famicom (its controllers are built in, and the Zapper goes in the expansion port). A real Zapper needs a CRT television.
- **In an emulator,** set controller port 2 to a Zapper: the mouse aims and the button fires. The NES 2.0 header names the Zapper as the game's input device, which some emulators use to plug it in by themselves. In RetroArch (FCEUmm core): Quick Menu > Controls > Port 2 Controls > Device Type > Zapper, and Quick Menu > Core Options > Zapper Mode > Mouse. In MAME:

  ```
  mame nes -cart "Super Mario Bros Zapper.nes" -ctrl2 zapper
  ```
- **The PowerPak patch** makes the same game with that header byte set to 0, because the PowerPak's loader refuses the ROM with it set.
- **Title screen:** Select steps through the modes (SHOOTING CRUISE among them); Start begins, or shoot the line you want.
- **In play:** as in Super Mario Bros. Co-op (Select = bubble, Start = pause).

**Known issues**

- Each shot blacks out the screen for a frame (sometimes a few, to tell targets side by side apart), as Zapper games do.
- In a two-player game the bullets in the corner are drawn as fireballs.
- A real Zapper may miss small targets from far away.
- A bush or cloud on the move shows a stretched row for a frame or two.

**Patches.** No ROM included: you need your own copy of Super Mario Bros. Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Super Mario Bros. (World), iNES header | 40,976 bytes | `3337EC46` | `ea343f4e445a9050d4b4fbac2c77d0693b1d0922` | [`SuperMarioBrosZapper-v45.bps`](patches/SuperMarioBrosZapper/SuperMarioBrosZapper-v45.bps) |
| Super Mario Bros. (World), NES 2.0 header | 40,976 bytes | `393A432F` | `33d23c2f2cfa4c9efec87f7bc1321ce3ce6c89bd` | [`SuperMarioBrosZapper-v45-nes2header.bps`](patches/SuperMarioBrosZapper/SuperMarioBrosZapper-v45-nes2header.bps) |
| Super Mario Bros. (World), iNES header (makes the PowerPak version) | 40,976 bytes | `3337EC46` | `ea343f4e445a9050d4b4fbac2c77d0693b1d0922` | [`SuperMarioBrosZapper-v45-powerpak.bps`](patches/SuperMarioBrosZapper/SuperMarioBrosZapper-v45-powerpak.bps) |
| Super Mario Bros. (World), NES 2.0 header (makes the PowerPak version) | 40,976 bytes | `393A432F` | `33d23c2f2cfa4c9efec87f7bc1321ce3ce6c89bd` | [`SuperMarioBrosZapper-v45-powerpak-nes2header.bps`](patches/SuperMarioBrosZapper/SuperMarioBrosZapper-v45-powerpak-nes2header.bps) |

The game data after the 16-byte header: Super Mario Bros. (World): CRC32 `D445F698`, SHA-1 `facee9c577a5262dbe33ac4930bb0b58c8c037f7`.

The result: 262,160 bytes, CRC32 `C509CD95`, SHA-1 `ad0c7ead0d291eb260f4bfc9630e72f5c6ac143b` (the PowerPak version: CRC32 `9C2F73B4`, SHA-1 `6fcabefc5e71b6c9ac5afbc8b0f69afcb34f359c`). MMC3 (mapper 4), 128 KB PRG ROM, 128 KB CHR ROM, 8 KB work RAM, NES 2.0 header (header byte 15: the Zapper; 0 in the PowerPak version).

## Super Mario Bros. 3 Co-op

Super Mario Bros. 3 for **two players at once**: Mario and Luigi in the same level, on one screen. Version v9, an unofficial fan mod of Super Mario Bros. 3.

**What it does**

- **Two players at once:** Mario on controller 1 and Luigi on controller 2, in the same level. **2 PLAYER GAME** on the title screen is the co-op game (the original's take-turns two-player game and its battle game are gone).
- **Join during a game:** in a 1 PLAYER GAME, press Start on controller 2 during a level and Luigi appears next to Mario.
- **One map marker:** Mario walks the map and both players enter the level. Lives are shared.
- **A power-up for each player:** Luigi keeps his from level to level; the items from the map go to Mario.
- **One shared screen** that follows the point halfway between the players and keeps both on it. Push against the edge for two seconds while your partner holds it back, and your partner is brought next to you.
- **Bubbles:** press Select to go into a bubble (when your partner is playing): it floats over to your partner, and you are safe in it and keep your power-up. A, B or Select pops it. A player who loses a life while the partner plays on comes back in a bubble; the level starts over only when both are down.
- **Pipes, doors and the goal:** the player who goes into a pipe or door takes the partner along; whoever takes the goal card ends the level for both.
- Enemies that face, chase or throw at the player go for whichever player is nearer. Autoscrolling levels push and carry both players.
- Luigi is green when small, big or with the leaf; with the other suits he wears the suit's colors (the nearest match in the level's sprite palettes).
- **1 PLAYER GAME** is the original game.

**How to play**

- **Title screen:** Select chooses 1 PLAYER GAME or 2 PLAYER GAME; Start begins.
- **In play:** Select goes into a bubble; A, B or Select pops it. Start on controller 2 joins a 1 PLAYER GAME. Start on either controller pauses.

**Known issues**

- **MMC5:** the co-op game runs on the MMC5 mapper (the original is MMC3), for the room and the banking the second player needs. It needs an emulator or flash cart with MMC5 support. In testing, it did not start on a PowerPak.
- **Slowdown** with both players in a few busy places: 1-5's long slope with the Buzzy Beetles, 2-1, 7-8's piranha maze, the World 2 fortress and pyramid, the first tank of World 8. In random two-player play, 0.3% of frames ran late (the one-player original: 0.1%).
- **Mario's only:** the P-meter on the status bar is Mario's, and the world map shows Mario only. A few enemies still look only at Mario.
- **Vertical areas** (the pipe mazes of 7-1 and 7-6, ...): a player who climbs more than about a screen above the partner leaves the top of the screen; their own bubble (Select) or the partner climbing after them brings them back.
- A fireball's puff can hide part of Luigi for a moment.

**Patches.** No ROM included: you need your own copy of Super Mario Bros. 3. Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Super Mario Bros. 3 (USA), PRG1 (Rev 1), iNES header | 393,232 bytes | `0B742B33` | `6bd518e85eb46a4252af07910f61036e84b020d1` | [`SuperMarioBros3Coop-v9.bps`](patches/SuperMarioBros3Coop/SuperMarioBros3Coop-v9.bps) |
| Super Mario Bros. 3 (USA), PRG1 (Rev 1), NES 2.0 header | 393,232 bytes | `E8C3AF69` | `a25d2dcbf6ec3634a84318bfe2cfe28d5331d815` | [`SuperMarioBros3Coop-v9-nes2header.bps`](patches/SuperMarioBros3Coop/SuperMarioBros3Coop-v9-nes2header.bps) |
| Super Mario Bros. 3 (USA), PRG0, iNES header | 393,232 bytes | `85A79D9C` | `a03e7e526e79df222e048ae22214bca2bc49c449` | [`SuperMarioBros3Coop-v9-prg0.bps`](patches/SuperMarioBros3Coop/SuperMarioBros3Coop-v9-prg0.bps) |
| Super Mario Bros. 3 (USA), PRG0, NES 2.0 header | 393,232 bytes | `661019C6` | `5f9019040fe23cb412a484e1ef430e59e589f9b4` | [`SuperMarioBros3Coop-v9-prg0-nes2header.bps`](patches/SuperMarioBros3Coop/SuperMarioBros3Coop-v9-prg0-nes2header.bps) |

The game data after the 16-byte header: Super Mario Bros. 3 (USA), PRG1 (Rev 1): CRC32 `2E6301ED`, SHA-1 `bb894d104c796f69ba16587eb66c0275f5c2fc02`; Super Mario Bros. 3 (USA), PRG0: CRC32 `A0B0B742`, SHA-1 `a611b90b4833b20a364bf06ee3be3b9093ea4df9`.

The result: 786,448 bytes, CRC32 `A5EC2926`, SHA-1 `fb3e315e4304f72fc4eeb8cb95e67a17593581b6`. MMC5 (mapper 5), 512 KB PRG ROM, 256 KB CHR ROM, 8 KB work RAM, NES 2.0 header.

## Mario Bros. Extra

A Mario Bros.-style arcade game for **one or two players at once**, made from Super Mario Bros. 3's battle game: Super Mario Bros. 3 enemies come out of the pipes, with its power-ups, cards and bonus games. Version v5, an unofficial fan mod of Super Mario Bros. 3.

**What it does**

- A title and menu after the NES Mario Bros., with Super Mario Bros. 3's MARIO BROS. logo: 1 PLAYER GAME A/B, 2 PLAYER GAME A/B (both players at once), 2 PLAYER BATTLE, and the TOP score.
- Bump the floor under enemies to flip them, then kick them off; 15 phases that repeat faster; the last enemy turns blue and fast; a POW block.
- Enemies: Goomba, Spiny, Sidestepper, Fighter Fly, Para-Goomba, Buzzy Beetle, Bob-omb (goes off when left flipped) and Cheep Cheep; fireballs, Bullet Bills and Boo as hazards.
- Kicked enemies send coins out of the pipes, and sometimes power-ups with their abilities: Fire Flower, Super Leaf (tail, slow fall), Tanooki Suit (statue), Frog Suit (high jumps), Hammer Suit, Starman, 1-Up. A hit costs the suit.
- Score (kick combos, coins, bumped fireballs), 4 lives and one more at 20000, and Super Mario Bros. 3 cards: the last enemy's card, cards bumped out of your partner, three cards give lives.
- Bonus phases: coins against the clock, Super Mario Bros. 3's coin fountain and its [?]-block ladder game.
- **2 PLAYER BATTLE** is Super Mario Bros. 3's battle game as it was, first to three rounds.

**How to play**

- **Title screen:** Select or up/down picks the game; Start starts.
- **In play:** left/right (hold B to run), A jumps, B uses the suit (fireball, hammer, tail; Tanooki Suit: Down + B for the statue); hold A while falling with a tail to fall slowly. Start on either controller pauses. After losing a life, A drops you from the platform at the top.

**Known issues**

- Players stay small with any suit (the arena's floors are too close together for big Mario): suits show as colors, ears and tail, or a helmet.
- In Super Mario Bros. 3's static-coin battle round a stalemate can last, as in Super Mario Bros. 3.

**Patches.** No ROM included: you need your own copy of Super Mario Bros. 3. Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Super Mario Bros. 3 (USA), PRG1 (Rev 1), iNES header | 393,232 bytes | `0B742B33` | `6bd518e85eb46a4252af07910f61036e84b020d1` | [`MarioBrosExtra-v5.bps`](patches/MarioBrosExtra/MarioBrosExtra-v5.bps) |
| Super Mario Bros. 3 (USA), PRG1 (Rev 1), NES 2.0 header | 393,232 bytes | `E8C3AF69` | `a25d2dcbf6ec3634a84318bfe2cfe28d5331d815` | [`MarioBrosExtra-v5-nes2header.bps`](patches/MarioBrosExtra/MarioBrosExtra-v5-nes2header.bps) |
| Super Mario Bros. 3 (USA), PRG0, iNES header | 393,232 bytes | `85A79D9C` | `a03e7e526e79df222e048ae22214bca2bc49c449` | [`MarioBrosExtra-v5-prg0.bps`](patches/MarioBrosExtra/MarioBrosExtra-v5-prg0.bps) |
| Super Mario Bros. 3 (USA), PRG0, NES 2.0 header | 393,232 bytes | `661019C6` | `5f9019040fe23cb412a484e1ef430e59e589f9b4` | [`MarioBrosExtra-v5-prg0-nes2header.bps`](patches/MarioBrosExtra/MarioBrosExtra-v5-prg0-nes2header.bps) |

The game data after the 16-byte header: Super Mario Bros. 3 (USA), PRG1 (Rev 1): CRC32 `2E6301ED`, SHA-1 `bb894d104c796f69ba16587eb66c0275f5c2fc02`; Super Mario Bros. 3 (USA), PRG0: CRC32 `A0B0B742`, SHA-1 `a611b90b4833b20a364bf06ee3be3b9093ea4df9`.

The result: 786,448 bytes, CRC32 `36E3E0CD`, SHA-1 `45eb82cc72a03cce2faadfb543f4b6b42380e6bc`. MMC3 (mapper 4), 512 KB PRG ROM, 256 KB CHR ROM, 8 KB work RAM (no battery), NES 2.0 header.

## Wrecking Crew Co-op

Wrecking Crew for **up to four players at once**: Mario, Luigi, Wario and Waluigi wreck the walls together. Version v2, an unofficial fan mod of Wrecking Crew.

**What it does**

- Mario (controller 1), Luigi (2), Wario (3) and Waluigi (4). Players 3 and 4 need a Four Score.
- **2 PLAYER GAME is played at the same time** (the original took turns). Anyone can drop in with Start on their own controller during play: they come in at the phase's start, blinking, with 5 lives.
- Each player has their own score, lives and golden hammer; the phase intro shows everyone's.
- A phase is cleared when the walls are gone, whoever broke them. Enemies, Foreman Spike and fireballs go after the nearest player.
- The screen keeps the highest and lowest player in view. Players don't block or hurt each other.
- A player who is hit loses a life and comes back at their start spot after about a second, safe for 2 seconds; the phase starts over only when everybody is down.
- Out of lives: GAME OVER under your score, and Start gives 5 new lives (score 0).
- Bonus stages are played together.
- The one-player game, DESIGN mode and the demo are the original.

**How to play**

- **Title screen:** Select to 2 PLAYER GAME, then Start.
- **In play:** Start on controller 2, 3 or 4 joins, or rejoins after a game over. Any Start pauses.
- Players 3 and 4 need the Four Score: see [Three or four players](#three-or-four-players-nes-four-score).

**Known issues**

- The bonus stage header shows only Mario's and Luigi's scores.
- Some slowdown with four players (3.4% of frames run late).
- Waluigi's face is white.
- There is no 3 or 4 PLAYER GAME on the title screen: players 3 and 4 join with Start.

**Patches.** No ROM included: you need your own copy of Wrecking Crew. Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Wrecking Crew (World), iNES header | 40,976 bytes | `658D4FD4` | `31635f1a5255fe8954c5a275b067f603bb7af408` | [`WreckingCrewCoop-v2.bps`](patches/WreckingCrewCoop/WreckingCrewCoop-v2.bps) |
| Wrecking Crew (World), NES 2.0 header | 40,976 bytes | `96581FF3` | `444ad5a33aecc1a2f59df3d91517b948a39235ec` | [`WreckingCrewCoop-v2-nes2header.bps`](patches/WreckingCrewCoop/WreckingCrewCoop-v2-nes2header.bps) |

The game data after the 16-byte header: Wrecking Crew (World): CRC32 `9B506A48`, SHA-1 `dee513dad7223cfc81bcd859d0aac6746349cb25`.

The result: 81,936 bytes, CRC32 `AF01A3D6`, SHA-1 `7107b6239f2a202c321d2e2258c9229bc6ff9ae4`. MMC3 (mapper 4), 64 KB PRG ROM, 16 KB CHR ROM, 8 KB work RAM, NES 2.0 header (the original is NROM).

## Excitebike 4-Player

Excitebike for **up to four riders at once**, with a split screen for two players. Version v2, an unofficial fan mod of Excitebike.

**What it does**

- Up to four riders with a Four Score; two without one.
- **Joining:** on the title screen, Start or A on controller 2, 3 or 4 joins; the bike appears on the start grid with its number (1P-4P). Select on a joined controller leaves. Controller 1 runs the menus.
- **Two players: a split screen.** Player 1's view is on top, player 2's below, with the status bar between them (both heat gauges and the time). Each view follows its own rider anywhere on the track; the other rider shows in your view when near, and you can bump each other then.
- **Three or four players: one screen** that follows the leader; a rider left behind is pushed along at the left edge. The first across the line wins; the others have 10 seconds.
- Every rider has the original's controls and rules: speed, lanes, engine heat with their own gauge, crashes, and mashing A or B to run back to the bike.
- Colors: player 1 red, 2 light blue, 3 green, 4 purple.
- With two or more players, gas and turbo count as held for a few frames after they're let go, so the Four Score's TURBO switches don't take the gas away.
- SELECTION A races the players alone; SELECTION B adds computer riders when three play (none with two); DESIGN mode's tracks work too.
- One player is the original game.

**How to play**

- **Title screen:** Start or A on controllers 2-4 to join, Select to leave; controller 1 picks SELECTION A, SELECTION B or DESIGN and starts.
- **In the race:** A gas, B turbo (it heats the engine), up/down to change lanes, left/right to lean. Start on any joined controller pauses.
- Players 3 and 4 need the Four Score: see [Three or four players](#three-or-four-players-nes-four-score).

**Known issues**

- The split screen has no stands or banner.
- Status letters can drop out near a rider flying high (the NES shows 8 sprites on a line).
- When both lap times show at once, one LAP label is missing.
- In the split screen, a view at rest cuts off the last five lines of the nearest hay bales.

**Patches.** No ROM included: you need your own copy of Excitebike. Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Excitebike (Japan, USA), iNES header | 24,592 bytes | `2BB33C69` | `2e9897846e54a4a9865e87de7517c6710bdec255` | [`Excitebike4P-v2.bps`](patches/Excitebike4P/Excitebike4P-v2.bps) |
| Excitebike (Japan, USA), NES 2.0 header | 24,592 bytes | `625BF658` | `8e807f8aa465891affc51939687009b36943aade` | [`Excitebike4P-v2-nes2header.bps`](patches/Excitebike4P/Excitebike4P-v2-nes2header.bps) |

The game data after the 16-byte header: Excitebike (Japan, USA): CRC32 `49AEB3A6`, SHA-1 `ba8d9227a0d02b62ee6cb9e691fa5a5134c303a8`.

The result: 40,976 bytes, CRC32 `EF52B9A2`, SHA-1 `6d825d379e020b9ecc87e9eb76ac5f3f07bf8b20`. MMC3 (mapper 4) with four-screen VRAM, 32 KB PRG ROM, 8 KB CHR ROM, 8 KB work RAM, NES 2.0 header (the original is NROM).

## Metroid Co-op

Metroid for **two players at once**: Samus and her brother Solomon Aran explore Zebes together. Version v2.6, an unofficial fan mod of Metroid.

**What it does**

- Samus (orange) and Solomon (blue and white). Player 2 joins or leaves with Start on controller 2 on the START/CONTINUE screen; left/right there swaps who plays whom.
- The screen follows both; the one behind holds it back. Push at the edge for 2.5 seconds and the partner is brought over. In vertical shafts a player off the screen is brought beside the other.
- Doors and elevators take both players.
- Separate energy, missiles and status bar (player 2's at the upper right); three shots or bombs each.
- Power-ups and tank capacity are shared; drops go to whoever touches them; enemies go after the nearer player.
- A downed player comes back after 2 seconds with 30 energy; the game is over only when both are down.
- **Saved games:** battery-backed RAM with three files, on screens like the Famicom Disk System version's. Each player gets their own missiles back from a file. Names, erasing a file (KILL MODE) and the original passwords are there too.
- **Speed option:** SLOW LESS FLICKER or FAST MORE FLICKER.
- One-player Metroid is the original game.

**How to play**

- **START/CONTINUE screen:** Start on controller 2 joins or leaves; left/right swaps the characters; Select, then Start, sets the speed. CONTINUE shows the saved files.
- **Saving:** pause and press Up + A on controller 2 (or reach the password screen after a game over), then SAVE and pick a file.
- **In play:** Start on either controller pauses.

**Known issues**

- Some slowdown (Tourian with Metroids runs at about half speed).
- Solomon's colors don't change for missiles or the Varia suit.
- A password continue gives player 2 the same energy and missiles as player 1 (a saved file keeps both players').
- The ending shows one player.

**Patches.** No ROM included: you need your own copy of Metroid. Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Metroid (USA), iNES header | 131,088 bytes | `5236255F` | `c0f1909a06af3acbe14742e59db0b2764d97eabf` | [`MetroidCoop-v2.6.bps`](patches/MetroidCoop/MetroidCoop-v2.6.bps) |
| Metroid (USA), NES 2.0 header | 131,088 bytes | `D1A02CAB` | `2080059bea4563ffff7535e6c0a0f3bc2f34b194` | [`MetroidCoop-v2.6-nes2header.bps`](patches/MetroidCoop/MetroidCoop-v2.6-nes2header.bps) |

The game data after the 16-byte header: Metroid (USA): CRC32 `70080810`, SHA-1 `fdbfc7871962f72a1ef57e5a7e456164fb93430b`.

The result: 262,160 bytes, CRC32 `BA265811`, SHA-1 `ac513d154def4716fa8a54a12884840917b67586`. MMC3 (mapper 4), 256 KB PRG ROM, 8 KB CHR RAM, 8 KB battery-backed work RAM, NES 2.0 header (the original is MMC1).

## Castlevania Co-op

Castlevania for **two players at once**: Simon and Trevor (a second Belmont, in red) take on Dracula's castle together. Version v6, an unofficial fan mod of Castlevania.

**What it does**

- Simon (controller 1) and Trevor (controller 2) on one screen.
- A 1P/2P choice on the title screen (a 2P start shows both walking up to the castle); in a one-player game, Start on controller 2 drops Trevor in where Simon stands.
- A shared screen: push at the edge for 2.5 seconds and the partner is brought over. Doors, stairs and the gate take both.
- Each player has their own health, hearts, whip, subweapon and double or triple shot; score, time and lives are shared. The status bar has rows for SIMON, TREVOR and the ENEMY, with each player's subweapon.
- Enemies go after the nearer player; a subweapon comes back to whoever threw it.
- A player who goes down comes back beside the partner 2 seconds later (full health, 5 hearts, the leather whip); a life is lost only when both are down.
- Either player can take the crystal ball at a stage's end; the partner comes along.
- One-player Castlevania is the original game.

**How to play**

- **Title screen:** left/right or Select on either controller picks 1P or 2P; Start on controller 2 always starts a game for two.
- **In play:** Start on controller 2 joins a one-player game; either Start pauses.

**Known issues**

- The busiest scenes slow down (stage 12 the most).
- Trevor shares a palette with hearts and some enemies.
- Enemy spawners and hidden treasures go by the main player's position.
- The ending shows one player.
- Reported once and not reproduced: the music stopping for good.

**Patches.** No ROM included: you need your own copy of Castlevania. Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Castlevania (USA) (Rev 1), iNES header | 131,088 bytes | `856114C8` | `7a20c44f302fb2f1b7adffa6b619e3e1cae7b546` | [`CastlevaniaCoop-v6.bps`](patches/CastlevaniaCoop/CastlevaniaCoop-v6.bps) |
| Castlevania (USA) (Rev 1), NES 2.0 header | 131,088 bytes | `12A6CB14` | `4e3ef47de86a941c37359bb3acfa5542a0fa7876` | [`CastlevaniaCoop-v6-nes2header.bps`](patches/CastlevaniaCoop/CastlevaniaCoop-v6-nes2header.bps) |

The game data after the 16-byte header: Castlevania (USA) (Rev 1): CRC32 `B668C7FC`, SHA-1 `3dcb69a8c861c041aeb56c04e39adf6d332eda3a`.

The result: 262,160 bytes, CRC32 `A716215E`, SHA-1 `13afe73cb3205d1fbdd7f7303adc97f42df4e71e`. MMC3 (mapper 4), 256 KB PRG ROM, 8 KB CHR RAM, 8 KB work RAM, NES 2.0 header (the original is UNROM).

## Zelda II Co-op

Zelda II: The Adventure of Link for **two players at once**: two Links, green and orange, on one adventure. Version v5, an unofficial fan mod of Zelda II: The Adventure of Link.

**What it does**

- CO-OP under the title logo. Start on controller 2 during play brings player 2 in beside player 1 with full meters; player 2 stays in until reset.
- A shared screen; push at the edge for 2.5 seconds and the partner is brought over. Exits, town doors and elevators take both.
- On the overworld one Link walks for both, and either controller steers.
- Experience, levels, spells, items, keys, containers and lives are shared; each player has their own magic and life (player 2's after P2 on the top line).
- Each player's Start opens their own spell menu, and the spell is paid from that player's magic.
- Enemies go after the nearer player; a boss is beaten whoever lands the last hit; one key opens a locked door for both.
- A player who goes down comes back beside the partner after 2 seconds with half their life; a life is lost only when both are down.
- The battery save works as in the original.

**How to play**

- **Joining:** Start on controller 2 during play.
- **Spells:** each player's Start opens their own spell menu.
- **Saving:** Up + A on the other player's controller while a spell menu is open.

**Known issues**

- Busy scenes slow down a little (about 1% of frames).
- Player 2 has one palette (the Shield spell doesn't recolor him).
- Dark Link can be hurt only by the player he's fighting.
- Player 2 isn't shown on the overworld map and isn't saved.
- The ending shows one Link.

**Patches.** No ROM included: you need your own copy of Zelda II: The Adventure of Link. Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Zelda II: The Adventure of Link (USA), iNES header | 262,160 bytes | `E3C788B0` | `353489a57f24a429572e76bd455bc51d821f7036` | [`ZeldaIICoop-v5.bps`](patches/ZeldaIICoop/ZeldaIICoop-v5.bps) |
| Zelda II: The Adventure of Link (USA), NES 2.0 header | 262,160 bytes | `861C3FE6` | `08fa60f23e477752fdd850b1fd4171c6ca025127` | [`ZeldaIICoop-v5-nes2header.bps`](patches/ZeldaIICoop/ZeldaIICoop-v5-nes2header.bps) |

The game data after the 16-byte header: Zelda II: The Adventure of Link (USA): CRC32 `BA322865`, SHA-1 `11333adb723a5975e0ecca3aee8f4747aa8d2d26`.

The result: 393,232 bytes, CRC32 `BDEA48EE`, SHA-1 `cb089fd0b3e81775ccb6a4a18ac5011c0254f60f`. MMC3 (mapper 4), 256 KB PRG ROM, 128 KB CHR ROM, 8 KB battery-backed work RAM, NES 2.0 header (the original is MMC1).

## Kid Icarus Co-op

Kid Icarus for **two players at once**: two Pits fight their way out of the Underworld, across the Overworld and up to the Sky World together, on one screen. Version v1.1, an unofficial fan mod of Kid Icarus.

**What it does**

- Player 1 is the original Pit; player 2 is a second Pit in blue with red hair, with a health bar in the upper right.
- **Climbing worlds (1 and 3):** the screen scrolls up for whoever climbs; a player who drops below the bottom of the screen comes back beside the partner.
- **World 2:** the player behind holds the screen back; keep pushing against the right edge for about 2.5 seconds and your partner is brought over. **World 4:** both fly.
- **Doors:** whoever walks into a door goes in, and the partner waits outside. In the fortresses the partner follows into the next room.
- Enemies go after the nearer player; either player's arrows hit them.
- Hearts, score, treasures, weapons, arrow strength and items are shared; health, invincibility and the eggplant curse are each player's own. Hearts and items go to whoever touches them.
- A player whose health runs out comes back beside the partner 2.5 seconds later with half a health bar; the game is over only when both are down at once.
- A one-player game is the original game.

**How to play**

- **START/CONTINUE screen:** Start on controller 2 switches between 1 PLAYER and 2 PLAYERS; then player 1 picks START or CONTINUE as usual.
- **In play:** Start on either controller pauses.

**Known issues**

- The busiest moments slow down a little more than the original (about 2% of frames late in two-player games).
- Rooms behind doors are visited by one player at a time.
- The ending shows one Pit.
- Player 2 shares a palette with the health bars and some enemies.

**Patches.** No ROM included: you need your own copy of Kid Icarus. Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Kid Icarus (USA, Europe), iNES header | 131,088 bytes | `F54EECE6` | `ea586e7e2b884ed67b99eaec0678a8faf8c94f46` | [`KidIcarusCoop-v1.1.bps`](patches/KidIcarusCoop/KidIcarusCoop-v1.1.bps) |

The game data after the 16-byte header: Kid Icarus (USA, Europe): CRC32 `D770C1A9`, SHA-1 `2c27ec6ecc67645a3a3dec3496dc4ab5d35049af`.

The result: 262,160 bytes, CRC32 `02DC537B`, SHA-1 `4952cb05a02ee3829d9e87e2a292fc4190d026ee`. MMC1 (mapper 1), 256 KB PRG ROM, 8 KB CHR RAM, 8 KB work RAM, NES 2.0 header.

## Punch-Out!! Vs

Mike Tyson's Punch-Out!! with **player 2 as the opponent**: every boxer from Glass Joe to Mike Tyson, with Little Mac's controls and the boxer's own special move. Version v3, an unofficial fan mod of Mike Tyson's Punch-Out!!

**What it does**

- All 14 boxers, each punch his own (the same tells, flashes, timing and damage as when the computer throws it).
- Select: the boxer's special (Honda Rush, Bull Charge, Tiger Punch, Dreamland Express, ...) on a 30-second cooldown (45 for the instant-knockdown ones); the boxer's energy bar turns red when it's ready.
- A fair fight: no automatic dodges or blocks for player 2; a blocked punch chips the boxer's energy and costs Little Mac no heart.
- One player is the original game.

**How to play**

- **During a fight,** Start on controller 2 takes the opponent (and gives him back).
- **Controller 2:** B / A punch with the hand on the screen's left / right, Up + B / A for a heavy punch, Down blocks, Left / Right sidestep, Select for the special.

**Known issues**

- None recorded yet. It's an experiment like the others: please report what you find.

**Patches.** No ROM included: you need your own copy of Mike Tyson's Punch-Out!! Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Mike Tyson's Punch-Out!! (Japan, USA), iNES header | 262,160 bytes | `83DB7938` | `5d287f933931b14504eb2a3c40fef1af2ae083ea` | [`PunchOutVs-v3.bps`](patches/PunchOutVs/PunchOutVs-v3.bps) |
| Mike Tyson's Punch-Out!! (Japan, USA), NES 2.0 header | 262,160 bytes | `12F19390` | `afe3a325657bd9a19612ac064847137d9258d2a4` | [`PunchOutVs-v3-nes2header.bps`](patches/PunchOutVs/PunchOutVs-v3-nes2header.bps) |

The game data after the 16-byte header: Mike Tyson's Punch-Out!! (Japan, USA): CRC32 `92A2185C`, SHA-1 `339eb36acbbbec96c8d177f0265253a5764cc1fb`.

The result: 262,160 bytes, CRC32 `D4619DC3`, SHA-1 `62dabf5be291190a41064b6572ea92a1e66ddbf9`. MMC2 (mapper 9), 128 KB PRG ROM, 128 KB CHR ROM: the original's board, nothing added (iNES header).

## Punch-Out!! Two Macs

Mike Tyson's Punch-Out!! with **two Little Macs side by side** against one boxer, one on each controller. Version v3, an unofficial fan mod of Mike Tyson's Punch-Out!!

**What it does**

- Controller 1 is the left Mac, controller 2 the right one, each with all of Mac's moves: punches, dodges, block, duck, star punch.
- The boxer's punches come at the Mac on their side; he blocks and dodges either Mac's punches as he does Little Mac's.
- Energy, hearts, stars and points are shared; a Mac who is knocked down plays the count alone and gets up with his own controller.
- Round starts, knockdowns and round ends show one Mac, as in the original.
- One Mac is the original game.

**How to play**

- **Each controller:** B / A body punches, Up + B / A face punches, Left / Right dodge, Down blocks (twice: duck), Start for the star punch.
- **Controller 2's Select** during a fight switches between one Mac and two from the next round.

**Known issues**

- Both Macs wear the same colors (the palettes are shared with the ring and crowd).
- The star uppercut's legs are drawn once, in the middle.
- When the fight resumes after a cutscene, the left Mac's old picture shows for a frame or two.

**Patches.** No ROM included: you need your own copy of Mike Tyson's Punch-Out!! Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Mike Tyson's Punch-Out!! (Japan, USA), iNES header | 262,160 bytes | `83DB7938` | `5d287f933931b14504eb2a3c40fef1af2ae083ea` | [`PunchOutTwoMacs-v3.bps`](patches/PunchOutTwoMacs/PunchOutTwoMacs-v3.bps) |
| Mike Tyson's Punch-Out!! (Japan, USA), NES 2.0 header | 262,160 bytes | `12F19390` | `afe3a325657bd9a19612ac064847137d9258d2a4` | [`PunchOutTwoMacs-v3-nes2header.bps`](patches/PunchOutTwoMacs/PunchOutTwoMacs-v3-nes2header.bps) |

The game data after the 16-byte header: Mike Tyson's Punch-Out!! (Japan, USA): CRC32 `92A2185C`, SHA-1 `339eb36acbbbec96c8d177f0265253a5764cc1fb`.

The result: 262,160 bytes, CRC32 `569E5E9E`, SHA-1 `2e3465755de3fe4629f35e810263b1425e783875`. MMC2 (mapper 9), 128 KB PRG ROM, 128 KB CHR ROM: the original's board, nothing added (iNES header).

## Co-op Tetris

NES Tetris for **two players at once on one playfield**, with two new modes, BLAST and COLORS. Version v4, an unofficial fan mod of Tetris.

**What it does**

- On the GAME TYPE screen, Select moves to the new mode box: SOLO (the original game), BLAST or COLORS. A-TYPE, B-TYPE, all ten starting levels and the B-TYPE heights work in every mode.
- **BLAST:** player 2's pieces are antimatter. When antimatter completes a line, it explodes and also takes out the line above and the line below (an antimatter Tetris can remove 6). Antimatter that lands without completing a line stays in the stack, blinking. One team score.
- **COLORS:** each player's blocks have their own color, and a cleared line pays each player for their own blocks in it. Lines and level are shared; the scores show as 1P and 2P.
- In both co-op modes the falling pieces block each other, each player starts on their own side of the well, and only one player at a time can be locking or clearing lines.

**How to play**

- Controller 1 is player 1 and controller 2 is player 2. The menus use controller 1 (player 2 can also pick the mode, with up/down).
- Start on either controller pauses.

**Known issues**

- A top-out by either player ends the game for both.
- Co-op games don't go into the high score table.

**Patches.** No ROM included: you need your own copy of Tetris. Pick the row that matches your ROM file:

| your ROM file | size | CRC32 | SHA-1 | patch |
|---|---|---|---|---|
| Tetris (USA), iNES header | 49,168 bytes | `6D72C53A` | `77747840541bfc62a28a5957692a98c550bd6b2b` | [`CoopTetris-v4.bps`](patches/CoopTetris/CoopTetris-v4.bps) |
| Tetris (USA), NES 2.0 header | 49,168 bytes | `D16EA396` | `3026d28b63d94c921fe58364f8b0659d10b5a0ac` | [`CoopTetris-v4-nes2header.bps`](patches/CoopTetris/CoopTetris-v4-nes2header.bps) |

The game data after the 16-byte header: Tetris (USA): CRC32 `1394F57E`, SHA-1 `fd9079cb5e8479eb06d93c2ae5175bfce871746a`.

The result: 65,552 bytes, CRC32 `237D8244`, SHA-1 `62c59dbeb308a2c23d18ba7e274157ed7ad22d39`. MMC1 (mapper 1), 32 KB PRG ROM, 32 KB CHR ROM (the original has 16 KB), iNES header.

## Credits

- NINTENDO, of course! Thank you for these gifts to the world. And Konami for Castlevania, and
  Alexey Pajitnov for Tetris.
- Coding by Anthropic Claude Opus 5.5 with Claude Code
- Benj Edwards (Co-op Mod Design Guidance)
- Built on these disassemblies:
  [doppelganger's Super Mario Bros.](https://gist.github.com/1wErt3r/4048722),
  [Southbird's Super Mario Bros. 3](https://github.com/captainsouthbird/smb3),
  [nmikstas's Metroid](https://github.com/nmikstas/metroid-disassembly) and
  [Mike Tyson's Punch-Out!!](https://github.com/nmikstas/mike-tysons-punch-out-disassembly),
  [josephstevenspgh's Castlevania](https://github.com/josephstevenspgh/Castlevania-Labelled-Disassembly),
  [Trax's Zelda II](https://github.com/FiendsOfTheElements/z2disassembly) and
  [CelestialAmber's Tetris](https://github.com/CelestialAmber/TetrisNESDisasm). Wrecking Crew,
  Excitebike and Kid Icarus were disassembled for these mods.
- Toad and Peach sprites in the Super Mario Bros. mods adapted from Super Mario Maker 2 (Toad),
  Super Mario Maker (small Peach) and Super Mario Bros. 2 (big Peach).
- Zelda II Co-op: Arc, FatRatKnight, Inzult and Rising_Tempest, the authors of the TASVideos
  speedrun [3254M](https://tasvideos.org/3254M) ("warpless"), whose movie, played back in an
  emulator, took the original game through four palaces while the project mapped what memory it
  uses.

Super Mario Bros., Super Mario Bros. 3, Metroid, Zelda II: The Adventure of Link, Kid Icarus,
Wrecking Crew, Excitebike and Mike Tyson's Punch-Out!! are © Nintendo. Castlevania is © Konami.
Tetris is a trademark of The Tetris Company. These are unofficial fan modifications, not made or
endorsed by Nintendo, Konami or The Tetris Company, and they contain no ROMs.
