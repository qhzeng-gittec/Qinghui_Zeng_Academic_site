<img src="https://github.com/user-attachments/assets/a838e8f8-d0f0-4ce5-b84f-5b5e5cbafecd" alt="image" width="300" align="right">

I’m Qinghui Zeng, an undergraduate at [Jinan University](https://english.jnu.edu.cn/), majoring in Information and Computational Science, under math department. I will be graduated by the summer of 2025. and I am seeking graduate study opportunities in applied or computational mathematics.

For inquiries, you can reach me at [zengqh23@outlook.com](mailto:zengqh23@outlook.com).

## Academic Qualifications
My studies focus on both fundamental mathematical knowledge and its applications. I have completed several advanced courses:

| Course                     |
|----------------------------|
| Numerical Methods for Partial Differential Equations |
| Real Analysis               |
| General Physics             |
| Topology                    |
| Differential Geometry       |
| Ordinary Differential Equations |
| Optimization Methods        |


Additionally, I achieved an overall score of 7.0 in IELTS (Reading: 8.5, Listening: 7.5, Writing: 6.5, Speaking: 6.0) and a total score of 326 in the GRE General Test (Verbal: 156, Quantitative: 170).

## Research Interests
My research interest covers various areas of applied mathematic, including mathematical modeling of physical processes, analysis of PDEs arising from physics and engineering. and numerical methods for solving these equations.
The [SOP](https://github.com/qhzeng-gittec/Qinghui_Zeng_CV/blob/main/Statement%20of%20Purpose.md) describes how my interest has developed.  
## Projects Overview
I have worked on research projects in three main areas: wave and waveguide computation, data-driven fluid dynamics, and Machine Learning in Bioinformatics. Among these, my primary interest lies in using mathematical analysis and classical numerical methods to study and model physical phenomena, as demonstrated in my work on wave propagation and waveguide computations. These projects have honed my skills in coding, academic writing, and effectively communicating with professors to discuss and refine research ideas, better preparing me for future research endeavors.

---
## Wave and Waveguide Computation
These works are conducted under the guidance of Professor [Jianxin Zhu](https://faculty.jnu.edu.cn/xxkxjsxy/zjx2/list.htm).

### [Computation of Eigenmodes in 2-Layer Waveguide with a Curved Interface](https://drive.google.com/file/d/1-giY1xNVN1cCthW2_tEGN3MSqhV22StS/view?usp=drive_link)&nbsp;&nbsp;&nbsp;&nbsp;(2024.9 – )
The Helmholtz equation is commonly used to model wave propagation. In this work, we consider an open waveguide that is separated into two layers along the depth axis by a curved interface. Previous studies have utilized an orthogonal coordinate transformation, followed by an equation transformation to flatten the curved interface, then, a Perfectly Matched Layer (PML) is added to truncate the open domain for finite computational regions. However, the equation transformation results in a new partial differential equation with varying coefficients, complicating the analysis. Building on research that uses piecewise Kummer functions to approximate eigenfunctions, we adapted this method to the transformed Helmholtz equation and derived an iterative relation for the eigenmode. Additionally, we derived the approximated solution for this relation, which serves as an initial guess to numerically solve for the eigenvalues. Formulas were derived separately for the optical waveguide in the Transverse Electric (TE) and Transverse Magnetic (TM) cases. Numerical examples demonstrate that our asymptotic solutions converge well to the exact eigenvalue.

### [The DtN-Riccati Method for 3-D Helmholtz Equation](https://drive.google.com/file/d/1-64_bIOeH3vN1deOnDFdYVuF5J6dVYmc/view?usp=drive_link)&nbsp;&nbsp;&nbsp;&nbsp;(2024.5 – 2024.6)
An efficient approach for long-range computation of the Helmholtz equation in a waveguide is to reformulate it as the operator differential Riccati equation for the Dirichlet-to-Neumann (DtN) map. However, the original 1995 paper by Lu and McLaughlin that proposed this algorithm focused on 2D waveguides, whereas many real-world waveguides are inherently 3D.

In this work, I extend this algorithm to three-dimensional case, enabling it to handle more complex sources and waveguides. I derive the radiation condition specific to the 3D Helmholtz equation and developed a finite basis version of the algorithm by expanding matrices onto local basis functions at each step, significantly reducing memory usage and computational costs. Numerical examples and comparisons validate the accuracy of the proposed method across different waveguides.

---

## Data-Driven Fluid Dynamics
These works are supervised by Professor [Xiaoning Zheng](https://scholar.google.com/citations?user=rXW31d8AAAAJ&hl=zh-CN).

### [Hybrid Time-Marching with Neural Network Approach for Solving Nonlinear PDEs](https://github.com/qhzeng-gittec/helloitisqinghui/blob/main/projects/data_driven_pde_solver.md)&nbsp;&nbsp;&nbsp;&nbsp;(2023.11 – 2024.4)
This project explores a hybrid time-marching approach that integrates neural networks with traditional numerical methods to solve nonlinear partial differential equations (PDEs). By utilizing convolutional neural networks (CNNs) to approximate spatial derivative operators and incorporating time-marching schemes like Euler's method, the approach aims to combine data-driven techniques with physically meaningful temporal evolution.

### [Data-Driven PDE Solver of Finite Basis Representation](https://github.com/qhzeng-gittec/helloitisqinghui/blob/main/projects/finite_basis_neural_solver.md)&nbsp;&nbsp;&nbsp;&nbsp;(2023.11 – 2024.4)
This project draws inspiration from the finite element method (FEM) to develop a data-driven approach for solving PDEs. It represents the solutions of PDEs by a linear combination of locally supported spline basis functions, and a neural network is then trained to map the parameters of the PDE to the coefficients of these basis functions.

---

## Applications of Machine Learning in Bioinformatics
### [Seinformer: A Deep Learning Framework Combining EPInformer and Sei to Predict Gene Expression from DNA Sequence](https://github.com/JasonLinjc/Seinformer)&nbsp;&nbsp;&nbsp;&nbsp;(2024.4 – )
This project, in collaboration with [Dr. Jiecong Lin](https://www.linkedin.com/in/jiecong-lin-0665902a2), a postdoctoral researcher at Harvard Medical School, focused on improving the performance of EPInformer—a transformer-based machine learning model developed by Dr. Lin to predict gene expression levels using regulatory DNA fragments and the DNA sequences themselves. To enhance its accuracy, I integrated SEI, a CNN-based model specifically designed to extract gene features from DNA sequences, as a DNA sequence encoder within EPInformer. This integration led to a significant improvement in the model's predictive accuracy.
