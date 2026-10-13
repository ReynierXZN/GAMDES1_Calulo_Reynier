# Game Design Document (GDD)

## High Concept

**Premise:**  
A compact 2D precision platformer where a small character climbs through dangerous levels using only running, jumping, and dashing.

**Hook:**  
The game looks simple at first, but it has challenging movement, timing puzzles, and difficult sections that encourage players to keep trying and learn from their mistakes.

**Player Fantasy:**  
The player becomes a skilled and determined climber who improves through practice, learns from mistakes, and feels accomplished after completing difficult sections.

---

## Formal Elements

**Players:**  
Single player.

**Objectives:**  
Reach the end of each level by navigating platforms, spikes, moving hazards, and gaps using precise movement and timing.

**Rules:**  
- The player can run left and right, jump.  
- The player can grab on obstacles.  
- Touching hazards such as spikes, lasers, or crushing blocks causes the player to restart the current section.  
- Some objects can change the player's movement, such as ice, bounce pads, and wind.  
- Optional collectibles can be placed in risky areas. They are not required to complete the level.

**Procedures:**  
1. The player starts at a designated spawn point.  
2. The player moves through the level using running, jumping, and dashing.  
3. The player avoids hazards and uses different platforming mechanics.  
4. When the player dies, they respawn at the start of the current room or checkpoint.  
5. When the player reaches the exit, the next room or level loads.  
6. Players can replay levels to improve their time, collect missed items, or practice difficult sections.

**Resources:**  
- Player skill, including timing, movement, and knowledge of the mechanics.  
- Movement tools such as dashing, wall-jumping, moving platforms, and bounce pads.  
- Optional collectibles that reward skilled play but are not required for progression.

**Conflict:**  
The main conflict is between the player's current skill and the challenges of the level. Players must overcome tight gaps, hazards, precise dash timing, and sequences that require multiple movement mechanics.

**Boundaries:**  
- The game takes place in separate 2D levels or rooms with clear starting and ending points.  
- Player movement is limited to the movement mechanics included in the game.  
- Success depends mainly on the player's skill, timing, and understanding of the game's mechanics.

**Outcome:**  
- Short-term: complete individual levels by reaching the exit without dying (or with acceptable deaths).  
- Long-term: finish all levels, optionally collecting harder-to-reach items and improving speed and consistency, building a sense of mastery over increasingly complex platforming challenges.

---

## Core Loop

The core loop is a tight input–action–feedback cycle that repeats every few seconds within a level:

1. **Input:** The player presses run, jump, and/or dash in response to the current geometry and hazards.  
2. **Action:** The character moves through the level, performing jumps, dashes, wall interactions, etc., according to the physics and rules.  
3. **Feedback:**  
   - Visual: character position, hazard animations, particles on near-misses or deaths.  
   - Audio: jump/dash sounds, hit/death sounds, music that reinforces tension and flow.  
   - Immediate consequence: either safe progress, a near-miss, or instant death and respawn.  
4. **Adjustment:** The player internalizes what went wrong or right (too-early dash, missed jump, wrong angle) and immediately tries again with refined timing and route choice.  
5. **Progression:** After enough iterations, the player executes the sequence cleanly, reaches the next checkpoint or level end, and feels a clear sense of improvement.

This loop is worth repeating because each attempt teaches something specific about timing, positioning, or route optimization. Failures are short and informative, and successes feel earned, creating a strong “one more try” rhythm that matches the Celeste-like prototype built in Lab 3.

---

## Revision Note (Post Peer Read-Around)

After peer feedback, I clarified the Core Loop to explicitly call out “Adjustment” as its own step and tied the feedback directly to short, informative failures. This better reflects the Lab 3 prototype’s fast respawn and tight platforming rhythm.

# GDD Section V: Level Design

## 5.1 Level Layout Pattern

**Layout Pattern:** Linear with short optional side paths.

The level is primarily **linear**: the player moves from a defined start point through a sequence of rooms or sections toward a single exit. A few **optional side paths** branch off briefly to hold collectibles or reward riskier movement, but they always reconnect to the main route.

**Why this fits our Core Loop (Section IV):**  
Our core loop is built on short, repeated attempts: input → action → feedback → adjustment → progression. A linear layout lets us:

- Control exactly when new mechanics and hazards appear.
- Keep deaths fast and respawns close, so the “one more try” rhythm stays tight.
- Build a clear difficulty curve from simple jumps to complex dash-and-grab sequences.
- Use optional branches to reward mastery without confusing the main path.

A hub-and-spoke or fully open layout would spread the player’s attention across many routes and make it harder to guarantee that each player encounters the intended teaching moments in order. Linear design keeps the learning sequence intentional.

