# Left 2 Die — Testing Plan

---

## 1. Overview
This document defines the testing plan for *Left 2 Die*, a multiplayer, action-adventure shooter game with survival and zombie mechanics. It includes user stories, acceptance criteria, test procedures, boundary and edge testing, expected results, and candidates for automation. The goal is to ensure gameplay is fair, responsive, and free of logic errors, while also preparing for scalable automated testing.

---

## 2. User Stories and Acceptance Criteria

### User Story 1: Surviving a Horde Encounter
**As a** player, I want to survive waves of infected, including special infected, so that I can progress through the level and reach the safe zone.  

- **Acceptance Criterion 1**
    - Requirement(s): Combat system and enemy AI must function correctly.
    - Purpose: Ensure the player can defend and survive.
    - Test Case:
        a) Feature: Player combat against standard infected  
        b) Test: Engage 5 regular zombies using melee and firearms  
        c) Expected Result / Behavior: All zombies take damage and die according to weapon stats; player health decreases correctly  
        d) Automation Candidate: Rule-based automated test of combat damage calculations  

- **Acceptance Criterion 2**
    - Requirement(s): Special infected attacks are handled properly  
    - Purpose: Ensure challenge from special infected is fair and consistent  
    - Test Case:
        a) Feature: Special infected (Tank, Hunter) attack  
        b) Test: Spawn one Tank and one Hunter near player  
        c) Expected Result / Behavior: Player receives damage correctly; enemy abilities trigger as expected  
        d) Automation Candidate: High-volume automated test for repeated enemy ability checks  

---

### User Story 2: Using Strategic Resources
**As a** player, I want to scavenge medkits, ammo, and melee weapons so that I can manage my health and resources throughout the levels.  

- **Acceptance Criterion 1**
    - Requirement(s): Inventory and resource system  
    - Purpose: Ensure resource limits and pickups function  
    - Test Case:
        a) Feature: Picking up items  
        b) Test: Collect medkits, ammo, and melee items until inventory full  
        c) Expected Result / Behavior: Items are added until max inventory; additional items cannot be picked up  
        d) Automation Candidate: Rule-based automation for inventory limits  

- **Acceptance Criterion 2**
    - Requirement(s): AI dynamically places resources  
    - Purpose: Encourage exploration and strategy  
    - Test Case:
        a) Feature: Resource spawning  
        b) Test: Play the level multiple times to verify medkits/ammo appear in varied locations  
        c) Expected Result / Behavior: Resources spawn logically without clustering or gaps; player can find items  
        d) Automation Candidate: High-volume automation simulating repeated playthroughs  

---

### User Story 3: Calling for Extraction
**As a** player, I want to call a helicopter or boat for extraction at the end of a map so that I can progress safely.  

- **Acceptance Criterion 1**
    - Requirement(s): Extraction system via radio  
    - Purpose: Ensure level completion triggers correctly  
    - Test Case:
        a) Feature: Call helicopter at extraction point  
        b) Test: Player activates radio at correct location  
        c) Expected Result / Behavior: Helicopter arrives; level progression begins; enemies continue to attack until arrival  
        d) Automation Candidate: Rule-based automated test of extraction trigger  

- **Acceptance Criterion 2**
    - Requirement(s): Extraction under pressure (enemy attacks)  
    - Purpose: Test challenge balance  
    - Test Case:
        a) Feature: Extraction with surrounding enemies  
        b) Test: Player surrounded by 5-10 infected when calling extraction  
        c) Expected Result / Behavior: Extraction still triggers correctly; enemies behave as expected  
        d) Automation Candidate: Repetitive simulation of extraction under enemy conditions  

---

## 3. Boundary and Edge Testing

### Boundary / Edge 1: Player Health & Damage
- Requirement(s): Player health system  
- Purpose: Prevent incorrect health calculation and ensure fair combat  

- Test Case 1:
    a) Upper Boundary: Maximum HP  
    b) Testing data used: 99, 100, 101  
    c) Expected Result / Behavior: HP never exceeds max; damage is calculated correctly  
    d) Automation Candidate: Rule-based automated health tests  

- Test Case 2:
    a) Lower Boundary: Minimum HP / death  
    b) Testing data used: 0, 1, -1  
    c) Expected Result / Behavior: Player dies at 0 HP; no negative HP occurs  
    d) Automation Candidate: Rule-based automated death and damage verification  

---

### Boundary / Edge 2: AI Spawn & Horde System
- Requirement(s): Enemy spawn logic  
- Purpose: Ensure game handles extreme enemy counts and spawn positions  

- Test Case 1:
    a) Upper Boundary: Maximum spawn  
    b) Testing data used: 49, 50, 51 enemies  
    c) Expected Result / Behavior: Game handles max enemies without freezing; enemies attack correctly  
    d) Automation Candidate: High-volume automated enemy spawn test  

- Test Case 2:
    a) Lower Boundary: Minimum spawn / 0 enemies  
    b) Testing data used: 0, 1, 2 enemies  
    c) Expected Result / Behavior: Level remains playable; no crash or logic error  
    d) Automation Candidate: Rule-based automated test of AI spawn edge cases  

---

### Boundary / Edge 3: Extraction / Level Completion
- Requirement(s): Extraction triggers level progression  
- Purpose: Prevent incorrect or broken level completion  

- Test Case 1:
    a) Upper Boundary: Extraction at last possible moment  
    b) Testing data used: Player surrounded by max enemies at extraction point  
    c) Expected Result / Behavior: Extraction still triggers; level progresses; no crashes  
    d) Automation Candidate: Repetitive automated test simulating end-of-level extraction  

- Test Case 2:
    a) Lower Boundary: Extraction attempted too early  
    b) Testing data used: Player calls extraction at 10% level completion  
    c) Expected Result / Behavior: Extraction sequence initiates correctly; AI spawns appropriately; game continues  
    d) Automation Candidate: Rule-based automated test of early extraction logic  

---

## 4. Automated Test List
| Test Candidate | Type of Automation |
|----------------|-----------------|
| Combat damage calculations | Rule-based |
| Inventory limit checks | Rule-based |
| Enemy spawn and AI logic | High-volume |
| Resource placement and pickups | High-volume |
| Extraction triggers | Repetitive / Rule-based |
| Player health and death edge cases | Rule-based |

---

