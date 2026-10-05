# Task 3 — Identify Constraint Violations

## Railway Level-Crossing Control System (ARLCCS)
### Realistic Violation Scenarios

---

## Violation V1: Constraint C1 Violated

**Constraint:**
```
Train_Present → ¬Barrier_Open
```

**Violation Scenario:**
```
Train_Present = TRUE
Barrier_Open = TRUE
```

**What Exactly Has Gone Wrong:**  
The system has detected that a train is actively present within the railway crossing (Train_Present = TRUE), but the barrier controlling road access is simultaneously in the open position (Barrier_Open = TRUE). This is a critical safety violation.

**How We Know the Constraint is Violated:**
- The implication rule states: "If a train is present, then the barrier MUST NOT be open."
- Both conditions are true: (1) Train detected in crossing, (2) Barrier is open.
- The consequent (¬Barrier_Open) is FALSE when it should be TRUE.
- Therefore, the implication Train_Present → ¬Barrier_Open evaluates to FALSE.

**Consequences:**  
Road traffic may attempt to cross the railway line while the train is present, leading to potential collision, loss of life, and property damage.

**Detection Method:**  
The safety-monitoring unit should continuously check train presence and barrier state; when this condition is detected, a critical alert should be triggered immediately.

---

## Violation V2: Constraint C2 Violated

**Constraint:**
```
Barrier_Closing → Warning_Active
```

**Violation Scenario:**
```
Barrier_Closing = TRUE
Warning_Active = FALSE
```

**What Exactly Has Gone Wrong:**  
The barriers have begun their closing sequence (Barrier_Closing = TRUE) but the warning signals (lights and audible alarms) have not been activated (Warning_Active = FALSE). Drivers are unaware that the crossing is about to be blocked.

**How We Know the Constraint is Violated:**
- The rule requires: "If barriers are closing, then warnings must be active."
- The antecedent (Barrier_Closing) is TRUE, but the consequent (Warning_Active) is FALSE.
- This makes the implication Barrier_Closing → Warning_Active evaluate to FALSE.
- The constraint is directly violated.

**Consequences:**  
Drivers approaching the crossing will not receive timely warning; they may not stop in time, leading to collision with descending barriers or dangerous last-second braking.

**Detection Method:**  
The system must verify that warning activation occurs before or at the same time as barrier closure. Any barrier closing event without corresponding warning activation should trigger a fault state.

---

## Violation V3: Constraint C3 Violated

**Constraint:**
```
Train_Entering → Barrier_Closed
```

**Violation Scenario:**
```
Train_Entering = TRUE
Barrier_Closed = FALSE
```

**What Exactly Has Gone Wrong:**  
The train has begun entering the railway crossing (Train_Entering = TRUE), but the barriers are not yet fully closed (Barrier_Closed = FALSE). The crossing remains partially or fully open.

**How We Know the Constraint is Violated:**
- The rule mandates: "If a train is entering, the barriers must be fully closed."
- Train_Entering is TRUE but Barrier_Closed is FALSE.
- The implication Train_Entering → Barrier_Closed is FALSE.
- The constraint is violated at a critical moment—train arrival.

**Consequences:**  
The train may collide with the barriers if they are partially down, or road traffic might still be on the crossing, leading to multi-vehicle collision with the train.

**Detection Method:**  
The train-detection sensor must not signal train entry until the barrier-position sensor confirms full closure. If train entry is detected while barriers are opening or not fully closed, an emergency stop should be triggered.

---

## Violation V4: Constraint C4 Violated

**Constraint:**
```
Sensor_Failed → (Barrier_Closed ∧ Warning_Active)
```

**Violation Scenario:**
```
Sensor_Failed = TRUE
Barrier_Closed = FALSE
Warning_Active = FALSE
```

**What Exactly Has Gone Wrong:**  
The system has detected a sensor failure (Sensor_Failed = TRUE), but the fail-safe response has not been executed. The barriers remain open (Barrier_Closed = FALSE) and warnings are not active (Warning_Active = FALSE).

