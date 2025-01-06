# 🚕 **Exploratory Data Analysis of Taxi Service and Weather Influence**

## 📝 **General Description**
This project focuses on conducting an Exploratory Data Analysis (EDA) of three datasets related to taxi services in a specific city. The primary goal is to understand the operations and performance of taxi companies, analyze trip trends across neighborhoods, and explore how weather conditions influence trip durations. 

---

## 📂 **Step-by-Step Guide**

### 📥 **1. Library Imports and Dataset Loading**
Essential libraries were imported, and datasets were loaded for analysis:

```python
import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import ttest_ind, levene

# Load datasets
df_companies = pd.read_csv('/datasets/project_sql_result_01.csv')
df_neighborhoods = pd.read_csv('/datasets/project_sql_result_04.csv')
df_trips_weather = pd.read_csv('/datasets/project_sql_result_07.csv')
```

---

### 🔍 **2. Initial Data Exploration**

#### 🛠️ Dataset Information
Explored the structure and contents of each dataset:

```python
# Companies dataset
print(df_companies.info())
print(df_companies.head())

# Neighborhoods dataset
print(df_neighborhoods.info())
print(df_neighborhoods.head())

# Trips and weather dataset
print(df_trips_weather.info())
print(df_trips_weather.head())
```

#### 🔧 Data Cleaning
Identified and addressed missing values and duplicates:

```python
# Check for duplicates
df_companies = df_companies.drop_duplicates()
df_neighborhoods = df_neighborhoods.drop_duplicates()
df_trips_weather = df_trips_weather.drop_duplicates()

# Fill missing values (example for demonstration)
df_trips_weather['duration_seconds'].fillna(0, inplace=True)
```

---

### 📊 **3. Key Analyses**

#### 🏙️ Top 10 Neighborhoods
Analyzed neighborhoods with the highest average trips:

```python
# Top 10 neighborhoods
top_neighborhoods = df_neighborhoods.nlargest(10, 'average_trips')

# Visualization
top_neighborhoods.plot.bar(x='dropoff_location_name', y='average_trips', title='Top 10 Neighborhoods by Average Trips')
plt.show()
```

#### 🚕 Top Taxi Companies
Identified the most popular taxi companies:

```python
# Top 10 companies
top_companies = df_companies.nlargest(10, 'trips_amount')

# Visualization
top_companies.plot.bar(x='company_name', y='trips_amount', title='Top 10 Taxi Companies by Trips')
plt.show()
```

---

### 🌦️ **4. Weather Influence Analysis**

#### 📊 Hypothesis Testing
Examined if weather conditions significantly influence trip durations:

```python
# Separate data by weather conditions
good_weather = df_trips_weather[df_trips_weather['weather_conditions'] == 'Good']['duration_seconds']
bad_weather = df_trips_weather[df_trips_weather['weather_conditions'] == 'Bad']['duration_seconds']

# Levene's Test for Equal Variance
levene_stat, levene_p = levene(good_weather, bad_weather)
equal_var = levene_p > 0.05

# T-test
t_stat, p_value = ttest_ind(good_weather, bad_weather, equal_var=equal_var)

print(f"Levene p-value: {levene_p}")
print(f"T-test p-value: {p_value}")
```

---

### 🏁 **5. Conclusion**

1. **Top Taxi Companies:** Flash Cab is the market leader in trip volume, followed by Taxi Affiliation Services and Medallion Leasing.
2. **Neighborhood Insights:** Loop and River North are the busiest neighborhoods for trip completions.
3. **Weather Impact:** Weather conditions significantly influence trip durations, as indicated by statistical tests.

This analysis provides actionable insights for taxi companies, urban planners, and policymakers to optimize services and address weather-related challenges effectively.

---

© 2025 | Francisco SLG | TripleTen

