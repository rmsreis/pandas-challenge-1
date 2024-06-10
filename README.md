# Client Purchase Analysis

This project analyzes the purchase data of clients to identify the top clients by quantity and their contributions to the company's revenue and profit.

## Summary

The analysis shows that the top 5 clients by quantity have significantly contributed to the company's revenue and profit. The Total Profit for these clients ranges from X to Y million dollars. The highest spending client ordered over Z units and generated the most profit.

## Steps

1. **Data Preparation**
   - Ensure all necessary columns exist, such as `profit`, which is calculated as the difference between `total_price` and `line_cost`.

2. **Identify Top Clients**
   - The top 5 clients are identified based on the number of entries in the data.

3. **Create Summary DataFrame**
   - A summary DataFrame is created for the top 5 clients, aggregating the total units purchased, total shipping price, total revenue, and total profit.

4. **Convert Monetary Values to Millions**
   - The monetary values are converted to millions of dollars for better readability.

5. **Rename Columns for Presentation**
   - The columns are renamed to reflect the changes and make the DataFrame suitable for presentation.

## Results

The analysis shows that the top 5 clients by quantity have significantly contributed to the company's revenue and profit. The Total Profit for these clients ranges from `X` to `Y` million dollars. The highest spending client ordered over `Z` units and generated the most profit.

## Code

The following code was used to perform the analysis:

```python
import pandas as pd

# Sample DataFrame structure for demonstration purposes
data = {
    'client_id': [24741, 33615, 38378, 46820, 66037, 24741, 33615],
    'qty': [100, 200, 150, 50, 300, 250, 100],
    'shipping_price': [700, 800, 600, 200, 900, 750, 400],
    'total_price': [10000, 20000, 15000, 5000, 25000, 18000, 12000],
    'line_cost': [9000, 18000, 13000, 4500, 23000, 16000, 11000]
}

df = pd.DataFrame(data)

# Ensure the profit column exists
df['profit'] = df['total_price'] - df['line_cost']

# Step 1: Define a function to convert currency to millions of dollars
def to_millions(value):
    return value / 1_000_000

# Step 2: Identify the top 5 clients by the number of entries
top_clients = df['client_id'].value_counts().head(5)
top_client_ids = top_clients.index.tolist()

# Step 3: Create a summary DataFrame for the top 5 clients
summary_df = df[df['client_id'].isin(top_client_ids)].groupby('client_id').agg({
    'qty': 'sum',
    'shipping_price': 'sum',
    'total_price': 'sum',
    'profit': 'sum'
}).reset_index()

# Step 4: Apply the currency conversion function to the relevant columns
money_columns = ['shipping_price', 'total_price', 'profit']
for column in money_columns:
    summary_df[column] = summary_df[column].apply(to_millions)

# Step 5: Rename columns for presentation
summary_df.columns = ['Client ID', 'Total Units Purchased', 'Total Shipping Price (in millions)', 'Total Revenue (in millions)', 'Total Profit (in millions)']

# Get values for the summary
x = summary_df['Total Profit (in millions)'].min()
y = summary_df['Total Profit (in millions)'].max()
z = summary_df['Total Units Purchased'].max()

# Create the summary text with the dynamic values
summary_text = f"""
The analysis shows that the top 5 clients by quantity have significantly contributed to the company's revenue and profit. 
The Total Profit for these clients ranges from {x:.2f} to {y:.2f} million dollars. 
The highest spending client ordered over {z} units and generated the most profit.
"""

print(summary_text)
```


Designed by Roberto dos Reis / @rmsreis

