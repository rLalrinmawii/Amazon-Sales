# Unified-Mentor-Projects
Analyzing Amazon Sales data
# Analyzing Amazon Sales Data

## Overview

Sales management has gained importance to meet increasing competition and the need for improved methods of distribution to reduce cost and increase profits. Sales management today is the most important function in a commercial and business enterprise. In this project, ETL (Extract-Transform-Load) was performed on an Amazon dataset and the sales trends were analyzed month-wise, year-wise, and yearly month-wise. Key metrics and factors were identified, and meaningful relationships between attributes were shown through thorough research and findings.

## Dataset Description

The dataset contains detailed records of sales transactions from various global regions, including specifics such as:
- **Region**
- **Country**
- **Item Type**
- **Sales Channel (online or offline)**
- **Order Priority**
- **Order Date**
- **Order ID**
- **Ship Date**
- **Units Sold**
- **Unit Price**
- **Unit Cost**
- **Total Revenue**
- **Total Cost**
- **Total Profit**

Each row represents a unique transaction, providing comprehensive insights into sales performance and profitability across different product categories and geographical locations.

## Libraries Used

- `pandas`: For data manipulation and analysis.
- `matplotlib`: For creating static, animated, and interactive visualizations.
- `seaborn`: For making statistical graphics in Python.

## Data Preparation

1. **Load the dataset**:
   ```python
   file_path = '/Users/sm/Documents/received/UNI PG/internship_UM/Project 1/Amazon Sales data.csv'
   data = pd.read_csv(file_path)
   ```

2. **Display basic information**:
   ```python
   print("Number of rows:", data.shape[0])
   print("Number of columns:", data.shape[1])
   print(data.head())
   ```

3. **Convert date columns to datetime format**:
   ```python
   data['Order Date'] = pd.to_datetime(data['Order Date'])
   data['Ship Date'] = pd.to_datetime(data['Ship Date'])
   ```

4. **Extract year and month from order dates**:
   ```python
   data['Order Year'] = data['Order Date'].dt.year
   data['Order Month'] = data['Order Date'].dt.month
   ```

## Analysis and Visualization

### Monthly Sales Trend

The monthly sales trends were analyzed over different years, and separate line plots for each year were created. These plots illustrate the monthly total revenue for each year from 2010 to 2017.

**Code for monthly sales trend**:
```python
monthly_sales = data.groupby(['Order Year', 'Order Month'])['Total Revenue'].sum().reset_index()
sns.lineplot(x='Order Month', y='Total Revenue', hue='Order Year', data=monthly_sales, palette='viridis')
plt.title('Monthly Sales Trend')
plt.xlabel('Month')
plt.ylabel('Total Revenue')
plt.show()
```

### Yearly Sales Trend

The yearly sales trend was analyzed by aggregating the total revenue for each year and visualizing the results using both a bar chart and a line plot.

**Code for yearly sales trend**:
```python
yearly_sales = data.groupby('Order Year')['Total Revenue'].sum().reset_index()
sns.barplot(x='Order Year', y='Total Revenue', data=yearly_sales, palette='coolwarm')
plt.title('Yearly Sales Trend')
plt.xlabel('Year')
plt.ylabel('Total Revenue (in millions)')
plt.show()
```

### Monthly Sales Trend Across All Years

The monthly sales trend across all years was analyzed to reveal fluctuations in total revenue by month.

**Code for monthly sales trend across all years**:
```python
monthly_sales = data.groupby('Order Month')['Total Revenue'].sum().reset_index()
sns.lineplot(x='Order Month', y='Total Revenue', data=monthly_sales, color='b', marker='o')
plt.title('Monthly Sales Trend Across All Years')
plt.xlabel('Month')
plt.ylabel('Total Revenue')
plt.show()
```

### Sales Distribution by Region

The total revenue distribution across different regions was analyzed.

**Code for sales distribution by region**:
```python
region_sales = data.groupby('Region')['Total Revenue'].sum().sort_values(ascending=False).reset_index()
sns.barplot(x='Total Revenue', y='Region', data=region_sales, palette='rocket')
plt.title('Total Revenue by Region')
plt.xlabel('Total Revenue (USD)')
plt.ylabel('Region')
plt.show()
```

### Sales Distribution by Top Countries

The total revenue distribution across the top 10 countries was analyzed.

**Code for sales distribution by top countries**:
```python
top_countries = data.groupby('Country')['Total Revenue'].sum().sort_values(ascending=False).head(10).reset_index()
sns.barplot(x='Total Revenue', y='Country', data=top_countries, palette='mako')
plt.title('Total Revenue by Top 10 Countries')
plt.xlabel('Total Revenue (USD)')
plt.ylabel('Country')
plt.show()
```

### Key Metrics and Factors

#### Total Units Sold by Item Type

The total units sold distribution across different item types was analyzed.

**Code for total units sold by item type**:
```python
item_sales = data.groupby('Item Type')['Units Sold'].sum().sort_values(ascending=False).reset_index()
sns.barplot(x='Units Sold', y='Item Type', data=item_sales, palette='muted')
plt.title('Total Units Sold by Item Type')
plt.xlabel('Total Units Sold')
plt.ylabel('Item Type')
plt.show()
```

#### Average Unit Price by Item Type

The average unit price distribution across different item types was analyzed.

**Code for average unit price by item type**:
```python
avg_unit_price = data.groupby('Item Type')['Unit Price'].mean().sort_values(ascending=False).reset_index()
sns.barplot(x='Unit Price', y='Item Type', data=avg_unit_price, palette='pastel')
plt.title('Average Unit Price by Item Type')
plt.xlabel('Average Unit Price (USD)')
plt.ylabel('Item Type')
plt.show()
```

#### Total Profit by Sales Channel

The total profit distribution across different sales channels was analyzed.

**Code for total profit by sales channel**:
```python
sales_channel_profit = data.groupby('Sales Channel')['Total Profit'].sum().reset_index()
sns.barplot(x='Total Profit', y='Sales Channel', data=sales_channel_profit, palette='deep')
plt.title('Total Profit by Sales Channel')
plt.xlabel('Total Profit (USD)')
plt.ylabel('Sales Channel')
plt.show()
```

## Findings

1. **Monthly Sales Trends**: The peak sales months varied across different years.
2. **Yearly Sales Trends**: The highest total revenue was recorded in 2012, with a general decline observed from 2013 to 2015 and a slight improvement in 2017.
3. **Monthly Sales Across All Years**: February, October, and July had the highest total revenues.
4. **Sales Distribution by Region**: Sub-Saharan Africa and Europe contributed the most to total revenue.
5. **Sales Distribution by Top Countries**: Honduras, Myanmar, and Djibouti were the top three countries in total revenue.
6. **Total Units Sold by Item Type**: Cosmetics, Clothes, and Beverages were the top three item types.
7. **Average Unit Price by Item Type**: High variability in average unit prices across item types.
8. **Total Profit by Sales Channel**: Offline sales channels generated higher total profit compared to online sales channels.

This analysis provides insights into sales trends, revenue distribution, and key factors affecting sales performance, helping to inform sales management strategies.
