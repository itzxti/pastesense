## Requirements

- Visual Studio 2022 or Newer
- The **Desktop development with C++** workload
- The **C++ Clang tools for Windows** and **vcpkg** components
- An x64 processor with AVX2 support
- Internet access for the first dependency restore

FreeType is declared in `vcpkg.json` and is restored automatically by Visual Studio/MSBuild.

## Build

Open a **Developer PowerShell for Visual Studio** at the repository root and run:

```powershell
msbuild cs2\velocity-cs2\velocity-cs2.vcxproj /m /p:Configuration=Ship /p:Platform=x64
```

The Ship build is written to `cs2\bin\cs2.dll`. Use `Configuration=Development` to produce `cs2\bin\velocity-cs2-dev.dll` with development diagnostics.

If you use a standalone vcpkg installation instead of Visual Studio's bundled copy, set `VCPKG_ROOT` to its directory before building.

---

# Pastesense — Extreme CS2 HVH Feature Specification

Expand Pastesense into a highly sophisticated CS2 HVH framework for servers where third-party client modifications are explicitly permitted.

The priority is not simply adding more toggles. Every system should interact with the others and produce measurable improvements in targeting, survivability, and consistency.

## 1. Advanced Ragebot

Build a modular ragebot architecture with:

### Target selection

- Distance
- FOV
- Health
- Damage potential
- Lethality
- Threat level
- Visibility
- Historical hit rate
- Enemy anti-aim state
- Configurable priority weighting

### Hitboxes

- Head
- Neck
- Chest
- Stomach
- Pelvis
- Arms
- Legs
- Configurable hitbox groups
- Per-weapon hitbox priorities

### Multipoint

- Dynamic multipoint scales
- Per-hitbox scales
- Adaptive point selection
- Head priority
- Body priority
- Damage-aware point selection
- Visibility-aware point selection

## 2. Adaptive Resolver

Do not rely on a single resolver.

Create a resolver framework containing independent strategies:

```text
Static
Jitter
Low Delta
High Delta
Spin
Freestanding
Moving
Standing
Airborne
Brute Force
Adaptive
```

The resolver should track:

- Previous enemy states
- Resolver hypothesis
- Shot result
- Hit/miss
- Damage
- Target position
- Orientation changes
- Animation/state changes

Maintain confidence values for resolver hypotheses and adapt based on observed results.

Example conceptual system:

```text
Enemy #4

Static      12% confidence
Jitter      64% confidence
Freestand   18% confidence
Spin         6% confidence

Current strategy: Jitter
```

Allow the resolver to reconsider its hypothesis after unsuccessful shots.

## 3. Shot Analysis

Create a complete shot recorder.

Record:

```text
Timestamp
Target
Weapon
Target position
Local position
Predicted position
Resolver state
Hitbox
Multipoint
Hitchance
Expected damage
Actual damage
Shot result
Miss reason
```

Add a post-round analysis screen showing:

- Accuracy
- Resolver success rate
- Missed shots
- Miss categories
- Average damage
- Headshot percentage
- Resolver confidence
- Target-specific statistics

## 4. Adaptive Hitchance

Implement more than a basic percentage threshold.

Consider:

- Weapon
- Distance
- Target velocity
- Target state
- Spread
- Movement
- Resolver confidence
- Multipoint quality
- Expected damage

Allow separate thresholds for:

```text
Head
Body
Lethal
Low HP
Moving target
Standing target
```

## 5. Autostop / Movement

Create a movement optimizer capable of selecting appropriate stopping behavior based on:

- Current velocity
- Desired hitbox
- Weapon
- Target distance
- Ground state
- Current tick
- Shot timing

Include configurable:

- Full stop
- Directional stop
- Counter-strafe
- Early stop
- Late stop
- Weapon-specific stop settings

## 6. Advanced Anti-Aim

Expand anti-aim into a state machine.

States:

```text
Standing
Walking
Running
Slow Walk
Crouching
Airborne
Landing
Shooting
Post-Shot
Low HP
Manual Override
```

Each state can independently configure:

- Yaw
- Jitter
- Jitter range
- Jitter speed
- Pitch
- Direction
- Freestanding
- Body orientation
- Switch timing

Add deterministic and randomized patterns.

## 7. Anti-Aim Pattern Generator

Create a pattern editor allowing users to construct sequences such as:

```text
Tick 0-4     → Left
Tick 5-8     → Right
Tick 9-12    → Center
Tick 13-16   → Random
Repeat
```

Allow patterns to be saved inside configs.

## 8. Freestanding Analysis

Create a visibility-based directional analysis system.

