# How to Beat The Market!

### Research Direction: Analyzing the Financial Health of Middle Market Firms

By Noah Levine, Patrick Williams, Yuan Wang, Cillian Fisher

This is a website to showcase our final project for FIN 377 - Data Science for Finance course at Lehigh University.

## Table of contents
1. [Introduction](#introduction)
2. [Codes](#meth)
3. [Analysis Section](#section3)
4. [Summary](#summary)

## Introduction  <a name="introduction"></a>

The main purpose of this project is to explore the effectiveness and reliability of various financial metrics and valuation multiples in assessing the financial health and performance of middle market companies in the context of mergers and acquisitions (M&A). Specifically, our research aims to identify which financial metrics demonstrate the strongest correlation with commonly used valuation multiples across different economic sectors in the middle market. This will provide clearer investment strategies and enhance financial assessment methodologies, thereby facilitating more informed decision-making in the M&A process.

## Methodology <a name="meth"></a>

Here is some code that we used to develop our analysis. 

We began by importing neccessary packages and defining our dataframe: 

```python
import numpy as np
import pandas as pd
df = pd.read_stata('ccm.dta')
#df.head()  
pd.set_option('display.max_columns', None)
#print(df.columns)
```

We then filtered our Market Caps and took out companies with no gross profit, calculating Market Capitlization:

```python
# Filter Market Caps and companies that dont have gross profit
MiddleMarket_data = df[(df['mkvalt'] >= 0) & (df['mkvalt'] <= 12000)]
# Calculate market capitalization
MiddleMarket_data['Avg_Price'] = (MiddleMarket_data['prch_c'] + MiddleMarket_data['prcl_c']) / 2
MiddleMarket_data['Market_Cap'] = MiddleMarket_data['Avg_Price'] * MiddleMarket_data['csho']
```

More filtering to find where EBITDA was positive and then selected relevant columsn for analysis.
We also re-ordered the columns for readibility:

```python
filtered_data = MiddleMarket_data.loc[MiddleMarket_data['ebitda'] > 0, ['tic','ebitda','dvc','ob','conm','fdate','lt','fyr','xrd','cogs','oibdp','capx','at','revt', 'xsga','ppent','csho','ppegt', 'che','ceq','lct','prcl_c','prch_c','Avg_Price','Market_Cap','oiadp','invt','sich','emp','txt','xint','act']]
#filtered_data
filtered_data.columns = ['Ticker', 'EBITDA', 'Dividends', 'Operating Income', 'Company Name', 'Fiscal Date', 'Long-Term Debt', 'Fiscal Year', 'Research and Development Expenses', 'Cost of Goods Sold', 'Operating Income Before Depreciation', 'Capital Expenditures', 'Total Assets', 'Revenue', 'Selling, General, and Administrative Expenses', 'Property, Plant, and Equipment Net', 'Common Shares Outstanding', 'Gross Property, Plant, and Equipment', 'Cash and Equivalents', 'Common Equity', 'Current Liabilities', '52-Week Low Price', '52-Week High Price','Avg_Price','Market_Cap','OpInc After Dep','Inventory','SP Index Code','Employees','Taxes','Interest Expense','Current Assets']
filtered_data.reindex()
filtered_data = filtered_data[['Ticker', 'Company Name', 'Market_Cap','Fiscal Date', 'Fiscal Year','Employees','SP Index Code', 'EBITDA', 'Operating Income', 'Dividends', 'Long-Term Debt', 'Research and Development Expenses', 'Cost of Goods Sold', 'Operating Income Before Depreciation', 'Capital Expenditures', 'Total Assets', 'Revenue', 'Selling, General, and Administrative Expenses', 'Property, Plant, and Equipment Net', 'Common Shares Outstanding', 'Gross Property, Plant, and Equipment', 'Cash and Equivalents', 'Common Equity', 'Current Liabilities', '52-Week Low Price', '52-Week High Price','Avg_Price','Market_Cap','OpInc After Dep','Inventory','SP Index Code','Employees','Taxes','Interest Expense','Current Assets']]
```

Then we did some Machine Learning using ExplainableBoostingRegressor

```python
from sklearn.model_selection import train_test_split
from interpret.glassbox import ExplainableBoostingRegressor 
from interpret import show

X = selected_df.drop(columns=['Ticker', 'Division'])
y = selected_df['EV/EBITDA']

# Split the dataset into training and testing sets
seed = 42
np.random.seed(seed)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.20, random_state=seed)

# Initialize the ExplainableBoostingRegressor
ebm = ExplainableBoostingRegressor(random_state=seed)

# Fit the model
ebm.fit(X_train, y_train)

# Get the global feature importances from the model
ebm_global = ebm.explain_global()
show(ebm_global)
```


## Analysis Section <a name="section3"></a>

Here are some graphs that we created in our analysis. We saved them to the `pics/` subfolder and include them via the usual markdown syntax for pictures.

![](pics/plot1.png)
<br><br>
Some analysis here
<br><br>
![](pics/plot2.png)
<br><br>
More analysis here.
<br><br>
![](pics/plot3.png)
<br><br>
More analysis.

## Summary <a name="summary"></a>

Blah blah



## About the team

<img src="pics/julio.jpg" alt="julio" width="300"/>
<br>
Julio is a senior at Lehigh studying finance.
<br><br><br>
<img src="pics/don2.jpg" alt="don" width="300"/>
<br>
Don is an assistant professor at Lehigh.


## More 

To view the GitHub repo for this website, click [here](https://github.com/cillianfisher/finalProject).
