# Project Idea: Predictive Cyber Incident Commander

## 1. Core Idea

The project is a real-time AI-powered cyber defence decision system that observes an unfolding cyberattack, reconstructs what is happening, predicts how the attacker is likely to progress, and recommends the safest defensive action before the attack reaches critical systems.

The system is not simply an intrusion detector.

Its purpose is to answer four progressively harder questions:

1. **Is something suspicious happening?**
2. **What is the attacker currently doing?**
3. **What are they likely to do or attack next?**
4. **What defensive action should be taken now?**

The intended pipeline is:

\[
\boxed{
\text{Observe}
\rightarrow
\text{Detect}
\rightarrow
\text{Reconstruct}
\rightarrow
\text{Predict}
\rightarrow
\text{Decide}
}
\]

The final product will be an interactive application in which cybersecurity events arrive continuously, the AI's understanding of the attack changes in real time, the attack path is visualised across the organisation's network, future attack behaviour is predicted, and defensive actions are recommended.

The project will initially operate entirely within a simulated organisation and simulated cyber environment.

---

# 2. Business Problem

Modern organisations operate thousands of interconnected digital assets:

- employee accounts;
- laptops;
- workstations;
- servers;
- databases;
- cloud resources;
- applications;
- email systems;
- APIs;
- network infrastructure;
- administrative accounts.

These systems continuously generate enormous volumes of security telemetry.

Cybersecurity products monitor this telemetry and produce alerts when unusual or potentially malicious activity is detected.

The problem is that these detection systems produce far more information than human security analysts can manually investigate in depth.

A 2026 Ponemon Institute study reported organisations receiving an average of approximately 4,330 security alerts per day, while only 37% were investigated.

Other industry research has similarly identified:

- excessive alert volume;
- large numbers of false positives;
- disconnected security tools;
- analyst burnout;
- investigation delays;
- difficulty correlating information across systems.

The fundamental business problem is therefore not simply:

> Organisations cannot detect cyberattacks.

The deeper problem is:

\[
\boxed{
\textbf{Cybersecurity detection produces information faster than human analysts can understand and act upon it.}
}
\]

A genuine attack may also generate many individually weak alerts across different systems.

For example:

```text
02:01  Unusual login
02:03  Suspicious PowerShell execution
02:05  Credential access
02:08  Internal server connection
02:11  Large data transfer
```

Each event alone may not justify shutting down a system.

Together they may describe a developing attack.

Humans therefore have to determine:

\[
\text{Are these events related?}
\]

\[
\text{What stage is the attack currently at?}
\]

\[
\text{Which systems are compromised?}
\]

\[
\text{Where could the attacker move next?}
\]

\[
\text{Should we intervene now or continue observing?}
\]

These decisions become increasingly difficult as the number of users, devices, systems and alerts grows.

---

# 3. Why Existing Detection Alone Is Not Enough

A traditional security detection system may produce:

```text
ALERT

Suspicious PowerShell Execution

Severity: Medium
```

This tells the analyst that something unusual occurred.

It does not necessarily tell the analyst:

- why it matters;
- whether it belongs to a wider attack;
- what the attacker is trying to accomplish;
- which asset they may target next;
- whether immediate intervention is justified;
- which defensive action creates the best trade-off between security and business disruption.

This distinction is central to the project.

The system is therefore not intended to merely perform:

\[
\text{Event}
\rightarrow
\text{Malicious / Benign}
\]

Instead, it aims to perform:

\[
\boxed{
\text{Events}
\rightarrow
\text{Attack state}
\rightarrow
\text{Attack progression}
\rightarrow
\text{Predicted future}
\rightarrow
\text{Defensive decision}
}
\]

---

# 4. The Main Research Question

The project's central question is:

> **Can an AI system continuously understand an unfolding cyberattack, predict its likely progression, and recommend defensive actions quickly enough to reduce attack propagation while avoiding unnecessary disruption to legitimate business activity?**

This contains three major AI problems.

### Detection

Determine whether incoming activity is suspicious.

### Prediction

Determine what the attacker is likely to do next.

### Decision optimisation

Determine what defensive action should be taken given uncertainty, risk and operational cost.

---

# 5. The User of the System

The intended user is a Security Operations Centre analyst or cyber incident responder.

The AI is not initially intended to completely replace the analyst.

Instead, it functions as a:

\[
\boxed{\textbf{Cyber Incident Commander / AI Defence Copilot}}
\]

The analyst should be able to see:

- what is currently happening;
- why the AI believes it is suspicious;
- which machines/accounts are involved;
- the reconstructed attack path;
- predicted next targets;
- predicted next attack stage;
- threat confidence;
- recommended defensive actions;
- expected benefit of each action;
- expected operational cost;
- uncertainty in the recommendation.

High-impact actions should initially require human approval.

---

# 6. Example Scenario

Consider a fictional company with the following infrastructure:

```text
Employees
    │
    ├── Laptop-A
    ├── Laptop-B
    └── Laptop-C

Servers
    │
    ├── FileServer
    ├── FinanceServer
    └── AuthenticationServer

Databases
    │
    ├── CustomerDB
    └── FinanceDB
```

At the beginning:

```text
SYSTEM STATUS: NORMAL

Threat Confidence: 3%
```

Everything appears green.

---

## Event 1

```text
22:41:02

Unusual login detected

User: Alice
Device: Laptop-A
Source IP: Unknown
```

The system may calculate:

\[
P(\text{attack})=0.28
\]

Recommendation:

> Continue monitoring.

There is not yet enough evidence to justify disruption.

---

## Event 2

```text
22:41:08

Suspicious PowerShell execution
Device: Laptop-A
```

Threat confidence changes:

\[
28\%\rightarrow57\%
\]

The system updates its hypothesis:

> Possible credential compromise followed by suspicious execution.

---

## Event 3

```text
22:41:15

Credential access behaviour detected
```

Threat confidence rises:

\[
57\%\rightarrow84\%
\]

The AI identifies the likely attack stage:

\[
\boxed{\text{Credential Access}}
\]

and predicts:

```text
Likely next stage:

Lateral Movement       69%
Persistence            18%
Collection              9%
Other                   4%
```

---

## Event 4

```text
22:41:22

Laptop-A → FinanceServer
```

The attack graph changes.

```text
Alice
  │
  ▼
Laptop-A 🔴
  │
  ▼
FinanceServer 🟠
  │
  ▼
FinanceDB 🟢
```

The system now identifies FinanceDB as a critical reachable asset.

Prediction:

```text
NEXT TARGET

FinanceDB          76%
FileServer         15%
Authentication      6%
Other               3%
```

---

# 7. Decision Intelligence

The system now has to choose between multiple possible actions.

For example:

```text
Monitor only
Block external IP
Revoke Alice's sessions
Disable Alice's account
Isolate Laptop-A
Isolate FinanceServer
Escalate to human responder
```

Each action has benefits and costs.

For example:

### Isolate Laptop-A

Potential benefit:

- prevents attacker from continuing from the compromised endpoint.

Operational cost:

- one employee temporarily loses access.

### Isolate FinanceServer

Potential benefit:

- strongly protects financial systems.

Operational cost:

- could disrupt many employees or critical business processes.

Therefore the system should not merely ask:

\[
\text{Which action stops the attacker?}
\]

It should ask:

\[
\boxed{
\text{Which action produces the greatest reduction in cyber risk for the lowest operational cost?}
}
\]

---

# 8. Possible Reward Function

A reinforcement-learning agent could eventually be trained around a reward function such as:

\[
R=
R_{\text{containment}}
-
C_{\text{compromise}}
-
C_{\text{business disruption}}
-
C_{\text{false response}}
-
C_{\text{delay}}
\]

Example values could initially be:

```text
Attack successfully contained        +100

Critical database protected          +150

Attacker spreads to another device   -80

Critical asset compromised           -300

Normal employee laptop isolated      -10

Critical server isolated unnecessarily
                                      -100

Attack allowed to continue too long  -50
```

The exact reward system would be a major design and experimentation component rather than something fixed arbitrarily.

---

# 9. Human-in-the-Loop Response

The system should not automatically perform every action.

Instead, actions could be categorised by impact.

### Low-impact action

Examples:

```text
Increase monitoring
Gather additional evidence
Block known malicious IP
```

Potentially automatable.

### Medium-impact action

Examples:

```text
Revoke login sessions
Temporarily isolate employee laptop
```

AI recommendation + optional automatic execution depending on confidence.

### High-impact action

Examples:

```text
Disable administrative account
Disconnect production server
Take finance system offline
```

Human approval required.

The philosophy is:

\[
\boxed{
\text{AI handles speed and complexity}
+
\text{human retains authority over high-impact decisions}
}
\]

---

# 10. Confidence-Aware Decision Making

One of the most important problems is deciding when there is enough evidence to intervene.

For example:

```text
PowerShell execution
```

alone may be legitimate.

An IT administrator may use PowerShell every day.

So:

\[
P(\text{attack})=20\%
\]

The system should probably monitor.

But:

```text
Unusual login
+
PowerShell
+
Credential dumping
+
Internal movement
```

may push the estimated threat probability toward:

\[
P(\text{attack})=97\%
\]

Therefore the system could eventually use different decision thresholds.

For example:

\[
P<40\%
\]

Monitor.

\[
40\%\leq P<70\%
\]

Gather additional evidence.

\[
70\%\leq P<90\%
\]

Alert human + recommend containment.

\[
P\geq90\%
\]

Consider automated low-risk containment.

These thresholds are conceptual for now and would need experimental justification.

The key idea is:

\[
\boxed{
\textbf{The system should know when it is uncertain.}
}
\]

---

# 11. Real-Time Architecture

The application should behave as an event-driven system.

It should not wait for an entire attack to finish.

Each incoming event updates the current state.

\[
S_t
+
E_{t+1}
\rightarrow
S_{t+1}
\]

The architecture could eventually resemble:

```text
                  LIVE SECURITY EVENTS
                          │
                          ▼
                EVENT PROCESSING
                          │
         ┌────────────────┼─────────────────┐
         │                │                 │
         ▼                ▼                 ▼
   Detection         Sequence         Attack Graph
     Model             Model             Engine
         │                │                 │
         └────────────────┼─────────────────┘
                          ▼
                    CURRENT STATE
                          │
              ┌───────────┴───────────┐
              │                       │
              ▼                       ▼
       Next-Move Predictor      Decision Agent
              │                       │
              ▼                       ▼
     "Likely DB next"      "Isolate Laptop-A"
```

Not every component needs to use deep learning.

Some may use:

- traditional algorithms;
- graphs;
- rule systems;
- probabilistic reasoning;
- trained ML models.

The objective is to use the best technique for each problem rather than forcing AI everywhere.

---

# 12. Potential AI Components

The exact models are not finalised yet.

Research and experimentation should determine the final architecture.

However, based on the project structure, several areas naturally align with techniques already studied.

---

## Component A — Event/Threat Classification

Possible objective:

\[
P(\text{malicious}\mid X)
\]

Possible models:

- neural network;
- random forest;
- XGBoost;
- autoencoder;
- VAE;
- sequence classifier.

Potential inputs:

```text
login frequency
source IP characteristics
process type
network connection
time
user behaviour
destination
packet/network features
```

---

# 13. Component B — Anomaly Detection

A model such as an autoencoder or VAE could learn what normal organisational activity looks like.

Given:

\[
X
\]

the model attempts to reconstruct:

\[
\hat X
\]

Large reconstruction error:

\[
||X-\hat X||
\]

could indicate unusual behaviour.

This may help detect activity not represented by predefined attack labels.

Whether this improves the system will need to be tested experimentally.

---

# 14. Component C — Sequence Understanding

Cyberattacks are temporal.

An event may only become dangerous because of what happened before it.

For example:

```text
Login
 ↓
PowerShell
 ↓
Credential access
 ↓
Internal connection
 ↓
Data collection
```

A sequence model could receive:

\[
E_1,E_2,...,E_t
\]

and estimate:

\[
P(E_{t+1})
\]

or:

\[
P(\text{next attack stage})
\]

Possible models:

- LSTM;
- GRU;
- Transformer;
- temporal model.

Because LSTMs have already been studied, they would be a reasonable initial baseline.

---

# 15. Component D — Attack Graph

The company can be represented as a graph:

\[
G=(V,E)
\]

where nodes represent:

```text
Users
Laptops
Servers
Databases
Applications
Accounts
```

and edges represent relationships such as:

```text
Can access
Logged into
Connected to
Has administrator privileges on
Communicated with
Depends on
```

Example:

```text
             Alice
               │
               ▼
           Laptop-A
            /     \
           ▼       ▼
     FileServer   FinanceServer
                      │
                      ▼
                  FinanceDB
```

As events arrive, the graph changes.

A compromised node could become red.

A suspected node could become orange.

Potential attack paths could be highlighted.

Graph algorithms can calculate:

- reachable assets;
- shortest attack paths;
- important nodes;
- critical dependencies;
- likely blast radius.

Later research could investigate Graph Neural Networks or Temporal Graph Neural Networks, but they are not required for the first version.

---

# 16. Component E — Next-Move Prediction

The system should attempt to predict one or both of:

### Next attack stage

Example:

```text
Lateral Movement    61%
Collection          23%
Persistence         10%
Other                6%
```

### Next target

Example:

```text
FinanceDB         71%
FileServer        17%
HRServer           8%
Other              4%
```

Inputs may eventually include:

- current attack stage;
- previous event sequence;
- compromised entities;
- network topology;
- access privileges;
- asset criticality;
- known attacker behaviour patterns.

This is one of the most important research areas because it moves the project beyond reactive cybersecurity.

---

# 17. Component F — Defensive Decision Agent

The decision layer receives the current state.

For example:

```text
Current stage:
Credential Access

Compromised:
Laptop-A

Compromised user:
Alice

Critical asset reachable:
FinanceDB

Threat confidence:
84%

Estimated next target:
FinanceDB
```

The decision agent evaluates possible defensive actions.

Conceptually:

\[
a^*=\arg\max_a Q(s,a)
\]

where:

\[
s=\text{current cyber state}
\]

and:

\[
a=\text{possible defence action}
\]

Potential actions include:

```text
Continue monitoring
Gather evidence
Block IP
Revoke session
Disable account
Isolate endpoint
Restrict server access
Escalate to analyst
```

The agent needs to learn that both underreaction and overreaction are costly.

---

# 18. Why Reinforcement Learning Is Appropriate

Cyber defence is sequential.

An action now changes what happens later.

For example:

### Action

```text
Monitor only
```

Possible consequence:

```text
Attacker reaches FinanceDB
```

### Action

```text
Isolate Laptop-A
```

Possible consequence:

```text
Attack contained
One employee disrupted
```

The problem is therefore not merely:

\[
X\rightarrow Y
\]

It is:

\[
\boxed{
S_t
\rightarrow
A_t
\rightarrow
S_{t+1}
\rightarrow
R_t
}
\]

which matches reinforcement learning naturally.

---

# 19. Simulation Environment

The first version will not interact with a real corporate network.

Instead, a simulated organisation will be created.

Example:

```text
100 employees
100 laptops
10 servers
5 databases
5 administrator accounts
```

Each asset will have properties such as:

```text
business importance
access privileges
security level
connections
normal activity
current state
```

The hidden simulator will know the ground truth.

For example:

```text
Actual compromised device:
Laptop-42

Actual attacker target:
FinanceDB

Actual attack path:
Laptop-42
→ Server-4
→ FinanceServer
→ FinanceDB
```

The AI does not receive this directly.

It receives only observable events.

This provides known labels for evaluating:

- attack detection;
- next-stage prediction;
- next-target prediction;
- attack-path reconstruction;
- containment decisions.

---

# 20. Attack Simulation

Attacks should not be random nonsense.

The scenarios should eventually be grounded in recognised cybersecurity behaviour such as MITRE ATT&CK.

Possible attack stages include:

```text
Initial Access
Execution
Persistence
Privilege Escalation
Defense Evasion
Credential Access
Discovery
Lateral Movement
Collection
Command and Control
Exfiltration
Impact
```

Example simulated attack:

```text
Phishing
 ↓
Credential theft
 ↓
Account login
 ↓
PowerShell
 ↓
Credential dumping
 ↓
Internal reconnaissance
 ↓
Lateral movement
 ↓
Database access
 ↓
Data exfiltration
```

Different simulated attackers could use different strategies.

---

# 21. Normal Behaviour Simulation

Normal behaviour is equally important.

Otherwise the AI will simply learn:

> Anything unusual = attack.

The simulated company must therefore generate legitimate activity such as:

```text
Employee logs in
Employee accesses file server
Admin runs PowerShell
Database backup occurs
Software update runs
Developer accesses server
Large legitimate file transfer
Employee works late
Employee travels overseas
```

This creates realistic ambiguity.

The AI then has to distinguish:

\[
\text{Unusual but legitimate}
\]

from:

\[
\text{Malicious}
\]

---

# 22. Public Datasets

Synthetic data will initially make experimentation easier, but the project should also investigate real public cybersecurity datasets.

Potential examples include:

### UNSW-NB15

Contains millions of labelled network records containing normal activity and several categories of attacks.

Potential use:

- network intrusion classification;
- anomaly detection;
- attack-category classification.

### CICIDS2017

Contains simulated enterprise network traffic including benign behaviour and multiple cyberattack categories.

Potential use:

- intrusion detection;
- sequence modelling;
- validation against less artificial data.

Other datasets should be researched during the dataset-selection phase.

The project may eventually combine:

\[
\boxed{
\text{Public real-world-style data}
+
\text{controlled synthetic attack simulations}
}
\]

---

# 23. Possible Role of GANs / VAEs

Generative techniques should only be used if they solve a real problem.

One potential problem is class imbalance.

Real systems may contain:

\[
99.9\%\text{ normal behaviour}
\]

and comparatively few examples of specific attacks.

A GAN or VAE could potentially generate additional attack-like data.

Possible experiment:

### Baseline

Train classifier using original imbalanced dataset.

### Experiment

Generate additional minority-class attack examples using generative model.

Compare:

- recall;
- precision;
- F1;
- false-positive rate;
- ability to detect rare attacks.

If synthetic generation does not improve performance, it should not be included simply to increase complexity.

---

# 24. Real-Time Responsiveness

Training is performed beforehand.

During operation the models perform inference only.

Therefore an event can be processed quickly.

For each new event:

\[
E_t
\]

the application updates:

```text
Threat probability
Attack stage
Attack graph
Next-target prediction
Recommended action
```

The demonstration can deliberately introduce events every few seconds so the audience can understand the progression.

The actual AI does not necessarily require several seconds per decision.

---

# 25. Proposed Application Interface

The app should feel like a cyber command centre.

A possible dashboard layout:

```text
┌───────────────────────────────────────────────┐
│ LIVE THREAT STATUS                            │
│ Threat Level: CRITICAL                        │
│ Confidence: 91%                               │
│ Current Stage: Lateral Movement               │
└───────────────────────────────────────────────┘

┌──────────────────────┐ ┌──────────────────────┐
│ LIVE ATTACK GRAPH    │ │ AI PREDICTION        │
│                      │ │                      │
│ Alice                │ │ Next target:         │
│   ↓                  │ │ FinanceDB       74%  │
│ Laptop-A 🔴          │ │ FileServer      18%  │
│   ↓                  │ │ Other            8%  │
│ Server-B 🟠          │ │                      │
│   ↓                  │ │ Next stage:          │
│ FinanceDB 🟢         │ │ Collection      66%  │
└──────────────────────┘ └──────────────────────┘

┌───────────────────────────────────────────────┐
│ RECOMMENDED DEFENCE                           │
│                                               │
│ 1. Isolate Laptop-A                           │
│ 2. Revoke Alice's sessions                    │
│                                               │
│ Expected containment: HIGH                    │
│ Business disruption: LOW                      │
│                                               │
│ [APPROVE]        [DECLINE]                    │
└───────────────────────────────────────────────┘

┌───────────────────────────────────────────────┐
│ EVENT STREAM                                  │
│ 22:41:02 Unusual login                        │
│ 22:41:08 PowerShell                           │
│ 22:41:15 Credential access                    │
│ 22:41:22 Internal connection                  │
└───────────────────────────────────────────────┘
```

---

# 26. Interactive Simulation

An important feature should be allowing the user to ignore or accept AI recommendations.

For example:

AI recommends:

> Isolate Laptop-A.

User chooses:

```text
IGNORE
```

The simulation continues.

Later:

```text
FinanceServer compromised.
```

Then:

```text
FinanceDB accessed.
```

The dashboard can show how the incident progressed because intervention was delayed.

Alternatively:

User accepts:

```text
ISOLATE LAPTOP-A
```

Then:

```text
Attack path interrupted.

Threat contained.
```

This makes the application much more than a static dashboard.

It demonstrates that cyber defence is a **sequential decision problem**.

---

# 27. Evaluation Metrics

Each AI component should be evaluated separately.

## Detection

Possible metrics:

\[
\text{Precision}
\]

\[
\text{Recall}
\]

\[
F_1
\]

\[
\text{False Positive Rate}
\]

Cybersecurity may place especially high importance on recall and false-negative behaviour.

---

## Next-stage prediction

Possible metrics:

\[
\text{Top-1 accuracy}
\]