Evaluate candidate orientations and determine which direction exposes the least useful target surface.

Visualize the selected direction in the GUI.

Provide debug information explaining the decision.

## 9. Enemy Threat Analysis

Create an enemy threat-ranking system.

Calculate a threat value from:

- Distance
- Weapon
- Health
- Historical accuracy
- Current target
- Visibility
- Resolver confidence
- Recent shots
- Damage potential

Display:

```text
Enemy       Threat
Player A    92%
Player B    71%
Player C    38%
```

Use this information as an optional target-priority input.

## 10. Weapon Intelligence

Create weapon-specific profiles.

Example:

```text
AWP
├── Hitchance
├── Minimum damage
├── Multipoint
├── Autostop
├── Target priority
└── Resolver behavior

Scout
├── Hitchance
├── Minimum damage
├── Multipoint
├── Autostop
└── Resolver behavior
```

Automatically switch configurations when weapons change.

## 11. Damage Simulation

Implement a damage-analysis layer capable of estimating:

- Potential damage
- Lethality
- Armor effects
- Hitbox selection
- Distance effects
- Weapon characteristics

Expose:

```text
Expected Damage
Minimum Damage
Lethal
Target HP
Target Armor
```

Use this to improve target and point selection.

## 12. Visual Debugging

Add an optional developer overlay showing:

- Player hitboxes
- Multipoints
- Resolver direction
- Predicted position
- Current target
- Selected point
- Aim position
- Spread cone
- Shot trajectory
- Autostop state
- Anti-aim state

Everything should be individually toggleable.

## 13. Lag / Network Awareness

Create a network-state monitor that tracks information available to the client, such as:

- Latency
- Interpolation state
- Packet timing
- Tick timing
- Local/server timing information

Use these measurements to make prediction and shot timing more consistent.

## 14. Configuration Profiles

Support complete profiles:

```text
Aggressive
Safe
AWP
Scout
Rifle
Pistol
Anti-Jitter
Anti-Spin
Adaptive
Experimental
```

Add automatic profile switching based on weapon/state if enabled.

## 15. Performance Architecture

Separate the project into modules:

```text
Pastesense
├── Core
├── Game
├── Entities
├── Schema
├── Interfaces
├── Renderer
├── GUI
├── Aimbot
├── Resolver
├── AntiAim
├── Prediction
├── Movement
├── Damage
├── WeaponSystem
├── Config
├── Statistics
├── Diagnostics
└── Debug
```

Avoid turning the project into one enormous feature file.

Every subsystem should have clear interfaces and lifecycle management.

## 16. Automatic Diagnostics

Add a diagnostic screen showing:

```text
CS2 Build       ✓
Schema          ✓
Interfaces      ✓
Renderer        ✓
Entity System   ✓
Prediction      ✓
Aimbot          ✓
Resolver        ✓
Config          ✓
```

If something becomes incompatible after a CS2 update, identify the exact subsystem instead of crashing.

## 17. Testing Framework

Create a local testing/benchmark mode.

Measure:

- Target-selection latency
- Resolver decisions
- Shot accuracy
- Average damage
- Prediction error
- Autostop effectiveness
- Hitchance decisions
- CPU usage
- Frame-time impact

The objective is to make improvements measurable rather than relying on subjective impressions.

## 18. Final Design Goal

Pastesense should be designed as an adaptive system rather than a collection of independent cheat features.

The major systems should communicate:

```text
Enemy Analysis
      ↓
Resolver
      ↓
Target Selection
      ↓
Multipoint
      ↓
Damage Analysis
      ↓
Hitchance
      ↓
Movement / Autostop
      ↓
Shot
      ↓
Shot Analysis
      ↓
Resolver Feedback
      ↓
Adaptive Configuration
```

Prioritize accuracy, adaptability, stability, and measurable performance over simply adding more menu options.

Do not add mechanisms intended to compromise, disable, or bypass anti-cheat systems or interfere with another user's software. The competitive objective should come from improving Pastesense's own HVH systems.

---

## Implementation guidance

This framework should be organized around data-driven subsystems instead of monolithic toggles:

- Enemy analysis should feed both resolver and target-priority layers.
- Resolver confidence should directly influence aimbot target selection and hitchance.
- Hitbox and multipoint logic should be damage and visibility aware.
- Movement and anti-aim should share state with shot timing, not operate independently.
- Diagnostics and benchmarking must remain part of the runtime architecture so CS2 updates can be isolated to the exact failing subsystem.

The end goal is a consistent, measurable HVH loop: detect, resolve, select, simulate, shoot, analyze, and adapt.
