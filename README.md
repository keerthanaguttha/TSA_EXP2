# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Name  : Guttha Keerthana
Date  : 18-03-2025
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
### Load the dataset :
```
import pandas as pd 
import numpy as np 
import matplotlib.pyplot as plt 
data = pd.read_csv('FINAL_USO.csv')
data.head()
```
### Resampling data :
```
data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

resampled_data = data.resample('Y').sum()
resampled_data.head()

resampled_data.index = resampled_data.index.year

resampled_data.reset_index(inplace=True)
resampled_data.rename(columns={'Date':'Year'},inplace=True)

years = resampled_data['Year'].tolist()
Volume = resampled_data['Volume'].tolist()

resampled_data.head()

A - LINEAR TREND ESTIMATION

X = [i - years[len(years) // 2] for i in years]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, Volume)]
n = len(years)
b = (n * sum(xy) - sum(Volume) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(Volume) - b * sum(X)) / n
linear_trend = [a + b * X[i] for i in range(n)]

print(f"Linear Trend: y={a:.2f} + {b:.2f}x")

resampled_data['Linear Trend'] = linear_trend
resampled_data['Polynomial Trend'] = poly_trend

resampled_data['Volume'].plot(kind='line',color='blue',marker='o')
resampled_data['Linear Trend'].plot(kind='line',color='black',linestyle='--')
plt.xlabel('Volume')
plt.ylabel('Linear Trend')
plt.title('Volume vs Linear Trend')
plt.legend(['Volume', 'Linear Trend'])
plt.show()


B- POLYNOMIAL TREND ESTIMATION

print(f"\nPolynomial Trend: y={a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x²")
resampled_data['Volume'].plot(kind='line',color='blue',marker='o')
resampled_data['Polynomial Trend'].plot(kind='line',color='black',marker='o')
plt.xlabel('Volume')
plt.ylabel('Polynomial Trend')
plt.title('Volume vs Polynomial Trend')
plt.legend(['Volume', 'Polynomial Trend'])
plt.show()
```
### OUTPUT
A - LINEAR TREND ESTIMATION

![image](https://github.com/user-attachments/assets/281e4997-9b29-4019-b3e1-e58860ff4b7e)

B- POLYNOMIAL TREND ESTIMATION

![image](https://github.com/user-attachments/assets/ef5bde40-d918-4106-8552-0cb79f161eb4)


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
