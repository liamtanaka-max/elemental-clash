# Elemental Clash

A 2-player local platform fighter that runs in your browser. Five elemental fighters, one floating shrine, three stocks each. The higher your damage %, the farther you fly — knock your rival past the edge of the screen to take a stock.

Everything — characters, stage, effects and sound — is drawn and synthesized with code. No images, no audio files, no libraries. Just one HTML file.

## Play

- **Online:** https://liamtanaka-max.github.io/elemental-clash/ (once GitHub Pages is enabled: Settings → Pages → Deploy from branch `main`, folder `/ (root)`)
- **Locally:** download `index.html` and double-click it.

## Fighters

| Fighter | Element | Style |
|---|---|---|
| **Pyro** | Fire | Hard-hitting brawler, burning trails |
| **Tide** | Water | Floaty, bubble traps, counter, best recovery |
| **Volt** | Thunder | Fastest fighter, light hits, chargeable bolt |
| **Lumen** | Light | Long reach, laser beam, projectile-reflecting mirror |
| **Umbra** | Dark | Slow and heavy, homing orb, shadow grab, void pit |

## Controls

| Action | Player 1 | Player 2 |
|---|---|---|
| Move | A / D | ← / → |
| Jump / double jump | W | ↑ |
| Crouch / fast-fall / drop through | S | ↓ |
| Attack | F | K |
| Special | G | L |
| Shield (hold) | H | ; |
| Dodge | H + direction | ; + direction |

Hold a direction while attacking for tilts and aerials. **Up + Special** is always a recovery. Grab ledges to get back on stage.

`Esc` pause · `` ` `` show hitboxes · `M` mute

## How the code is organized

`index.html` is split into 12 labeled sections (search for the `=====` headers):

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
12. Main loop (fixed 60 FPS time step)

Knockback formula:

```
knockback = base + (percent × scaling × damage / 10) × (100 / (weight + 100))
```

## Ideas / roadmap

- [ ] New fighters: Earth, Wind, Ice
- [ ] More stages
- [ ] Gamepad support
- [ ] CPU opponent
