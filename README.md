### DEVELOPED BY: SREEKUMAR S
### REGISTER NUMBER: 212223240157
### DATE:

# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION

### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```
Load the dataset
```python
file_path = 'AirPassengers.csv'  # Update this path if needed
data = pd.read_csv(file_path)
```
Extract the Year and Passenger data
```python
data['Year'] = pd.to_datetime(data['Month']).dt.year
yearly_data = data.groupby('Year')['#Passengers'].sum().reset_index()

years = yearly_data['Year'].tolist()
passengers = yearly_data['#Passengers'].tolist()
```
Linear Trend Estimation
```python
X = [i - years[len(years) // 2] for i in years]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, passengers)]

n = len(years)
b = (n * sum(xy) - sum(passengers) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(passengers) - b * sum(X)) / n
linear_trend = [a + b * X[i] for i in range(n)]
```
Polynomial Trend Estimation (2nd degree for simplicity)
```python
x3 = [i ** 3 for i in X]
x4 = [i ** 4 for i in X]
x2y = [i * j for i, j in zip(x2, passengers)]

coeff = [[len(X), sum(X), sum(x2)],
         [sum(X), sum(x2), sum(x3)],
         [sum(x2), sum(x3), sum(x4)]]

Y = [sum(passengers), sum(xy), sum(x2y)]
A = np.array(coeff)
B = np.array(Y)
```
Solve for polynomial coefficients
```python
solution = np.linalg.solve(A, B)
a_poly, b_poly, c_poly = solution
poly_trend = [a_poly + b_poly * X[i] + c_poly * (X[i] ** 2) for i in range(n)]
```
Prepare the results
```python
yearly_data['Linear_Trend'] = linear_trend
yearly_data['Polynomial_Trend'] = poly_trend
```
Display the trend equations
```python
print("Linear Trend Equation: y = {:.2f} + {:.2f}x".format(a, b))
print("Polynomial Trend Equation: y = {:.2f} + {:.2f}x + {:.2f}x^2".format(a_poly, b_poly, c_poly))
```
Visualization for Linear Trend
```python
plt.figure(figsize=(10, 6))
plt.plot(years, passengers, label='Actual Data', marker='o')
plt.plot(years, linear_trend, label='Linear Trend', linestyle='--')
plt.xlabel('Year')
plt.ylabel('Number of Passengers')
plt.title('Linear Trend Estimation for Air Passengers')
plt.legend()
plt.grid(True)
plt.show()
```
Visualization for Polynomial Trend
```python
plt.figure(figsize=(10, 6))
plt.plot(years, passengers, label='Actual Data', marker='o')
plt.plot(years, poly_trend, label='Polynomial Trend', linestyle='-.')
plt.xlabel('Year')
plt.ylabel('Number of Passengers')
plt.title('Polynomial Trend Estimation for Air Passengers')
plt.legend()
plt.grid(True)
plt.show()
```
### OUTPUT
A - LINEAR TREND ESTIMATION

![image](https://github.com/user-attachments/assets/3cbb5f26-71d0-48e8-aaaf-96cbd2e87450)

B- POLYNOMIAL TREND ESTIMATION

![image](https://github.com/user-attachments/assets/6dfd4288-eadc-4678-b234-897866d281e4)

### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
