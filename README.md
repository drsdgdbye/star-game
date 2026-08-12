# StarGame

A 2D space shooter built with **Java** and **libGDX** (1.9.9). Pilot a starfighter that descends, dodges and destroys waves of enemy ships while keeping your health and score up.

The game is a multi-module Gradle project sharing platform-independent game logic in the `core` module with desktop (LWJGL) and Android launchers.

## Features

- Side-scrolling/vertical space shooter with a starfield background
- Main ship with health (HP), laser shooting and two-frame damage animation
- Three enemy ship types (small, middle, big) with different stats
- Level system: difficulty grows with your score (`level = frags / 10 + 1`, affecting enemy bullet damage)
- Bullet/enemy collisions, hit detection and animated explosions
- HUD showing frags, HP and current level
- Pause button, game over screen with "New Game" button
- Background music and sound effects (laser shots, explosions)
- Object pooling for bullets, enemies and explosions to avoid GC churn

## Screenshots

Coming soon.

Add screenshots of the menu, gameplay and game-over screens to `assets/screenshots/` and reference them here:

```
assets/screenshots/menu.png
assets/screenshots/gameplay.png
assets/screenshots/game-over.png
```

## Controls

| Platform | Action | Input |
|---|---|---|
| Desktop | Move left / right | Arrow keys (`←` / `→`) |
| Desktop | Shoot | `Space` |
| Android | Move | Touch left / right half of the screen |
| Both | Pause | Pause button (top right corner) |

## Requirements

- **JDK 8+**
- **Android SDK 28** (with platform `android-28`) — only to build/run the Android module
- Gradle isn't required to be installed separately; the project includes the Gradle wrapper (`./gradlew`)

## Build & Run

### Desktop

```bash
./gradlew desktop:run
```

### Android

Make sure `local.properties` points to your Android SDK (`sdk.dir=...`) or `ANDROID_HOME` is set, then build and install:

```bash
./gradlew android:installDebug
```

You can also open the project in Android Studio / IntelliJ IDEA and run any of the launchers directly:

- `desktop/src/ru/drsdgdby/desktop/DesktopLauncher.java`
- `android/src/ru/drsdgdby/AndroidLauncher.java`

## Project Structure

```
StarGame/
├── core/        # Platform-independent game logic (shared by desktop & Android)
│   └── src/ru/drsdgdby/
│       ├── base/       # BaseScreen (input & coordinate transforms), Sprite, SpritesPool, buttons
│       ├── screen/     # MenuScreen, GameScreen
│       ├── math/       # Rect, Rnd, MatrixUtils
│       ├── pool/       # BulletPool, EnemyShipPool, ExplosionPool (object pools)
│       ├── sprite/     # Background, Star, menu & game sprites, ships (Ship, MainShip, EnemyShip)
│       └── utils/      # EnemyShipEmitter, Font, Regions
├── desktop/     # LWJGL desktop launcher (400x533 window, VSync, fixed aspect)
├── android/     # Android launcher (portrait) + shared assets
│   └── assets/  # Textures (TextureAtlas), sounds, fonts
├── build.gradle
└── settings.gradle
```

Key source files:

| File | Purpose |
|---|---|
| `core/src/ru/drsdgdby/StarGame.java` | Entry point, sets the menu screen as the first screen |
| `core/src/ru/drsdgdby/screen/GameScreen.java` | Main gameplay loop: update, collisions, draw, states (PLAY / PAUSE / GAME_OVER) |
| `core/src/ru/drsdgdby/screen/MenuScreen.java` | Main menu with Start / Exit buttons |
| `core/src/ru/drsdgdby/utils/EnemyShipEmitter.java` | Enemy spawn logic and level scaling |
| `core/src/ru/drsdgdby/sprite/game/ships/MainShip.java` | Player ship: movement, shooting, touch/keyboard input |
| `core/src/ru/drsdgdby/base/BaseScreen.java` | Screen base class with world/screen coordinate conversion |

## Tech Stack

- Java
- [libGDX](https://libgdx.badlogicgames.com/) 1.9.9
- Gradle multi-project build (desktop + android + core modules)
- LWJGL backend for desktop
- TextureAtlas-packed graphics, object pooling, custom math utils

## Roadmap

Planned improvements (tracked as in-code TODOs):

- Add asteroids
- Back button and improved pause handling
- Screen fade transition between menu and gameplay
- Music fade-out on timer

## License

Not licensed yet. Add a license and link it here before public distribution.