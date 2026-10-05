# Task 2 — Formalize Constraints

## Railway Level-Crossing Control System (ARLCCS)
### Formal Expression of Selected Constraints

---

## Constraint C1 (Formalized)
**Original Constraint:** The barrier must not open while a train is present in the crossing.

**Formal Expression:**
```
Train_Present → ¬Barrier_Open
```

**Explanation:**  
If a train is present in the crossing, then the barrier must NOT be open. This is a conditional rule: whenever the train presence condition is TRUE, the barrier state must be FALSE (closed).

---

## Constraint C2 (Formalized)
**Original Constraint:** Warning signals must be activated before the barriers start closing.

**Formal Expression:**
```
Barrier_Closing → Warning_Active
```

**Explanation:**  
If barriers are beginning to close, then warnings must already be active. The implication ensures that warning activation always precedes or coincides with barrier closure.

---

## Constraint C3 (Formalized)
**Original Constraint:** The barriers must be fully closed before the train enters the crossing.

**Formal Expression:**
```
Train_Entering → Barrier_Closed
```

**Explanation:**  
If a train is entering the crossing, then the barriers must be in a fully closed state. This ensures the crossing is protected before train arrival.

---

## Constraint C4 (Formalized)
**Original Constraint:** If a sensor fails, the system must immediately transition to a safe state (barriers down, warnings on).

**Formal Expression:**
```
Sensor_Failed → (Barrier_Closed ∧ Warning_Active)
```

**Explanation:**  
If any sensor fails, then both conditions must be true: barriers must be closed AND warnings must be active. The conjunction (∧) ensures both safety measures are in place simultaneously.

---

## Constraint C5 (Formalized)
**Original Constraint:** The barriers must remain closed until the safety-monitoring unit confirms the train has completely cleared the crossing.

**Formal Expression:**
```
¬Train_Cleared → Barrier_Closed
```

**Explanation:**  
Equivalently: If the train has NOT cleared the crossing, then the barriers must remain closed. This prevents premature opening.

---

## Constraint C6 (Formalized)
**Original Constraint:** The traffic signal must show "stop" (red) for road traffic whenever the barriers are closing or closed.

**Formal Expression:**
```
(Barrier_Closing ∨ Barrier_Closed) → Traffic_Stop
```

**Explanation:**  
If barriers are either in the process of closing OR already closed, then the traffic signal must display "stop." The disjunction (∨) combines both barrier states into one condition.

---

## Constraint C7 (Formalized)
**Original Constraint:** The system must not open the barriers while warning signals are still active.

**Formal Expression:**
```
Warning_Active → ¬Barrier_Open
```

**Explanation:**  
If warnings are active, then the barriers must NOT be open. Active warnings indicate potential danger; barriers must be closed in response.

---

## Constraint C8 (Formalized)
**Original Constraint:** In an emergency condition, the barriers must override any open command and remain closed, with warnings activated.

**Formal Expression:**
```
Emergency_Condition → (Barrier_Closed ∧ Warning_Active ∧ ¬Allow_Open_Command)
```

**Explanation:**  
If an emergency condition exists, then three things must be true simultaneously: barriers must be closed, warnings must be active, and any open command must be blocked. This represents the highest safety priority.

---
