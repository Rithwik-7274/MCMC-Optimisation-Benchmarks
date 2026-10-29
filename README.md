# MCMC Samplers & Stochastic Optimization Benchmarks

[Read the full paper](Report.pdf)

This repository contains from-scratch implementations of advanced Markov Chain Monte Carlo (MCMC) samplers and stochastic optimization algorithms.

This project focuses on the low-level algorithmic implementation, numerical stability, and performance benchmarking of computational statistics methods. The codebase explores how effectively these algorithms estimate parameters in Bayesian models and escape local optima in highly non-convex landscapes.

## 🧠 Core Algorithms Implemented

### 1. MCMC Samplers

* **Random Walk Metropolis-Hastings (RWMH):** A baseline MCMC sampler utilizing Gaussian proposal distributions with symmetric acceptance criteria.
* **Adaptive Rejection Metropolis Sampling (ARMS):** An advanced sampler that dynamically constructs a piecewise linear upper hull in log-space to bound the target density. It natively includes Gilks' (1995) Metropolis correction step to handle non-log-concave regions.

### 2. Stochastic Optimization

* **Simulated Annealing (SA):** A global optimization metaheuristic overlaid on both the RWMH and ARMS samplers.
* **Cooling Schedules:** Implemented both parameterized **Geometric** and **Logarithmic** cooling schedules.

## 🔬 Experiments & Benchmarks

The notebook applies the algorithms to several complex mathematical and statistical scenarios:

### 1. Bayesian Posterior Estimation (Real-World Modeling)

* **Poisson-Log-Normal Model:** Recovering a hidden rate parameter ($\theta$) given 50 observations drawn from a Poisson distribution. The unnormalized log-posterior (Log-Likelihood + Log-Prior) is used as the strict target density for both RWMH and ARMS.
* **Performance Metrics:** Evaluates both algorithms on Acceptance Rate, Effective Samples generated, and ESS per second.

### 2. Global Optimization on Non-Convex Landscapes

* **Inverted Rastrigin Function:** A highly non-convex landscape used to test the samplers' ability to escape massive numbers of local optima.
* **Inverted Ackley Function:** Features a nearly flat outer region with a sharp central peak.
* **Gaussian Mixture Models:** Target densities with varying weights, means, and standard deviations.
* **Grid Search:** A systematic evaluation of SA convergence speed across various geometric decay rates ($\eta$) and logarithmic constants ($c$).
* **Effective Sample Size (ESS):** Calculated using Fast Fourier Transforms (FFT) to efficiently compute the autocorrelation sequence and measure sampling efficiency.

## ⚙️ Engineering & Numerical Stability

Special attention was given to edge cases and hardware precision limits common in statistical computing:

* **Log-Sum-Exp Trick:** Implemented during exact analytical inverse transform sampling in the ARMS algorithm to prevent floating-point overflow on extreme slopes.
* **Continuous Jitter Integration:** Solves the grid-blindness problem in high-resolution hull sampling by allowing ARMS to hit microscopic SA peaks.
* **Execution Safeguards:** Infinite loop prevention during dynamic hull construction in deep distribution tails.
* **Type Hinting & Configurations:** Systems-level typing and central dataclass configurations for reproducible hyperparameter tuning.

## 📈 Visualizations

The notebook generates automated analytical plots, including:

* **Trace Plots & Autocorrelation Bar Charts:** For mixing and burn-in analysis.
* **2D Contour Trajectories:** Overlaying the MCMC sampling paths directly onto topological landscape maps.
* **Convergence Speed Graphs:** Plotting objective values across cooling epochs.
