# TSA-Ex-1b
# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 31/10/26

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data

### Dataset used:
ice_cream
### Software Required:
Google colab

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Read dataset
data = pd.read_csv('/content/ice_cream.csv')

data.head()

# Convert DATE column to datetime
data['DATE'] = pd.to_datetime(data['DATE'])

# Set DATE as index
data.set_index('DATE', inplace=True)

# Original data
data['IPN31152N'] = pd.to_numeric(data['IPN31152N'])

# 1. Regular Differencing
data['ice_cream_diff'] = data['IPN31152N'].diff()

# 2. Seasonal Adjustment
result = seasonal_decompose(
    data['IPN31152N'],
    model='additive',
    period=12
)
data['ice_cream_sea_diff'] = result.resid

# 3. Log Transformation
data['ice_cream_log'] = np.log(data['IPN31152N'])

# 4. Log Transformation and Regular Differencing
data['ice_cream_log_diff'] = data['ice_cream_log'].diff()

# 5. Log Transformation and Seasonal Differencing
data['ice_cream_log_seasonal_diff'] = (
    data['ice_cream_log'] - data['ice_cream_log'].shift(12)
)

# Plot all transformations
plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['IPN31152N'], label='Original')
plt.legend(loc='best')
plt.title('Original Ice Cream Data')
plt.xlabel('Date')
plt.ylabel('Production')

plt.subplot(6, 1, 2)
plt.plot(data['ice_cream_diff'], label='Regular Differencing')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Differenced Values')

plt.subplot(6, 1, 3)
plt.plot(data['ice_cream_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Adjusted Values')

plt.subplot(6, 1, 4)
plt.plot(data['ice_cream_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log Values')

plt.subplot(6, 1, 5)
plt.plot(
    data['ice_cream_log_diff'],
    label='Log Transformation and Regular Differencing'
)
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Log Differenced Values')

plt.subplot(6, 1, 6)
plt.plot(
    data['ice_cream_log_seasonal_diff'],
    label='Log Transformation and Seasonal Differencing'
)
plt.legend(loc='best')
plt.title('Log Transformation and Seasonal Differencing')
plt.xlabel('Date')
plt.ylabel('Seasonally Differenced Log Values')

plt.tight_layout()
plt.show()

# Plot original dataset
data['IPN31152N'].plot(kind='line', figsize=(12, 5))
plt.title('Time Series Plot of Ice Cream Data')
plt.xlabel('Date')
plt.ylabel('IPN31152N')
plt.grid(True)
plt.show()
```

### OUTPUT:


Original Data:

<img width="1899" height="283" alt="image" src="https://github.com/user-attachments/assets/0c0cd1f7-091a-4609-b6eb-f82c0a370942" />



REGULAR DIFFERENCING:

<img width="1909" height="291" alt="image" src="https://github.com/user-attachments/assets/b736bd2b-ccb8-451d-8118-7dad29a52839" />


SEASONAL ADJUSTMENT:
<img width="958" height="146" alt="image" src="https://github.com/user-attachments/assets/fb129d5e-5e51-405b-9312-2e9bfb9ae142" />


LOG TRANSFORMATION:

<img width="1918" height="301" alt="image" src="https://github.com/user-attachments/assets/40441a47-3672-44c8-b5c3-795af737365c" />


<img width="1914" height="597" alt="image" src="https://github.com/user-attachments/assets/e569f973-3305-49b6-bc19-583b4e5d7842" />




<img width="1351" height="534" alt="image" src="https://github.com/user-attachments/assets/d285f3b0-bcd8-408a-88a5-a31e915b96fe" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
