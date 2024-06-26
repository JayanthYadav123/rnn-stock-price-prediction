# Stock Price Prediction

## AIM

To develop a Recurrent Neural Network model for stock price prediction.

## Problem Statement and Dataset

Developing an RNN model for stock price prediction involves leveraging historical market data to capture temporal dependencies. The goal is to design an LSTM or GRU-based architecture capable of learning sequential patterns in stock prices for accurate forecasting. 

<img width="407" alt="image" src="https://github.com/JayanthYadav123/rnn-stock-price-prediction/assets/94836154/a866766e-ea41-4ab1-8086-def2a15018fe">


## Design Steps
### Step 1:
Read the csv file and create the Data frame using pandas.
### Step 2:
Select the " Open " column for prediction. Or select any column of your interest and scale the values using MinMaxScaler.
### Step 3:
Create two lists for X_train and y_train. And append the collection of 60 readings in X_train, for which the 61st reading will be the first output in y_train.
### Step 4:

Create a model with the desired number of nuerons and one output neuron.
### Step 5:

Follow the same steps to create the Test data. But make sure you combine the training data with the test data.
### Step 6:

Make Predictions and plot the graph with the Actual and Predicted values.v



## Program
#### Name: G.Jayanth
#### Register Number: 212221230030.

```

import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from sklearn.preprocessing import MinMaxScaler
from keras import layers
from keras.models import Sequential

dataset_train = pd.read_csv('/content/trainset (1).csv')
dataset_train.columns
dataset_train.head()
train_set = dataset_train.iloc[:,1:2].values
type(train_set)
train_set.shape
sc = MinMaxScaler(feature_range=(0,1))
training_set_scaled = sc.fit_transform(train_set)
training_set_scaled.shape
X_train_array = []
y_train_array = []
for i in range(60, 1259):
  X_train_array.append(training_set_scaled[i-60:i,0])
  y_train_array.append(training_set_scaled[i,0])
X_train, y_train = np.array(X_train_array), np.array(y_train_array)
X_train1 = X_train.reshape((X_train.shape[0], X_train.shape[1],1))
X_train.shape
length = 60
n_features = 1
model = Sequential()
model.add(layers.SimpleRNN(50,input_shape=(60,1)))
model.add(layers.Dense(1))
model.compile(optimizer='adam', loss='mse')
print("Name:G Jayanth")
print("Register Number: 212221230030")

model.summary()
model.fit(X_train1,y_train,epochs=100, batch_size=32)
dataset_test = pd.read_csv('/content/testset.csv')
test_set = dataset_test.iloc[:,1:2].values
test_set.shape
dataset_total = pd.concat((dataset_train['Open'],dataset_test['Open']),axis=0)
price = dataset_total.values
price = price.reshape(-1,1)
price = price.reshape(-1,1)

X_test = []
y_test = []

for i in range(60,1384):
  X_test.append(inputs_scaled[i-60:i,0])
  y_test.append(inputs_scaled[i,0])
X_test = np.array(X_test)
X_test = np.reshape(X_test,(X_test.shape[0], X_test.shape[1],1))
X_test.shape
predicted_stock_price_scaled = model.predict(X_test)
predicted_stock_price = sc.inverse_transform(predicted_stock_price_scaled)

print("Name: G.Jayanth")
print("Register Number: 212221230030")

plt.plot(np.arange(0,1384),price, color='cyan', label = 'Test(Real) Google stock price')
plt.plot(np.arange(60,1384),predicted_stock_price, color='yellow', label = 'Predicted Google stock price')

plt.title('Google Stock Price Prediction')
plt.xlabel('Time')
plt.ylabel('Google Stock Price')
plt.legend()
plt.show()
from sklearn.metrics import mean_squared_error as mse
mse(y_test,predicted_stock_price)

```
## Output

### True Stock Price, Predicted Stock Price vs time
<img width="448" alt="image" src="https://github.com/JayanthYadav123/rnn-stock-price-prediction/assets/94836154/a01536eb-d2d4-44c2-8316-caa5ae4682de">


### Mean Square Error
<img width="323" alt="image" src="https://github.com/JayanthYadav123/rnn-stock-price-prediction/assets/94836154/ee556dcf-0bd8-4d18-88d3-75612d5ddebc">


## Result :
Thus, we have successfully created a Simple RNN model for Stock Price Prediction.