**How We Know the Constraint is Violated:**
- The rule states: "If a sensor fails, then barriers must be closed AND warnings must be active."
- Sensor_Failed is TRUE, but both Barrier_Closed and Warning_Active are FALSE.
- The conjunction (Barrier_Closed ∧ Warning_Active) evaluates to FALSE.
- The implication Sensor_Failed → (Barrier_Closed ∧ Warning_Active) is FALSE.

**Consequences:**  
Without fail-safe action, the system may operate on corrupted or missing sensor data, unable to reliably detect train presence, leading to unprotected crossing access.

**Detection Method:**  
The system must implement automatic fail-safe logic: upon detecting any sensor fault (redundancy check, timeout, or sensor self-test failure), immediately close barriers and activate warnings without waiting for explicit commands.

---

## Violation V5: Constraint C5 Violated

**Constraint:**
```
¬Train_Cleared → Barrier_Closed
```

**Violation Scenario:**
```
Train_Cleared = FALSE
Barrier_Closed = FALSE
```

**What Exactly Has Gone Wrong:**  
The safety-monitoring unit has NOT confirmed that the train has completely cleared the crossing (Train_Cleared = FALSE), yet the barriers are in the open position (Barrier_Closed = FALSE). The crossing is unprotected while a train may still be present.

**How We Know the Constraint is Violated:**
- The rule states: "If the train has NOT cleared the crossing, then barriers must remain closed."
- ¬Train_Cleared is TRUE (Train_Cleared is FALSE), but Barrier_Closed is FALSE.
- The implication ¬Train_Cleared → Barrier_Closed is FALSE.

**Consequences:**  
Road traffic may enter the crossing while the train is still passing through, resulting in collision.

**Detection Method:**  
A countdown timer or rear-end train-detection sensor should confirm that the train has fully exited before allowing barrier opening. The control system must wait for explicit clearance from the safety-monitoring unit.

---

## Violation V6: Constraint C6 Violated

**Constraint:**
```
(Barrier_Closing ∨ Barrier_Closed) → Traffic_Stop
```

**Violation Scenario:**
```
Barrier_Closing = TRUE
Barrier_Closed = FALSE
Traffic_Stop = FALSE
```

**What Exactly Has Gone Wrong:**  
The barriers are actively closing (Barrier_Closing = TRUE), but the traffic signal is not showing "stop" to road traffic (Traffic_Stop = FALSE). Drivers see no signal to stop and may attempt to proceed.

**How We Know the Constraint is Violated:**
- The rule requires: "If barriers are closing or closed, then traffic signal must show stop."
- (Barrier_Closing ∨ Barrier_Closed) evaluates to TRUE.
- Traffic_Stop is FALSE.
- The implication evaluates to FALSE; constraint is violated.

**Consequences:**  
Drivers may not recognize the danger and proceed into the closing barrier or crossing zone, causing injury or death.

**Detection Method:**  
The traffic-signal control system must be interlinked with barrier control. Any barrier closing or closed event must immediately trigger the traffic signal to red/stop.

---

## Violation V7: Constraint C7 Violated

**Constraint:**
```
Warning_Active → ¬Barrier_Open
```

**Violation Scenario:**
```
Warning_Active = TRUE
Barrier_Open = TRUE
```

**What Exactly Has Gone Wrong:**  
Warning signals (lights and alarms) are actively alerting drivers and pedestrians (Warning_Active = TRUE), indicating imminent danger, but the barriers are simultaneously open to traffic (Barrier_Open = TRUE). This is contradictory and confusing.

**How We Know the Constraint is Violated:**
- The rule states: "If warnings are active, barriers must not be open."
- Warning_Active is TRUE but Barrier_Open is TRUE.
- ¬Barrier_Open is FALSE when it should be TRUE.
- The implication Warning_Active → ¬Barrier_Open is FALSE.

**Consequences:**  
Drivers receive conflicting information: warnings tell them danger is imminent, but open barriers suggest it is safe to proceed. This confusion can lead to accidents and loss of life.

**Detection Method:**  
The system must enforce coupling between warning signals and barrier state. If warnings are triggered, barriers must close. If barriers are open, warnings must be off.