---

## 5.2 Annotated Level Map

Below is a simple top-down/side-view sketch of the level. The player moves left to right.

```text
[START]──[Safe Zone]──[Gap + Spikes]──[Moving Platform]──[Rest Zone]──[Wall + Grab]──[Dash Gap]──[Hazard Corridor]──[EXIT]
   │                                                                                          │
   └──[Optional Side Path: Collectible]──────────────────────────────────────────────────────┘
```

**Annotations:**

- **START:** Player spawns on a flat, safe platform.
- **Safe Zone (Pacing Beat: Rest):** No hazards; player can test basic run and jump.
- **Gap + Spikes:** First real obstacle; introduces danger and precise jumping.
- **Moving Platform:** Requires timing; player must wait and jump at the right moment.
- **Rest Zone (Pacing Beat: Rest):** Short flat area with no immediate threat; player can breathe and observe the next section.
- **Wall + Grab:** Introduces grabbing/climbing on vertical surfaces.
- **Dash Gap:** Requires a well-timed dash to cross a wider gap.
- **Hazard Corridor (Pacing Beat: Tension Rise):** Combines spikes, moving hazards, and tight timing; this is the level’s peak challenge.
- **EXIT:** Door or end marker that loads the next room/level.
- **Optional Side Path:** A riskier route with a collectible; not required to finish.

**Pacing beats marked on map:**

- **Rest:** Safe Zone (early), Rest Zone (middle).
- **Tension Rise:** Hazard Corridor (late), just before EXIT.

---

## 5.3 Pacing and Difficulty Curve

Difficulty rises in steps, with short rests between spikes in challenge.

```text
Difficulty
   ▲
   │                         ┌──────────────┐
   │                         │ Hazard       │
   │                ┌────────┤ Corridor     │
   │                │        └──────────────┘
   │        ┌───────┤ Wall + Grab → Dash Gap
   │        │       │
   │  ┌─────┤ Moving Platform
   │  │     │
   │  │ Gap + Spikes
   │  │
   └──┴─────┴────────────────────────────────▶ Level Progress
     Safe   Rest   Mid Challenge   Peak     Exit
     Zone   Zone
```

**How difficulty changes:**

1. **Safe Zone:** Very low difficulty; player learns basic movement.
2. **Gap + Spikes:** Low-to-medium; introduces risk of death.
3. **Moving Platform:** Medium; adds timing.
4. **Rest Zone:** Difficulty drops briefly; player recovers and observes.
5. **Wall + Grab → Dash Gap:** Medium-to-high; chains mechanics together.
6. **Hazard Corridor:** High; combines multiple hazards and requires precise execution.
7. **EXIT:** Challenge ends; player feels relief and accomplishment.

**Flow channel point:**  
The **Moving Platform** section is where most players are likely inside the flow channel: the challenge is noticeable but manageable, feedback is immediate, and success feels earned without being frustrating.

**Boredom risk:**  
If the **Rest Zone** is too long or too empty, players may get bored before the next challenge. Keep it short and visually interesting.

**Anxiety risk:**  
The **Hazard Corridor** risks pushing players into anxiety if it is too long or if checkpoints are too far apart. Keep the corridor short and place the respawn close to its start.

---

## 5.4 Teaching Mechanics Through Level Sequencing

The level introduces and reinforces the mechanics the player needs to finish it.

| Mechanic | Where Introduced | Teaching Technique |
|----------|------------------|--------------------|
| Running and Jumping | Safe Zone, right after START | **Isolated safe space:** flat area with no hazards where the player can experiment freely. |
| Avoiding Spikes / Hazards | Gap + Spikes section | **Forced encounter:** the only path forward crosses a spike-lined gap, so the player must learn to jump precisely. |
| Timing with Moving Platforms | Moving Platform section | **Environmental cue:** the platform’s movement pattern is visible before the player must commit, teaching rhythm through observation. |
| Wall Grabbing | Wall + Grab section | **Forced encounter:** a vertical wall blocks the path, requiring the player to grab and climb. |
| Dashing | Dash Gap section | **Environmental cue:** a clearly wider gap signals that a normal jump is not enough, prompting use of dash. |
| Combining Mechanics | Hazard Corridor | **Forced encounter:** the corridor requires chaining jump, grab, and dash in quick succession. |

**Summary of teaching sequence:**

1. Teach basic movement in a safe space.
2. Introduce danger with a simple hazard.
3. Add timing with a moving obstacle.
4. Give a short rest.
5. Teach vertical movement (grab).
6. Teach horizontal burst movement (dash).
7. Combine everything in a final challenge.
8. End with a clear exit and sense of accomplishment.

