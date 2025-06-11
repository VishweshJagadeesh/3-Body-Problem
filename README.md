# The 3 Body Problem
### 1. Introduction
The 3-body problem is a classical problem in celestial mechanics that describes the motion of three massive bodies interacting with each other under the influence of gravity. This problem has significant applications in understanding the orbits of planets, moons, and artificial satellites.

The goal is to predict the future **positions and velocities** of the three bodies given their initial states.

### 2. Assumptions and Simplifications
* **Isolated System**: The system consists only of the two interacting bodies, with no external forces acting on them.
* **Point Masses**: The bodies are treated as point masses, having all their mass concentrated at a single point.
* **Newtonian Gravity**: The force between the two bodies is described by Newton's law of universal gravitation.

### 3. Mathematical formulation
A planet is presented as a particle that has a position $\vec{p}$. $F_{p_i \ / \ p_j}$ is the gravitational force that $p_i$ is exerting on $p_j$

$$ \vec{F}_{p_i \ / \ p_j} = G \frac{m_i \ m_j}{|\vec{p}_i - \vec{p}_j|^3} \left(\vec{p}_i - \vec{p}_j \right) $$

Here $\vec{p} = [p_x, p_y, p_z]$ contains the coordinates of the planet.

By using Newton's second law of motion on each planet:

* On planet 1 ($\vec{p}_1$):
$$ m_1 \frac{d^2 \vec{p}_1}{dt^2} = G \left(\frac{m_3 \ m_1}{|\vec{p}_3 - \vec{p}_1|^3} \left(\vec{p}_3 - \vec{p}_1 \right)  +   \frac{m_2 \ m_1}{|\vec{p}_2 - \vec{p}_1|^3} \left(\vec{p} _2 - \vec{p}_1 \right) \right)$$

resulting in:

$$\boxed{ \frac{d^2 \vec{p}_1}{dt^2} = G m_3 \frac{\vec{p}_3 - \vec{p}_1}{|\vec{p}_3 - \vec{p}_1|^3} +  G m_2 \frac{\vec{p}_2 - \vec{p}_1}{|\vec{p}_2 - \vec{p}_1|^3} } $$

The work is repeated for the remaining planets ($\vec{p}_2$ and $\vec{p}_3$), finally obtaining the system of odinary differential equations ODE's:


$$
\boxed{
\begin{array}{c}
\displaystyle \frac{d^2 \vec{p}_1}{dt^2} = G m_3 \frac{\vec{p}_3 - \vec{p}_1}{|\vec{p}_3 - \vec{p}_1|^3} +  G m_2 \frac{\vec{p}_2 - \vec{p}_1}{|\vec{p}_2 - \vec{p}_1|^3} \\[0.2cm]
\displaystyle \frac{d^2 \vec{p}_2}{dt^2} = G m_3 \frac{\vec{p}_3 - \vec{p}_2}{|\vec{p}_3 - \vec{p}_2|^3} +  G m_1 \frac{\vec{p}_1 - \vec{p}_2}{|\vec{p}_2 - \vec{p}_2|^3}\\[0.2cm]
\displaystyle \frac{d^2 \vec{p}_3}{dt^2} = G m_1 \frac{\vec{p}_1 - \vec{p}_3}{|\vec{p}_1 - \vec{p}_3|^3} +  G m_2 \frac{\vec{p}_2 - \vec{p}_3}{|\vec{p}_2 - \vec{p}_3|^3}
\end{array}
} 
$$


### 4. Packaging our problem for Python
#### Dimensionless version
We might need to rescale our problem to simplify and allowing more stability. This by defining new variables:

