# Hybrid Time-Marching with Neural Network Approach for Solving Nonlinear PDEs 
![Cylinder Flow Simulation](https://github.com/user-attachments/assets/bb4551ae-25c8-45bc-946f-128cd005efa8)

<p><sub>This image is not a result of the research presented here.</sub></p>
## Introduction

Many physical phenomena evolve over time, where their future states depend on the current state and interactions with neighboring states. For example, the momentum equation in the Navier-Stokes (NS) equations is based on physical principles where the change in momentum within a small time period is related to momentum diffusion and external forces acting on the control volume. These phenomena are modeled through various orders of spatial derivatives and their nonlinear combinations.

Traditional numerical methods, such as explicit finite difference methods, require constructing complicated matrices, while forward evolution is performed using methods like Euler's method.

Data-driven approaches, such as DeepONet and Fourier Neural Operators (FNO), often fail to explicitly incorporate temporal evolution, which can lead to instability. This research aims to combine the universal approximation capabilities of neural networks with physically meaningful time-marching methods to address these limitations.

## Methodology

This approach leverages the connection between convolutional neural networks (CNNs) and finite difference methods. Consider a 1D signal sampled at discrete spatial points with step size $h$, denoted as $f = [u_1, u_2, \dots, u_n]$. A trained CNN kernel, such as $[1/h, -2/h, 1/h]$, when convolved with $f$, produces a central difference approximation for the second derivative. By learning spatial differential operators using CNNs with various kernels, we can approximate higher-order derivatives. 

After passing snapshots from previous time steps through the CNN, spatial derivatives of different orders at each grid point are computed. These derivative values, along with spatial and temporal information, are fed into a fully connected neural network to model their nonlinear interactions.

For example, the momentum equation from the Navier-Stokes equations is:

$$
\frac{\partial \mathbf{u}}{\partial t} = -\frac{1}{\rho} \nabla p + \nu \nabla^2 \mathbf{u} - (\mathbf{u} \cdot \nabla) \mathbf{u}
$$

This equation involves zero, first, and second-order derivatives, forming nonlinear terms. A 3-channel CNN without activation functions can approximate the identity mapping, derivatives $\nabla$, $\nabla^2$. For the velocity at the first element $\mathbf{u}_1$, the approximated derivative values $a = \nabla p$, $b = \nabla^2 \mathbf{u}_1$, and $c =  \nabla \mathbf{u}_1$ are calculated. These, along with $x,t$ (although actually the external field does not vary in space and time), are fed into a feedforward network that approximates the right-hand side of the NS equation:

$$- \frac{1}{\rho} a + \nu b - (\mathbf{u}_1 \cdot c)$$

### Key Steps in the Algorithm:

#### 1. CNN-based Spatial Derivative Computation
The initial solution of the PDE, similar to a one-channel image, is passed through a multi-channel CNN without activation functions. This maps the initial condition to a space spanned by spatial derivatives of different orders.

#### 2. Incorporation of Spatial and Temporal Information
Spatial encoding and temporal encoding (if external fields change with time and position) are concatenated to the CNN output, allowing the model to capture spatio-temporal dependencies.

#### 3. Nonlinear Right-hand Side Approximation
A feedforward network is applied channel-wise at each spatial grid point, aggregating derivatives of different orders and spatio-temporal information to approximate the nonlinear terms in the PDE.

#### 4. Temporal Advancement
Once the right-hand side is computed, time-stepping methods, such as Euler's method, are used to evolve the solution to the next time step.

## Numerical Example

The proposed approach was implemented to solve the incompressible 2D Navier-Stokes equations, with a viscosity coefficient $\nu = 1 \times 10^{-3}$ and zero boundary conditions. The reference solution was obtained using a finite difference method, serving as both the training and comparison data. The model was trained on coarser grids, and the solution was computed for multiple time steps for each initial condition.

The loss function during training was the mean squared error (MSE) between the predicted and reference solutions at different time steps. The predicted solution exhibited a 7-8% error relative to the reference solution. Further improvements are needed, as the best results for neural operator solvers on this dataset have achieved less than 1% error.

## Future Work

Improvements could include using solutions from the previous $n$ time steps as initial values, rather than just one, similar to multi-step methods in finite difference schemes. This could enhance both accuracy and stability. Another improvement would be incorporating conservation laws for the whole system, ensuring that the flux sums to zero across all computational cells. This constraint could be added to the loss function during training.

### Remarks

This project was developed in April 2024, under the guidance of Professor [Xiaoning Zheng](https://scholar.google.com/citations?user=rXW31d8AAAAJ&hl=zh-CN). While the method shows promise, further refinements were limited by several factors. As an undergraduate project, competing with state-of-the-art machine learning algorithms is challenging and requires extensive experience. Moreover, my interests lie more in theoretical research, making the process of testing and refining codes somewhat less appealing.
