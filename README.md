# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
   
### PROGRAM:
```
/*
Name: M THEJESWARAN
Register Number: 212223240168
*/

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

data = pd.read_csv('Games.csv')
data['Year'] = pd.to_datetime(data['Release'], format='%b-%y', errors='coerce').dt.year
data['Year'] = pd.to_numeric(data['Year'], errors='coerce')

data = data.sort_values(by='Year')

plt.figure(figsize=(10, 6))
plt.xlabel('Year')
plt.ylabel('Sales (Millions)')
plt.title('Video Game Sales Over the Years')
plt.plot(data['Year'], data['Sales'], color='blue', label='Game Sales')
plt.legend()
plt.show()

data2=data
data2['diff'] = data2['Sales'].diff()
data2 = data2.dropna()
plt.figure(figsize=(10, 6))
x=data2['Year']
y=data2["diff"]
plt.xlabel('Year')
plt.ylabel('Sales Difference (Millions)')
plt.title('Yearly Change in Global Video Game Sales')
plt.plot(x, y , color='red', label='Sales Difference')
plt.legend()
plt.show()

data1=data
data1['SeasonalAdjustment'] = data1['Sales'].rolling(window=12, min_periods=1).mean()
data1=data1.dropna(subset=['SeasonalAdjustment']) 
plt.figure(figsize=(10, 6))
plt.xlabel('Year')
plt.ylabel('Seasonally Adjusted Global Sales')
plt.title('Seasonal Adjustment of Global Video Game Sales')
plt.plot(data1['Year'], data1["SeasonalAdjustment"], color='green', label='Seasonal Adjustment')
plt.legend()
plt.show()

data3 = data2[data2['diff'] > 0] 
data3['Log'] = np.log(data3['diff'])
plt.figure(figsize=(10, 6))
plt.xlabel('Year')
plt.ylabel('Log Transformed Sales Difference')
plt.title('Log Transformation of Yearly Sales Change')
plt.plot(data3['Year'], data3['Log'], label="Log Transformation", color='magenta')
plt.legend()
plt.show()
```

### OUTPUT:

###ORIGINAL DATA:
![image](https://github.com/user-attachments/assets/10a8ef1c-4129-4451-a3dd-ebbd8bdbc38e)

###REGULAR DIFFERENCING:
![image](https://github.com/user-attachments/assets/e26cdd79-e625-4362-8d7a-9e04827944d2)

###SEASONAL ADJUSTMENT:
![image](https://github.com/user-attachments/assets/ace399ff-e8ac-42ce-94b6-7e6d444416fa)

###LOG TRANSFORMATION:
![image](https://github.com/user-attachments/assets/23e962b0-ab73-444c-95b0-88db8458dbc1)

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
