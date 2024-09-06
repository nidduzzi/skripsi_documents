# Methods

## Research Design

1. Problem Specification
    1. General statement of different goals
    2. Specific examples of input and outputs
        1. Forward Problems
            1. Initial condition (IC) problem
            2. IC and additional parameters
        2. Inverse Problems
            1. Parameter discovery
            2. Initial condition discovery
2. Literature Review
    1. PDE problems
        1. Traditional methods
        2. Machine learning methods
            1. function approximation
            2. Operator Learning
            3. Spectral space learning
    2. LSSVR
        1. Derivation
        2. KKT
        3. Uses
    3. Spectral computations
        1. spectral method
        2. operations in spectral space
        3. Weather Forecasting
            1. Traditional methods
                1. Computational requirements
                2. Unknown physics already using statistical models
            2. Machine learning methods
3. Computational Model Design
4. Implementation
5. Experimental Scenarios
    1. Proof of concept using simple ODE (antiderivative)
    2. Forward problem of predicting temperature field from parameters like forcing term or material properties
    3. Initial value problem of diffusion-reaction PDE with source term
    4. Partially known physics like weather forecasting using WeatherBench2 dataset
    5. Inverse problem of optimal control of the heat equation (arxiv 2110.13297)
    6. Hyperparameter search
        1. Best kernel.
        2. Kernel parameters.
        3. Regularization constant.
    7. Ablation studies
        1. Number of basis for different kinds of inputs and outputs
        2. Multiple single least squares regression
        3. Same mode regression
        4. Shared kernel matrix
        5. nu-SVR, epsilon-SVR
6. Data generation/retrieval & preprocessing
7. Experiments
8. Analysis
9. Conclusion

## Autoregression with SVR

1. train from all data u & predict second earliest training data u^\*\_1 from earliest training data u_0
2. add new training data with third earliest u_2 training data as label for prediction of second earliest training data u^\*\_1
3. redo from step one but shift by one timestep
