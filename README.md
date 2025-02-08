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

# 5 Top 10 Busiest Dates
```diff
import matplotlib.pyplot as plt
busiest_dates.head(10).plot(kind='line', color='blue')
plt.title('Top 10 Busiest Dates (Line Chart)')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
<img width="665" alt="image" src="https://github.com/user-attachments/assets/c60aedbc-cbd0-45bf-a3f2-7b23ae4a6719" />

# Download listings dataset of Hong Kong from 
https://data.insideairbnb.com/united-states/hi/hawaii/2024-09-13/data/listings.csv.gz
```diff
import pandas as pd
listings = pd.read_csv('/content/listings (1).csv')
```

# Check the columns
```diff
listings.columns
```
<img width="608" alt="image" src="https://github.com/user-attachments/assets/afad202e-bace-4533-bcd5-0db02193c22b" />

# Room type and price is given seperately 
```diff
import matplotlib.pyplot as plt
price_by_room = listings.groupby('room_type')['price'].mean()
print(price_by_room)

# Plot price by room type
price_by_room.plot(kind='bar', color='cyan')
plt.title('Average Price by Room Type')
plt.ylabel('Average Price')
plt.xlabel('Room Type')

plt.show()
```
<img width="635" alt="image" src="https://github.com/user-attachments/assets/075e79f9-9e64-4caf-b336-71153aa3c7eb" />

# Which are the top 10 neighborhoods with the most listings?
```diff
neighborhood_counts = listings['neighbourhood'].value_counts().head(10)
print("Top 10 Neighborhoods by Listings:")
print(neighborhood_counts)

# Plot neighborhoods with most listings
neighborhood_counts.plot(kind='bar', color='lightcoral')
plt.title('Top 10 Neighborhoods by Listings')
plt.ylabel('Number of Listings')
plt.xlabel('Neighborhood')
plt.xticks(rotation=90)
plt.show()
```
<img width="661" alt="image" src="https://github.com/user-attachments/assets/32911172-b7cd-4373-a66f-e649572ee26d" />

# Geographical Distribution of Listings (Price Colored)
```diff
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='viridis', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```
<img width="697" alt="image" src="https://github.com/user-attachments/assets/7fc371d8-5784-4f22-9691-ddf0d42fd7f3" />

# Let us see the listings on a real map

Hotter Areas (Red/Yellow): High Density: The areas that appear in red or yellow (the "hot" colors) indicate higher density or concentration of listings. This means there are more listings in these areas. Popular Locations: These regions might be more
popular or in high demand. It could be near tourist attractions, popular neighborhoods, or central areas in Hawaii where people tend to stay more often. Colder Areas (Green/Blue):

Low Density: Areas with blue or green (the "cold" colors) indicate a lower
concentration of listings. These regions have fewer listings available. Less Popular Locations: These areas might be less popular or further from key attractions. If you're looking at pricing or other factors, lower density could imply less competition in these regions, which might indicate more affordable areas or less tourist traffic. Density Patterns:

Clustered Areas: If you notice clusters of heatmap intensity, they represent hotspots. These might correspond to high-traffic areas like resorts, beaches, or urban centers. Spread-Out Listings: If the heatmap shows a more uniform
distribution, it could suggest that listings are more evenly spread across the region, which may reflect a more balanced demand for rentals across different areas of Hong kong.

```diff
import folium
from folium.plugins import HeatMap
import pandas as pd


Hong_kong_data = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around Hong kong
m = folium.Map(location=[42.65265406144247, -73.75935740854021], zoom_start=10)

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in Hong_kong_data.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data).add_to(m)

# Save the map as an HTML file to view in a browser
m.save('Hong_kong_heatmap.html')

# If you're using Jupyter Notebook, you can display the map directly in the notebook:
m
```

<img width="651" alt="image" src="https://github.com/user-attachments/assets/9e62157d-fa19-46a9-b76c-29f1013e5849" />

# How do I find location for my city?
Type your city name on google maps
Click on What`s here
<img width="822" alt="image" src="https://github.com/user-attachments/assets/4140427c-d55f-4755-a00b-66a458c1919d" />


