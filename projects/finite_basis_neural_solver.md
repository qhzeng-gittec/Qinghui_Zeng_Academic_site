# Neural Network-Based PDE Solution Representation Using Locally Supported Spline Basis Functions
## Introduction

The finite element method (FEM) approximates solutions to partial differential equations (PDEs) using local basis functions. These basis functions $\{\phi_i\}$ are typically simple, locally supported functions that are non-zero within specific subdomains, enhancing the accuracy of the solution. The approximate solution is expressed as:

$$
u(x) \approx \sum_{i} c_{i} \phi_{i}(x)
$$

where $c_i$ are coefficients determined using calculus of variations. This research investigates whether a neural network can learn these coefficients $c_i$ from a predefined set of local basis functions $\{\phi_i\}$.

Inspired by Lu Lu's work on [POD-DeepONet](https://www.sciencedirect.com/science/article/pii/S0045782522001207), which used POD basis functions and CNNs to approximate solution coefficients, this study explores the use of locally supported splines for improved performance due to their locality and flexibility.

## Methodology

The first step is to select locally supported basis functions. Splines are ideal because they are non-zero only within a localized region, as shown below:

<img src="https://github.com/user-attachments/assets/0672f421-a2b8-40d1-a47d-b1e04feb0c70" alt="Spline Function Representation" width="400" />

By overlapping neighboring splines, a continuous solution is obtained. The coefficients corresponding to these splines are predicted by a neural network.

## Implementation and Testing

To test the approach, the method was applied to a 2D Darcy flow problem, which models fluid flow through a porous medium:

$$
-\nabla \cdot \left( k(x, y) \nabla p(x, y) \right) = f(x, y)
$$

Here, $k(x, y)$ represents the permeability field, and $p(x, y)$ is the pressure field to be determined. The goal is to approximate $p(x, y)$ using locally supported spline basis functions.

The 2D spline basis functions $\phi_{ij}(x, y)$ are constructed as the outer product of 1D splines:

$$
\phi_{ij}(x, y) = \phi_i(x) \cdot \phi_j(y)
$$

Thus, the solution $p(x, y)$ is approximated as:

$$
p(x, y) \approx \sum_{i,j} c_{ij} \phi_{ij}(x, y)
$$

where $c_{ij}$ are the coefficients to be learned. The dataset for training the neural network was generated using random permeability fields $k(x, y)$, while the reference solutions were computed using a finite difference method. A convolutional neural network (CNN) was used to map $k(x, y)$ to the coefficients $c_{ij}$, minimizing the error between predicted and exact solutions at control points.


## Remarks

This project was under the guidiance of professor [Xiaoning Zheng](https://scholar.google.com/citations?user=rXW31d8AAAAJ&hl=en-US) carried out between March and April 2024. Although the approach shows potential, the implementation was not fully completed due to limited guidance from my professor, who was unavailable during critical stages of the project. Moreover, machine learning models often require extensive tuning, which I was unable to accomplish on my own. 

Upon further exploration, I discovered that the structure of this model resembles Kolmogorov-Arnold Networks (KAN). Both approaches utilize a linear combination of basis functions—in this case, spline functions—to approximate data, and they update the coefficients by minimizing a loss function. In this sense, the model I proposed can be viewed as a single-layer KAN with one output.
