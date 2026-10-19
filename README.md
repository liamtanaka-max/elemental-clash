# Elemental Clash

A 2-player platform fighter that runs in your browser — on one keyboard, or **online with a room code**. Five elemental fighters, three stages, three stocks each. The higher your damage %, the farther you fly — knock your rival past the edge of the screen to take a stock.

Everything — characters, stage, effects and sound — is drawn and synthesized with code. No images, no audio files. Just one HTML file (online play loads one small library, [PeerJS](https://peerjs.com/), to connect the two browsers).

## Play

- **Online:** https://liamtanaka-max.github.io/elemental-clash/ (once GitHub Pages is enabled: Settings → Pages → Deploy from branch `main`, folder `/ (root)`)
- **Locally:** download `index.html` and double-click it.

## Online play

1. One player chooses **PLAY ONLINE → CREATE ROOM** and gets a 5-letter room code.
2. They send the code to a friend, who chooses **PLAY ONLINE → JOIN ROOM** and types it in (Ctrl+V pastes).
3. In the room, both pick a fighter (the host picks the stage) and press **READY**. The match starts when both are ready.

The host is Player 1 (red) and the friend is Player 2 (blue). Online, **each player uses their own Player 1 controls**, which can be changed from the room's ⚙ CONTROLS button before the fight. Online matches can't be paused: `Esc` opens a menu while the fight keeps going.

How it works: the two browsers connect directly with WebRTC (PeerJS's free server only introduces them). Both computers run the same match with the same button presses, using **rollback netcode**: your own buttons work right away, and the game guesses the rival's buttons until they arrive. If a guess was wrong, it rewinds to a saved copy of the match and quickly replays the last few frames with the real buttons, so the game never freezes to wait. Both players need an internet connection and should use the same version of the page. Turn on hitbox view (`` ` ``) in an online match to see the ping, input delay and rollback count.

## Stages

| Stage | What it's like |
|---|---|
| **Elemental Shrine** | Balanced: a floating temple with three platforms |
| **Magma Forge** | A long iron bridge over lava with two low grates — lots of room to fight |
| **Storm Spire** | A tiny peak in a thunderstorm, with platforms hanging past the edges — early KOs |

## Fighters

| Fighter | Element | Style |
|---|---|---|
| **Pyro** | Fire | Hard-hitting brawler, burning trails |
| **Tide** | Water | Floaty, bubble traps, counter, best recovery |
| **Volt** | Thunder | Fastest fighter, light hits, chargeable bolt |
| **Lumen** | Light | Long reach, laser beam, projectile-reflecting mirror |
| **Umbra** | Dark | Slow and heavy, homing orb, shadow grab, void pit |

## Controls

| Action | Player 1 (and online) | Player 2 |
|---|---|---|
| Move | A / D | ← / → |
| Up / Down (aim, crouch, fast-fall, drop through) | W / S | ↑ / ↓ |
| Jump / double jump | Space | Enter |
| Attack (hold to charge) | **Left Click** | . |
| Special | Right Click | / |
| Shield (hold) / Dodge (tap) | Left Shift | Right Shift |
| Grab | E | , |

Every key can be changed on the **CONTROLS** screen (from the home menu, the ⚙ CONTROLS button on character select or in an online room, or the pause menu). Bindings are saved in your browser.

Hold a direction while attacking for tilts and aerials. **Up + Special** is always a recovery. Grab ledges to get back on stage.

**Grabs:** press Grab next to your rival (it goes through shields, and works out of shield too). While holding them, press a direction to throw (forward, back, up, or down — down throw pops them up for a combo), or Attack to pummel. If you're grabbed, mash any button to break free sooner. In the air, Grab does an aerial.

`Esc` pause · `` ` `` show hitboxes · `M` mute

## How the code is organized

`index.html` is split into 13 labeled sections (search for the `=====` headers):

1. Setup & helpers
2. Input
3. Sound (Web Audio synth)
4. Particles
5. Fighter data — **add new fighters here**
6. Stage data — **add new stages here**
7. Poses & drawing
8. Fighter class (state machine, physics)
9. Projectiles
10. Match class (hits, knockback, camera, HUD)
11. UI & screens
12. Online multiplayer (rooms, codes, lockstep sync)
13. Main loop (fixed 60 FPS time step)

Knockback formula:

```
knockback = base + (percent × scaling × damage / 10) × (100 / (weight + 100))
```

## Ideas / roadmap

- [ ] New fighters: Earth, Wind, Ice
- [x] More stages (Magma Forge, Storm Spire)
- [ ] Even more stages
- [ ] Gamepad support
- [ ] CPU opponent
