# Neural Network-Based PDE Solution Representation Using Locally Supported Spline Basis Functions

## Background

The finite element method uses local basis functions to approximate the solution of a PDE. The method first defines a function space \( \{\phi_i\} \), where the basis functions are often simple functions that exist in separate subdomains. This approach increases the accuracy of the solution by allowing the choice of smaller grid sizes.

The solution is then assumed to be represented by this set of functions:

$$ u(x) \approx \sum_{i} c_{i} \phi_{i}(x) $$

The coefficients  $c_i$ are typically solved using calculus of variations methods, which are particularly suitable for time-independent PDEs. My goal is to explore whether a neural network can be trained to find these coefficients \( c_{i} \) when a set of basis functions \( \{\phi_i\} \) is given. The idea is straightforward.

This work was inspired by Lu Lu's POD-DeepONet, where the author uses POD basis functions. However, I believe that using local basis functions could yield better results.

## Methods

First, I needed to find a set of locally supported basis functions. These functions should be continuous and have a value of zero outside a certain region, with some overlap in their regions of support. This overlap allows for the construction of a continuous function when the basis functions are summed. 

One approach is to use spline functions. These are zero-valued at neighboring grids and non-zero at the center, as shown in the figure. The coefficients of these basis functions are then produced by a feedforward neural network.
![output](https://github.com/user-attachments/assets/0672f421-a2b8-40d1-a47d-b1e04feb0c70)

## Implementation and Testing

I tested this method on a 2D Darcy flow problem:

$$
-\nabla \cdot \left( k(x, y) \nabla p(x, y) \right) = f(x, y)
$$

This equation describes the flow of a fluid through a porous medium. The goal was to find the solution given the permeability field $k(x, y)$.

The 2D spline basis function $\phi_{ij}(x, y)$ is constructed as the outer product of two 1D spline functions:

$$ \phi_{ij}(x, y) = \phi_i(x) \cdot \phi_j(y) $$

The solution $u(x, y)$ of the PDE is then approximated as a linear combination of these spline basis functions:

$$ u(x, y) \approx \sum_{i,j} c_{ij} \phi_{ij}(x, y) $$

Here, $\phi_{ij}(x, y)$ are the spline basis functions, and $c_{ij}$ are the coefficients to be determined.

The training dataset was generated using a random function field, and the reference solution was obtained from a finite difference method. I used a CNN to map the permeability field $k(x, y)$ to the coefficients. The network was trained by minimizing the difference between the exact solution and the solution at control points.

### other notes
These works was constructed between March and April, 2024

Although the approach seems workable, I was unable to finish implementing it because the professor was too busy to offer further guidance, and I understand that machine learning requires numerous adjustments, which might not be accomplished on my own. It was really a pitty.

