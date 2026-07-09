# 07 — Implications

> *Statistics, sets, temporal meaning. What the numbers teach us.*

---

## 7.1 Frequency as signal

A concept with 900 occurrences ("atelier") is 83× more likely to be retrieved than one with 11 ("Pierre"). This is not bias — it's an **empirical relevance metric**.

The vector space naturally prioritizes what matters most, without any weighting, without any manual intervention. The lived frequency of a concept in the conversation IS its importance weight.

| Concept | Occurrences | Weight |
|:--------|:-----------:|:------:|
| atelier | 917 | Highest |
| travel | 868 | Very high |
| code | 685 | Very high |
| mémoire | 428 | High |
| m4z3 | 384 | High |
| sarah | 302 | High |
| libre | 181 | Medium |
| mercier | 158 | Medium |
| tortue | 80 | Low |
| pierre | 11 | Low but precise |

---

## 7.2 Sets and proximity

311,442 atoms in a 384-dimensional space. A point cloud in an hypercube.

**Cosine distance is relative:** "close" means "closer than the average distance in the dataset." An atom is not close to another in an absolute sense — it's close **relative to all other pairs**.

**L3 doors partition by affinity:** The three semantic circles (L1 = focus, L2 = vault, L3 = doors) organize the space not by manual tagging, but by proximity to founding atoms. An atom is in the "loss" door because it sits near Eva, Pierre, and Geoffrey — not because someone tagged it.

---

## 7.3 Temporal meaning

A fact is not a fixed point. "The kill switch is at €140k" in June is one fact. "The kill switch is at €220k" in July is another. Without timestamps, the system would average them into one wrong fact. With timestamps, it **tells a story**.

The temporal dimension prevents:
- **Concept averaging:** Two different states merged into one lying average
- **False recency:** Old facts weighting equally with new ones
- **Dead concepts:** Unused atoms taking space without being flagged

---

## 7.4 The delta

The core insight of UB1K isn't the atoms themselves — it's the **distance between them**. The delta between what was and what is. Between the old fact and the new one. Between L1 (the moment lived) and L2 (the moment stored).

L1 is the present. L2 is the past. The delta is the time it takes for an experience to become a memory.
