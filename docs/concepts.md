# Core Concepts

## State over Status

Status reflects point-in-time signals.

State reflects system truth over time.

---

## Recovery vs Resolution

A system can return to service without being stable.

Sentra distinguishes between:
- recovery (system is back)
- resolution (system is proven stable)

---

## Safe-to-Act

Actions should not be taken based solely on availability.

They should be gated based on:
- system posture  
- signal confidence  
- validation over time  

---

## Multi-Signal Evaluation

No single signal is sufficient.

Sentra evaluates system posture using signals across:
- application  
- infrastructure  
- network  
- physical domains  
