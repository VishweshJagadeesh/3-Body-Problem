# The 3 Body Problem

### Overview

This repository contains a Python implementation of the classical 3-body problem, a famous problem in celestial mechanics that models the motion of three massive bodies interacting under Newtonian gravity.

While the full mathematical formulation of the problem—including the derivation of the governing equations and dimensional analysis—can be quite detailed, all of that has been explained interactively in the accompanying Jupyter Notebook:

👉 **[main.ipynb](./main.ipynb)**

The notebook provides:

* A clear breakdown of the physical assumptions.
* Derivation of the second-order and first-order ODE systems.
* Visualization of the orbits.
* An explanation of the dimensionless formulation for improved numerical stability.

### Contents

* `main.ipynb`: Main notebook with math, theory, and code.
* `main.py` (if applicable): ODE solver implementation.
* `README.md`: Project overview and instructions.

### How to Run

1. Clone the repository:

   ```bash
   git clone [https://github.com/your-username/3-body-problem.git](https://github.com/VishweshJagadeesh/3-Body-Problem.git)
   cd 3-Body-Problem
   ```
2. Install the required packages:

   ```bash
   pip install -r requirements.txt
   ```
3. Open the notebook:

   ```bash
   jupyter notebook main.ipynb
   ```
