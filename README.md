# The 3 Body Problem

### 1. Introduction

The 3-body problem is a classical problem in celestial mechanics that describes the motion of three massive bodies interacting with each other under the influence of gravity. This problem has significant applications in understanding the orbits of planets, moons, and artificial satellites.

The goal is to predict the future **positions and velocities** of the three bodies given their initial states.

### 2. Assumptions and Simplifications

* **Isolated System**: The system consists only of the three interacting bodies, with no external forces acting on them.
* **Point Masses**: The bodies are treated as point masses, having all their mass concentrated at a single point.
* **Newtonian Gravity**: The force between the bodies is described by Newton's law of universal gravitation.

### 3. Mathematical Formulation

A planet is presented as a particle that has a position **p**. The gravitational force that body *i* exerts on body *j* is:

```
F_{i/j} = G * (m_i * m_j) / |p_i - p_j|^3 * (p_i - p_j)
```

Using Newton's second law on each body:

For planet 1:

```
d²p₁/dt² = G * m₃ * (p₃ - p₁) / |p₃ - p₁|³ + G * m₂ * (p₂ - p₁) / |p₂ - p₁|³
```

Similarly for the other two bodies:

```
d²p₂/dt² = G * m₃ * (p₃ - p₂) / |p₃ - p₂|³ + G * m₁ * (p₁ - p₂) / |p₁ - p₂|³

d²p₃/dt² = G * m₁ * (p₁ - p₃) / |p₁ - p₃|³ + G * m₂ * (p₂ - p₃) / |p₂ - p₃|³
```

### 4. Packaging Our Problem for Python

#### Dimensionless Version

To simplify and improve stability, we rescale using:

```
p' = p / L
t' = t * sqrt(G*M / L^3)
m' = m / M
```

After substituting and simplifying:

```
d²p'₁/dt'² = m'₃ * (p'₃ - p'₁) / |p'₃ - p'₁|³ + m'₂ * (p'₂ - p'₁) / |p'₂ - p'₁|³
```

And similarly for p'₂ and p'₃.

### 5. System of First Order ODEs

Define velocity vectors:

```
f₁ = dp'₁/dt'
f₂ = dp'₂/dt'
f₃ = dp'₃/dt'
```

Then the system becomes:

```
df₁/dt' = m'₃ * (p'₃ - p'₁) / |p'₃ - p'₁|³ + m'₂ * (p'₂ - p'₁) / |p'₂ - p'₁|³
df₂/dt' = m'₃ * (p'₃ - p'₂) / |p'₃ - p'₂|³ + m'₁ * (p'₁ - p'₂) / |p'₁ - p'₂|³
df₃/dt' = m'₁ * (p'₁ - p'₃) / |p'₁ - p'₃|³ + m'₂ * (p'₂ - p'₃) / |p'₂ - p'₃|³
```

### 6. Initial Conditions

At t' = 0, we define:

```
p'_{i0} = [x₀, y₀, z₀]
v'_{i0} = [vx₀, vy₀, vz₀]
```

Where `i = 1, 2, 3` for each body.

---

This Markdown file is now GitHub-compatible. For better visualization, you may link to a PDF or host a rendered version elsewhere.
