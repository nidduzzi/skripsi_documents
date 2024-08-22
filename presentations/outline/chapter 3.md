Autoregression with SVR:
1. train from all data u & predict second earliest training data u^*_1 from earliest training data u_0
2. add new training data with third earliest u_2 training data as label for prediction of second earliest training data u^*_1
3. redo from step one but shift by one timestep