---

## Violation V8: Constraint C8 Violated

**Constraint:**
```
Emergency_Condition → (Barrier_Closed ∧ Warning_Active ∧ ¬Allow_Open_Command)
```

**Violation Scenario:**
```
Emergency_Condition = TRUE
Barrier_Closed = FALSE
Warning_Active = TRUE
Allow_Open_Command = TRUE
```

**What Exactly Has Gone Wrong:**  
An emergency condition has been detected (Emergency_Condition = TRUE), such as an unauthorized person on the tracks or a stalled vehicle in the crossing. However, the system response is incomplete:
- Barriers have NOT been closed (Barrier_Closed = FALSE)
- Warnings ARE active (Warning_Active = TRUE) ✓
- Open commands are still being accepted (Allow_Open_Command = TRUE)

Only one of three required safety measures is in place.

**How We Know the Constraint is Violated:**
- The rule requires all three conditions: Barrier_Closed ∧ Warning_Active ∧ ¬Allow_Open_Command.
- (FALSE ∧ TRUE ∧ FALSE) evaluates to FALSE.
- The implication Emergency_Condition → FALSE is FALSE.

**Consequences:**  
Despite emergency conditions, if an operator commands the barriers to open, the system will obey. The train could proceed into the crossing where the emergency object or person is located, causing catastrophe.

**Detection Method:**  
Emergency detection must trigger a multi-layer response: automatically close barriers, activate alarms, and disable all open commands until emergency is manually cleared by authorized personnel.

---

## Violation V9: Constraint C10 Violated

**Constraint:**
```
Communication_Lost → (Barrier_Closed ∧ Warning_Active ∧ Fail_Safe_Triggered)
```

**Violation Scenario:**
```
Communication_Lost = TRUE
Barrier_Closed = TRUE
Warning_Active = FALSE
Fail_Safe_Triggered = FALSE
```

**What Exactly Has Gone Wrong:**  
Communication between the control center and the field equipment has been lost (Communication_Lost = TRUE). The system has partially responded:
- Barriers have closed (Barrier_Closed = TRUE) ✓
- Warnings have NOT been activated (Warning_Active = FALSE)
- Fail-safe mode has NOT been triggered (Fail_Safe_Triggered = FALSE)

The response is incomplete; only one of three required safety measures is active.

**How We Know the Constraint is Violated:**
- The rule requires: Communication_Lost → (Barrier_Closed ∧ Warning_Active ∧ Fail_Safe_Triggered).
- (TRUE ∧ FALSE ∧ FALSE) = FALSE.
- The implication evaluates to FALSE.

**Consequences:**  
Without warning activation and fail-safe mode, drivers may not understand why barriers are suddenly down. If communication is restored with incorrect information, the system might operate unpredictably.

**Detection Method:**  
Communication loss must trigger an atomic fail-safe response: simultaneously close barriers, activate all warning systems, and lock the system into a protected state until communication is restored and verified.

---

## Summary Table of Violations

| Violation | Constraint | Violated Condition | Primary Issue | Safety Impact |
|-----------|------------|-------------------|---------------|----------------|
| V1 | C1 | Train present + Barrier open | Barriers not protective | Collision risk |
| V2 | C2 | Barrier closing + No warnings | Drivers unaware | Barrier strike/accident |
| V3 | C3 | Train entering + Barrier not closed | Premature opening | Train/barrier collision |
| V4 | C4 | Sensor failed + No fail-safe response | System unreliable | Loss of train detection |
| V5 | C5 | Train not cleared + Barrier open | Premature opening | Train/vehicle collision |
| V6 | C6 | Barrier closing + No traffic stop signal | Drivers confused | Crossing entry accident |
| V7 | C7 | Warnings active + Barrier open | Contradictory state | Driver confusion/accident |
| V8 | C8 | Emergency + Open commands allowed | Emergency response incomplete | Catastrophic collision |
| V9 | C10 | Communication lost + Partial fail-safe | Incomplete response | System unreliability |

---

