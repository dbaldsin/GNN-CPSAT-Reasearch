# Bridging Structure and Search  
### Hybrid GNN–CP-SAT Optimization for University Course Timetabling

 **Paper:** *Bridging Structure and Search: Hybrid Neural–Symbolic Optimization for University Course Timetabling*  
 **Venue:** AAAI (Camera-Ready)  
 **Affiliation:** Carnegie Mellon University – Qatar

---

##  Abstract

University course timetabling is a large-scale combinatorial optimization problem involving thousands of variables and tightly coupled hard and soft constraints. Symbolic solvers such as CP-SAT guarantee feasibility but struggle with scalability, while neural approaches can learn structural patterns but fail to respect hard constraints.

This work introduces a **hybrid neural–symbolic framework** that integrates **Graph Neural Networks (GNNs)** with **Google OR-Tools CP-SAT**. The GNN learns structural priors from optimally solved subinstances and provides high-confidence scheduling hints that warm-start CP-SAT’s search. The resulting system achieves **consistent penalty reductions (up to 22.1%)**, faster convergence, and **100% feasibility** across real-world ITC 2019 instances—without modifying the underlying solver.

---

##  Contributions

- Propose a **general neural–symbolic optimization framework** for large-scale timetabling
- Train a GNN on **optimally solved subinstances** to learn structural scheduling patterns
- Introduce a **confidence-based hint injection mechanism** compatible with CP-SAT
- Demonstrate **significant penalty reduction and runtime improvement** on ITC 2019 benchmarks
- Show strong **generalization** from a single training instance to unseen instances

---

##  Method Overview

### Problem Domain
- International Timetabling Competition (ITC) 2019
- Thousands of classes, rooms, and time slots
- Hard constraints (must be satisfied)
- Soft constraints (penalty minimization)

---

### Hybrid Architecture

1. **CP-SAT Baseline**
   - Guarantees feasibility
   - Serves as symbolic optimizer

2. **Graph Neural Network**
   - Encodes timetabling structure as a heterogeneous graph
   - Predicts room–time assignments per class

3. **Hinting Mechanism**
   - Convert GNN logits into confidence scores
   - Select top-confidence assignments (≈20%)
   - Inject as hints using `AddHint` in CP-SAT

4. **Final Optimization**
   - CP-SAT completes schedule with hard constraints enforced

This design preserves solver guarantees while leveraging learned structural knowledge.

---

##  Experimental Results

### Main Instance (`pu-d9-fal19-late`)

| Model | Feasible | Penalty | Runtime (s) |
|-----|---------|--------|-------------|
| CP-SAT | ✅ | 196,026 | 3,182 |
| **Hybrid (GNN + CP-SAT)** | ✅ | **162,796** | **3,181** |

**Penalty Reduction:** 16.95%  
**Feasibility:** 100%

---

### Generalization Performance

- Up to **22.1% penalty reduction** on unseen instances
- Up to **21.2% runtime improvement**
- No observed degradation on any benchmark
- Trained on a **single instance**, evaluated across many

---

##  Implementation

- **Language:** Python  
- **Symbolic Solver:** Google OR-Tools (CP-SAT)  
- **Neural Model:** GATv2-based Graph Neural Network  
- **Frameworks:** PyTorch, PyTorch Geometric  
- **Datasets:** ITC 2019 University Timetabling