\[
\text{Top-k accuracy}
\]

\[
F_1
\]

---

## Next-target prediction

Possible metrics:

\[
\text{Top-1 target accuracy}
\]

\[
\text{Top-3 target accuracy}
\]

This may be especially useful because multiple next targets can be plausible.

---

## Decision agent

The most important metrics may include:

```text
Attack containment rate
Time to containment
Critical assets compromised
False containment actions
Operational disruption
Average defensive cost
```

A combined measure could eventually compare:

\[
\text{Security protection}
\]

against:

\[
\text{Operational disruption}
\]

---

# 28. Possible Baselines

The project should not simply show that the final AI works.

It should demonstrate that it improves upon simpler strategies.

Potential baselines include:

### Baseline 1

Always monitor until confidence exceeds fixed threshold.

### Baseline 2

Always isolate the first suspicious device.

### Baseline 3

Rule-based response.

Example:

```text
IF threat confidence > 80%
THEN isolate device
```

### Baseline 4

Human-like heuristic strategy.

### Proposed model

Learned decision policy.

Then compare:

\[
\boxed{
\text{Does learned decision intelligence outperform simple cyber-response rules?}
}
\]

That would provide genuine experimental value.

---

# 29. Existing Industry Systems

The project operates in an active commercial research area.

Modern security platforms already perform parts of the proposed workflow.

Examples include systems capable of:

- alert correlation;
- automated investigation;
- attack reconstruction;
- automatic attack disruption;
- entity containment;
- predictive threat-path analysis.

This validates that the business problem is real.

However, the project should not simply attempt to recreate:

> An AI that summarises alerts.

The stronger project direction is:

\[
\boxed{
\textbf{Predictive, sequential cyber defence decision making}
}
\]

Specifically:

> Given an evolving attack state, what is most likely to happen next and what intervention produces the best expected outcome?

---

# 30. What Makes the Project Different From a Basic Cybersecurity ML Project

A normal student cybersecurity project might be:

\[
\text{Network packet}
\rightarrow
\text{Attack / Normal}
\]

Our proposed system is:

\[
\text{Event stream}
\]

↓

\[
\text{Threat detection}
\]

↓

\[
\text{Temporal attack understanding}
\]

↓

\[
\text{Attack graph}
\]

↓

\[
\text{Next-move prediction}
\]

↓

\[
\text{Defensive decision optimisation}
\]

↓

\[
\text{Interactive response}
\]

That changes the project from a classification exercise into a complete AI decision-support system.

---

# 31. Why AI May Perform Better Than Human-Only Investigation

The project targets areas where computers have structural advantages.

### Volume

AI can simultaneously process much larger numbers of events than a human.

### Temporal memory

A sequence model can continuously consider historical behaviour.

### Graph complexity

Algorithms can analyse thousands of relationships between accounts, devices and servers.

### Probability

The system can maintain multiple competing hypotheses rather than making one immediate binary judgment.

### Repeated optimisation

A decision model can evaluate the consequences of many possible response policies during simulation.

### Speed

Inference can occur as events arrive rather than waiting for a human to manually gather evidence.

Humans remain important for:

- unusual scenarios;
- incomplete context;
- organisational knowledge;
- ethical considerations;
- high-impact business decisions;
- final authority.

---

# 32. Main Technical Risks

The project has several important challenges.

### Synthetic-data realism

A badly designed simulator may create unrealistic attacks.

The system could then learn patterns that would not generalise.

### Reward hacking

The RL agent may discover behaviour that maximises its reward but makes no operational sense.

For example:

> Isolate every machine immediately.

That could stop attacks but destroy business operations.

Therefore the reward design must strongly penalise unnecessary disruption.

### False confidence

The system must not produce highly confident decisions from insufficient evidence.

### Dataset mismatch

Public intrusion datasets may not contain the exact event structure required for attack-path prediction.

### Scope

Attempting to perfectly reproduce an enterprise SOC would be unrealistic.

The project needs a controlled fictional environment while preserving the important decision complexity.

---

# 33. Scope Philosophy

The objective is not:

> Build Microsoft Defender.

Instead:

\[
\boxed{
\text{Build a constrained but complete research prototype of predictive cyber defence.}
}
\]

A smaller simulated network with meaningful attack paths is preferable to an enormous but shallow system.

For example:

```text
30 users
30 endpoints
8 servers
4 critical databases
```

may be enough to demonstrate the concept initially.

