# SF-DOOM: 3D Raycasting Engine inside GMod (StarfallEx)

A high-performance, client-running, pseudo-3D Raycasting Game Engine inspired by classic **DOOM** and **Wolfenstein 3D**, written entirely from scratch in **Lua** for the **StarfallEx** addon in Garry's Mod.

This project delivers a smooth, cinematic gameplay experience with an incredibly optimized performance budget of **only ~22 Ops per frame** (~550 total Ops at 25 FPS).

---

## Features

* **Custom 3D Raycasting Engine:** Pure mathematical line-of-sight tracing using high-speed trigonometry (`math.cos`/`math.sin`) optimized for Lua-JIT.
* **Smart Performance Management (Object Pool):** Monsters and pickable items use an advanced pooling system (`availablepp` and `usedpp`) to handle asynchronous rendering without choking the Starfall CPU Quota (`quotaAverage`).
* **Software-level Depth Buffer (Z-Buffer):** Pixel-perfect sprite clipping that allows monsters and pickable items to correctly hide behind geometric walls.
* **Flawless Frame Pacing:** Runs at a locked cinematic 25 FPS with perfectly linear frametime distribution—eliminating micro-stutters and input lag.
* **Standalone Client Render Pipeline:** Runs entirely on clientside inside a Render Target texture (`render.createRenderTarget`), keeping the server's network channel (`in`/`out`) completely quiet.
* **Classic Mechanics:** Functional HUD, ammunition counters (Pistol/Shotgun), Red Keycard locks, interactable doors, and basic Monster AI pathfinding.

## Technical Deep Dive & Optimizations

Unlike heavy Expression 2 unoptimized scripts that drain 800+ Ops just by existing, **SF-DOOM** utilizes the true power of Garry's Mod's Lua-JIT compiler:

1. **Upfront Global Cache:** All high-frequency mathematical and rendering functions (e.g., `math.cos`, `render.drawRect`) are localized before the main `think` hook loop, minimizing global table lookup overhead.
2. **Early Exit Raycasting:** Optimized ray step increments prevent the CPU from running unnecessary iterations once a boundary collision is registered.
3. **Dynamic Budgeting:** Due to the Z-buffer layout, as the screen becomes saturated with monsters, the code dynamically prioritizes quick 2D rect fills over distant wall fog calculations, automatically stabilizing the CPU load.

---

## 🗺️ Roadmap & Campaign Levels

Currently porting the classic **Knee-Deep in the Dead** episode maps using optimized grid arrays:
- [ ] **E1M1: Hangar** (In Progress)
- [ ] **E1M2: Nuclear Plant** (Planned)
- [ ] **E1M3: Toxin Refinery** (Planned)

---

## 🎮 How to Play in GMod

1. Spawn a **Starfall Processor** on any Sandbox server.
2. Open the editor and paste the `DOOM.txt` source code.
3. **Controls:**
   - `W`, `A`, `S`, `D` — Movement & Turning
   - `1`, `2` — Switch Weapon (Pistol / Shotgun)
   - `F` — Interact / Open Doors / Exit Level
   - `X` — Shoot / Fire Weapon
4. Profit!
