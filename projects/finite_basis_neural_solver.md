# Neural Network-Based PDE Solution Representation Using Locally Supported Spline Basis Functions

## Introduction

The finite element method (FEM) is a widely used technique for approximating the solutions of partial differential equations (PDEs). It relies on local basis functions to represent the solution in a discrete domain. In this method, a function space \( \{\phi_i\} \) is defined, where the basis functions \( \phi_i \) are typically simple, locally supported functions that are non-zero in specific subdomains. This localized nature of the basis functions enhances the accuracy of the solution, particularly by enabling finer grid discretization.

The approximate solution can be written as:

$$ u(x) \approx \sum_{i} c_{i} \phi_{i}(x) $$

where \( c_i \) are the coefficients to be determined. Traditionally, these coefficients are obtained through calculus of variations techniques, which are particularly suitable for time-independent PDEs. The objective of this work is to explore whether a neural network can be trained to learn these coefficients \( c_i \), given a pre-defined set of local basis functions \( \{\phi_i\} \).

This research is motivated by Lu Lu’s work on [POD-DeepONet](https://www.sciencedirect.com/science/article/pii/S0045782522001207), where POD basis functions were used to approximate solutions. Here, I hypothesize that utilizing locally supported basis functions, such as splines, may offer better performance due to their locality and flexibility.

## Methodology

The first step in this approach is to identify a set of locally supported basis functions. Splines are a natural choice for this purpose. These functions are zero-valued outside their neighboring grid points and non-zero at the center, as illustrated in the figure below:
<img src="https://github.com/user-attachments/assets/0672f421-a2b8-40d1-a47d-b1e04feb0c70" alt="Spline Function Representation" width="400" />

With some overlap between neighboring regions, the linear combination of a set of spline functions produces a continuous representation of the solution.

The coefficients corresponding to these splines are predicted by a neural network.
## Implementation and Testing

To test the proposed method, I applied it to a 2D Darcy flow problem, which models the flow of a fluid through a porous medium:

$$
-\nabla \cdot \left( k(x, y) \nabla p(x, y) \right) = f(x, y)
$$

Here,  $k(x, y)$ represents the permeability field, and $p(x, y)$ is the pressure field to be determined. The goal is to approximate the solution $p(x, y)$ using locally supported spline basis functions.

The 2D spline basis functions $\phi_{ij}(x, y)$ were constructed as the outer product of 1D splines:

$$ \phi_{ij}(x, y) = \phi_i(x) \cdot \phi_j(y) $$

Thus, the solution $p(x, y)$ is approximated as a linear combination of these basis functions:

$$ u(x, y) \approx \sum_{i,j} c_{ij} \phi_{ij}(x, y) $$

where $c_{ij}$ are the coefficients to be determined. The dataset for training the neural network was generated using random permeability fields $k(x, y)$, while the reference solutions were computed using a traditional finite difference method. A convolutional neural network (CNN) was used to map the permeability field $k(x, y)$ to the corresponding coefficients $c_{ij}$, minimizing the difference between the predicted and exact solutions at specific control points.

## Remarks

This project was under the guidiance of professor [Xiaoning Zheng](https://scholar.google.com/citations?user=rXW31d8AAAAJ&hl=en-US) carried out between March and April 2024. Although the approach shows potential, the implementation was not fully completed due to limited guidance from my professor, who was unavailable during critical stages of the project. Moreover, machine learning models often require extensive tuning, which I was unable to accomplish on my own. 

Upon further exploration, I discovered that the structure of this model resembles Kolmogorov-Arnold Networks (KAN). Both approaches utilize a linear combination of basis functions—in this case, spline functions—to approximate data, and they update the coefficients by minimizing a loss function. In this sense, the model I proposed can be viewed as a single-layer KAN with one output.