---

## Revision Note (Post Peer Gallery Walk)

*After the peer gallery walk, I adjusted the pacing so the Rest Zone is shorter and placed it closer to the Hazard Corridor, reducing the risk of boredom while still giving players a breather before the level’s peak challenge.*

# GDD Section VI: Systems and Balance

This section defines the numbers behind the Core Loop (Section IV) and the level structure (Section V). All values are **provisional** and are meant to be tuned in playtesting. Distances are in tiles; time is in seconds.

## 6.1 Resource Economy

The game deliberately has very few resources: the player is a single character with one-hit death and no inventory. Every resource is listed below, including the ones that have no sink.

| Resource | Starting value | Source (how the player gets it) | Sink (how it is spent or lost) | Cap / notes |
|---|---|---|---|---|
| **Dash charge** | 1 | Refills to max on touching the ground. A refill crystal restores 1 charge mid-air and respawns 2.5 s after use. Also refilled on respawn. | Each dash costs 1 charge. | Max 1 in Levels 1–3, max 2 in Levels 4–5. |
| **Wall stamina** | 120 | Refills to full on touching the ground. Also refilled on respawn. | Holding still on a wall: 5 per second. Climbing: 20 per second (2 tiles/s). Wall jump: 20 flat. At 0 the player slides off. | Cap 120. Never carried between rooms. |
| **Death count** | 0 | +1 each time the player touches a hazard. | None, by design. | Display only. No gameplay effect, so it cannot become a balance problem. |
| **Level time** | 0:00 | Runs in real time from entering a level (paused in menus). | None. Resets on a full level restart; the best time per level is kept. | Used only for the optional speed goal (par times in 6.2). |
| **Collectibles** | 0 | 1 per level, placed on the optional side path (Section V, 5.2). | None. It is a permanent tally and is never spent. | Banked only when the player reaches the next checkpoint or exit. Dying first returns it to the level. |

**Resources with no source or sink, and why this is safe:**

- **Death count, level time, and collectibles have no sink.** They are scores, not currencies. Nothing in the game can be bought with them, so they cannot inflate or make the game easier or harder. Their only effect is pride and replay value.
- **Health and lives do not exist.** Touching a hazard is instant death with a respawn at the room or checkpoint start. Removing health keeps each attempt short, which the Core Loop depends on.
- **Dash charge and stamina have both a source and a sink, and both refill on the ground.** The player can never run out permanently. The worst case is falling and landing, which refills everything.

**Design rule from tuning:** any room that requires *n* dashes must give the player *n* sources of dash charge along the route (ground contact or a refill crystal). See the paper simulation below.

## 6.2 Progression Curve

The player character never levels up: speed, jump height, and health are fixed. **Capability grows in two ways:** the toolset expands in steps (new abilities and objects), and the player's own skill improves. **Challenge grows** by adding hazards and by chaining more mechanics in a single sequence.

Base values: maximum jump gap = 4 tiles, dash adds 4 tiles of reach, so a jump plus dash reaches 8 tiles. In Level 1 the Dash Gap is 6 tiles wide, so it uses 75% of the player's reach.

| Level | New capability or object | Hazards per screen | Mechanics chained in one sequence | Tightest gap vs. player reach | Target deaths per room | Target time per room |
|---|---|---|---|---|---|---|
| 1 | Run, jump, grab, dash (1 charge) | 1 | 1–2 | 75% | 3 | 20 s |
| 2 | Bounce pads, ice | 2 | 2 | 80% | 6 | 30 s |
| 3 | Wind, refill crystals | 3 | 2–3 | 85% | 10 | 45 s |
| 4 | Second dash charge | 4 | 3 | 85% | 15 | 60 s |
| 5 | All objects combined | 5 | 3–4 | 90% | 20 | 75 s |

**Scaling relationship:** each level adds exactly one new tool but raises hazard density by 1 per screen and often lengthens the chain by one mechanic. Challenge therefore grows faster than the toolset, and the gap is closed by player skill, which is the only stat that actually increases. Rest Zones (Section V) reset the pressure between peaks.

**Pacing checks tied to the Core Loop:** an attempt should last about 5–10 seconds, and checkpoints are never more than one screen or about 30 seconds apart. At 20 deaths per room and 10 seconds per attempt, even the hardest rooms cost the player roughly 3–4 minutes.

## 6.3 Symmetry, Asymmetry, and Fairness

**The game is asymmetric.** There is one player and no opposing player. The player has a small, fixed movement kit, and the level has fixed hazards and platforms. The two sides do not have equal capabilities, so fairness has to be designed in rather than assumed.

**What makes the outcome feel fair (player vs. the level):**