- $\vec{p'} = \vec{p}/L$
- $m' = m/M$
- $t' = t \sqrt{GM/L^3}$

Were $\vec{p'}$, $m'$ and $t'$ are dimensionless variables, and $L$ and $M$ are reference values.


By replacing the rescaled variables we obtain the following equation:

$$
\displaystyle \frac{d^2 (L \vec{p'}_1)}{d(\frac{t'}{\sqrt{GM/L^3}})^2} = G m_3 \frac{L(\vec{p'}_3 - \vec{p'}_1)}{|L(\vec{p'}_3 - \vec{p'}_1)|^3} +  G m_2 \frac{L(\vec{p'}_2 - \vec{p'}_1)}{|L(\vec{p'}_2 - \vec{p'}_1)|^3}
$$

Leading to:

$$\displaystyle \frac{L \ GM}{L^3}\frac{d^2 \vec{p'}_1}{dt'^2} = G m_3 \frac{L}{L^3} \frac{\vec{p'}_3 - \vec{p'}_1}{|\vec{p'}_3 - \vec{p'}_1|^3} +  G m_2 \frac{L}{L^3} \frac{\vec{p'}_2 - \vec{p'}_1}{|\vec{p'}_2 - \vec{p'}_1|^3}$$

After simplifying:

$$
\boxed{
\displaystyle \frac{d^2 \vec{p'}_1}{dt'^2} = \frac{m_3}{M} \frac{\vec{p'}_3 - \vec{p'}_1}{|\vec{p'}_3 - \vec{p'}_1|^3} + \frac{m_2}{M}  \frac{\vec{p'}_2 - \vec{p'}_1}{|\vec{p'}_2 - \vec{p'}_1|^3}
}
$$

Finally we obtain the rescaled system of ODE:

$$
\boxed{
\begin{array}{c}
\displaystyle \frac{d^2 \vec{p'}_1}{dt'^2} = m_3' \frac{\vec{p'}_3 - \vec{p'}_1}{|\vec{p'}_3 - \vec{p'}_1|^3} + m_2'  \frac{\vec{p'}_2 - \vec{p'}_1}{|\vec{p'}_2 - \vec{p'}_1|^3} \\[0.2cm]
\displaystyle \frac{d^2 \vec{p'}_2}{dt'^2} = m_3' \frac{\vec{p'}_3 - \vec{p'}_2}{|\vec{p'}_3 - \vec{p'}_2|^3} + m_1'  \frac{\vec{p'}_1 - \vec{p'}_2}{|\vec{p'}_1 - \vec{p'}_2|^3}\\[0.2cm]
\displaystyle \frac{d^2 \vec{p'}_3}{dt'^2} = m_1' \frac{\vec{p'}_1 - \vec{p'}_3}{|\vec{p'}_1 - \vec{p'}_3|^3} + m_2'  \frac{\vec{p'}_2 - \vec{p'}_3}{|\vec{p'}_2 - \vec{p'}_3|^3}
\end{array}
} 
$$


#### Transforming into a system of first ODE's

By defining new functions $\vec{f}_1$, $\vec{f}_2$ and $\vec{f}_3$ defined by:

$$ \vec{f}_1 = \frac{d \vec{p'}_1}{dt} $$
$$ \vec{f}_2 = \frac{d \vec{p'}_2}{dt} $$
$$ \vec{f}_3 = \frac{d \vec{p'}_3}{dt} $$


The system of first order ODE is obtained:
$$
\boxed{
\begin{array}{l}
\vec{f}_1 & = & \displaystyle \frac{d \vec{p'}_1}{dt}\\
\vec{f}_2 & = & \displaystyle \frac{d \vec{p'}_2}{dt}\\
\vec{f}_3 & = & \displaystyle \frac{d \vec{p'}_3}{dt}\\
\displaystyle \frac{d \vec{f}_1}{dt} & = & \displaystyle m_3' \frac{\vec{p'}_3 - \vec{p'}_1}{|\vec{p'}_3 - \vec{p'}_1|^3} +  m_2' \frac{\vec{p'}_2 - \vec{p'}_1}{|\vec{p'}_2 - \vec{p'}_1|^3} \\[0.2cm]
\displaystyle \frac{d \vec{f}_2}{dt} & = & \displaystyle m_3' \frac{\vec{p'}_3 - \vec{p'}_2}{|\vec{p'}_3 - \vec{p'}_2|^3} +  m_1' \frac{\vec{p'}_1 - \vec{p'}_2}{|\vec{p'}_2 - \vec{p'}_2|^3}\\[0.2cm]
\displaystyle \frac{d \vec{f}_3}{dt} & = & \displaystyle m_1' \frac{\vec{p'}_1 - \vec{p'}_3}{|\vec{p'}_1 - \vec{p'}_3|^3} +  m_2' \frac{\vec{p'}_2 - \vec{p'}_3}{|\vec{p'}_2 - \vec{p'}_3|^3}
\end{array}
} 
$$

We are looking to solve for $\vec{p'}_1$, $\vec{p'}_2$ and $\vec{p'}_3$. Where at $t' = 0$, we have informations about the initial position and velocities of the planets (Initial Conditions | IVP):

* $\displaystyle \vec{p'}_{i_{t'=0}} = \vec{p'}_{i_{0}} = \left[p'_{_i{x_0}}, p'_{_i{y_0}}, p'_{_i{z_0}} \right]$
* $\displaystyle \vec{v'}_{i_{t'=0}} = \vec{v'}_{i_{0}} = \left[v'_{_i{x_0}}, v'_{_i{y_0}}, v'_{_i{z_0}} \right]$
* $\vec{p'}_i$ position vector, $\vec{v'}_i$ velocity vector for $i=1, 2, 3$ (3 here representing the number of planets interacting with each other.

