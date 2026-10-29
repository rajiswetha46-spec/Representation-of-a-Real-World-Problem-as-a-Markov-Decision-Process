# Representation-of-a-Real-World-Problem-as-a-Markov-Decision-Process
### Name: Swetha R
### Reg No: 212225100055

## Aim

To model a Smart Home Temperature Control System using a Markov Decision Process (MDP) by defining its states, actions, transition probabilities, rewards, and Python representation.

## Problem Statement

To model a Smart Home Temperature Control System using a Markov Decision Process (MDP) by identifying its states, actions, transition probabilities, reward function, and discount factor. The system aims to maintain a comfortable room temperature by making suitable decisions based on the current temperature conditions. It should also minimize unnecessary air conditioner usage, reduce electricity consumption, and avoid excessive cooling. The MDP approach helps the system evaluate possible outcomes of its actions and make effective temperature control decisions over time.

### Problem Description

The Smart Home Temperature Control System operates based on three temperature states: Hot, Comfortable, and Cold. At each state, the system can choose one of three actions:

AC ON
AC OFF
Reduce Cooling

The system receives rewards for maintaining a comfortable room temperature and penalties for excessive cooling or uncomfortable temperature conditions.

The problem can be represented using a Markov Decision Process:

$$ MDP=(S,A,P,R,\gamma) $$

Where:

S = Set of states

A = Set of actions

P = Transition probability

R = Reward function

γ = Discount factor

---

## MDP Components


| Component                  | Description                                                                            |
| -------------------------- | -------------------------------------------------------------------------------------- |
| Agent                      | Smart Temperature Control System                                                       |
| Environment                | Room with an air conditioner (AC)                                                      |
| State Space (S)            | Hot, Comfortable, Cold                                                                 |
| Action Space (A)           | AC ON, AC OFF, Reduce Cooling                                                          |
| Transition Probability (P) | Probability of the room temperature changing from one state to another after an action |
| Reward Function (R)        | Rewards for maintaining a comfortable temperature and penalties for excessive cooling  |
| Discount Factor (γ)        | 0.9                                                                                    |
| Goal                       | Maintain a comfortable room temperature while reducing electricity consumption         |


---

## State Space

The state space represents the possible temperature conditions of the room in the Smart Home Temperature Control System.

S = {Hot, Comfortable, Cold}

The states are:

Hot<br>
Comfortable<br>
Cold



---

## Sample State

A sample state represents the current temperature condition of the room.

S = Hot

For example, if the room temperature is 30°C, the current state is Hot. The system can turn on the air conditioner (AC) to reduce the room temperature.



---

## Action Space

The action space represents all possible actions the agent can take to control the room temperature.

A = {
    AC ON,
    AC OFF,
    Reduce Cooling
}

The actions are:

AC ON<br>
AC OFF<br>
Reduce Cooling


---

## Sample Action

A sample action represents one possible action selected by the agent based on the current room temperature.

```text
A = AC ON
```

For example, when the room temperature is high (Hot state), the system selects the **AC ON** action to reduce the room temperature and maintain a comfortable environment.

---

## Transistion Probability
The transition probability explains how the room temperature changes from one state to another after an action is taken.

General form:

$$ P(s′|s,a) $$

This means:

Probability of reaching the next state s′ after taking action a in the current state s.

For this Smart Home Temperature Control System, the transitions are considered probabilistic.

| Current State | Action         | Next State  | Probability |
| ------------- | -------------- | ----------- | ----------- |
| Hot           | AC ON          | Comfortable | 0.8         |
| Hot           | AC ON          | Hot         | 0.2         |
| Comfortable   | Reduce Cooling | Comfortable | 0.8         |
| Comfortable   | Reduce Cooling | Cold        | 0.2         |
| Cold          | AC OFF         | Comfortable | 0.7         |
| Cold          | AC OFF         | Cold        | 0.3         |

Example:

P(Comfortable | Hot, AC ON) = 0.8

This means when the room temperature is Hot and the AC is turned ON, there is an 80% probability that the room will reach a Comfortable state.

## Reward Function
## Reward Function

The reward function defines the feedback received by the agent after taking an action.

General form:

```math
R(s,a,s′)
```

The reward system for the Smart Home Temperature Control System is:

| **Situation**                          | **Reward** |
| -------------------------------------- | ---------: |
| Room reaches a comfortable temperature |        +10 |
| Maintains a comfortable temperature    |         +5 |
| Room remains hot after AC is turned ON |         -2 |
| Room becomes too cold                  |         -5 |
| Unnecessary AC usage                   |         -3 |

A positive reward encourages the system to maintain a comfortable room temperature.

A negative reward discourages excessive cooling and unnecessary electricity consumption.

The discount factor is:

```math
γ = 0.9
```

For example, if the room temperature is Hot, the system turns ON the AC to reach a comfortable temperature.

```text
Hot → AC ON → Comfortable
```

The system receives a positive reward when the room reaches a comfortable temperature.

---

## Graphical Representation

The MDP graph represents states as nodes and actions as transitions between states.

The graph should include:

1. States as nodes.
2. Actions as arrows.
3. Rewards on transitions.
4. Transition probabilities if applicable.

                               P=0.2, R=-2
                  ┌───────────────┐
                  ▼               │
              ┌────────┐          │
              │  HOT   │──────────┘
              └────────┘
                  │
                  │ AC ON
                  │ P=0.8, R=+10
                  ▼
          ┌────────────────┐
          │  COMFORTABLE   │◄──────────────┐
          └────────────────┘               │
                  │                        │
                  │ Reduce Cooling         │ AC OFF
                  │ P=0.2, R=-5            │ P=0.7, R=+10
                  ▼                        │
              ┌────────┐                   │
              │  COLD  │───────────────────┘
              └────────┘
                  ▲
                  │ Self-loop
                  │ P=0.3, R=-2
                  └──────────────
Example Transistion: 
```
Hot -- AC ON / P=0.8 / Reward=+10 --> Comfortable
Hot -- AC ON / P=0.2 / Reward=-2 --> Hot
```
---

## Python Representation

The following Python program represents the MDP using dictionaries.

It displays the state space, action space, transition probabilities, reward function, and discount factor.
```
print("Name: SWETHA R")
print("Register Number: 212225100055")

states = ["Hot", "Comfortable", "Cold"]
actions = ["AC ON", "AC OFF", "Reduce Cooling"]
gamma = 0.9

transitions = {
    ("Hot", "AC ON"): {"Comfortable": 0.8, "Hot": 0.2},
    ("Comfortable", "Reduce Cooling"): {"Comfortable": 0.8, "Cold": 0.2},
    ("Cold", "AC OFF"): {"Comfortable": 0.7, "Cold": 0.3}
}

rewards = {
    ("Hot", "AC ON", "Comfortable"): 10,
    ("Hot", "AC ON", "Hot"): -2,
    ("Comfortable", "Reduce Cooling", "Comfortable"): 5,
    ("Comfortable", "Reduce Cooling", "Cold"): -5,
    ("Cold", "AC OFF", "Comfortable"): 10,
    ("Cold", "AC OFF", "Cold"): -2
}

print("\n--- STATE SPACE ---")
for i, s in enumerate(states, 1):
    print(f"S{i}: {s}")

print("\n--- ACTION SPACE ---")
for i, a in enumerate(actions, 1):
    print(f"A{i}: {a}")

print("\n--- TRANSITIONS & REWARDS ---")
for (s, a), next_states in transitions.items():
    for ns, p in next_states.items():
        r = rewards[(s, a, ns)]
        print(f"{s} --{a}--> {ns} | P={p} | R={r}")

print("\n--- DISCOUNT FACTOR ---")
print("Gamma =", gamma)
print("\nMDP Representation Completed Successfully!")
```
---
## Output
<img width="587" height="552" alt="Screenshot 2026-10-29 095454" src="https://github.com/user-attachments/assets/1e96a033-b798-41cf-b201-21cd1af2f537" />


## Result

The Smart Home Temperature Control System was successfully represented as a Markov Decision Process using Python dictionaries.

The model contains three states, three actions, transition probabilities, and a reward function. The discount factor was set to γ = 0.9 to consider future rewards.

The graphical representation illustrates the relationship between states, actions, transition probabilities, and rewards.

This project demonstrates how an MDP can be used to model a practical smart home temperature control system and make suitable decisions to maintain a comfortable room temperature while reducing unnecessary electricity consumption.

---

