# EX.NO.09        A project on Time series analysis on weather forecasting using ARIMA model 
### Date: 17-5-25
### Name: STREEVALSAN V
### AIM: 212223240158
To Create a project on Time series analysis on weather forecasting using ARIMA model in  Python and compare with other models.
### ALGORITHM:
1. Explore the dataset of weather 
2. Check for stationarity of time series time series plot
   ACF plot and PACF plot
   ADF test
   Transform to stationary: differencing
3. Determine ARIMA models parameters p, q
4. Fit the ARIMA model
5. Make time series predictions
6. Auto-fit the ARIMA model
7. Evaluate model predictions
### PROGRAM:
# Import the neccessary packages
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.arima.model import ARIMA
from sklearn.metrics import mean_squared_error
```
# Load the dataset
```
data = pd.read_csv("/content/seattle-weather.csv")
```
# Convert 'Date' column to datetime format
```
data['date'] = pd.to_datetime(data['date'])
```
# Set 'Date' column as index
```
data.set_index('date', inplace=True)
```
# Arima Model
```
def arima_model(data, target_variable, order):
    train_size = int(len(data) * 0.8)
    train_data, test_data = data[:train_size], data[train_size:]

    model = ARIMA(train_data[target_variable], order=order)
    fitted_model = model.fit()

    forecast = fitted_model.forecast(steps=len(test_data))

    rmse = np.sqrt(mean_squared_error(test_data[target_variable], forecast))

    plt.figure(figsize=(10, 6))
    plt.plot(train_data.index, train_data[target_variable], label='Training Data')
    plt.plot(test_data.index, test_data[target_variable], label='Testing Data')
    plt.plot(test_data.index, forecast, label='Forecasted Data')
    plt.xlabel('Date')
    plt.ylabel(target_variable)
    plt.title('ARIMA Forecasting for ' + target_variable)
    plt.legend()
    plt.show()

    print("Root Mean Squared Error (RMSE):", rmse)

arima_model(data, 'temp_max', order=(5,1,5))
```
### OUTPUT:

![image](https://github.com/user-attachments/assets/c057d479-9382-426a-96b9-1a033be556c8)


### RESULT:
Thus the program run successfully based on the ARIMA model using python.
