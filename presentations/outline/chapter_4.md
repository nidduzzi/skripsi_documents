# Results

## Computational Model

1. Data Preparation
    1. Data generation/retrieval
        - Manufactured solutions using randomly generated spectral coefficients. Input functions such as initial condition or parameters like material density distribution are computed analytically from the solution when possible or using finite differences otherwise (e.g. torch.gradient function).
        - Dataset retrieval using wget from archives like WeatherBench storage bucket or purpose-built packages like cds-api.
    2. Data specification
        - source: generated, assimilated observations (ERA5)
        - format: features, grid size, ranges
        - visualizations of the maps/code used to get the data.
2. Data transformation
    1. Windowing or other preprocessing to get input and output functions for the LSSVR
    2. Basis transform such as the Fourier transform of input and output functions to get basis coefficients of both functions
    3. Split data into train, test, & validation datasets.
    4. Fit scaler on training dataset input functions and scale every dataset input function with it
    5. Show some correlations or non correlations between different coefficients
3. Training
    1. LSSVR model is trained to predict output function coefficients from input function or its coefficients
    2. Complex inputs and outputs are split into their components and are processed as normal real valued inputs and outputs
    3. compute kernel matrix
    4. construct block matrices
    5. compute bias and Lagrangian coefficients
4. Evaluation
    1. Scale inputs using the same scaler fitted on the training data
    2. These scaled inputs are then used by the LSSVR to predict output function coefficients
        1. compute kernel matrix between support vectors and input functions to evaluate.
        2. Matrix multiply with Lagrangian basis and add bias to compute predicted output coeffecients
    3. The predicted coefficients are rearranged to complex form if needed and then used with the chosen basis to evaluate the approximated output function at desired coordinates
