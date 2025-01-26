# Insights-from-data-set
doing an analysis for the dataset about paris:
•⁠  ⁠For the following analysis, I have downloaded the following data from: https://data.insideairbnb.com/france/ile-de-france/paris/2024-09-06/data/calendar.csv.gz
```
import pandas as pd
data = pd.read_csv('calendar.csv')
```
# 1 :white_check_mark: We need to know the number of available and unavailable rooms
```
data.available.value_counts()
```
<img width="231" alt="image" src="https://github.com/user-attachments/assets/0741d05b-6e0e-4445-976a-4dbe100e6e18" />

T stands for available, F stand for not available

# 2 Purpose: Calculates the percentage of available (t) and unavailable (f) dates.
```diff
Explaination: value_counts(normalize = True) gives proportions. Multiplying 100 converts the proportions into percentage
availability_percentage = data['available'].value_counts(normalize=True) * 100
availability_percentage
```
<img width="292" alt="image" src="https://github.com/user-attachments/assets/d50f1300-6f9b-4f54-8dde-46a0f2489e2d" />

# 3 Let's Count the busiest day! :triangular_flag_on_post:
```diff
busiest_dates = data[data['available'] == 'f']['date'].value_counts()
print('Busiest Dates:')
print(busiest_dates.head())
```
<img width="219" alt="image" src="https://github.com/user-attachments/assets/c7a61fa5-969f-4a8f-ac60-5914a5d05e72" />
# 4 Plot a bar graph to show availability percentage
```diff
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['green','red'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Avilable (t/f)')
plt.show()
```
<img width="583" alt="image" src="https://github.com/user-attachments/assets/95f033b1-14dd-4ce7-97ca-7709ab838a0b" />


