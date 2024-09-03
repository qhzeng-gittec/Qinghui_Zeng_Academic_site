# Hybrid Time-Marching With Neural Network Approach for Solving Nonlinear PDEs 
![cilinderfolow](https://github.com/user-attachments/assets/bb4551ae-25c8-45bc-946f-128cd005efa8)

## Background

Most physical phenomena develop over time, and the state at the next time step (viewed from a discrete aspect) is determined by its current state and the effect of neighboring states. This is why almost all physical phenomena can be described by partial differential equations.

In traditional numerical methods, complex nonlinear neighboring effects (nonlinear terms in PDEs) can be approximated by finite differences, so the discrete points satisfy an ODE. This approach aligns well with physical principles.

However, many classical data-driven methods do not explicitly incorporate temporal advancement (like DeepONet or FNO), which can lead to instability and confusion in the solutions. My goal is to develop a method that combines the universal approximation capabilities of data-driven approaches with physically meaningful time-marching methods.

## Methods

Let's start by noticing the connection between CNN (convolutional neural network) and finite difference.

Consider a 1D signal sampled from a function, with a spatially discrete step size $h$. Let's denote it as $f = [u_1, u_2, \dots, u_n]$. Assume a trained CNN kernel is like $[1/h, -2/h, 1/h]$. It happens that if the data $f$ is convolved by this kernel, the result is the central difference scheme for the second derivative. Following this idea, I found that a multi-channel CNN is capable of discretizing complex PDEs. For example, the momentum equation of the Navier-Stokes equations is 

$$  \frac{\partial \mathbf{u}}{\partial t} = -\frac{1}{\rho} \nabla p + \nu \nabla^2 \mathbf{u} - (\mathbf{u} \cdot \nabla) \mathbf{u} $$

It involves zero, first, and second-order derivatives, and they form a nonlinear term. To approximate the operator on the right-hand side, one can set the CNN (without a nonlinear activation function) to have three channels, each channel's kernel acting as a different order of gradient operator. After a 2D vorticity field (scalar field) is passed through it, the output would have three channels representing the derivatives of the vorticity at each sampled point. Then, accompanied by spatial and time data, we can approximate the RHS operator by a simple feedforward neural network, no matter how complex the nonlinear part is. Now, the equation can be written as $\frac{du}{dt} = f(u,\theta)$, where $f( ,\theta)$ represents the trained neural network with paramter $\theta$. This ODE can be solved by a simple numerical ODE solver like the Euler method (higher-order methods may not be stable during training) to obtain the solution at different time steps.

To sum up, this algorithm's structure is quite simple:

### CNN Processing
The initial solution of the PDE, just like a 1-channel image, is passed to a multi-kernel CNN layer without a nonlinear activation function.

### Incorporating Spatial and Time Encoding
An array of position encoding is concatenated to the CNN output, forming a few more channels. 

### Nonlinear Function Representation
A layer of a feedforward network is applied to each "pixel," aggregating operator output by different CNN kernels. This layer represents the nonlinear function on the right-hand side of the PDE.

### Time Advancement

## Implementation and Testing

To validate my method, I used it to solve the incompressible 2D Navier-Stokes (NS) equations, with a viscosity coefficient \( \nu = 1e-3\) as shown above, and a zero boundary condition. The reference solution is solved numerically using the finite difference method. This is also where the training data comes from, but it is coarser. The solution is calculated at multiple time steps for each initial condition, and the loss is the MSE error between the predicted solution and the reference one at different time steps. Compared to the reference solution, the predicted solution usually has a 7~8% error, indicating that more detailed diagnostics need to be done, as the best result achieved for neural operator solvers on this dataset is below 1%.

## Future Work
I have come up with a few more ideas to improve the accuracy of this method. The first one is better treatment of boundary conditions. In the above test case, the boundary condition is imposed simply by data points, but actually, I can update only the inner points while fixing the boundary unchanged.

Another possible improvement is using previous \(n\) time steps' solutions as initial values instead of just one. This way, each solution is derived based on the previous \(n\) steps, which is called a multiple-step method in finite difference.

### Some Other Remarks
This project was developed in April 2024, under the guidance of Professor Xiaoning Zheng. Although this method seems promising, I was not able to further refine it for multiple reasons. On the one hand, for an undergraduate project, it is really hard to outperform other machine learning algorithms. It requires abundant experience in machine learning and a higher level of knowledge. In addition, I am more interested in more theoretical work, and testing and refining codes might be a bit boring for me.
