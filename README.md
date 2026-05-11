# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 11-05-2026


### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Step 1: Load the dataset
data = pd.read_csv('/content/Social_media_impact_on_life.csv')

# Step 2: Create artificial date column
data['Date'] = pd.date_range(start='2024-01-01',
                             periods=len(data),
                             freq='D')

# Step 3: Set Date as index
data.set_index('Date', inplace=True)

# Step 4: Convert selected column to numeric
data['Avg_Daily_Usage_Hours'] = pd.to_numeric(
    data['Avg_Daily_Usage_Hours'],
    errors='coerce'
)

# Remove missing values
data = data.dropna(subset=['Avg_Daily_Usage_Hours'])

# Step 5: Resample data monthly
monthly_usage = data['Avg_Daily_Usage_Hours'].resample('M').mean()

# Step 6: Perform seasonal decomposition
decomposition = seasonal_decompose(
    monthly_usage,
    model='additive',
    period=2
)

# Step 7: Plot decomposition
plt.figure(figsize=(10, 12))

# Original Data
plt.subplot(411)
plt.plot(monthly_usage, label='Monthly Avg Usage')
plt.legend(loc='upper left')
plt.title('Monthly Average Social Media Usage')

# Trend Plot
plt.subplot(412)
plt.plot(decomposition.trend,
         label='Trend',
         color='orange')
plt.legend(loc='upper left')
plt.title('Trend Plot')

# Seasonal Plot
plt.subplot(413)
plt.plot(decomposition.seasonal,
         label='Seasonal',
         color='green')
plt.legend(loc='upper left')
plt.title('Seasonality Plot')

# Residual Plot
plt.subplot(414)
plt.plot(decomposition.resid,
         label='Residual',
         color='red')
plt.legend(loc='upper left')
plt.title('Residual Plot')

plt.tight_layout()
plt.show()
```

### OUTPUT:
### MONTHLY AVERAGE USAGE:
<img width="735" height="263" alt="image" src="https://github.com/user-attachments/assets/b358e621-7e8d-44de-8895-b117f32fbdd5" />

### TREND PLOT:
<img width="748" height="223" alt="image" src="https://github.com/user-attachments/assets/5c6e4e28-e899-4a1b-9f69-746fcd82c502" />

### SESONALITY PLOT:
<img width="735" height="221" alt="image" src="https://github.com/user-attachments/assets/135df5ee-673a-409b-8036-757e441e483e" />

### RESIDUAL PLOT:
<img width="723" height="232" alt="image" src="https://github.com/user-attachments/assets/53f0243e-a98a-4e0e-81a1-1b95171f728c" />

### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
