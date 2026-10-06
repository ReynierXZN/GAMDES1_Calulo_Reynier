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
