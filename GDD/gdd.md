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