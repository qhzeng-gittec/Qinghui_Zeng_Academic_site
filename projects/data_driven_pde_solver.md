# Backgrounds

Most physical phenomena develop over time, and the state at the next time step (viewed from a discrete aspect) is determined by its current state, as well as the effect of neighbors. This is why almost all physical phenomena can be described by partial differential equations.

In traditional numerical methods, complex nonlinear neighboring effects (nonlinear terms in PDEs) can be approximated by finite differences, so the discrete points satisfy an ODE. This approach aligns well with physical principles.

However, many classical data-driven methods do not explicitly incorporate temporal advancement (like DeepONet or FNO), which can lead to instability and confusion in the solutions. My goal is to develop a method that combines the universal approximation capabilities of data-driven approaches with the physically meaningful time-marching methods.

# Methods

Let's start by noticing the connection between CNN (convolutional neural network) and finite difference.

Consider a 1D signal sampled from a function, with a spatially discrete step size \(h\). Let's denote it as \(f = [u_1, u_2, \dots, u_n]\). Assume a trained CNN kernel is like \([1/h, -2/h, 1/h]\). It happens that if the data \(f\) is convolved by this kernel, the result is the central difference scheme for the second derivative.

### Initial Encoding
I began by encoding the initial solution of the PDE, along with spatial and temporal coordinates at each point, into a structure resembling a multi-channel image. This encoding provided a comprehensive representation of the problem space for the neural network.

### CNN Application
This encoded structure was passed through a CNN layer to simulate the required derivatives. The CNN was trained to approximate these derivatives, similar to how finite difference methods discretize them.

### Nonlinear Function Representation
The neural network was then utilized to represent the nonlinear function on the right-hand side of the PDE, allowing it to capture complex relationships between the variables.

### Time Advancement
I initially advanced the solution in time following classical finite difference methods. However, challenges in accuracy prompted further refinement.

# Methods and Tools

The dataset used is the same as in previous experiments involving the Navier-Stokes (NS) equations. In this approach, small convolutional neural network (CNN) kernels are trained to approximate derivatives, akin to the discretization in finite difference methods. The right-hand side of a PDE can generally be expressed as a function of various orders of derivatives, spatial coordinates \(x\), and time \(t\). Traditional finite difference methods derive a discretization scheme for the right-hand side of the PDE through analytical means. My approach, however, aims to automatically learn this discretization scheme from the data using neural networks. The time-stepping is then performed similarly to classical finite difference methods.

# Challenges and Refinements

### Challenge 1: Accuracy Issues
The initial approach, while computationally efficient, resulted in lower accuracy compared to other data-driven methods.

**Refinement:** To address this, I increased the number of parameters in the neural network, which helped improve accuracy but also led to longer training times.

### Challenge 2: Data Limitation
Even with increased parameters, the accuracy plateaued due to limited training data.

**Refinement:** I introduced additional training data, which further improved accuracy, but the increase was marginal. This led to the exploration of other techniques.

### Challenge 3: Temporal Prediction
The use of a single-step time advancement was insufficient for capturing the dynamics of the solution over time.

**Refinement:** I adopted a multi-step approach, where solutions from multiple previous time steps were used to predict the solution at time step \(n+1\). This significantly improved the temporal accuracy of the solution.

# Responsibilities

[Provide a detailed description of your specific role in this project. For example, were you responsible for designing the neural network architecture, conducting experiments, analyzing results, or writing the code?]

# Innovation and Contribution

I introduced a method of incorporating time advancement in neural network-based PDE solvers, which enhances the interpretability of the solution process. Leveraging the universal approximation theorem, the method can approximate any form of time-dependent PDE. Additionally, by selecting the CNN kernel size and the number of layers according to the order of derivatives in the PDE, the method efficiently utilizes known information about the equation.
