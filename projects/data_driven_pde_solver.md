# Hybrid Time-Marching with Neural Network Approach for Solving Nonlinear PDEs 
![Cylinder Flow Simulation](https://github.com/user-attachments/assets/bb4551ae-25c8-45bc-946f-128cd005efa8)

<p><sub>This image is not a result of the research presented here.</sub></p>

## Introduction

Many physical phenomena evolve over time, and their future states depend on the current state and interactions with neighboring states. These interactions can often be described by partial differential equations (PDEs). Traditional numerical methods approximate the nonlinear effects between neighboring states, which manifest as nonlinear terms in PDEs, through finite difference schemes, transforming the problem into a system of ordinary differential equations (ODEs). This approach aligns well with established physical principles.

However, classical data-driven approaches, such as deep operator networks(DeepONet) and Fourier Neural Operators (FNO), often fail to incorporate temporal evolution explicitly, which can lead to instability in the solutions. This research aims to combine the universal approximation capabilities of neural networks with physically meaningful time-marching methods to address these limitations.

## Methodology

This approach draws on the inherent connection between convolutional neural networks (CNNs) and finite difference methods. Consider a 1D signal sampled from a function at discrete spatial points with step size $h$, denoted as $f = [u_1, u_2, \dots, u_n]$. A trained CNN kernel, such as $[1/h, -2/h, 1/h] $, when convolved with $f$, produces the central difference approximation for the second derivative. Extending this idea, a multi-channel CNN can discretize PDEs by representing different spatial derivatives. 

For example, the momentum equation from the Navier-Stokes equations is:

$$
\frac{\partial \mathbf{u}}{\partial t} = -\frac{1}{\rho} \nabla p + \nu \nabla^2 \mathbf{u} - (\mathbf{u} \cdot \nabla) \mathbf{u}
$$

This equation involves zero, first, and second-order derivatives, forming nonlinear terms. To approximate these operators, a multi-channel CNN without activation functions can be employed. Each channel's kernel acts as a discrete gradient operator, extracting spatial derivatives from a scalar vorticity field. The spatial and temporal data is then processed by a feedforward neural network to approximate the nonlinear terms on the right-hand side of the PDE. The system of ODEs derived from the neural network can be solved using time integration methods such as Euler's method.

In summary, the key steps in the algorithm are:

### 1. CNN-based Spatial Derivative Computation
The initial solution of the PDE, similar to a one-channel image, is passed through a multi-channel CNN without activation functions. This maps the initial condition to a space spanned by the spatial derivatives of different orders.

### 2. Incorporation of Spatial and Temporal Information
Spatial encoding and temporal encoding (if applicable) are concatenated to the CNN output, allowing for the incorporation of spatio-temporal dependencies.

### 3. Nonlinear Right-hand Side Approximation
A feedforward network is applied channel-wise at each spatial grid point, aggregating derivatives of different orders along with spatio-temporal information. This step approximates the nonlinear right-hand side of the PDE.

### 4. Temporal Advancement
Once the right-hand side has been computed, time advancement methods such as Euler's method are employed to evolve the solution to the next time step.

## Numerical Example

To evaluate the proposed approach, the algorithm was implemented to solve the incompressible 2D Navier-Stokes equations, with a viscosity coefficient $\nu = 1 \times 10^{-3}$ and zero boundary conditions. The reference solution was obtained using a finite difference method, serving as both the training and comparison data. The model was trained on coarser grids, with the solution computed for multiple time steps for each initial condition.

The loss function used during training was the mean squared error (MSE) between the predicted and reference solutions at different time steps. While the predicted solution exhibited a 7-8% error relative to the reference solution, more detailed analysis is needed, as the best results for neural operator solvers on this dataset have achieved less than 1% error.

## Future Work

A possible improvement to this method would involve using solutions from the previous $n$ time steps as initial values, rather than just one. This approach, analogous to multi-step methods in finite difference schemes, could improve the accuracy and stability of the method.

### Remarks

This project was developed in April 2024, under the guidance of Professor [Xiaoning Zheng](https://scholar.google.com/citations?user=rXW31d8AAAAJ&hl=zh-CN). While the method shows promise, further refinements were limited by several factors. As an undergraduate project, competing with state-of-the-art machine learning algorithms is challenging and requires extensive experience. Moreover, my interests lie more in theoretical research, making the process of testing and refining codes somewhat less appealing.
