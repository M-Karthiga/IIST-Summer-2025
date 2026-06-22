# Dynamics of Forced Particles
**Summer Research Internship · Department of Mathematics, IIST Thiruvananthapuram**  
*Karthiga M (IS00611) · Supervised by Dr. C. V. Anil Kumar*

---

## Overview

This repository contains the full implementation and analysis from a summer research project investigating the **rotational orientation dynamics of spheroidal particles** suspended in oscillating creeping shear flows. The work bridges nonlinear dynamical systems theory with computational fluid mechanics, applying both classical numerical integration and the **Harmonic Balance Method (HBM)** to characterise periodic, quasi-periodic, and chaotic regimes.

The governing equations are derived from Brenner's torque model and extend Jeffery's classical orbit theory to include an external time-periodic torque — representative of magnetic or electric forcing on a dipolar particle.

---

## Research Highlights

- **Reproduced and extended** the results of *"Dynamics of a driven spheroid in a slow oscillating creeping shear flow"* (Kumar et al.)
- Identified that **strong oscillatory shear suppresses chaos** and promotes regular dynamics — a counterintuitive finding with implications for suspension engineering
- Demonstrated that **particle shape (aspect ratio)** combined with **flow frequency and amplitude** can be tuned to achieve selective orientation dynamics, enabling **shape-based particle separation**
- Applied the **Harmonic Balance Method** to the nonlinear orientation ODEs and compared results with direct RK4 integration
- Characterised dynamics through **Poincaré sections**, **Lyapunov exponents**, **phase portraits**, and **3D trajectory attractors**

---

## Repository Structure

```
.
├── orientationODE.m              # Core ODE system (Cartesian & spherical coords)
├── simulateSpheroid.m            # RK4 simulation runner for prolate/oblate cases
├── run_HBM_cases.m               # Harmonic Balance Method implementation & solver
├── HBM_final.m                   # Final HBM driver with Newton-Raphson iteration
├── computePR.m                   # Poincaré section computation
├── Final_supplementary_report_phy_of_fluid.m   # Plot generation for all regimes
├── IIST_Final_Report.pdf         # Main project report (theory + analysis)
└── IIST_Supplementary_report.pdf # MATLAB simulation plots (RK4 + HBM)
```

---

## Physical Setup

A single spheroid of **aspect ratio** $r_e = a/b$ is suspended in a 1D oscillating shear flow:

$$\mathbf{V} = a\dot{\gamma}\, y \cos(\omega_1 t)\, \mathbf{e}_x$$

An external periodic torque (magnetic/electric forcing) acts on the particle:

$$\mathbf{L}_\text{ext} = \mathbf{k} \times \mathbf{u}\, \cos(\omega_2 t)$$

The orientation unit vector $\mathbf{u} = (u_1, u_2, u_3)$ evolves under coupled nonlinear ODEs derived from Brenner's torque model. The flow regime is **Stokes flow** ($Re \ll 1$), neglecting inertia and Brownian motion.

**Parameter ranges explored:**

| Parameter | Values |
|---|---|
| Aspect ratio $r_e$ | 0.2 – 2.0 (oblate to prolate) |
| Shear amplitude $\alpha$ | 0.1 (weak), 1.0 (strong) |
| Oscillation frequency $\omega_1$ | 0.0 (simple shear), 0.1 (slow oscillation) |
| External torque strength $k_2$ | 0 – 15 |

---

## Methods

### Runge-Kutta 4th Order (RK4)
Direct time integration with adaptive step-size control in MATLAB. Used to characterise full nonlinear dynamics including transients, chaos, and strange attractors.

### Harmonic Balance Method (HBM)
A frequency-domain approach that approximates periodic steady-state solutions by expressing all quantities as truncated Fourier series:

$$u_k(t) = \bar{u}_{k0} + \sum_{l=1}^{n} \left\{ \bar{u}^c_{kl} \cos(l\omega t) + \bar{u}^s_{kl} \sin(l\omega t) \right\}$$

Galerkin projection yields a system of nonlinear algebraic equations solved via **Newton-Raphson iteration**. Parameters used: $n = 15$ harmonics, 400 time samples, penalty parameter $\lambda = 100$ for the unit vector constraint.

---

## Key Findings

| Flow Regime | Prolate ($r_e = 1.6$) | Oblate ($r_e = 0.6$) |
|---|---|---|
| Simple shear (no oscillation) | Multiple chaotic windows | Mildly regular |
| Weak oscillating shear | Single continuous chaotic regime | Fully regularised |
| Strong oscillating shear | **Chaos suppressed** → periodic | Fully regularised |

- **Weak oscillations** act as an effective chaos-control mechanism
- **Oblate spheroids** are significantly more stable than prolate under oscillatory forcing
- HBM consistently converged to stable periodic orbits, consistent with the regularisation observed in RK4 simulations under oscillatory conditions
- Lyapunov exponents confirmed: dominant $\lambda_{\max} \leq 0$ under slow oscillatory shear across all tested aspect ratios

---

## Particle Separation Mechanism

The sensitivity of orientation dynamics to particle shape and flow parameters can be exploited for **shape-selective particle separation** in colloidal suspensions. By tuning $\alpha$, $\omega_1$, and $k_2$, one can selectively destabilise particles of a specific aspect ratio while leaving others in regular orbits — allowing isolation of prolate or oblate populations from a mixed suspension.

---

## Dependencies

- MATLAB R2020a or later
- No external toolboxes required (uses built-in `ode45`, `fft`, `lsqnonlin`)

---

## Background & References

1. *Dynamics of a driven spheroid in a slow oscillating creeping shear flow* — primary reference paper
2. G. B. Jeffery, "The motion of ellipsoidal particles immersed in a viscous fluid," *Proc. R. Soc. London A*, 102(715):161–179, 1922
3. S. H. Strogatz, *Nonlinear Dynamics and Chaos*, Westview Press
4. H. Brenner, torque model for spheroidal particles in linear viscous flow

---

## Reports

| Document | Description |
|---|---|
| [`IIST_Final_Report.pdf`](./IIST_Final_Report.pdf) | Full theoretical derivation, methods, and analysis |
| [`IIST_Supplementary_report.pdf`](./IIST_Supplementary_report.pdf) | MATLAB simulation plots for all flow regimes (RK4 + HBM) |

---

## Author

**Karthiga M** · IS00611  
Department of Mathematics  
Indian Institute of Space Science and Technology, Thiruvananthapuram  

*Supervised by Dr. C. V. Anil Kumar (Mathematics, IIST) and Dr. Praveen Krishna (Aerospace Engineering, IIST)*
