# Left 2 Die — Boundary & Edge Testing

## 🎯 Goal
Identify extreme, unusual, or unexpected inputs in the game that could break mechanics. Plan tests to ensure the game handles these cases gracefully.

---

## Logic Point A: Player Health & Damage System
*Critical because damage and survival determine game balance and fairness.*

| Boundary Input       | Test Data Example         | Expected Outcome                                                                 |
|---------------------|--------------------------|---------------------------------------------------------------------------------|
| Minimum Health       | Player HP = 1            | Single strong hit kills player; game registers death correctly without crash.   |
| Maximum Health       | Player HP = 100          | Damage calculation reduces HP correctly; no negative or over-max health occurs. |
| Simultaneous Attacks | Player hit by 3 enemies at once | HP reduces by cumulative damage; player survives if HP > 0; no errors occur. |

---

## Logic Point B: AI Spawn & Horde System
*Critical because dynamic spawning affects difficulty, performance, and player experience.*

| Boundary Input             | Test Data Example                       | Expected Outcome                                                                 |
|----------------------------|----------------------------------------|---------------------------------------------------------------------------------|
| Minimum Spawn              | 0 infected spawn                        | Level still functions; player can move and explore; no crashes.                 |
| Maximum Spawn              | 50 infected spawn at once               | Game handles high enemy count without freezing; player can still act.           |
| Spawn Too Close to Player  | Special infected spawns 1 unit away    | Enemy attacks player immediately; collision and damage work correctly.          |

---

## Logic Point C: Extraction / Level Completion
*Critical because signaling for extraction must trigger level progression without breaking game flow.*

| Boundary Input         | Test Data Example                         | Expected Outcome                                                                 |
|------------------------|------------------------------------------|---------------------------------------------------------------------------------|
| Extraction Trigger Early | Player calls radio at 10% level progress | Extraction sequence starts; AI may spawn enemies; player can still survive.     |
| Extraction Trigger Late  | Player calls radio surrounded by 10 enemies | Extraction event works; player can survive until helicopter/boat arrives.      |
| No Player Interaction   | Player never reaches extraction point    | Level does not progress; game does not crash; timeout handled correctly.       |

---

## 🧩 Reflection

- **Most fragile logic point:** AI Spawn & Horde System — too many enemies or weird spawn positions could crash the game.  
- **Things to watch out for when coding:** Damage calculation order, enemy collision detection, and extraction triggers under heavy enemy load.  
- **Most surprising boundary case:** Spawning a special infected immediately next to the player — creates instant danger and tests all collision/damage systems simultaneously.  
