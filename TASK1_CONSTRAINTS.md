# Task 1 — Identify Constraints

## Railway Level-Crossing Control System (ARLCCS)
### Constraint Identification and Analysis

---

## Constraint C1
**Constraint ID:** C1  
**Constraint in Simple English:** The barrier must not open while a train is present in the crossing.  
**Reason:** Opening the barrier could allow road traffic to enter the crossing while the train is passing, causing collision and endangering lives.

---

## Constraint C2
**Constraint ID:** C2  
**Constraint in Simple English:** Warning signals (lights and alarms) must be activated before the barriers start closing.  
**Reason:** Drivers must have adequate warning time to stop their vehicles before the barriers descend, preventing accidents and allowing safe evacuation.

---

## Constraint C3
**Constraint ID:** C3  
**Constraint in Simple English:** The barriers must be fully closed before the train enters the crossing.  
**Reason:** Partially closed barriers cannot provide adequate protection; a train could strike a barrier or allow vehicles to pass through, causing accidents.

---

## Constraint C4
**Constraint ID:** C4  
**Constraint in Simple English:** If a sensor fails, the system must immediately transition to a safe state (barriers down, warnings on).  
**Reason:** Sensor failure could lead to incorrect detection of train presence; maintaining a closed/warning state prevents accidents until the fault is resolved.

---

## Constraint C5
**Constraint ID:** C5  
**Constraint in Simple English:** The barriers must remain closed until the safety-monitoring unit confirms the train has completely cleared the crossing.  
**Reason:** Opening barriers prematurely while any part of the train is still in the crossing could result in vehicles entering the crossing and colliding with the train.

---

## Constraint C6
**Constraint ID:** C6  
**Constraint in Simple English:** The traffic signal must show "stop" (red) for road traffic whenever the barriers are closing or closed.  
**Reason:** A "stop" signal ensures road traffic obeys the barrier control; without it, drivers might not respond to the barrier and attempt to cross.

---

## Constraint C7
**Constraint ID:** C7  
**Constraint in Simple English:** The system must not open the barriers while warning signals are still active.  
**Reason:** Active warnings indicate an imminent or present train; opening barriers during this state would contradict the warning and confuse drivers.

---

## Constraint C8
**Constraint ID:** C8  
**Constraint in Simple English:** In an emergency condition, the barriers must override any open command and remain closed, with warnings activated.  
**Reason:** Emergency conditions (e.g., unauthorized crossing attempt, object on tracks) require the safest possible state to prevent accidents.

---

## Constraint C9
**Constraint ID:** C9  
**Constraint in Simple English:** If barrier movement fails (barrier stuck midway), the system must not allow the train to enter until the barrier is fully lowered or a manual override is authorized.  
**Reason:** A stuck barrier cannot provide protection; allowing train passage could result in collision with the barrier or vehicles.

---

## Constraint C10
**Constraint ID:** C10  
**Constraint in Simple English:** Communication loss between the control center and the field equipment must trigger automatic barrier closure and warning activation.  
**Reason:** Loss of communication could leave the system in an unsafe state; automatic closure ensures continued protection even if remote control is unavailable.

---

## Constraint C11
**Constraint ID:** C11  
**Constraint in Simple English:** The system must maintain a consistent state where barriers are either fully open or fully closed (no partial opening).  
**Reason:** Partial barrier positions create ambiguity about crossing safety and could allow vehicles to enter partially protected areas.

---

## Constraint C12
**Constraint ID:** C12  
**Constraint in Simple English:** Incorrect sensor readings (e.g., detecting a train when none is present) must trigger a system diagnostic and maintain safe state until resolved.  
**Reason:** False positives disrupt traffic unnecessarily; false negatives risk accidents. Diagnostics ensure data integrity before resuming normal operation.

---
