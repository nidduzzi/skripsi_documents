# Introduction

## Background

- The goal of scientific computing
- Ubiquitousnes/importance of PDEs in modern scientific understanding
  - Refrigeration
  - Aerodynamics of vehicles (rockets, cars)
  - Structural integrity of infrastructure
  - Understanding of plate tectonics
- One system that affects many peoples lives is the weather system
  - This affects everyone to varying degrees
  - The kinds of things people do on a day to day basis
    - for example, rainfall during certain periods of the day will affect consumer patterns which in turn will affect businesses
  - Weather on a longer timescale is important to sectors such as solar energy, construction, and a very important industry which is agriculture
  - In terms of national security concerns, weather affects defense capabilities of the military
  - In the long term climate resiliency and sustainability strategies depend on climate projections
  - sea level rise will cause coastal areas to flood, this is especially concerning for a archipelago like Indonesia where many population centers lie in areas that will flood with a few meters of sea level rise

- However, desipite years of research, prediction of weather remains a challenge largely due to variety of systems present in the atmosphere
  - There are unknown quantities in addition to the already known physical laws
  - The massive differences in scale involved in the system adds another challenge because it means very fine grids is needed to compute the problem (explain grids before this)
  - 
<!-- - Another field that can reap benefits from solving PDEs is ultrasonic testing. This widely used in the construction and manufacturing industries as a quality assurance tool. It allows the user to view the internal structure of objects via the interactions between the ultrasonic wave and material
- This is critical to quality infrastructure and products
- The maintenance of said infrastructure also uses this tool to allow engineers and planners to know if critical damage has occured or if any minor maintenance needs to happen
-  -->
- Traditional methods of solving PDEs have several challenges:
  - the solvers intrinsically need the user to know the equations, meaning problems with unknown equations (such as in pure data problems, the unknown equations part may not be the umbrella term and infact may be just a subset of the umbrella term) are not able to be solved
  - The accuracy of some methods which are mesh-based are directly tied to the size of the mesh used
  - This is another layer of complication due to the different mesh requirements for different problems (our method also need different basis for different problems so this might not be a good point)
  - Another issue with these methods is the fact that as parameters change the solution needs to be recomputed entirely
- Data driven methods have also been used to solve partial differential equations:
  - a naive approach is function approximation of the solution from parameter and coordinates to solution (10.1109/72.712178)
  - this has the same issue with changing the parameters in traditional numerical solvers
  - Retraining may in fact be costlier than traditional numerical solvers recomputing the solution
  - Because of this issue, other approaches that avoid this limitation has also been proposed
  - These methods map input functions to output functions in their discretized form using various network architectures (CNN, FNN, GNN, Transformers, etc. *address these individually to extend the discussion*)
  - For example, some approaches map initial conditions to future state of the system
  - while others map parameter functions to solution functions
  - One disadvantage of these approaches is the fixed discretization of input and output functions
  - This limits the flexibility of the model since input functions need to be discretized the same way in spatial and temporal space
  - The fixed discretization of the output also means that interpolation may need to be used to approximate intermediate values between grid points
  - This may not always be ideal in certain situations (need example & citation)
- Some data driven approaches incorporate prior knowledge of the physics into the model, while there are many approaches to do this, on that has been popularized in recent years is the Physics informed Neural Network (PINN).
  - This method incorporates knowledge by exploiting the fact that derivatives of neural network outputs can be computed with relative ease using autograd.
  - The computed derivatives can then be used to compute the residuals of PDEs of the problem.
  - The total loss is then the difference with the truth in addition to the residual
- Operator learning is another approach that tries to find the mapping between functions instead of function values:
  - Deeponet is an approach based on the universal approximation theorem
    - The basic architecture consists of two networks where the first called the branch takes in the input function and outputs an embedding
    - The second network takes in coordinates to evaluate the output function at and outputs an embedding the same shape as the output of the first network
    - The two outputs are then combined through a dot product to compute the predicted value of the output function
    - This architecture allows the smooth evaluation and non uniform colocation points meaning it avoids the issues with fixed grids
  - Neural operators are a class of neural networks which takes a different approach where the network contains "blocks" that modifies inputs from the previous layer in a different space such as Fourier space in the case of Fourier Neural Operator (FNO) the output is a gridded
  - Spectral Neural Operators avoids the problem of fixed grids by mapping between function spaces using coeffecients orthogonal function series such as Fourier or Chebyshev
    - This avoids the issue of fixed grid outputs since the network only operates on the coefficients.
    - For sufficiently low number of modes, the cost is relatively low since the model does not need to compute through many grid points
    - The cost is minimized and offset to the preprocessing step where the discretized functions are transformed into coefficients of a finite series of orthogonal functions
    - This transformation process is relatively mature and has many efficient algorithms such as the fast fourier transform for the fourier series
  - A similar approach proposed by Du et al. termed neural spectral methods incorporates knowledge on the problem into the loss
    - The loss function incorporates a term that is the residual of the known PDE
    - This is simillar to PINNs with the difference being the residual is in terms of basis function coefficients instead of function values

- due to the cyclical nature of weather, analysis exploiting this periodicity (fourier analysis) has been used previously in analyzing weather data.
- in fact, one of ways of analysing weather is to look at long term trends and subtract them from observations. For example, accross multiple years seasons will tend to have the same temperatures. Subtracting this from daily observations allow researchers to see the deviation from expected temperatures.
- Give example like: for example, in Beijing, the temperature on the 3rd of October year over year averaged 16 degrees celcius. However, last year, it was 17 degrees celcius. This means a difference of 17-16=1 degrees. This difference is called the anomaly. The difference can be furter accounted for better if other trends such as within the same year is also incorporated (<https://doi.org/10.1155/2019/4164097>)
Limitations:
- continuous functions (discontinuity can mess up the predictions i.e. gibbs oscilation)
- Fourier basis (maybe Chebyshev if time allows)
- Python only with libraries such as Pytorch, Xarray, Numpy, Pandas for faster performance
- Dense data only, sparse data assimilation is done by some other approach such as 4D-var assimilation or PINNs (which may be practical once it can be trained faster)
Aims:
- novel use of SVMs
- interpretability: partial dependence plots, Shapely values (SHAP), Local Interpretable Model-agnostic Explanations (LIME)