- **Everything is learnable and repeatable.** Hazards run on fixed, deterministic patterns that restart when the player enters or respawns in a room, so every attempt shows the same pattern.
- **The level never asks for more than the toolset allows.** Every required jump, dash, and grab is within the numbers in 6.2 (never over 90% of the player's reach), and new mechanics are taught first in a safe or forced-encounter setting (Section V, 5.4).
- **Deaths are the player's own.** Without randomness or hidden rules, a death can always be traced to a late input, a bad angle, or a misread cue.
- **Failure is cheap.** There is no health, no lives, instant respawn, and checkpoints within one screen.
- **Forgiving input windows.** Coyote time (6 frames after leaving a ledge) and a jump buffer (6 frames before landing) make the controls match what the player *meant* to do. Hitboxes for hazards are slightly smaller than their sprites.
- **Optional content carries the risk.** Collectibles sit on risky side paths, so players choose their own difficulty and the main route stays achievable.

## 6.4 Randomness and Probability

**The game uses no randomness in gameplay.** This is a design decision: a precision platformer depends on the player learning exact patterns. If a hazard behaved differently each attempt, the player could not tell whether a death was their mistake or bad luck, and the "Adjustment" step of the Core Loop would stop working.

| System | Uses randomness? | Probability values | Purpose |
|---|---|---|---|
| Hazard patterns (moving platforms, lasers, crushing blocks) | No | 0% random, fixed schedule | Learnable timing |
| Dash charge, stamina, refill crystals | No | Fixed values and fixed 2.5 s respawn | Predictable resource economy |
| Collectible and hazard placement | No | Fixed per level | Consistent routes and fair risk |
| Death-burst particle direction, ambient particles | Yes, cosmetic only | Uniform random angle and spawn time | Visual variety. Has no effect on collisions or outcome. |

**Protection against an unwinnable run:**

- Because nothing affecting the outcome is random, every room has one verified solution that the designers must complete before it ships.
- Respawning resets all room state (hazard timers, crystals, stamina, dash charge), so a bad attempt can never leave the room in a broken state.
- Dash charge and stamina refill on the ground, so the player cannot run out of either permanently.
- Collectibles are optional, so missing one never blocks the path.
- Design rule from 6.1: a room that needs *n* dashes provides *n* charge sources.

## 6.5 Paper Simulation and Tuning (Step 5)

**Wall stamina.** The Hazard Corridor has a 6-tile wall: climbing costs 6 tiles ÷ 2 tiles/s × 20 = 60, plus a 20 wall jump, so 80 total. The player may also pause to read the hazards (5 per second).

| Attempt | Pause on wall | Total spent | Result at max 100 | Result at max 120 |
|---|---|---|---|---|
| A | 0 s | 80 | Pass (20 left) | Pass (40 left) |
| B | 2 s | 90 | Pass (10 left) | Pass (30 left) |
| C | 4 s | 100 | Pass (0 left, no margin) | Pass (20 left) |
| D | 6 s | 110 | **Fail** | Pass (10 left) |
| E | 8 s | 120 | Fail | Pass (0 left, no margin) |

*Finding:* with a max of 100, the player has only about 4 seconds to observe and think on the wall, which punishes careful play and contradicts the "learn from mistakes" hook. **Change made: stamina max raised from 100 to 120**, giving about 8 seconds of margin. The 4-tile wall in the Wall + Grab tutorial costs 40 + 20 = 60, leaving 60 spare.

**Dash charge.** Walking the Hazard Corridor with a 1-charge cap showed that any sequence needing two dashes before touching the ground cannot be completed. **Change made:** the Level 1 corridor is limited to one dash, and the design rule in 6.1 now requires matching charge sources for any room that needs more.

**Peer playtest notes (to complete after trading with another group):**

- Group tested: ____________________
- What broke or felt unfair: ____________________
- Revision made in response: ____________________

## Reflection (Section VI)

**Which resource was hardest to balance, and what did tuning reveal?** Wall stamina. At 100 it looked fine on paper, but simulating a player who pauses to read the hazards showed that the margin for thinking was only about 4 seconds. That made careful play riskier than rushing, which is the opposite of the intended hook. Raising it to 120 fixed that. The dash simulation also revealed that a one-charge cap makes some sequences impossible unless the level supplies refill points.

**How confident is the group that a player cannot get an unwinnable run?** Very confident, because nothing that affects the outcome is random and every room resets fully on respawn. The remaining risk is a room that was designed wrongly (such as the dash-count problem above), which is why every room must be completed by a designer before it ships. Adding randomness would make the game worse, since it would blur the link between a player's mistake and a death.
