# Tronstad2019
caller.m - Script running simulations on fnn, lstm and stacked lstm regression with different cases  
fnn_regression_fnc.m - Function for testing fnn regression on simulated data with given conditions  
lstm_regression_fnc.m - Function for testing 1-layer lstm regression on simulated data with given conditions  
lstm_stacked_regression_fnc.m - Function for testing 2-layer lstm regression on simulated data with given conditions 
sim_gen_Z - Function for generating simulated impedance spectra from ischemic liver  

Requires Matlab2018a and the Neural Network Toolbox

Example:

%Simulation settings:  
spred=5;               %Liver-to-liver variation  
noise_power=10;        %Level of white gaussian noise (dBW) in the simulated measurement  
drift=100;             %Sets drift in Ohms per hour  
drift_direction=1;     %Sets direction of drift (0 is both directions, 1 is increasing impedance, -1 is decreasing impedance)  
hyppighet=10; 	       %Time (in minutes) between each simulated measurement point  

%Input data settings:  
N=100;                 %Number of livers in the training and test set  
w=10.^(1:7);           %Resistance and reactance at seven frequencies as input  

%Neural network training settings  
epochs=500;            %Epochs for training of the LSTM network  
l2=0.01;               %Regularization value  
nodes=5;               %Hidden layer size  
minibatchsize=32;      %Minibatch size in training of the LSTM network  
standardize=1; 	       %Standardize predictors  

display=1;             %Showing plots of simulated data and ANN training (1=yes, 0=no)  

[acc,fit]=lstm_regression_fnc(epochs, hyppighet, w,spred,l2,nodes,minibatchsize,noise_power,drift, drift_direction, N,standardize,display)  

%Gives the obtained rmse prediction accuracy on the test set in acc, and the model fit on training data in fit.   
