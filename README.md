# American Option Pricing via Finite Difference Methods

This project implements and compares several finite difference schemes for pricing American put options under the Black–Scholes framework.

The American pricing problem leads to a parabolic variational inequality (obstacle problem). After spatial discretization, each time step reduces to solving a linear complementarity problem (LCP).

---

## Mathematical Problem

The price \( u(t,x) \) of an American option satisfies:

\[
\min(\partial_t u + Au + q(t), u - g) = 0
\]

where:

- \( A \) is the Black–Scholes spatial operator  
- \( g \) is the payoff function  
- the obstacle condition enforces early exercise  

After spatial discretization, the problem becomes:

\[
\min(Bx - b,\; x - g) = 0
\]

at each time step.

---

## Implemented Schemes

### Explicit Euler
- First-order time discretization  
- Baseline scheme  
- Used for convergence and stability analysis  

### Implicit Euler (IE)
- Reformulated as a linear complementarity problem  
- Solved using:
  - PSOR (Projected Successive Over-Relaxation)
  - Semi-Smooth Newton  

### Crank–Nicolson (CN)
- Second-order time discretization  
- Improved accuracy compared to implicit Euler  

### BDF (Backward Differentiation Formula)
- Second-order time scheme  
- Initialized with implicit Euler  
- Solved using Semi-Smooth Newton  

---

## Nonlinear Solvers

### PSOR
- Simple and robust  
- Iteration count increases with spatial refinement  
- Over-relaxation (\(\omega \in (1,2)\)) significantly reduces iterations  

### Semi-Smooth Newton
- Reformulates the LCP as:
  \[
  F(x) = \min(Bx - b,\; x - g)
  \]
- Fast local convergence  
- Efficient for fine grids  

---

## Numerical Analysis

The study includes:

- Convergence order estimation  
- Stabilization towards reference value \( \bar{v} \)  
- Influence of spatial refinement  
- CPU time comparison  
- Behavior with smooth payoff \( \varphi_1 \)  
- Behavior with discontinuous payoff \( \varphi_2 \)  

Main observations:

- Explicit Euler is first-order accurate.   
- PSOR convergence deteriorates as the spatial grid is refined.  
- Over-relaxation significantly reduces iteration counts.  
- Newton-based approaches provide improved accuracy at comparable computational cost. 
