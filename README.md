## SustAlnify

#### Created an ML/ DL model for the prediction of daily average electricity prices at the Power Exchange using the Power Exchange Data for the year 2010 to 2017.
#### Predict the daily average electricity prices for all the days in the year 2018 and stored it in a CSV file having two columns: ‘Date’ and ‘Predicted Average Price (EUR/MWh)’.
 
#### Initially the data had to be done a lot of the preprocessing as it had a lot of the outliers and the uneven values. For the pre processing first we replaced the outliers with the average of its neighbours. And then grouped the data of the each of the year according to the mean and indexes.
 
* Then we created a deep copy of the DataFrame, sets the "Date" column as the index, and then adds new columns representing the price at different time lags (from 1 to n). The original DataFrame is not modified, and rows with missing values resulting from the shift operation are removed. The function returns the modified DataFrame. The code then applies this function to a DataFrame named df with n set to 7, resulting in a new DataFrame called shifted_df.
*	Using the minmaxscaler the data was then fit and transformed.

![Screenshot 2024-02-12 000927](https://github.com/sap-aayush/sustalnify_energy_price_prediction/assets/113010235/a95f5bc2-d6cb-4c15-8f1a-43ffa3ef23c6)


* After splitting the dataset into train and the test set, they were reshaped and the torch.float() was applied.
*	Then we defined a PyTorch dataset class, TimeSeriesDataset, tailored for time series data. It takes input sequences X and y during initialization and implements required methods (__len__ and __getitem__). Instances of this class, train_dataset and test_dataset, are created using training and testing data. These datasets can be employed with PyTorch data loaders for efficient handling of time series data during model training and evaluation.
*	Finally we defined a Long Short-Term Memory (LSTM) neural network model using PyTorch. The LSTM class is a subclass of nn.Module and takes parameters such as input_size, hidden_size, num_stacked_layers. The model architecture includes an LSTM layer with specified parameters, followed by a dropout layer and a fully connected (linear) layer. The forward method implements the forward pass of the model. It initializes the hidden and cell states, passes the input through the LSTM layer, applies dropout, and then passes the final sequence element through the linear layer. An instance of this model is created (model = LSTM(1, 4, 1)) and is moved to the CPU (model.to('cpu')). The resulting model can be used for tasks such as time series prediction or sequence modeling.
 
*	Then we trained each of the epoch and validated them hands on.
 

 
 
* Optimization condition for the renewable energy

*	X = Q_grid
*	Thus (X*0.15) + [(1050-X)*0.05] + 150*1     >=   0.2*1200
*	Therefore, Q_grid = 375MWH and Q_exchange = 675MWH, Q_solar = 150MWH on Jan 1st 2018
*	This optimizes the both of the price as well as renewable enrgy.
*	This ensures that the renewable energy percentage is always greater than 20 per cent for any given day, while also maintaining the optimum price paid
*	And the total price of the energy is 38564.3369294945 in Euros.
*	MSE = 10.1
*	R^2 = 0.76
*	The outputs of the prediction of the Jan 2018 are as : 
 ![Screenshot 2024-02-12 001329](https://github.com/sap-aayush/sustalnify_energy_price_prediction/assets/113010235/076ed239-c8c9-4c57-b3e7-c6601e1c50d6)

 
