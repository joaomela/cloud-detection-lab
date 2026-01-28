# Detection Overview


This document describes the detection philosophy used in this lab and how detections are designed to minimize noise while maximizing signal.


---


## Detection Principles


Detections in this lab are:
-  Behavior-based rather than signature-based
-  Focused on attacker intent
-  Aligned with MITRE ATT&CK techniques


---


## Signal vs Noise


A detection is considered high signal when:
-  It represents abnormal behavior
-  It is difficult to generate during normal operations
-  It has a clear attacker objective


Low-signal detections (high noise) are avoided, such as:
-  Single failed login attempts
-  Legitimate administrative activity


---


## Telemetry-Driven Detection


Each detection is based on:
-  A specific log source
-  A known attack behavior
-  Clear visibility into the event


If no reliable telemetry exists, the detection is not implemented.


---


## Mapping Detections to MITRE ATT&CK


Each detection is explicitly mapped to:
-  A MITRE ATT&CK tactic
- A MITRE ATT&CK technique


This ensures detections align with real-world attacker behavior rather than hypothetical threats.


---


## Detection Lifecycle

1. Identify attacker behavior
2. Identify available telemetry
3. Design detection logic
4. Evaluate false positives
5. Document rationale