The complexity can be increased once the core system works.

---

# 34. Development Philosophy

The project should be built progressively.

The initial system can begin with:

\[
\text{Simulated events}
\rightarrow
\text{basic detection}
\rightarrow
\text{visual attack graph}
\]

Then add:

\[
\text{sequence prediction}
\]

Then:

\[
\text{next-target prediction}
\]

Then:

\[
\text{decision optimisation}
\]

Then:

\[
\text{real-time interactive app}
\]

The complete system should only integrate models that demonstrate measurable value.

---

# 35. Current Project Vision

The final vision is:

> **A real-time AI cyber defence system that continuously watches security events, reconstructs the developing attack across users and systems, predicts the attacker's likely next move, evaluates possible defensive responses, and recommends the action most likely to stop the attack while minimising disruption to legitimate business operations.**

In compressed form:

\[
\boxed{
\textbf{What is happening?}
}
\]

↓

\[
\boxed{
\textbf{Where is the attacker going next?}
}
\]

↓

\[
\boxed{
\textbf{What should we do before they get there?}
}
\]

That is the central identity of the project.

---

# 36. What Has Been Decided So Far

The following decisions are currently established:

- The project will focus on cybersecurity.
- It will target active cyber incidents rather than generic cyber awareness.
- It will not simply be an alert classifier.
- It will operate on continuous event streams.
- It will attempt to reconstruct an unfolding attack.
- It will represent relationships between assets using an attack/network graph.
- It will attempt to predict future attack behaviour.
- It will attempt to predict likely next targets.
- It will contain a decision-intelligence layer.
- Reinforcement learning is a strong candidate for the defensive decision problem.
- Defensive actions will have both security benefits and operational costs.
- High-impact actions will remain human-approved.
- The first version will use a simulated organisation.
- Attack scenarios should be based on recognised cyberattack behaviour such as MITRE ATT&CK.
- Public cybersecurity datasets will later be incorporated where appropriate.
- GAN/VAE techniques will only be included if experiments justify them.
- The application should operate interactively and appear real-time.
- The user should be able to accept or reject AI recommendations and see simulated consequences.
- The project will prioritise correctness, uncertainty awareness and explainability rather than blindly maximising automation.

---

# 37. What Has NOT Yet Been Decided

Several major decisions deliberately remain open because they require deeper research:

- exact cybersecurity event schema;
- exact public dataset(s);
- exact attack scenarios;
- exact graph representation;
- exact detection model;
- exact sequence model;
- whether a VAE is useful;
- whether GAN-generated data improves anything;
- whether next-target prediction should use sequence modelling, graph modelling or both;
- whether Q-learning is sufficient or a more advanced RL algorithm is required;
- reward-function weighting;
- autonomous-action confidence thresholds;
- exact simulated company topology;
- number of assets;
- exact frontend/backend technology;
- exact deployment architecture.

These should only be decided after the relevant research and experimentation.

---

# 38. Immediate Next Research Phase

Before implementation, the next phase should investigate:

1. How real cyberattacks progress through enterprise systems.
2. MITRE ATT&CK tactics and techniques in enough depth to model realistic sequences.
3. What security-event data actually looks like.
4. Which public datasets preserve useful temporal relationships between events.
5. How modern XDR/SIEM systems correlate alerts.
6. Existing research on next-stage and next-target prediction.
7. Existing approaches to attack graphs.
8. Existing autonomous cyber-response systems.
9. How cyber defence actions are normally chosen.
10. How to quantify the business cost of containment actions.
11. Existing reinforcement-learning research in autonomous cyber defence.
12. Which part of the proposed system can provide a meaningful technical contribution rather than merely recreating existing commercial functionality.

Only after this research should the final system architecture be locked.

---

# One-Line Project Pitch

> **An AI cyber incident commander that watches an attack unfold in real time, predicts where the attacker will move next, and recommends the safest intervention before critical systems are compromised.**

# Technical Pitch

> **A streaming predictive cyber-defence platform combining threat detection, temporal attack modelling, graph-based attack reconstruction, next-step prediction and reinforcement-learning-driven response optimisation within a simulated enterprise environment.**

# Business Pitch

> **Security teams cannot manually process and reason over every signal generated during fast-moving attacks. The system converts fragmented cyber events into an evolving attack model and helps defenders intervene earlier by predicting attack progression and optimising containment decisions.**