```python
import numpy as np
import pandas as pd
df = pd.read_stata('ccm.dta')
#df.head()  
pd.set_option('display.max_columns', None)
#print(df.columns)
```


```python
# Filter Market Caps and companies that dont have gross profit
MiddleMarket_data = df[(df['mkvalt'] >= 0) & (df['mkvalt'] <= 12000)]
# Calculate market capitalization
MiddleMarket_data['Avg_Price'] = (MiddleMarket_data['prch_c'] + MiddleMarket_data['prcl_c']) / 2
MiddleMarket_data['Market_Cap'] = MiddleMarket_data['Avg_Price'] * MiddleMarket_data['csho']
```

    /var/folders/_8/vpmh2zyd23z9mnscjwzk9t1r0000gn/T/ipykernel_35458/2959442128.py:4: PerformanceWarning: DataFrame is highly fragmented.  This is usually the result of calling `frame.insert` many times, which has poor performance.  Consider joining all columns at once using pd.concat(axis=1) instead. To get a de-fragmented frame, use `newframe = frame.copy()`
      MiddleMarket_data['Avg_Price'] = (MiddleMarket_data['prch_c'] + MiddleMarket_data['prcl_c']) / 2
    /var/folders/_8/vpmh2zyd23z9mnscjwzk9t1r0000gn/T/ipykernel_35458/2959442128.py:4: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      MiddleMarket_data['Avg_Price'] = (MiddleMarket_data['prch_c'] + MiddleMarket_data['prcl_c']) / 2
    /var/folders/_8/vpmh2zyd23z9mnscjwzk9t1r0000gn/T/ipykernel_35458/2959442128.py:5: PerformanceWarning: DataFrame is highly fragmented.  This is usually the result of calling `frame.insert` many times, which has poor performance.  Consider joining all columns at once using pd.concat(axis=1) instead. To get a de-fragmented frame, use `newframe = frame.copy()`
      MiddleMarket_data['Market_Cap'] = MiddleMarket_data['Avg_Price'] * MiddleMarket_data['csho']
    /var/folders/_8/vpmh2zyd23z9mnscjwzk9t1r0000gn/T/ipykernel_35458/2959442128.py:5: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      MiddleMarket_data['Market_Cap'] = MiddleMarket_data['Avg_Price'] * MiddleMarket_data['csho']



```python
#(MiddleMarket_data['ebitda'] > 1).sum()
#filtered_data = MiddleMarket_data[MiddleMarket_data['ebitda'] > 1]
#filtered_data['ebitda']
filtered_data = MiddleMarket_data.loc[MiddleMarket_data['ebitda'] > 0, ['tic','ebitda','dvc','ob','conm','fdate','lt','fyr','xrd','cogs','oibdp','capx','at','revt', 'xsga','ppent','csho','ppegt', 'che','ceq','lct','prcl_c','prch_c','Avg_Price','Market_Cap','oiadp','invt','sich','emp','txt','xint','act']]
#filtered_data
filtered_data.columns = ['Ticker', 'EBITDA', 'Dividends', 'Operating Income', 'Company Name', 'Fiscal Date', 'Long-Term Debt', 'Fiscal Year', 'Research and Development Expenses', 'Cost of Goods Sold', 'Operating Income Before Depreciation', 'Capital Expenditures', 'Total Assets', 'Revenue', 'Selling, General, and Administrative Expenses', 'Property, Plant, and Equipment Net', 'Common Shares Outstanding', 'Gross Property, Plant, and Equipment', 'Cash and Equivalents', 'Common Equity', 'Current Liabilities', '52-Week Low Price', '52-Week High Price','Avg_Price','Market_Cap','OpInc After Dep','Inventory','SP Index Code','Employees','Taxes','Interest Expense','Current Assets']
filtered_data.reindex()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Ticker</th>
      <th>EBITDA</th>
      <th>Dividends</th>
      <th>Operating Income</th>
      <th>Company Name</th>
      <th>Fiscal Date</th>
      <th>Long-Term Debt</th>
      <th>Fiscal Year</th>
      <th>Research and Development Expenses</th>
      <th>Cost of Goods Sold</th>
      <th>Operating Income Before Depreciation</th>
      <th>Capital Expenditures</th>
      <th>Total Assets</th>
      <th>Revenue</th>
      <th>Selling, General, and Administrative Expenses</th>
      <th>Property, Plant, and Equipment Net</th>
      <th>Common Shares Outstanding</th>
      <th>Gross Property, Plant, and Equipment</th>
      <th>Cash and Equivalents</th>
      <th>Common Equity</th>
      <th>Current Liabilities</th>
      <th>52-Week Low Price</th>
      <th>52-Week High Price</th>
      <th>Avg_Price</th>
      <th>Market_Cap</th>
      <th>OpInc After Dep</th>
      <th>Inventory</th>
      <th>SP Index Code</th>
      <th>Employees</th>
      <th>Taxes</th>
      <th>Interest Expense</th>
      <th>Current Assets</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AIR</td>
      <td>101.800</td>
      <td>0.100</td>
      <td>750.0</td>
      <td>AAR CORP</td>
      <td>2021-07-22</td>
      <td>565.300</td>
      <td>5</td>
      <td>NaN</td>
      <td>1364.600</td>
      <td>101.800</td>
      <td>11.300</td>
      <td>1539.700</td>
      <td>1651.400</td>
      <td>185.000</td>
      <td>380.100</td>
      <td>35.375</td>
      <td>640.300</td>
      <td>60.200</td>
      <td>974.400</td>
      <td>336.800</td>
      <td>8.5600</td>
      <td>47.99</td>
      <td>28.2750</td>
      <td>1000.228125</td>
      <td>65.500</td>
      <td>591.000</td>
      <td>5080.0</td>
      <td>4.700</td>
      <td>18.200</td>
      <td>5.000</td>
      <td>937.000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AIR</td>
      <td>149.300</td>
      <td>0.000</td>
      <td>850.0</td>
      <td>AAR CORP</td>
      <td>2022-07-22</td>
      <td>539.400</td>
      <td>5</td>
      <td>NaN</td>
      <td>1470.300</td>
      <td>149.300</td>
      <td>17.300</td>
      <td>1573.900</td>
      <td>1817.100</td>
      <td>197.500</td>
      <td>349.200</td>
      <td>35.391</td>
      <td>607.500</td>
      <td>58.900</td>
      <td>1034.500</td>
      <td>348.200</td>
      <td>30.9000</td>
      <td>45.49</td>
      <td>38.1950</td>
      <td>1351.759245</td>
      <td>116.200</td>
      <td>604.100</td>
      <td>5080.0</td>
      <td>4.500</td>
      <td>26.600</td>
      <td>2.400</td>
      <td>1007.200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AIR</td>
      <td>179.300</td>
      <td>0.000</td>
      <td>740.0</td>
      <td>AAR CORP</td>
      <td>2023-07-21</td>
      <td>734.000</td>
      <td>5</td>
      <td>NaN</td>
      <td>1591.300</td>
      <td>179.300</td>
      <td>29.500</td>
      <td>1833.100</td>
      <td>1990.600</td>
      <td>220.000</td>
      <td>367.900</td>
      <td>34.916</td>
      <td>636.700</td>
      <td>81.800</td>
      <td>1099.100</td>
      <td>351.500</td>
      <td>33.7500</td>
      <td>52.83</td>
      <td>43.2900</td>
      <td>1511.513640</td>
      <td>151.400</td>
      <td>624.700</td>
      <td>5080.0</td>
      <td>5.000</td>
      <td>31.400</td>
      <td>12.200</td>
      <td>1097.900</td>
    </tr>
    <tr>
      <th>5</th>
      <td>AAL</td>
      <td>4103.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>AMERICAN AIRLINES GROUP INC</td>
      <td>2023-02-26</td>
      <td>70515.000</td>
      <td>12</td>
      <td>NaN</td>
      <td>37631.000</td>
      <td>4103.000</td>
      <td>2906.000</td>
      <td>64716.000</td>
      <td>48971.000</td>
      <td>7237.000</td>
      <td>38294.000</td>
      <td>650.642</td>
      <td>58323.000</td>
      <td>9960.000</td>
      <td>-5799.000</td>
      <td>21496.000</td>
      <td>11.6514</td>
      <td>21.42</td>
      <td>16.5357</td>
      <td>10758.820919</td>
      <td>1805.000</td>
      <td>2279.000</td>
      <td>4512.0</td>
      <td>129.700</td>
      <td>59.000</td>
      <td>1962.000</td>
      <td>15269.000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>AAL</td>
      <td>6267.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>AMERICAN AIRLINES GROUP INC</td>
      <td>2024-02-23</td>
      <td>68260.000</td>
      <td>12</td>
      <td>NaN</td>
      <td>38716.000</td>
      <td>6267.000</td>
      <td>2596.000</td>
      <td>63058.000</td>
      <td>52788.000</td>
      <td>7805.000</td>
      <td>38703.000</td>
      <td>654.273</td>
      <td>60800.000</td>
      <td>8488.000</td>
      <td>-5202.000</td>
      <td>22062.000</td>
      <td>10.8600</td>
      <td>19.08</td>
      <td>14.9700</td>
      <td>9794.466810</td>
      <td>4013.000</td>
      <td>2400.000</td>
      <td>4512.0</td>
      <td>132.100</td>
      <td>299.000</td>
      <td>2145.000</td>
      <td>13572.000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>21958</th>
      <td>HYFM</td>
      <td>36.742</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>HYDROFARM HLDNG GP INC</td>
      <td>2022-03-31</td>
      <td>256.062</td>
      <td>12</td>
      <td>NaN</td>
      <td>374.733</td>
      <td>36.742</td>
      <td>5.402</td>
      <td>891.242</td>
      <td>479.420</td>
      <td>67.945</td>
      <td>95.718</td>
      <td>44.618</td>
      <td>104.009</td>
      <td>28.384</td>
      <td>635.180</td>
      <td>88.415</td>
      <td>24.3550</td>
      <td>95.48</td>
      <td>59.9175</td>
      <td>2673.399015</td>
      <td>21.808</td>
      <td>189.134</td>
      <td>3524.0</td>
      <td>0.720</td>
      <td>-19.137</td>
      <td>2.138</td>
      <td>269.384</td>
    </tr>
    <tr>
      <th>21968</th>
      <td>KARO</td>
      <td>84.155</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>KAROOOOO LTD</td>
      <td>2022-06-20</td>
      <td>59.330</td>
      <td>2</td>
      <td>9.673</td>
      <td>27.559</td>
      <td>84.155</td>
      <td>35.818</td>
      <td>200.247</td>
      <td>177.987</td>
      <td>66.273</td>
      <td>90.133</td>
      <td>30.951</td>
      <td>188.430</td>
      <td>47.427</td>
      <td>139.431</td>
      <td>40.451</td>
      <td>29.1000</td>
      <td>40.81</td>
      <td>34.9550</td>
      <td>1081.892205</td>
      <td>51.920</td>
      <td>1.644</td>
      <td>7370.0</td>
      <td>3.508</td>
      <td>13.318</td>
      <td>0.799</td>
      <td>72.275</td>
    </tr>
    <tr>
      <th>21969</th>
      <td>KARO</td>
      <td>81.977</td>
      <td>15.995</td>
      <td>NaN</td>
      <td>KAROOOOO LTD</td>
      <td>2023-06-21</td>
      <td>57.738</td>
      <td>2</td>
      <td>9.645</td>
      <td>37.580</td>
      <td>81.977</td>
      <td>31.582</td>
      <td>204.404</td>
      <td>191.082</td>
      <td>71.525</td>
      <td>86.729</td>
      <td>30.951</td>
      <td>197.416</td>
      <td>52.622</td>
      <td>144.982</td>
      <td>43.012</td>
      <td>20.0000</td>
      <td>39.50</td>
      <td>29.7500</td>
      <td>920.792250</td>
      <td>52.286</td>
      <td>4.313</td>
      <td>7370.0</td>
      <td>4.039</td>
      <td>15.544</td>
      <td>0.550</td>
      <td>79.699</td>
    </tr>
    <tr>
      <th>21976</th>
      <td>HSHP</td>
      <td>23.744</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>HIMALAYA SHIPPING LTD</td>
      <td>2024-04-12</td>
      <td>445.001</td>
      <td>12</td>
      <td>NaN</td>
      <td>9.146</td>
      <td>23.744</td>
      <td>413.055</td>
      <td>599.206</td>
      <td>36.736</td>
      <td>3.846</td>
      <td>561.263</td>
      <td>43.900</td>
      <td>570.381</td>
      <td>25.553</td>
      <td>154.205</td>
      <td>25.300</td>
      <td>4.3000</td>
      <td>7.11</td>
      <td>5.7050</td>
      <td>250.449500</td>
      <td>14.626</td>
      <td>0.634</td>
      <td>NaN</td>
      <td>0.002</td>
      <td>0.000</td>
      <td>21.406</td>
      <td>32.807</td>
    </tr>
    <tr>
      <th>21985</th>
      <td>CLCO</td>
      <td>277.522</td>
      <td>87.511</td>
      <td>NaN</td>
      <td>COOL COMPANY LTD</td>
      <td>2024-03-28</td>
      <td>1250.363</td>
      <td>12</td>
      <td>NaN</td>
      <td>77.315</td>
      <td>277.522</td>
      <td>195.088</td>
      <td>2056.943</td>
      <td>379.010</td>
      <td>24.173</td>
      <td>1885.885</td>
      <td>53.703</td>
      <td>1998.375</td>
      <td>136.846</td>
      <td>735.990</td>
      <td>293.330</td>
      <td>11.0000</td>
      <td>14.50</td>
      <td>12.7500</td>
      <td>684.713250</td>
      <td>200.893</td>
      <td>3.659</td>
      <td>NaN</td>
      <td>1.647</td>
      <td>0.556</td>
      <td>73.080</td>
      <td>154.253</td>
    </tr>
  </tbody>
</table>
<p>9342 rows × 32 columns</p>
</div>




```python
# Reorder the columns
filtered_data = filtered_data[['Ticker', 'Company Name', 'Market_Cap','Fiscal Date', 'Fiscal Year','Employees','SP Index Code', 
                               'EBITDA', 'Operating Income', 'Dividends', 
                               'Long-Term Debt', 'Research and Development Expenses', 
                               'Cost of Goods Sold', 'Operating Income Before Depreciation', 
                               'Capital Expenditures', 'Total Assets', 'Revenue', 
                               'Selling, General, and Administrative Expenses', 
                               'Property, Plant, and Equipment Net', 
                               'Gross Property, Plant, and Equipment', 'Cash and Equivalents', 
                               'Common Equity', 'Current Liabilities', 'Common Shares Outstanding', 
                               '52-Week Low Price', '52-Week High Price', 'Avg_Price', 
                                'Inventory', 'OpInc After Dep','Interest Expense','Taxes', 'Current Assets']]

# Display the reordered DataFrame
filtered_data = filtered_data[(filtered_data['Operating Income'] >= .00)]
filtered_data.replace([np.inf, -np.inf], np.nan, inplace=True)
filtered_data.fillna(0, inplace=True)
filtered_data = filtered_data[(filtered_data['Market_Cap'] >= 100)]
filtered_data.describe()

```

    /var/folders/_8/vpmh2zyd23z9mnscjwzk9t1r0000gn/T/ipykernel_35458/362217121.py:17: FutureWarning: Setting an item of incompatible dtype is deprecated and will raise in a future error of pandas. Value '0' has dtype incompatible with datetime64[ns], please explicitly cast to a compatible dtype first.
      filtered_data.fillna(0, inplace=True)





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Market_Cap</th>
      <th>Fiscal Year</th>
      <th>Employees</th>
      <th>SP Index Code</th>
      <th>EBITDA</th>
      <th>Operating Income</th>
      <th>Dividends</th>
      <th>Long-Term Debt</th>
      <th>Research and Development Expenses</th>
      <th>Cost of Goods Sold</th>
      <th>Operating Income Before Depreciation</th>
      <th>Capital Expenditures</th>
      <th>Total Assets</th>
      <th>Revenue</th>
      <th>Selling, General, and Administrative Expenses</th>
      <th>Property, Plant, and Equipment Net</th>
      <th>Gross Property, Plant, and Equipment</th>
      <th>Cash and Equivalents</th>
      <th>Common Equity</th>
      <th>Current Liabilities</th>
      <th>Common Shares Outstanding</th>
      <th>52-Week Low Price</th>
      <th>52-Week High Price</th>
      <th>Avg_Price</th>
      <th>Inventory</th>
      <th>OpInc After Dep</th>
      <th>Interest Expense</th>
      <th>Taxes</th>
      <th>Current Assets</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2565.155154</td>
      <td>9.635925</td>
      <td>12.313823</td>
      <td>4672.390885</td>
      <td>345.178820</td>
      <td>1477.291645</td>
      <td>28.439949</td>
      <td>2500.088561</td>
      <td>28.863912</td>
      <td>2378.094880</td>
      <td>345.178820</td>
      <td>99.539855</td>
      <td>3595.068219</td>
      <td>3230.708273</td>
      <td>507.434573</td>
      <td>932.470596</td>
      <td>1587.643820</td>
      <td>312.607887</td>
      <td>1009.996287</td>
      <td>671.269804</td>
      <td>67.036041</td>
      <td>34.127066</td>
      <td>65.607911</td>
      <td>49.867488</td>
      <td>481.058678</td>
      <td>236.122276</td>
      <td>66.140315</td>
      <td>34.307699</td>
      <td>1025.857042</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2717.436271</td>
      <td>3.803079</td>
      <td>23.895366</td>
      <td>2077.657616</td>
      <td>520.606361</td>
      <td>4531.653675</td>
      <td>115.608116</td>
      <td>7288.660880</td>
      <td>88.376601</td>
      <td>4699.410975</td>
      <td>520.606361</td>
      <td>209.489278</td>
      <td>8327.620485</td>
      <td>5782.312996</td>
      <td>980.975527</td>
      <td>1849.034995</td>
      <td>2875.506466</td>
      <td>558.295577</td>
      <td>1417.690558</td>
      <td>1272.459096</td>
      <td>76.138807</td>
      <td>40.416148</td>
      <td>69.069401</td>
      <td>53.981649</td>
      <td>1115.464011</td>
      <td>373.130720</td>
      <td>182.130914</td>
      <td>82.780385</td>
      <td>1604.366533</td>
    </tr>
    <tr>
      <th>min</th>
      <td>101.146145</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.188000</td>
      <td>0.000000</td>
      <td>-1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>4.088000</td>
      <td>0.188000</td>
      <td>0.000000</td>
      <td>20.175000</td>
      <td>13.895000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.043000</td>
      <td>-5921.471000</td>
      <td>0.000000</td>
      <td>0.585000</td>
      <td>0.001100</td>
      <td>2.190000</td>
      <td>1.405000</td>
      <td>0.000000</td>
      <td>-664.927000</td>
      <td>-41.133000</td>
      <td>-888.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>567.022015</td>
      <td>9.000000</td>
      <td>1.767000</td>
      <td>3530.000000</td>
      <td>62.692000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>372.338000</td>
      <td>0.000000</td>
      <td>355.933000</td>
      <td>62.692000</td>
      <td>12.632000</td>
      <td>729.140000</td>
      <td>589.837000</td>
      <td>104.000000</td>
      <td>110.875000</td>
      <td>224.554000</td>
      <td>45.739000</td>
      <td>225.870000</td>
      <td>101.391000</td>
      <td>23.974000</td>
      <td>8.900000</td>
      <td>22.090000</td>
      <td>15.810000</td>
      <td>22.616000</td>
      <td>29.700000</td>
      <td>3.198000</td>
      <td>1.748000</td>
      <td>197.934000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1467.084995</td>
      <td>12.000000</td>
      <td>4.850000</td>
      <td>3845.000000</td>
      <td>178.222000</td>
      <td>117.873000</td>
      <td>0.000000</td>
      <td>1007.659000</td>
      <td>0.000000</td>
      <td>910.268000</td>
      <td>178.222000</td>
      <td>37.079000</td>
      <td>1755.084000</td>
      <td>1460.860000</td>
      <td>226.903000</td>
      <td>306.543000</td>
      <td>581.100000</td>
      <td>136.316000</td>
      <td>604.900000</td>
      <td>289.300000</td>
      <td>44.384000</td>
      <td>20.150000</td>
      <td>43.700000</td>
      <td>32.048200</td>
      <td>136.026000</td>
      <td>111.100000</td>
      <td>19.200000</td>
      <td>14.900000</td>
      <td>515.363000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>3671.073840</td>
      <td>12.000000</td>
      <td>13.000000</td>
      <td>5900.000000</td>
      <td>442.800000</td>
      <td>904.600000</td>
      <td>25.241000</td>
      <td>2461.595000</td>
      <td>16.500000</td>
      <td>2360.575000</td>
      <td>442.800000</td>
      <td>101.910000</td>
      <td>3864.920000</td>
      <td>3369.810000</td>
      <td>512.817000</td>
      <td>910.730000</td>
      <td>1650.864000</td>
      <td>342.528000</td>
      <td>1307.748000</td>
      <td>692.904000</td>
      <td>82.450000</td>
      <td>43.125000</td>
      <td>84.840000</td>
      <td>64.350000</td>
      <td>414.077000</td>
      <td>306.397000</td>
      <td>60.000000</td>
      <td>49.418000</td>
      <td>1187.672000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>16531.765360</td>
      <td>12.000000</td>
      <td>300.000000</td>
      <td>9997.000000</td>
      <td>7101.000000</td>
      <td>48600.000000</td>
      <td>4207.700000</td>
      <td>182626.000000</td>
      <td>1144.400000</td>
      <td>55731.400000</td>
      <td>7101.000000</td>
      <td>3532.000000</td>
      <td>196392.000000</td>
      <td>77649.700000</td>
      <td>17903.300000</td>
      <td>17667.000000</td>
      <td>25327.400000</td>
      <td>7889.000000</td>
      <td>19880.177000</td>
      <td>16954.000000</td>
      <td>975.862000</td>
      <td>411.880000</td>
      <td>744.560000</td>
      <td>578.220000</td>
      <td>15396.771000</td>
      <td>3509.000000</td>
      <td>3596.000000</td>
      <td>822.241000</td>
      <td>18340.340000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# EV/EBITDA
filtered_data['Enterprise_Value'] = filtered_data['Market_Cap'] + filtered_data['Long-Term Debt'] - filtered_data['Cash and Equivalents']
filtered_data['EV/EBITDA'] = filtered_data['Enterprise_Value'] / filtered_data['EBITDA']
# P/E Ratio
filtered_data['EPS'] = filtered_data['Operating Income Before Depreciation'] / filtered_data['Common Shares Outstanding']
filtered_data['P/E'] = filtered_data['Avg_Price'] / filtered_data['EPS']
# Debt-to-Equity Ratio
filtered_data['Debt_to_Equity'] = filtered_data['Long-Term Debt'] / filtered_data['Common Equity']
# Return on Equity (ROE)
filtered_data['ROE'] = filtered_data['Operating Income Before Depreciation'] / filtered_data['Common Equity']
# Current Ratio
filtered_data['Current_Ratio'] = filtered_data['Total Assets'] / filtered_data['Current Liabilities']
# Quick Ratio
filtered_data['Quick_Ratio'] = (filtered_data['Total Assets'] - filtered_data['Inventory']) / filtered_data['Current Liabilities']
# Interest Covered Ratio
filtered_data['Interest_Coverage_Ratio'] = filtered_data['EBITDA'] / filtered_data['Interest Expense']
# Gross Margin
filtered_data['Gross_Margin'] = (filtered_data['Revenue'] - filtered_data['Cost of Goods Sold']) / filtered_data['Revenue']
# Operating Margin
filtered_data['Operating_Margin'] = filtered_data['Operating Income Before Depreciation'] / filtered_data['Revenue']
# Calculate Gross Profit
filtered_data['Gross Profit'] = filtered_data['Revenue'] - filtered_data['Cost of Goods Sold']
# Calculate Gross Profit Margin
filtered_data['Gross Profit Margin'] = (filtered_data['Gross Profit'] / filtered_data['Revenue']) 
#EV/GP 
filtered_data['EV/GP'] = filtered_data['Enterprise_Value'] / filtered_data['Gross Profit']
# Calculate EBITDA - Capex
filtered_data['EBITDA - Capex'] = filtered_data['EBITDA'] - filtered_data['Capital Expenditures']
# Calculate EBITDA - Capex margin
filtered_data['EBITDA - Capex Margin'] = (filtered_data['EBITDA - Capex'] / filtered_data['EBITDA']) 
filtered_data['EV/EBITDA-Capex'] = filtered_data['Enterprise_Value'] / filtered_data['EBITDA - Capex']
filtered_data['Free Cash Flow'] = (filtered_data['EBITDA']
                                   - filtered_data['Taxes']
                                   - filtered_data['Interest Expense']
                                   + (filtered_data['Current Assets'] - filtered_data['Current Liabilities'])
                                   - filtered_data['Capital Expenditures'])
filtered_data['FCF_Positive'] = (filtered_data['Free Cash Flow'] > 0).astype(int)
filtered_data['FCF Yield'] = filtered_data['Free Cash Flow'] / filtered_data['Market_Cap']
filtered_data['Invested_Capital'] = filtered_data['Long-Term Debt'] + filtered_data['Common Equity']
filtered_data['EBIT'] = filtered_data['Operating Income'] + filtered_data['Interest Expense'] + filtered_data['Taxes']
filtered_data['EV_EBIT'] = filtered_data['Enterprise_Value'] / filtered_data['EBIT']
filtered_data['ROIC'] = filtered_data['EBIT'] / filtered_data['Invested_Capital']
filtered_data['EBIT Margin (%)'] = (filtered_data['EBIT'] / filtered_data['Revenue']) 
filtered_data['EBIT_Positive'] = (filtered_data['EBIT'] > 0).astype(int)
filtered_data

filtered_data['Revenue per Employee'] = filtered_data['Revenue'] / filtered_data['Employees']

filtered_data['Total Debt Service'] = filtered_data['Long-Term Debt'] + filtered_data['Interest Expense']
filtered_data['Debt_Coverage_Ratio'] = filtered_data['Operating Income Before Depreciation'] / filtered_data['Total Debt Service']

filtered_data['Dividend (y/n)'] = (filtered_data['Dividends'] > 0).astype(int)

filtered_data['Price_Range_Ratio'] = (filtered_data['52-Week High Price'] - filtered_data['52-Week Low Price']) / filtered_data['52-Week Low Price']

filtered_data.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Market_Cap</th>
      <th>Fiscal Year</th>
      <th>Employees</th>
      <th>SP Index Code</th>
      <th>EBITDA</th>
      <th>Operating Income</th>
      <th>Dividends</th>
      <th>Long-Term Debt</th>
      <th>Research and Development Expenses</th>
      <th>Cost of Goods Sold</th>
      <th>Operating Income Before Depreciation</th>
      <th>Capital Expenditures</th>
      <th>Total Assets</th>
      <th>Revenue</th>
      <th>Selling, General, and Administrative Expenses</th>
      <th>Property, Plant, and Equipment Net</th>
      <th>Gross Property, Plant, and Equipment</th>
      <th>Cash and Equivalents</th>
      <th>Common Equity</th>
      <th>Current Liabilities</th>
      <th>Common Shares Outstanding</th>
      <th>52-Week Low Price</th>
      <th>52-Week High Price</th>
      <th>Avg_Price</th>
      <th>Inventory</th>
      <th>OpInc After Dep</th>
      <th>Interest Expense</th>
      <th>Taxes</th>
      <th>Current Assets</th>
      <th>Enterprise_Value</th>
      <th>EV/EBITDA</th>
      <th>EPS</th>
      <th>P/E</th>
      <th>Debt_to_Equity</th>
      <th>ROE</th>
      <th>Current_Ratio</th>
      <th>Quick_Ratio</th>
      <th>Interest_Coverage_Ratio</th>
      <th>Gross_Margin</th>
      <th>Operating_Margin</th>
      <th>Gross Profit</th>
      <th>Gross Profit Margin</th>
      <th>EV/GP</th>
      <th>EBITDA - Capex</th>
      <th>EBITDA - Capex Margin</th>
      <th>EV/EBITDA-Capex</th>
      <th>Free Cash Flow</th>
      <th>FCF_Positive</th>
      <th>FCF Yield</th>
      <th>Invested_Capital</th>
      <th>EBIT</th>
      <th>EV_EBIT</th>
      <th>ROIC</th>
      <th>EBIT Margin (%)</th>
      <th>EBIT_Positive</th>
      <th>Revenue per Employee</th>
      <th>Total Debt Service</th>
      <th>Debt_Coverage_Ratio</th>
      <th>Dividend (y/n)</th>
      <th>Price_Range_Ratio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
      <td>1865.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2565.155154</td>
      <td>9.635925</td>
      <td>12.313823</td>
      <td>4672.390885</td>
      <td>345.178820</td>
      <td>1477.291645</td>
      <td>28.439949</td>
      <td>2500.088561</td>
      <td>28.863912</td>
      <td>2378.094880</td>
      <td>345.178820</td>
      <td>99.539855</td>
      <td>3595.068219</td>
      <td>3230.708273</td>
      <td>507.434573</td>
      <td>932.470596</td>
      <td>1587.643820</td>
      <td>312.607887</td>
      <td>1009.996287</td>
      <td>671.269804</td>
      <td>67.036041</td>
      <td>34.127066</td>
      <td>65.607911</td>
      <td>49.867488</td>
      <td>481.058678</td>
      <td>236.122276</td>
      <td>66.140315</td>
      <td>34.307699</td>
      <td>1025.857042</td>
      <td>4752.635828</td>
      <td>27.859417</td>
      <td>6.509927</td>
      <td>19.133466</td>
      <td>inf</td>
      <td>inf</td>
      <td>inf</td>
      <td>inf</td>
      <td>inf</td>
      <td>0.346948</td>
      <td>0.141160</td>
      <td>852.613393</td>
      <td>0.346948</td>
      <td>7.056712</td>
      <td>245.638965</td>
      <td>0.503061</td>
      <td>-219.022422</td>
      <td>499.778189</td>
      <td>0.900268</td>
      <td>0.274336</td>
      <td>3510.084848</td>
      <td>1577.739658</td>
      <td>27.361607</td>
      <td>0.487102</td>
      <td>0.599242</td>
      <td>0.971582</td>
      <td>inf</td>
      <td>2566.228876</td>
      <td>inf</td>
      <td>0.467024</td>
      <td>17.122326</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2717.436271</td>
      <td>3.803079</td>
      <td>23.895366</td>
      <td>2077.657616</td>
      <td>520.606361</td>
      <td>4531.653675</td>
      <td>115.608116</td>
      <td>7288.660880</td>
      <td>88.376601</td>
      <td>4699.410975</td>
      <td>520.606361</td>
      <td>209.489278</td>
      <td>8327.620485</td>
      <td>5782.312996</td>
      <td>980.975527</td>
      <td>1849.034995</td>
      <td>2875.506466</td>
      <td>558.295577</td>
      <td>1417.690558</td>
      <td>1272.459096</td>
      <td>76.138807</td>
      <td>40.416148</td>
      <td>69.069401</td>
      <td>53.981649</td>
      <td>1115.464011</td>
      <td>373.130720</td>
      <td>182.130914</td>
      <td>82.780385</td>
      <td>1604.366533</td>
      <td>8140.491497</td>
      <td>118.632207</td>
      <td>9.047061</td>
      <td>93.089335</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.170307</td>
      <td>0.116370</td>
      <td>1320.881132</td>
      <td>0.170307</td>
      <td>6.457370</td>
      <td>395.059082</td>
      <td>2.194795</td>
      <td>10224.621665</td>
      <td>731.365411</td>
      <td>0.299723</td>
      <td>0.449700</td>
      <td>7986.258189</td>
      <td>4572.030232</td>
      <td>316.553944</td>
      <td>0.885960</td>
      <td>1.181264</td>
      <td>0.166209</td>
      <td>NaN</td>
      <td>7408.694022</td>
      <td>NaN</td>
      <td>0.499045</td>
      <td>618.010442</td>
    </tr>
    <tr>
      <th>min</th>
      <td>101.146145</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.188000</td>
      <td>0.000000</td>
      <td>-1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>4.088000</td>
      <td>0.188000</td>
      <td>0.000000</td>
      <td>20.175000</td>
      <td>13.895000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.043000</td>
      <td>-5921.471000</td>
      <td>0.000000</td>
      <td>0.585000</td>
      <td>0.001100</td>
      <td>2.190000</td>
      <td>1.405000</td>
      <td>0.000000</td>
      <td>-664.927000</td>
      <td>-41.133000</td>
      <td>-888.000000</td>
      <td>0.000000</td>
      <td>54.331145</td>
      <td>1.979820</td>
      <td>0.003847</td>
      <td>0.182750</td>
      <td>-2130.757991</td>
      <td>-483.593607</td>
      <td>0.791179</td>
      <td>0.598083</td>
      <td>-13.430188</td>
      <td>0.026388</td>
      <td>0.000714</td>
      <td>4.021000</td>
      <td>0.026388</td>
      <td>0.833274</td>
      <td>-1019.808000</td>
      <td>-76.922662</td>
      <td>-441118.500000</td>
      <td>-5275.209000</td>
      <td>0.000000</td>
      <td>-8.210014</td>
      <td>-533.578000</td>
      <td>-236.000000</td>
      <td>-6509.207271</td>
      <td>-0.273923</td>
      <td>-0.209345</td>
      <td>0.000000</td>
      <td>21.764279</td>
      <td>0.000000</td>
      <td>0.000719</td>
      <td>0.000000</td>
      <td>0.162122</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>567.022015</td>
      <td>9.000000</td>
      <td>1.767000</td>
      <td>3530.000000</td>
      <td>62.692000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>372.338000</td>
      <td>0.000000</td>
      <td>355.933000</td>
      <td>62.692000</td>
      <td>12.632000</td>
      <td>729.140000</td>
      <td>589.837000</td>
      <td>104.000000</td>
      <td>110.875000</td>
      <td>224.554000</td>
      <td>45.739000</td>
      <td>225.870000</td>
      <td>101.391000</td>
      <td>23.974000</td>
      <td>8.900000</td>
      <td>22.090000</td>
      <td>15.810000</td>
      <td>22.616000</td>
      <td>29.700000</td>
      <td>3.198000</td>
      <td>1.748000</td>
      <td>197.934000</td>
      <td>1030.996235</td>
      <td>10.338713</td>
      <td>1.826904</td>
      <td>5.218299</td>
      <td>0.708665</td>
      <td>0.145940</td>
      <td>3.608758</td>
      <td>3.016625</td>
      <td>4.253580</td>
      <td>0.219589</td>
      <td>0.071429</td>
      <td>200.158000</td>
      <td>0.219589</td>
      <td>3.552688</td>
      <td>33.336000</td>
      <td>0.557183</td>
      <td>11.655423</td>
      <td>92.655000</td>
      <td>1.000000</td>
      <td>0.095800</td>
      <td>703.162000</td>
      <td>52.805000</td>
      <td>2.094525</td>
      <td>0.033782</td>
      <td>0.032250</td>
      <td>1.000000</td>
      <td>188.365341</td>
      <td>378.120000</td>
      <td>0.104835</td>
      <td>0.000000</td>
      <td>0.610333</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1467.084995</td>
      <td>12.000000</td>
      <td>4.850000</td>
      <td>3845.000000</td>
      <td>178.222000</td>
      <td>117.873000</td>
      <td>0.000000</td>
      <td>1007.659000</td>
      <td>0.000000</td>
      <td>910.268000</td>
      <td>178.222000</td>
      <td>37.079000</td>
      <td>1755.084000</td>
      <td>1460.860000</td>
      <td>226.903000</td>
      <td>306.543000</td>
      <td>581.100000</td>
      <td>136.316000</td>
      <td>604.900000</td>
      <td>289.300000</td>
      <td>44.384000</td>
      <td>20.150000</td>
      <td>43.700000</td>
      <td>32.048200</td>
      <td>136.026000</td>
      <td>111.100000</td>
      <td>19.200000</td>
      <td>14.900000</td>
      <td>515.363000</td>
      <td>2665.485400</td>
      <td>14.390089</td>
      <td>4.123477</td>
      <td>8.841054</td>
      <td>1.260540</td>
      <td>0.238687</td>
      <td>5.159945</td>
      <td>4.497330</td>
      <td>9.379161</td>
      <td>0.323335</td>
      <td>0.117951</td>
      <td>457.231000</td>
      <td>0.323335</td>
      <td>5.521435</td>
      <td>120.700000</td>
      <td>0.768368</td>
      <td>17.567498</td>
      <td>287.804000</td>
      <td>1.000000</td>
      <td>0.208952</td>
      <td>1714.947000</td>
      <td>256.225000</td>
      <td>7.448310</td>
      <td>0.181428</td>
      <td>0.238174</td>
      <td>1.000000</td>
      <td>294.510407</td>
      <td>1037.879000</td>
      <td>0.168546</td>
      <td>0.000000</td>
      <td>0.957360</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>3671.073840</td>
      <td>12.000000</td>
      <td>13.000000</td>
      <td>5900.000000</td>
      <td>442.800000</td>
      <td>904.600000</td>
      <td>25.241000</td>
      <td>2461.595000</td>
      <td>16.500000</td>
      <td>2360.575000</td>
      <td>442.800000</td>
      <td>101.910000</td>
      <td>3864.920000</td>
      <td>3369.810000</td>
      <td>512.817000</td>
      <td>910.730000</td>
      <td>1650.864000</td>
      <td>342.528000</td>
      <td>1307.748000</td>
      <td>692.904000</td>
      <td>82.450000</td>
      <td>43.125000</td>
      <td>84.840000</td>
      <td>64.350000</td>
      <td>414.077000</td>
      <td>306.397000</td>
      <td>60.000000</td>
      <td>49.418000</td>
      <td>1187.672000</td>
      <td>5900.629650</td>
      <td>20.935576</td>
      <td>7.642744</td>
      <td>14.413687</td>
      <td>2.367176</td>
      <td>0.382670</td>
      <td>7.806976</td>
      <td>7.039109</td>
      <td>27.482591</td>
      <td>0.438664</td>
      <td>0.172881</td>
      <td>1019.600000</td>
      <td>0.438664</td>
      <td>8.576277</td>
      <td>319.000000</td>
      <td>0.881882</td>
      <td>28.045192</td>
      <td>672.243000</td>
      <td>1.000000</td>
      <td>0.386244</td>
      <td>3861.330000</td>
      <td>981.500000</td>
      <td>37.576915</td>
      <td>0.560254</td>
      <td>0.708807</td>
      <td>1.000000</td>
      <td>461.794066</td>
      <td>2512.600000</td>
      <td>0.265464</td>
      <td>1.000000</td>
      <td>1.672507</td>
    </tr>
    <tr>
      <th>max</th>
      <td>16531.765360</td>
      <td>12.000000</td>
      <td>300.000000</td>
      <td>9997.000000</td>
      <td>7101.000000</td>
      <td>48600.000000</td>
      <td>4207.700000</td>
      <td>182626.000000</td>
      <td>1144.400000</td>
      <td>55731.400000</td>
      <td>7101.000000</td>
      <td>3532.000000</td>
      <td>196392.000000</td>
      <td>77649.700000</td>
      <td>17903.300000</td>
      <td>17667.000000</td>
      <td>25327.400000</td>
      <td>7889.000000</td>
      <td>19880.177000</td>
      <td>16954.000000</td>
      <td>975.862000</td>
      <td>411.880000</td>
      <td>744.560000</td>
      <td>578.220000</td>
      <td>15396.771000</td>
      <td>3509.000000</td>
      <td>3596.000000</td>
      <td>822.241000</td>
      <td>18340.340000</td>
      <td>184019.754540</td>
      <td>3042.196552</td>
      <td>121.549714</td>
      <td>3071.858621</td>
      <td>inf</td>
      <td>inf</td>
      <td>inf</td>
      <td>inf</td>
      <td>inf</td>
      <td>0.960150</td>
      <td>0.930629</td>
      <td>21918.300000</td>
      <td>0.960150</td>
      <td>96.396181</td>
      <td>4813.000000</td>
      <td>1.000000</td>
      <td>6594.331528</td>
      <td>7473.177000</td>
      <td>1.000000</td>
      <td>6.303995</td>
      <td>194068.000000</td>
      <td>48929.100000</td>
      <td>6556.449349</td>
      <td>10.767444</td>
      <td>21.560327</td>
      <td>1.000000</td>
      <td>inf</td>
      <td>183704.000000</td>
      <td>inf</td>
      <td>1.000000</td>
      <td>26653.545455</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Group the data by "Ticker" and sort by "Fiscal Year"
grouped_data = filtered_data.sort_values(by=['Ticker', 'Fiscal Year']).groupby('Ticker')

# Calculate year-over-year changes in margins
filtered_data['YOY_Gross_Margin_Change'] = grouped_data['Gross_Margin'].pct_change()
filtered_data['YOY_EBIT_Margin_Change'] = grouped_data['EBIT Margin (%)'].pct_change()
filtered_data['YOY_Operating_Margin_Change'] = grouped_data['Operating_Margin'].pct_change()
filtered_data['YOY_Gross_Profit_Change'] = grouped_data['Gross Profit'].pct_change()
filtered_data['YOY_Revenue_Change'] = grouped_data['Revenue'].pct_change()
filtered_data['YOY_EBIT_Change'] = grouped_data['EBIT'].pct_change()
filtered_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Ticker</th>
      <th>Company Name</th>
      <th>Market_Cap</th>
      <th>Fiscal Date</th>
      <th>Fiscal Year</th>
      <th>Employees</th>
      <th>SP Index Code</th>
      <th>EBITDA</th>
      <th>Operating Income</th>
      <th>Dividends</th>
      <th>Long-Term Debt</th>
      <th>Research and Development Expenses</th>
      <th>Cost of Goods Sold</th>
      <th>Operating Income Before Depreciation</th>
      <th>Capital Expenditures</th>
      <th>Total Assets</th>
      <th>Revenue</th>
      <th>Selling, General, and Administrative Expenses</th>
      <th>Property, Plant, and Equipment Net</th>
      <th>Gross Property, Plant, and Equipment</th>
      <th>Cash and Equivalents</th>
      <th>Common Equity</th>
      <th>Current Liabilities</th>
      <th>Common Shares Outstanding</th>
      <th>52-Week Low Price</th>
      <th>52-Week High Price</th>
      <th>Avg_Price</th>
      <th>Inventory</th>
      <th>OpInc After Dep</th>
      <th>Interest Expense</th>
      <th>Taxes</th>
      <th>Current Assets</th>
      <th>Enterprise_Value</th>
      <th>EV/EBITDA</th>
      <th>EPS</th>
      <th>P/E</th>
      <th>Debt_to_Equity</th>
      <th>ROE</th>
      <th>Current_Ratio</th>
      <th>Quick_Ratio</th>
      <th>Interest_Coverage_Ratio</th>
      <th>Gross_Margin</th>
      <th>Operating_Margin</th>
      <th>Gross Profit</th>
      <th>Gross Profit Margin</th>
      <th>EV/GP</th>
      <th>EBITDA - Capex</th>
      <th>EBITDA - Capex Margin</th>
      <th>EV/EBITDA-Capex</th>
      <th>Free Cash Flow</th>
      <th>FCF_Positive</th>
      <th>FCF Yield</th>
      <th>Invested_Capital</th>
      <th>EBIT</th>
      <th>EV_EBIT</th>
      <th>ROIC</th>
      <th>EBIT Margin (%)</th>
      <th>EBIT_Positive</th>
      <th>Revenue per Employee</th>
      <th>Total Debt Service</th>
      <th>Debt_Coverage_Ratio</th>
      <th>Dividend (y/n)</th>
      <th>Price_Range_Ratio</th>
      <th>YOY_Gross_Margin_Change</th>
      <th>YOY_EBIT_Margin_Change</th>
      <th>YOY_Operating_Margin_Change</th>
      <th>YOY_Gross_Profit_Change</th>
      <th>YOY_Revenue_Change</th>
      <th>YOY_EBIT_Change</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AIR</td>
      <td>AAR CORP</td>
      <td>1000.228125</td>
      <td>2021-07-22 00:00:00</td>
      <td>5</td>
      <td>4.700</td>
      <td>5080.0</td>
      <td>101.800</td>
      <td>750.0</td>
      <td>0.1</td>
      <td>565.300</td>
      <td>0.0</td>
      <td>1364.600</td>
      <td>101.800</td>
      <td>11.300</td>
      <td>1539.700</td>
      <td>1651.400</td>
      <td>185.000</td>
      <td>380.100</td>
      <td>640.300</td>
      <td>60.200</td>
      <td>974.400</td>
      <td>336.800</td>
      <td>35.375</td>
      <td>8.560</td>
      <td>47.99</td>
      <td>28.2750</td>
      <td>591.000</td>
      <td>65.500</td>
      <td>5.000</td>
      <td>18.200</td>
      <td>937.000</td>
      <td>1505.328125</td>
      <td>14.787113</td>
      <td>2.877739</td>
      <td>9.825424</td>
      <td>0.580152</td>
      <td>0.104475</td>
      <td>4.571556</td>
      <td>2.816805</td>
      <td>20.360000</td>
      <td>0.173671</td>
      <td>0.061645</td>
      <td>286.80</td>
      <td>0.173671</td>
      <td>5.248703</td>
      <td>90.500</td>
      <td>0.888998</td>
      <td>16.633460</td>
      <td>667.500</td>
      <td>1</td>
      <td>0.667348</td>
      <td>1539.700</td>
      <td>773.200</td>
      <td>1.946881</td>
      <td>0.502176</td>
      <td>0.468209</td>
      <td>1</td>
      <td>351.361702</td>
      <td>570.300</td>
      <td>0.178503</td>
      <td>1</td>
      <td>4.606308</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AIR</td>
      <td>AAR CORP</td>
      <td>1351.759245</td>
      <td>2022-07-22 00:00:00</td>
      <td>5</td>
      <td>4.500</td>
      <td>5080.0</td>
      <td>149.300</td>
      <td>850.0</td>
      <td>0.0</td>
      <td>539.400</td>
      <td>0.0</td>
      <td>1470.300</td>
      <td>149.300</td>
      <td>17.300</td>
      <td>1573.900</td>
      <td>1817.100</td>
      <td>197.500</td>
      <td>349.200</td>
      <td>607.500</td>
      <td>58.900</td>
      <td>1034.500</td>
      <td>348.200</td>
      <td>35.391</td>
      <td>30.900</td>
      <td>45.49</td>
      <td>38.1950</td>
      <td>604.100</td>
      <td>116.200</td>
      <td>2.400</td>
      <td>26.600</td>
      <td>1007.200</td>
      <td>1832.259245</td>
      <td>12.272333</td>
      <td>4.218587</td>
      <td>9.053980</td>
      <td>0.521411</td>
      <td>0.144321</td>
      <td>4.520103</td>
      <td>2.785181</td>
      <td>62.208333</td>
      <td>0.190854</td>
      <td>0.082164</td>
      <td>346.80</td>
      <td>0.190854</td>
      <td>5.283331</td>
      <td>132.000</td>
      <td>0.884126</td>
      <td>13.880752</td>
      <td>762.000</td>
      <td>1</td>
      <td>0.563710</td>
      <td>1573.900</td>
      <td>879.000</td>
      <td>2.084482</td>
      <td>0.558485</td>
      <td>0.483738</td>
      <td>1</td>
      <td>403.800000</td>
      <td>541.800</td>
      <td>0.275563</td>
      <td>0</td>
      <td>0.472168</td>
      <td>0.098939</td>
      <td>0.033167</td>
      <td>0.332863</td>
      <td>0.209205</td>
      <td>0.100339</td>
      <td>0.136834</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AIR</td>
      <td>AAR CORP</td>
      <td>1511.513640</td>
      <td>2023-07-21 00:00:00</td>
      <td>5</td>
      <td>5.000</td>
      <td>5080.0</td>
      <td>179.300</td>
      <td>740.0</td>
      <td>0.0</td>
      <td>734.000</td>
      <td>0.0</td>
      <td>1591.300</td>
      <td>179.300</td>
      <td>29.500</td>
      <td>1833.100</td>
      <td>1990.600</td>
      <td>220.000</td>
      <td>367.900</td>
      <td>636.700</td>
      <td>81.800</td>
      <td>1099.100</td>
      <td>351.500</td>
      <td>34.916</td>
      <td>33.750</td>
      <td>52.83</td>
      <td>43.2900</td>
      <td>624.700</td>
      <td>151.400</td>
      <td>12.200</td>
      <td>31.400</td>
      <td>1097.900</td>
      <td>2163.713640</td>
      <td>12.067561</td>
      <td>5.135182</td>
      <td>8.430082</td>
      <td>0.667819</td>
      <td>0.163133</td>
      <td>5.215078</td>
      <td>3.437838</td>
      <td>14.696721</td>
      <td>0.200593</td>
      <td>0.090073</td>
      <td>399.30</td>
      <td>0.200593</td>
      <td>5.418767</td>
      <td>149.800</td>
      <td>0.835471</td>
      <td>14.444016</td>
      <td>852.600</td>
      <td>1</td>
      <td>0.564070</td>
      <td>1833.100</td>
      <td>783.600</td>
      <td>2.761248</td>
      <td>0.427473</td>
      <td>0.393650</td>
      <td>1</td>
      <td>398.120000</td>
      <td>746.200</td>
      <td>0.240284</td>
      <td>0</td>
      <td>0.565333</td>
      <td>0.051030</td>
      <td>-0.186232</td>
      <td>0.096264</td>
      <td>0.151384</td>
      <td>0.095482</td>
      <td>-0.108532</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CECO</td>
      <td>CECO ENVIRONMENTAL CORP</td>
      <td>221.591938</td>
      <td>2021-04-01 00:00:00</td>
      <td>12</td>
      <td>0.730</td>
      <td>3564.0</td>
      <td>30.514</td>
      <td>183.1</td>
      <td>0.0</td>
      <td>215.703</td>
      <td>0.0</td>
      <td>208.571</td>
      <td>30.514</td>
      <td>3.945</td>
      <td>419.314</td>
      <td>316.011</td>
      <td>76.926</td>
      <td>27.604</td>
      <td>45.909</td>
      <td>37.811</td>
      <td>202.658</td>
      <td>109.356</td>
      <td>35.367</td>
      <td>3.531</td>
      <td>9.00</td>
      <td>6.2655</td>
      <td>62.841</td>
      <td>20.593</td>
      <td>3.535</td>
      <td>3.672</td>
      <td>183.485</td>
      <td>399.483939</td>
      <td>13.091825</td>
      <td>0.862782</td>
      <td>7.261976</td>
      <td>1.064370</td>
      <td>0.150569</td>
      <td>3.834394</td>
      <td>3.259748</td>
      <td>8.631966</td>
      <td>0.339988</td>
      <td>0.096560</td>
      <td>107.44</td>
      <td>0.339988</td>
      <td>3.718205</td>
      <td>26.569</td>
      <td>0.870715</td>
      <td>15.035716</td>
      <td>93.491</td>
      <td>1</td>
      <td>0.421906</td>
      <td>418.361</td>
      <td>190.307</td>
      <td>2.099155</td>
      <td>0.454887</td>
      <td>0.602216</td>
      <td>1</td>
      <td>432.891781</td>
      <td>219.238</td>
      <td>0.139182</td>
      <td>0</td>
      <td>1.548853</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CECO</td>
      <td>CECO ENVIRONMENTAL CORP</td>
      <td>266.913360</td>
      <td>2022-04-10 00:00:00</td>
      <td>12</td>
      <td>0.730</td>
      <td>3564.0</td>
      <td>21.893</td>
      <td>213.9</td>
      <td>0.0</td>
      <td>210.240</td>
      <td>0.0</td>
      <td>220.450</td>
      <td>21.893</td>
      <td>2.616</td>
      <td>416.197</td>
      <td>324.140</td>
      <td>81.797</td>
      <td>26.841</td>
      <td>47.723</td>
      <td>31.995</td>
      <td>204.554</td>
      <td>116.685</td>
      <td>35.028</td>
      <td>5.770</td>
      <td>9.47</td>
      <td>7.6200</td>
      <td>68.481</td>
      <td>12.040</td>
      <td>2.952</td>
      <td>2.691</td>
      <td>189.011</td>
      <td>445.158360</td>
      <td>20.333365</td>
      <td>0.625014</td>
      <td>12.191722</td>
      <td>1.027797</td>
      <td>0.107028</td>
      <td>3.566842</td>
      <td>2.979955</td>
      <td>7.416328</td>
      <td>0.319893</td>
      <td>0.067542</td>
      <td>103.69</td>
      <td>0.319893</td>
      <td>4.293166</td>
      <td>19.277</td>
      <td>0.880510</td>
      <td>23.092720</td>
      <td>85.960</td>
      <td>1</td>
      <td>0.322052</td>
      <td>414.794</td>
      <td>219.543</td>
      <td>2.027659</td>
      <td>0.529282</td>
      <td>0.677309</td>
      <td>1</td>
      <td>444.027397</td>
      <td>213.192</td>
      <td>0.102691</td>
      <td>0</td>
      <td>0.641248</td>
      <td>-0.059107</td>
      <td>0.124694</td>
      <td>-0.300519</td>
      <td>-0.034903</td>
      <td>0.025724</td>
      <td>0.153625</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>21898</th>
      <td>NVT</td>
      <td>NVENT ELECTRIC PLC</td>
      <td>8013.274605</td>
      <td>2024-03-04 00:00:00</td>
      <td>12</td>
      <td>11.300</td>
      <td>3440.0</td>
      <td>772.300</td>
      <td>639.1</td>
      <td>119.7</td>
      <td>3019.600</td>
      <td>71.5</td>
      <td>1762.400</td>
      <td>772.300</td>
      <td>71.000</td>
      <td>6161.700</td>
      <td>3263.600</td>
      <td>728.900</td>
      <td>508.700</td>
      <td>1012.500</td>
      <td>185.100</td>
      <td>3142.100</td>
      <td>733.600</td>
      <td>165.069</td>
      <td>37.510</td>
      <td>59.58</td>
      <td>48.5450</td>
      <td>485.400</td>
      <td>630.900</td>
      <td>79.400</td>
      <td>-67.600</td>
      <td>1336.100</td>
      <td>10847.774605</td>
      <td>14.046063</td>
      <td>4.678650</td>
      <td>10.375857</td>
      <td>0.961013</td>
      <td>0.245791</td>
      <td>8.399264</td>
      <td>7.737595</td>
      <td>9.726700</td>
      <td>0.459983</td>
      <td>0.236641</td>
      <td>1501.20</td>
      <td>0.459983</td>
      <td>7.226069</td>
      <td>701.300</td>
      <td>0.908067</td>
      <td>15.468094</td>
      <td>1292.000</td>
      <td>1</td>
      <td>0.161232</td>
      <td>6161.700</td>
      <td>650.900</td>
      <td>16.665808</td>
      <td>0.105636</td>
      <td>0.199442</td>
      <td>1</td>
      <td>288.814159</td>
      <td>3099.000</td>
      <td>0.249209</td>
      <td>1</td>
      <td>0.588376</td>
      <td>0.105038</td>
      <td>-0.184342</td>
      <td>0.225324</td>
      <td>0.239739</td>
      <td>0.121898</td>
      <td>-0.084915</td>
    </tr>
    <tr>
      <th>21909</th>
      <td>ACA</td>
      <td>ARCOSA INC</td>
      <td>2058.140000</td>
      <td>2021-03-06 00:00:00</td>
      <td>12</td>
      <td>6.410</td>
      <td>3440.0</td>
      <td>283.700</td>
      <td>525.1</td>
      <td>9.8</td>
      <td>754.500</td>
      <td>0.0</td>
      <td>1428.800</td>
      <td>283.700</td>
      <td>82.100</td>
      <td>2646.700</td>
      <td>1935.600</td>
      <td>223.100</td>
      <td>931.200</td>
      <td>1612.500</td>
      <td>95.800</td>
      <td>1892.200</td>
      <td>310.300</td>
      <td>48.200</td>
      <td>28.140</td>
      <td>57.26</td>
      <td>42.7000</td>
      <td>276.800</td>
      <td>169.200</td>
      <td>10.600</td>
      <td>31.600</td>
      <td>664.900</td>
      <td>2716.840000</td>
      <td>9.576454</td>
      <td>5.885892</td>
      <td>7.254635</td>
      <td>0.398742</td>
      <td>0.149931</td>
      <td>8.529488</td>
      <td>7.637448</td>
      <td>26.764151</td>
      <td>0.261831</td>
      <td>0.146570</td>
      <td>506.80</td>
      <td>0.261831</td>
      <td>5.360773</td>
      <td>201.600</td>
      <td>0.710610</td>
      <td>13.476389</td>
      <td>514.000</td>
      <td>1</td>
      <td>0.249740</td>
      <td>2646.700</td>
      <td>567.300</td>
      <td>4.789071</td>
      <td>0.214342</td>
      <td>0.293087</td>
      <td>1</td>
      <td>301.965679</td>
      <td>765.100</td>
      <td>0.370801</td>
      <td>1</td>
      <td>1.034826</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21910</th>
      <td>ACA</td>
      <td>ARCOSA INC</td>
      <td>2804.056500</td>
      <td>2022-03-11 00:00:00</td>
      <td>12</td>
      <td>6.170</td>
      <td>3440.0</td>
      <td>267.000</td>
      <td>552.2</td>
      <td>9.8</td>
      <td>1234.800</td>
      <td>0.0</td>
      <td>1525.900</td>
      <td>267.000</td>
      <td>85.100</td>
      <td>3188.100</td>
      <td>2028.700</td>
      <td>235.800</td>
      <td>1222.800</td>
      <td>1985.800</td>
      <td>72.900</td>
      <td>1953.300</td>
      <td>364.000</td>
      <td>48.300</td>
      <td>47.650</td>
      <td>68.46</td>
      <td>58.0550</td>
      <td>324.500</td>
      <td>122.700</td>
      <td>23.400</td>
      <td>14.000</td>
      <td>767.900</td>
      <td>3965.956500</td>
      <td>14.853770</td>
      <td>5.527950</td>
      <td>10.502084</td>
      <td>0.632161</td>
      <td>0.136692</td>
      <td>8.758516</td>
      <td>7.867033</td>
      <td>11.410256</td>
      <td>0.247843</td>
      <td>0.131611</td>
      <td>502.80</td>
      <td>0.247843</td>
      <td>7.887742</td>
      <td>181.900</td>
      <td>0.681273</td>
      <td>21.802949</td>
      <td>548.400</td>
      <td>1</td>
      <td>0.195574</td>
      <td>3188.100</td>
      <td>589.600</td>
      <td>6.726521</td>
      <td>0.184938</td>
      <td>0.290629</td>
      <td>1</td>
      <td>328.800648</td>
      <td>1258.200</td>
      <td>0.212208</td>
      <td>1</td>
      <td>0.436726</td>
      <td>-0.053422</td>
      <td>-0.008386</td>
      <td>-0.102055</td>
      <td>-0.007893</td>
      <td>0.048099</td>
      <td>0.039309</td>
    </tr>
    <tr>
      <th>21911</th>
      <td>ACA</td>
      <td>ARCOSA INC</td>
      <td>2643.124000</td>
      <td>2023-03-06 00:00:00</td>
      <td>12</td>
      <td>5.230</td>
      <td>3440.0</td>
      <td>324.500</td>
      <td>896.4</td>
      <td>9.8</td>
      <td>1156.200</td>
      <td>0.0</td>
      <td>1665.900</td>
      <td>324.500</td>
      <td>138.000</td>
      <td>3340.600</td>
      <td>2242.800</td>
      <td>252.400</td>
      <td>1233.500</td>
      <td>2044.800</td>
      <td>160.400</td>
      <td>2184.400</td>
      <td>367.700</td>
      <td>48.400</td>
      <td>43.420</td>
      <td>65.80</td>
      <td>54.6100</td>
      <td>315.800</td>
      <td>170.400</td>
      <td>31.000</td>
      <td>70.400</td>
      <td>856.800</td>
      <td>3638.924000</td>
      <td>11.213941</td>
      <td>6.704545</td>
      <td>8.145220</td>
      <td>0.529299</td>
      <td>0.148553</td>
      <td>9.085124</td>
      <td>8.226271</td>
      <td>10.467742</td>
      <td>0.257223</td>
      <td>0.144685</td>
      <td>576.90</td>
      <td>0.257223</td>
      <td>6.307721</td>
      <td>186.500</td>
      <td>0.574730</td>
      <td>19.511657</td>
      <td>574.200</td>
      <td>1</td>
      <td>0.217243</td>
      <td>3340.600</td>
      <td>997.800</td>
      <td>3.646947</td>
      <td>0.298689</td>
      <td>0.444890</td>
      <td>1</td>
      <td>428.833652</td>
      <td>1187.200</td>
      <td>0.273332</td>
      <td>1</td>
      <td>0.515431</td>
      <td>0.037845</td>
      <td>0.530782</td>
      <td>0.099337</td>
      <td>0.147375</td>
      <td>0.105536</td>
      <td>0.692334</td>
    </tr>
    <tr>
      <th>21912</th>
      <td>ACA</td>
      <td>ARCOSA INC</td>
      <td>3310.875000</td>
      <td>2024-03-01 00:00:00</td>
      <td>12</td>
      <td>6.075</td>
      <td>3440.0</td>
      <td>339.400</td>
      <td>1621.2</td>
      <td>9.8</td>
      <td>1245.900</td>
      <td>0.0</td>
      <td>1709.600</td>
      <td>339.400</td>
      <td>203.500</td>
      <td>3577.900</td>
      <td>2307.900</td>
      <td>258.900</td>
      <td>1373.000</td>
      <td>2305.900</td>
      <td>104.800</td>
      <td>2332.000</td>
      <td>431.200</td>
      <td>48.600</td>
      <td>52.040</td>
      <td>84.21</td>
      <td>68.1250</td>
      <td>401.800</td>
      <td>179.900</td>
      <td>28.100</td>
      <td>36.700</td>
      <td>912.000</td>
      <td>4451.975000</td>
      <td>13.117192</td>
      <td>6.983539</td>
      <td>9.755082</td>
      <td>0.534262</td>
      <td>0.145540</td>
      <td>8.297542</td>
      <td>7.365724</td>
      <td>12.078292</td>
      <td>0.259240</td>
      <td>0.147060</td>
      <td>598.30</td>
      <td>0.259240</td>
      <td>7.441041</td>
      <td>135.900</td>
      <td>0.400412</td>
      <td>32.759198</td>
      <td>551.900</td>
      <td>1</td>
      <td>0.166693</td>
      <td>3577.900</td>
      <td>1686.000</td>
      <td>2.640555</td>
      <td>0.471226</td>
      <td>0.730534</td>
      <td>1</td>
      <td>379.901235</td>
      <td>1274.000</td>
      <td>0.266405</td>
      <td>1</td>
      <td>0.618178</td>
      <td>0.007841</td>
      <td>0.642055</td>
      <td>0.016414</td>
      <td>0.037095</td>
      <td>0.029026</td>
      <td>0.689717</td>
    </tr>
  </tbody>
</table>
<p>1865 rows × 69 columns</p>
</div>




```python
# Define a function to map SP Index Codes to divisions
def map_sp_index_to_division(sp_index_code):
    if sp_index_code >= 100 and sp_index_code <= 999:
        return 'Agriculture, Forestry and Fishing'
    elif sp_index_code >= 1000 and sp_index_code <= 1499:
        return 'Mining'
    elif sp_index_code >= 1500 and sp_index_code <= 1799:
        return 'Construction'
    elif sp_index_code >= 2000 and sp_index_code <= 3999:
        return 'Manufacturing'
    elif sp_index_code >= 4000 and sp_index_code <= 4999:
        return 'Transportation, Communications, Electric, Gas and Sanitary service'
    elif sp_index_code >= 5000 and sp_index_code <= 5199:
        return 'Wholesale Trade'
    elif sp_index_code >= 5200 and sp_index_code <= 5999:
        return 'Retail Trade'
    elif sp_index_code >= 6000 and sp_index_code <= 6799:
        return 'Finance, Insurance and Real Estate'
    elif sp_index_code >= 7000 and sp_index_code <= 8999:
        return 'Services'
    elif sp_index_code >= 9100 and sp_index_code <= 9729:
        return 'Public Administration'
    elif sp_index_code >= 9900 and sp_index_code <= 9999:
        return 'Nonclassifiable'
    else:
        return 'Unknown'

# Add a new column 'Division' based on 'SP Index Code'
filtered_data['Division'] = filtered_data['SP Index Code'].apply(map_sp_index_to_division)

```


```python
# Select columns of interest
selected_columns = ['Ticker', 'EV/EBITDA', 'P/E', 'EV_EBIT','Debt_to_Equity', 'ROE','FCF_Positive', 'FCF Yield', 'ROIC','Debt_Coverage_Ratio','Division',
                    'Current_Ratio', 'Quick_Ratio', 'Interest_Coverage_Ratio', 'Gross_Margin', 'Dividend (y/n)','Revenue per Employee',
                    'Operating_Margin', 'EV/GP' , 'EBIT Margin (%)', 'EV/EBITDA-Capex','YOY_Gross_Margin_Change', 'YOY_EBIT_Margin_Change','Price_Range_Ratio',
                    'YOY_Operating_Margin_Change', 'YOY_Gross_Profit_Change', 'YOY_Revenue_Change','YOY_EBIT_Change']

# Create a new DataFrame with selected columns
selected_df = filtered_data[selected_columns]
selected_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Ticker</th>
      <th>EV/EBITDA</th>
      <th>P/E</th>
      <th>EV_EBIT</th>
      <th>Debt_to_Equity</th>
      <th>ROE</th>
      <th>FCF_Positive</th>
      <th>FCF Yield</th>
      <th>ROIC</th>
      <th>Debt_Coverage_Ratio</th>
      <th>Division</th>
      <th>Current_Ratio</th>
      <th>Quick_Ratio</th>
      <th>Interest_Coverage_Ratio</th>
      <th>Gross_Margin</th>
      <th>Dividend (y/n)</th>
      <th>Revenue per Employee</th>
      <th>Operating_Margin</th>
      <th>EV/GP</th>
      <th>EBIT Margin (%)</th>
      <th>EV/EBITDA-Capex</th>
      <th>YOY_Gross_Margin_Change</th>
      <th>YOY_EBIT_Margin_Change</th>
      <th>Price_Range_Ratio</th>
      <th>YOY_Operating_Margin_Change</th>
      <th>YOY_Gross_Profit_Change</th>
      <th>YOY_Revenue_Change</th>
      <th>YOY_EBIT_Change</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AIR</td>
      <td>14.787113</td>
      <td>9.825424</td>
      <td>1.946881</td>
      <td>0.580152</td>
      <td>0.104475</td>
      <td>1</td>
      <td>0.667348</td>
      <td>0.502176</td>
      <td>0.178503</td>
      <td>Wholesale Trade</td>
      <td>4.571556</td>
      <td>2.816805</td>
      <td>20.360000</td>
      <td>0.173671</td>
      <td>1</td>
      <td>351.361702</td>
      <td>0.061645</td>
      <td>5.248703</td>
      <td>0.468209</td>
      <td>16.633460</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4.606308</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AIR</td>
      <td>12.272333</td>
      <td>9.053980</td>
      <td>2.084482</td>
      <td>0.521411</td>
      <td>0.144321</td>
      <td>1</td>
      <td>0.563710</td>
      <td>0.558485</td>
      <td>0.275563</td>
      <td>Wholesale Trade</td>
      <td>4.520103</td>
      <td>2.785181</td>
      <td>62.208333</td>
      <td>0.190854</td>
      <td>0</td>
      <td>403.800000</td>
      <td>0.082164</td>
      <td>5.283331</td>
      <td>0.483738</td>
      <td>13.880752</td>
      <td>0.098939</td>
      <td>0.033167</td>
      <td>0.472168</td>
      <td>0.332863</td>
      <td>0.209205</td>
      <td>0.100339</td>
      <td>0.136834</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AIR</td>
      <td>12.067561</td>
      <td>8.430082</td>
      <td>2.761248</td>
      <td>0.667819</td>
      <td>0.163133</td>
      <td>1</td>
      <td>0.564070</td>
      <td>0.427473</td>
      <td>0.240284</td>
      <td>Wholesale Trade</td>
      <td>5.215078</td>
      <td>3.437838</td>
      <td>14.696721</td>
      <td>0.200593</td>
      <td>0</td>
      <td>398.120000</td>
      <td>0.090073</td>
      <td>5.418767</td>
      <td>0.393650</td>
      <td>14.444016</td>
      <td>0.051030</td>
      <td>-0.186232</td>
      <td>0.565333</td>
      <td>0.096264</td>
      <td>0.151384</td>
      <td>0.095482</td>
      <td>-0.108532</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CECO</td>
      <td>13.091825</td>
      <td>7.261976</td>
      <td>2.099155</td>
      <td>1.064370</td>
      <td>0.150569</td>
      <td>1</td>
      <td>0.421906</td>
      <td>0.454887</td>
      <td>0.139182</td>
      <td>Manufacturing</td>
      <td>3.834394</td>
      <td>3.259748</td>
      <td>8.631966</td>
      <td>0.339988</td>
      <td>0</td>
      <td>432.891781</td>
      <td>0.096560</td>
      <td>3.718205</td>
      <td>0.602216</td>
      <td>15.035716</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.548853</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CECO</td>
      <td>20.333365</td>
      <td>12.191722</td>
      <td>2.027659</td>
      <td>1.027797</td>
      <td>0.107028</td>
      <td>1</td>
      <td>0.322052</td>
      <td>0.529282</td>
      <td>0.102691</td>
      <td>Manufacturing</td>
      <td>3.566842</td>
      <td>2.979955</td>
      <td>7.416328</td>
      <td>0.319893</td>
      <td>0</td>
      <td>444.027397</td>
      <td>0.067542</td>
      <td>4.293166</td>
      <td>0.677309</td>
      <td>23.092720</td>
      <td>-0.059107</td>
      <td>0.124694</td>
      <td>0.641248</td>
      <td>-0.300519</td>
      <td>-0.034903</td>
      <td>0.025724</td>
      <td>0.153625</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>21898</th>
      <td>NVT</td>
      <td>14.046063</td>
      <td>10.375857</td>
      <td>16.665808</td>
      <td>0.961013</td>
      <td>0.245791</td>
      <td>1</td>
      <td>0.161232</td>
      <td>0.105636</td>
      <td>0.249209</td>
      <td>Manufacturing</td>
      <td>8.399264</td>
      <td>7.737595</td>
      <td>9.726700</td>
      <td>0.459983</td>
      <td>1</td>
      <td>288.814159</td>
      <td>0.236641</td>
      <td>7.226069</td>
      <td>0.199442</td>
      <td>15.468094</td>
      <td>0.105038</td>
      <td>-0.184342</td>
      <td>0.588376</td>
      <td>0.225324</td>
      <td>0.239739</td>
      <td>0.121898</td>
      <td>-0.084915</td>
    </tr>
    <tr>
      <th>21909</th>
      <td>ACA</td>
      <td>9.576454</td>
      <td>7.254635</td>
      <td>4.789071</td>
      <td>0.398742</td>
      <td>0.149931</td>
      <td>1</td>
      <td>0.249740</td>
      <td>0.214342</td>
      <td>0.370801</td>
      <td>Manufacturing</td>
      <td>8.529488</td>
      <td>7.637448</td>
      <td>26.764151</td>
      <td>0.261831</td>
      <td>1</td>
      <td>301.965679</td>
      <td>0.146570</td>
      <td>5.360773</td>
      <td>0.293087</td>
      <td>13.476389</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.034826</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21910</th>
      <td>ACA</td>
      <td>14.853770</td>
      <td>10.502084</td>
      <td>6.726521</td>
      <td>0.632161</td>
      <td>0.136692</td>
      <td>1</td>
      <td>0.195574</td>
      <td>0.184938</td>
      <td>0.212208</td>
      <td>Manufacturing</td>
      <td>8.758516</td>
      <td>7.867033</td>
      <td>11.410256</td>
      <td>0.247843</td>
      <td>1</td>
      <td>328.800648</td>
      <td>0.131611</td>
      <td>7.887742</td>
      <td>0.290629</td>
      <td>21.802949</td>
      <td>-0.053422</td>
      <td>-0.008386</td>
      <td>0.436726</td>
      <td>-0.102055</td>
      <td>-0.007893</td>
      <td>0.048099</td>
      <td>0.039309</td>
    </tr>
    <tr>
      <th>21911</th>
      <td>ACA</td>
      <td>11.213941</td>
      <td>8.145220</td>
      <td>3.646947</td>
      <td>0.529299</td>
      <td>0.148553</td>
      <td>1</td>
      <td>0.217243</td>
      <td>0.298689</td>
      <td>0.273332</td>
      <td>Manufacturing</td>
      <td>9.085124</td>
      <td>8.226271</td>
      <td>10.467742</td>
      <td>0.257223</td>
      <td>1</td>
      <td>428.833652</td>
      <td>0.144685</td>
      <td>6.307721</td>
      <td>0.444890</td>
      <td>19.511657</td>
      <td>0.037845</td>
      <td>0.530782</td>
      <td>0.515431</td>
      <td>0.099337</td>
      <td>0.147375</td>
      <td>0.105536</td>
      <td>0.692334</td>
    </tr>
    <tr>
      <th>21912</th>
      <td>ACA</td>
      <td>13.117192</td>
      <td>9.755082</td>
      <td>2.640555</td>
      <td>0.534262</td>
      <td>0.145540</td>
      <td>1</td>
      <td>0.166693</td>
      <td>0.471226</td>
      <td>0.266405</td>
      <td>Manufacturing</td>
      <td>8.297542</td>
      <td>7.365724</td>
      <td>12.078292</td>
      <td>0.259240</td>
      <td>1</td>
      <td>379.901235</td>
      <td>0.147060</td>
      <td>7.441041</td>
      <td>0.730534</td>
      <td>32.759198</td>
      <td>0.007841</td>
      <td>0.642055</td>
      <td>0.618178</td>
      <td>0.016414</td>
      <td>0.037095</td>
      <td>0.029026</td>
      <td>0.689717</td>
    </tr>
  </tbody>
</table>
<p>1865 rows × 28 columns</p>
</div>



# FILTERING COMMENTED OUT BELOW (raw)


```python
selected_df.replace([np.inf, -np.inf], np.nan, inplace=True)

selected_df.fillna(0, inplace=True)
```

    /var/folders/_8/vpmh2zyd23z9mnscjwzk9t1r0000gn/T/ipykernel_35458/3317202709.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      selected_df.replace([np.inf, -np.inf], np.nan, inplace=True)
    /var/folders/_8/vpmh2zyd23z9mnscjwzk9t1r0000gn/T/ipykernel_35458/3317202709.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      selected_df.fillna(0, inplace=True)

selected_df = selected_df[(selected_df['Operating_Margin'] <= 2)& (selected_df['Operating_Margin'] >= 0.0)]
selected_df = selected_df[(selected_df['EV/EBITDA'] <= 30)& (selected_df['EV/EBITDA'] >= 1)]
selected_df = selected_df[(selected_df['EV_EBIT'] <= 30)& (selected_df['EV_EBIT'] >= 0)]
selected_df = selected_df[(selected_df['EBIT Margin (%)'] <= 1) & (selected_df['EBIT Margin (%)'] >= 0)]
selected_df = selected_df[(selected_df['Debt_to_Equity'] >= 0)]
selected_df = selected_df[(selected_df['YOY_Operating_Margin_Change'] >= -.75) & (selected_df['YOY_Operating_Margin_Change'] <= 5)]
selected_df = selected_df[(selected_df['Revenue per Employee'] <= 1200)]
selected_df = selected_df[(selected_df['ROE'] <= 1.3)]
# Display the reordered DataFrame
selected_df.replace([np.inf, -np.inf], np.nan, inplace=True)
selected_df.fillna(0, inplace=True)
selected_df= selected_df[(filtered_data['Market_Cap'] >= 100)]
selected_df.describe()

```python
# Create a mapping for grouping divisions
division_mapping = {
    'Unknown': 'Unknown_Nonclassifiable',
    'Nonclassifiable': 'Unknown_Nonclassifiable',
    'Mining': 'Mining_Trans_Comm_Gas_Sanitary',
    'Transportation, Communications, Electric, Gas and Sanitary service': 'Mining_Trans_Comm_Gas_Sanitary'
}

# Apply the mapping to the Division column in your DataFrame
selected_df['Division'] = selected_df['Division'].replace(division_mapping)

# Check the updated distribution
division_counts = selected_df['Division'].value_counts()
print(division_counts)
```

    Division
    Manufacturing                         753
    Retail Trade                          412
    Services                              317
    Construction                          119
    Wholesale Trade                       103
    Unknown_Nonclassifiable                55
    Finance, Insurance and Real Estate     55
    Mining_Trans_Comm_Gas_Sanitary         51
    Name: count, dtype: int64


    /var/folders/_8/vpmh2zyd23z9mnscjwzk9t1r0000gn/T/ipykernel_35458/487303733.py:10: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      selected_df['Division'] = selected_df['Division'].replace(division_mapping)



```python
# Define the multiples and metrics
multiples = ['EV/EBITDA', 'P/E', 'EV/GP','EV_EBIT','FCF Yield','EV/EBITDA-Capex']
metrics = ['Debt_Coverage_Ratio', 'ROE', 'EBIT Margin (%)',
           'YOY_Gross_Profit_Change','ROIC','FCF_Positive',
           'Gross_Margin','Quick_Ratio','Current_Ratio','Debt_to_Equity',
           'Revenue per Employee','FCF_Positive','YOY_Revenue_Change','YOY_EBIT_Change']

# Group data by sector
grouped_data = selected_df.groupby('Division')

# Calculate correlation between multiples and metrics for each sector
correlation_results = {}
for sector, group in grouped_data:
    correlation_results[sector] = {}
    for multiple in multiples:
        for metric in metrics:
            correlation = group[multiple].corr(group[metric])
            correlation_results[sector][(multiple, metric)] = correlation

# Display correlation results
for sector, result in correlation_results.items():
    print(f"--- {sector} ---")
    for (multiple, metric), correlation in result.items():
        print(f"{multiple} vs {metric}: {correlation}")

```

    --- Construction ---
    EV/EBITDA vs Debt_Coverage_Ratio: -0.6000929319263598
    EV/EBITDA vs ROE: -0.11153924420220634
    EV/EBITDA vs EBIT Margin (%): 0.35001681850772576
    EV/EBITDA vs YOY_Gross_Profit_Change: -0.33318687031519634
    EV/EBITDA vs ROIC: 0.29507524429292437
    EV/EBITDA vs FCF_Positive: -0.47947432436965204
    EV/EBITDA vs Gross_Margin: -0.4769550463288401
    EV/EBITDA vs Quick_Ratio: 0.49063103814358827
    EV/EBITDA vs Current_Ratio: 0.506207182171044
    EV/EBITDA vs Debt_to_Equity: 0.00869619952962617
    EV/EBITDA vs Revenue per Employee: -0.4874965658994136
    EV/EBITDA vs YOY_Revenue_Change: -0.11093975861237383
    EV/EBITDA vs YOY_EBIT_Change: 0.23329441003695683
    P/E vs Debt_Coverage_Ratio: -0.35566967270768346
    P/E vs ROE: -0.1221047133420028
    P/E vs EBIT Margin (%): 0.25334448270657467
    P/E vs YOY_Gross_Profit_Change: -0.23628795098093977
    P/E vs ROIC: 0.24216719619519986
    P/E vs FCF_Positive: -0.29199303407071975
    P/E vs Gross_Margin: -0.2889936604804572
    P/E vs Quick_Ratio: 0.5186692321997179
    P/E vs Current_Ratio: 0.5392367490483434
    P/E vs Debt_to_Equity: -0.04686769805111037
    P/E vs Revenue per Employee: -0.4443995177927245
    P/E vs YOY_Revenue_Change: 0.006908808839510782
    P/E vs YOY_EBIT_Change: 0.24384650445389855
    EV/GP vs Debt_Coverage_Ratio: -0.4739965864330813
    EV/GP vs ROE: -0.07490321273882761
    EV/GP vs EBIT Margin (%): 0.46254802781529586
    EV/GP vs YOY_Gross_Profit_Change: -0.18003963020785585
    EV/GP vs ROIC: 0.294793307770786
    EV/GP vs FCF_Positive: -0.37718704679738924
    EV/GP vs Gross_Margin: -0.41640354863259493
    EV/GP vs Quick_Ratio: 0.5206659189843458
    EV/GP vs Current_Ratio: 0.5325836557828691
    EV/GP vs Debt_to_Equity: 0.03549408664172033
    EV/GP vs Revenue per Employee: -0.4359446187730493
    EV/GP vs YOY_Revenue_Change: -0.020495705714647112
    EV/GP vs YOY_EBIT_Change: 0.25577357019839136
    EV_EBIT vs Debt_Coverage_Ratio: 0.1652375859183126
    EV_EBIT vs ROE: 0.05375993168780917
    EV_EBIT vs EBIT Margin (%): -0.4643636760723289
    EV_EBIT vs YOY_Gross_Profit_Change: -0.06354323077115626
    EV_EBIT vs ROIC: -0.39316318095216746
    EV_EBIT vs FCF_Positive: -0.03295135836807981
    EV_EBIT vs Gross_Margin: 0.5324592943715856
    EV_EBIT vs Quick_Ratio: 0.20301156315007587
    EV_EBIT vs Current_Ratio: 0.21641256397237715
    EV_EBIT vs Debt_to_Equity: -0.0070378251769558295
    EV_EBIT vs Revenue per Employee: -0.01178436997357374
    EV_EBIT vs YOY_Revenue_Change: -0.023748464685726937
    EV_EBIT vs YOY_EBIT_Change: -0.08041737243940922
    FCF Yield vs Debt_Coverage_Ratio: -0.13828871716562996
    FCF Yield vs ROE: 0.13694989872557778
    FCF Yield vs EBIT Margin (%): 0.2925954548924832
    FCF Yield vs YOY_Gross_Profit_Change: -0.040723638708072385
    FCF Yield vs ROIC: 0.2471598696513671
    FCF Yield vs FCF_Positive: 0.1798613960913382
    FCF Yield vs Gross_Margin: -0.26235704387284586
    FCF Yield vs Quick_Ratio: 0.10277534352539143
    FCF Yield vs Current_Ratio: 0.09073147695431019
    FCF Yield vs Debt_to_Equity: 0.1638262588969779
    FCF Yield vs Revenue per Employee: -0.2272979606798382
    FCF Yield vs YOY_Revenue_Change: -0.09271550526376722
    FCF Yield vs YOY_EBIT_Change: -0.07177400132360626
    EV/EBITDA-Capex vs Debt_Coverage_Ratio: -0.12051301331466975
    EV/EBITDA-Capex vs ROE: -0.02998682570021265
    EV/EBITDA-Capex vs EBIT Margin (%): 0.0045152072414584256
    EV/EBITDA-Capex vs YOY_Gross_Profit_Change: -0.0025161930540824615
    EV/EBITDA-Capex vs ROIC: 0.08927860028402178
    EV/EBITDA-Capex vs FCF_Positive: 0.07330314063467262
    EV/EBITDA-Capex vs Gross_Margin: -0.20247180337677678
    EV/EBITDA-Capex vs Quick_Ratio: 0.04347167666599999
    EV/EBITDA-Capex vs Current_Ratio: 0.04461591439063196
    EV/EBITDA-Capex vs Debt_to_Equity: -0.00889494636659311
    EV/EBITDA-Capex vs Revenue per Employee: -0.15076905360366127
    EV/EBITDA-Capex vs YOY_Revenue_Change: 0.09262388285703316
    EV/EBITDA-Capex vs YOY_EBIT_Change: -0.08806727282247699
    --- Finance, Insurance and Real Estate ---
    EV/EBITDA vs Debt_Coverage_Ratio: -0.28642827096589524
    EV/EBITDA vs ROE: -0.03069530463097867
    EV/EBITDA vs EBIT Margin (%): 0.2343453055169379
    EV/EBITDA vs YOY_Gross_Profit_Change: -0.22835098666645082
    EV/EBITDA vs ROIC: -0.08485885309227656
    EV/EBITDA vs FCF_Positive: -0.29040960582542213
    EV/EBITDA vs Gross_Margin: -0.18656678830126344
    EV/EBITDA vs Quick_Ratio: -0.05106440489738574
    EV/EBITDA vs Current_Ratio: -0.04870650115964276
    EV/EBITDA vs Debt_to_Equity: 0.05493645946221308
    EV/EBITDA vs Revenue per Employee: 0.06911347035321475
    EV/EBITDA vs YOY_Revenue_Change: -0.2066544191289918
    EV/EBITDA vs YOY_EBIT_Change: -0.0964300351820481
    P/E vs Debt_Coverage_Ratio: 0.49382650190735733
    P/E vs ROE: -0.24748012408005687
    P/E vs EBIT Margin (%): -0.17453764902459823
    P/E vs YOY_Gross_Profit_Change: -0.09348830802409998
    P/E vs ROIC: 0.588071796119638
    P/E vs FCF_Positive: 0.09723725490906569
    P/E vs Gross_Margin: -0.04484710255425555
    P/E vs Quick_Ratio: 0.6648632305940008
    P/E vs Current_Ratio: 0.6761439253808492
    P/E vs Debt_to_Equity: -0.3495162694999225
    P/E vs Revenue per Employee: -0.20807194592595005
    P/E vs YOY_Revenue_Change: -0.0730145233119591
    P/E vs YOY_EBIT_Change: 0.1229104982329992
    EV/GP vs Debt_Coverage_Ratio: -0.3215224235622979
    EV/GP vs ROE: 0.023906367052006643
    EV/GP vs EBIT Margin (%): 0.34964452178916194
    EV/GP vs YOY_Gross_Profit_Change: -0.18286727900358396
    EV/GP vs ROIC: -0.17604938326970296
    EV/GP vs FCF_Positive: -0.33200742695889623
    EV/GP vs Gross_Margin: -0.15179619954185244
    EV/GP vs Quick_Ratio: -0.2566256256609957
    EV/GP vs Current_Ratio: -0.25925663571973245
    EV/GP vs Debt_to_Equity: 0.1371859399526425
    EV/GP vs Revenue per Employee: 0.1443410257359768
    EV/GP vs YOY_Revenue_Change: -0.16041208802358264
    EV/GP vs YOY_EBIT_Change: -0.09258868015227775
    EV_EBIT vs Debt_Coverage_Ratio: 0.12957702104524824
    EV_EBIT vs ROE: -0.49746587793991054
    EV_EBIT vs EBIT Margin (%): -0.3219454668105717
    EV_EBIT vs YOY_Gross_Profit_Change: -0.15587626813517105
    EV_EBIT vs ROIC: -0.05587011742570543
    EV_EBIT vs FCF_Positive: -0.3177693039142977
    EV_EBIT vs Gross_Margin: 0.006353415554648913
    EV_EBIT vs Quick_Ratio: 0.29112247188432966
    EV_EBIT vs Current_Ratio: 0.2781719028751231
    EV_EBIT vs Debt_to_Equity: -0.5020025078977257
    EV_EBIT vs Revenue per Employee: 0.1640985761257495
    EV_EBIT vs YOY_Revenue_Change: -0.04349977751718658
    EV_EBIT vs YOY_EBIT_Change: -0.02162850106106789
    FCF Yield vs Debt_Coverage_Ratio: 0.01720108340131447
    FCF Yield vs ROE: -0.1613495900430674
    FCF Yield vs EBIT Margin (%): -0.11287942044207668
    FCF Yield vs YOY_Gross_Profit_Change: 0.21762096925427477
    FCF Yield vs ROIC: -0.12825526442977417
    FCF Yield vs FCF_Positive: 0.5361824903152305
    FCF Yield vs Gross_Margin: 0.11985343575355198
    FCF Yield vs Quick_Ratio: -0.09074304744816626
    FCF Yield vs Current_Ratio: -0.09103586194479354
    FCF Yield vs Debt_to_Equity: -0.07763414495815532
    FCF Yield vs Revenue per Employee: 0.016042241714260996
    FCF Yield vs YOY_Revenue_Change: 0.2035531950650106
    FCF Yield vs YOY_EBIT_Change: 0.047924877809801564
    EV/EBITDA-Capex vs Debt_Coverage_Ratio: -0.2454045827871857
    EV/EBITDA-Capex vs ROE: -0.0005518696012661004
    EV/EBITDA-Capex vs EBIT Margin (%): -0.00406527459056761
    EV/EBITDA-Capex vs YOY_Gross_Profit_Change: -0.20434350130072657
    EV/EBITDA-Capex vs ROIC: -0.15331432496369465
    EV/EBITDA-Capex vs FCF_Positive: -0.6285387785610335
    EV/EBITDA-Capex vs Gross_Margin: -0.3184065429472358
    EV/EBITDA-Capex vs Quick_Ratio: -0.09105073102566251
    EV/EBITDA-Capex vs Current_Ratio: -0.08962951185451004
    EV/EBITDA-Capex vs Debt_to_Equity: 0.06923059058930849
    EV/EBITDA-Capex vs Revenue per Employee: 0.03632034813364693
    EV/EBITDA-Capex vs YOY_Revenue_Change: -0.09746826714330595
    EV/EBITDA-Capex vs YOY_EBIT_Change: -0.11243565946505095
    --- Manufacturing ---
    EV/EBITDA vs Debt_Coverage_Ratio: -0.08353265120359772
    EV/EBITDA vs ROE: -0.015216001369615458
    EV/EBITDA vs EBIT Margin (%): 0.03232731415580292
    EV/EBITDA vs YOY_Gross_Profit_Change: -0.042001508663481193
    EV/EBITDA vs ROIC: 0.01862585568008507
    EV/EBITDA vs FCF_Positive: -0.011702069322012053
    EV/EBITDA vs Gross_Margin: 0.02781972868494477
    EV/EBITDA vs Quick_Ratio: -0.03291154477460787
    EV/EBITDA vs Current_Ratio: -0.04510865004898177
    EV/EBITDA vs Debt_to_Equity: 0.004211118472462574
    EV/EBITDA vs Revenue per Employee: 0.03270952000281645
    EV/EBITDA vs YOY_Revenue_Change: -0.029160522221667103
    EV/EBITDA vs YOY_EBIT_Change: -0.0015135474924003794
    P/E vs Debt_Coverage_Ratio: -0.05585106714725644
    P/E vs ROE: -0.010660795940625793
    P/E vs EBIT Margin (%): 0.014936565048563508
    P/E vs YOY_Gross_Profit_Change: -0.03235583519584277
    P/E vs ROIC: -0.000931950978190278
    P/E vs FCF_Positive: -0.0009019754467021625
    P/E vs Gross_Margin: 0.037101995558957046
    P/E vs Quick_Ratio: -0.009594699863440812
    P/E vs Current_Ratio: -0.020614838838028983
    P/E vs Debt_to_Equity: 0.003913856957936544
    P/E vs Revenue per Employee: 0.04502722745048825
    P/E vs YOY_Revenue_Change: -0.026289173597713586
    P/E vs YOY_EBIT_Change: 0.005121299178984063
    EV/GP vs Debt_Coverage_Ratio: 0.00011577679717668397
    EV/GP vs ROE: 0.19842019199447386
    EV/GP vs EBIT Margin (%): 0.30786253673143
    EV/GP vs YOY_Gross_Profit_Change: -0.005197908599505188
    EV/GP vs ROIC: 0.2017394420474303
    EV/GP vs FCF_Positive: -0.16536685728279057
    EV/GP vs Gross_Margin: -0.02511357537485578
    EV/GP vs Quick_Ratio: 0.20324875916008417
    EV/GP vs Current_Ratio: 0.17607287623807671
    EV/GP vs Debt_to_Equity: 0.09441303543314125
    EV/GP vs Revenue per Employee: 0.0657556980015711
    EV/GP vs YOY_Revenue_Change: 0.06641083772933827
    EV/GP vs YOY_EBIT_Change: 0.030658408156425287
    EV_EBIT vs Debt_Coverage_Ratio: 0.03247136171334447
    EV_EBIT vs ROE: -0.0015206865938115677
    EV_EBIT vs EBIT Margin (%): -0.02952521427318114
    EV_EBIT vs YOY_Gross_Profit_Change: 0.010549153575947694
    EV_EBIT vs ROIC: -0.038874286590746036
    EV_EBIT vs FCF_Positive: 0.007627336230877429
    EV_EBIT vs Gross_Margin: 0.08409733798150743
    EV_EBIT vs Quick_Ratio: 0.09960063311068053
    EV_EBIT vs Current_Ratio: 0.0940449287980594
    EV_EBIT vs Debt_to_Equity: 0.0002123054574905743
    EV_EBIT vs Revenue per Employee: 0.08650031576526235
    EV_EBIT vs YOY_Revenue_Change: 0.01439615198041673
    EV_EBIT vs YOY_EBIT_Change: 0.006206861173527318
    FCF Yield vs Debt_Coverage_Ratio: -0.07609545077785043
    FCF Yield vs ROE: -0.047183005152990065
    FCF Yield vs EBIT Margin (%): -0.13796269289036164
    FCF Yield vs YOY_Gross_Profit_Change: -0.044129031448314454
    FCF Yield vs ROIC: -0.10147123501375242
    FCF Yield vs FCF_Positive: 0.2460944295897931
    FCF Yield vs Gross_Margin: -0.2749550823337263
    FCF Yield vs Quick_Ratio: -0.08679560936895561
    FCF Yield vs Current_Ratio: -0.011732025734466437
    FCF Yield vs Debt_to_Equity: -0.023782684962443297
    FCF Yield vs Revenue per Employee: -0.015853009919912682
    FCF Yield vs YOY_Revenue_Change: -0.1055169671775934
    FCF Yield vs YOY_EBIT_Change: -0.07064845553080755
    EV/EBITDA-Capex vs Debt_Coverage_Ratio: 0.028574967560360737
    EV/EBITDA-Capex vs ROE: 0.009916613239436252
    EV/EBITDA-Capex vs EBIT Margin (%): 0.006210838249790685
    EV/EBITDA-Capex vs YOY_Gross_Profit_Change: 0.015032168908862187
    EV/EBITDA-Capex vs ROIC: 0.0072923354257044964
    EV/EBITDA-Capex vs FCF_Positive: -0.0052522593209120534
    EV/EBITDA-Capex vs Gross_Margin: 0.03130416735201622
    EV/EBITDA-Capex vs Quick_Ratio: 0.0238050275546683
    EV/EBITDA-Capex vs Current_Ratio: 0.03078534434550735
    EV/EBITDA-Capex vs Debt_to_Equity: 0.0019353285144276602
    EV/EBITDA-Capex vs Revenue per Employee: -0.06147876387876787
    EV/EBITDA-Capex vs YOY_Revenue_Change: 0.018256186426830228
    EV/EBITDA-Capex vs YOY_EBIT_Change: 0.0008880501884320863
    --- Mining_Trans_Comm_Gas_Sanitary ---
    EV/EBITDA vs Debt_Coverage_Ratio: -0.4824422865850665
    EV/EBITDA vs ROE: -0.3926828916959983
    EV/EBITDA vs EBIT Margin (%): -0.1702420490076805
    EV/EBITDA vs YOY_Gross_Profit_Change: -0.130028312092347
    EV/EBITDA vs ROIC: -0.21059369158434138
    EV/EBITDA vs FCF_Positive: -0.23752374278697055
    EV/EBITDA vs Gross_Margin: -0.37731376748812717
    EV/EBITDA vs Quick_Ratio: 0.21817537092847
    EV/EBITDA vs Current_Ratio: 0.21200322724851786
    EV/EBITDA vs Debt_to_Equity: 0.0009500641531548335
    EV/EBITDA vs Revenue per Employee: -0.15626516292148565
    EV/EBITDA vs YOY_Revenue_Change: -0.04071518064204393
    EV/EBITDA vs YOY_EBIT_Change: -0.1295192023006941
    P/E vs Debt_Coverage_Ratio: -0.2724524217729048
    P/E vs ROE: -0.33798357686992797
    P/E vs EBIT Margin (%): -0.33847684735519656
    P/E vs YOY_Gross_Profit_Change: -0.13388958307283325
    P/E vs ROIC: -0.21563052585076317
    P/E vs FCF_Positive: 0.11285725839343827
    P/E vs Gross_Margin: -0.41757968365296927
    P/E vs Quick_Ratio: -0.18571466245092677
    P/E vs Current_Ratio: -0.19482625501236447
    P/E vs Debt_to_Equity: -0.1375018051033901
    P/E vs Revenue per Employee: -0.18780988194613332
    P/E vs YOY_Revenue_Change: -0.12972202874186686
    P/E vs YOY_EBIT_Change: -0.08208232131678102
    EV/GP vs Debt_Coverage_Ratio: -0.42518085057926747
    EV/GP vs ROE: -0.32416175313924833
    EV/GP vs EBIT Margin (%): 0.12528007509943045
    EV/GP vs YOY_Gross_Profit_Change: -0.01781753417907237
    EV/GP vs ROIC: -0.07406133092588454
    EV/GP vs FCF_Positive: -0.33190306486991883
    EV/GP vs Gross_Margin: -0.2695126406002933
    EV/GP vs Quick_Ratio: 0.409261581403271
    EV/GP vs Current_Ratio: 0.4030288483038599
    EV/GP vs Debt_to_Equity: 0.020270935609739197
    EV/GP vs Revenue per Employee: -0.0031220611977551805
    EV/GP vs YOY_Revenue_Change: -0.03361728789562368
    EV/GP vs YOY_EBIT_Change: -0.004129513821654947
    EV_EBIT vs Debt_Coverage_Ratio: 0.05102904622184805
    EV_EBIT vs ROE: -0.23626083356021535
    EV_EBIT vs EBIT Margin (%): -0.4990794498622054
    EV_EBIT vs YOY_Gross_Profit_Change: 0.23080446004720057
    EV_EBIT vs ROIC: -0.6461684677192694
    EV_EBIT vs FCF_Positive: -0.016172513909861772
    EV_EBIT vs Gross_Margin: -0.12379817819286677
    EV_EBIT vs Quick_Ratio: 0.008220179619581887
    EV_EBIT vs Current_Ratio: 0.0014742607920850157
    EV_EBIT vs Debt_to_Equity: -0.22208021147804172
    EV_EBIT vs Revenue per Employee: -0.1600042132101418
    EV_EBIT vs YOY_Revenue_Change: 0.38586634136578657
    EV_EBIT vs YOY_EBIT_Change: 0.049223920548687544
    FCF Yield vs Debt_Coverage_Ratio: 0.1386054557653971
    FCF Yield vs ROE: 0.33175545259392675
    FCF Yield vs EBIT Margin (%): -0.15183703418543226
    FCF Yield vs YOY_Gross_Profit_Change: -0.09043340905080383
    FCF Yield vs ROIC: 0.1211497075165395
    FCF Yield vs FCF_Positive: 0.48267837568194955
    FCF Yield vs Gross_Margin: -0.3344793302629631
    FCF Yield vs Quick_Ratio: 0.18241717180295777
    FCF Yield vs Current_Ratio: 0.1903530161033857
    FCF Yield vs Debt_to_Equity: 0.46576485217704566
    FCF Yield vs Revenue per Employee: -0.1275043527486412
    FCF Yield vs YOY_Revenue_Change: -0.13334984093337618
    FCF Yield vs YOY_EBIT_Change: -0.024271314355601276
    EV/EBITDA-Capex vs Debt_Coverage_Ratio: 0.10046129604299552
    EV/EBITDA-Capex vs ROE: 0.09657561113070741
    EV/EBITDA-Capex vs EBIT Margin (%): -0.13049497131885635
    EV/EBITDA-Capex vs YOY_Gross_Profit_Change: 0.05125562808150505
    EV/EBITDA-Capex vs ROIC: 0.049869032447021976
    EV/EBITDA-Capex vs FCF_Positive: 0.26614092950688917
    EV/EBITDA-Capex vs Gross_Margin: 0.0005656974398895543
    EV/EBITDA-Capex vs Quick_Ratio: -0.1375303847571202
    EV/EBITDA-Capex vs Current_Ratio: -0.14167780274040856
    EV/EBITDA-Capex vs Debt_to_Equity: 0.05473237864551254
    EV/EBITDA-Capex vs Revenue per Employee: 0.029415015333322945
    EV/EBITDA-Capex vs YOY_Revenue_Change: 0.024935169242966883
    EV/EBITDA-Capex vs YOY_EBIT_Change: -0.010279601653154058
    --- Retail Trade ---
    EV/EBITDA vs Debt_Coverage_Ratio: -0.16411184974201615
    EV/EBITDA vs ROE: 0.0066318682840592535
    EV/EBITDA vs EBIT Margin (%): -0.07544528126320188
    EV/EBITDA vs YOY_Gross_Profit_Change: -0.014697632615822779
    EV/EBITDA vs ROIC: -0.06016637139247836
    EV/EBITDA vs FCF_Positive: -0.08982781356390236
    EV/EBITDA vs Gross_Margin: -0.10036787382056564
    EV/EBITDA vs Quick_Ratio: 0.0837993508737191
    EV/EBITDA vs Current_Ratio: 0.07897842287727909
    EV/EBITDA vs Debt_to_Equity: 0.0068116225195589694
    EV/EBITDA vs Revenue per Employee: -0.039813089889870014
    EV/EBITDA vs YOY_Revenue_Change: 0.0011362162013811615
    EV/EBITDA vs YOY_EBIT_Change: -0.007728377907848173
    P/E vs Debt_Coverage_Ratio: -0.14984045330241844
    P/E vs ROE: 0.00646831741291575
    P/E vs EBIT Margin (%): -0.08062929727571214
    P/E vs YOY_Gross_Profit_Change: 0.007397367540202719
    P/E vs ROIC: -0.060080091952066365
    P/E vs FCF_Positive: -0.03834431815139655
    P/E vs Gross_Margin: -0.0753604578266781
    P/E vs Quick_Ratio: 0.125686479446133
    P/E vs Current_Ratio: 0.1271437124732917
    P/E vs Debt_to_Equity: 0.002028660610429311
    P/E vs Revenue per Employee: -0.024113517418425594
    P/E vs YOY_Revenue_Change: 0.015663684551126066
    P/E vs YOY_EBIT_Change: -0.016600962499353555
    EV/GP vs Debt_Coverage_Ratio: -0.2360476649883384
    EV/GP vs ROE: 0.026105381638613652
    EV/GP vs EBIT Margin (%): 0.18129957462284796
    EV/GP vs YOY_Gross_Profit_Change: 0.15668548893430545
    EV/GP vs ROIC: -0.04072578156540951
    EV/GP vs FCF_Positive: -0.28719863094926673
    EV/GP vs Gross_Margin: -0.2899332972265223
    EV/GP vs Quick_Ratio: 0.38590521093685054
    EV/GP vs Current_Ratio: 0.3457459826274817
    EV/GP vs Debt_to_Equity: 0.022030812355728367
    EV/GP vs Revenue per Employee: -0.1287213568541267
    EV/GP vs YOY_Revenue_Change: 0.3101163756126926
    EV/GP vs YOY_EBIT_Change: -0.02432269072341076
    EV_EBIT vs Debt_Coverage_Ratio: 0.05089775318259092
    EV_EBIT vs ROE: 0.0011227131613570417
    EV_EBIT vs EBIT Margin (%): -0.005830376459047334
    EV_EBIT vs YOY_Gross_Profit_Change: 0.015553590319959969
    EV_EBIT vs ROIC: -0.009239911601379899
    EV_EBIT vs FCF_Positive: 0.14410585347621113
    EV_EBIT vs Gross_Margin: 0.06641814703689261
    EV_EBIT vs Quick_Ratio: 0.06142997122978154
    EV_EBIT vs Current_Ratio: 0.06269522269477922
    EV_EBIT vs Debt_to_Equity: -0.006558351832747493
    EV_EBIT vs Revenue per Employee: 0.05627881435960132
    EV_EBIT vs YOY_Revenue_Change: 0.028052971236058714
    EV_EBIT vs YOY_EBIT_Change: 0.013926544543730835
    FCF Yield vs Debt_Coverage_Ratio: 0.21668566781930926
    FCF Yield vs ROE: -0.0397056138871406
    FCF Yield vs EBIT Margin (%): -0.1053200167317194
    FCF Yield vs YOY_Gross_Profit_Change: -0.10318103615357453
    FCF Yield vs ROIC: -0.007882881936825039
    FCF Yield vs FCF_Positive: 0.5299479246636398
    FCF Yield vs Gross_Margin: 0.3645724850543398
    FCF Yield vs Quick_Ratio: -0.17756369154821217
    FCF Yield vs Current_Ratio: -0.11847771826063914
    FCF Yield vs Debt_to_Equity: -0.07777008510940944
    FCF Yield vs Revenue per Employee: 0.05623388687224514
    FCF Yield vs YOY_Revenue_Change: -0.23426709350763186
    FCF Yield vs YOY_EBIT_Change: 0.0446343563311743
    EV/EBITDA-Capex vs Debt_Coverage_Ratio: -0.007407352348306842
    EV/EBITDA-Capex vs ROE: 0.005663526364903849
    EV/EBITDA-Capex vs EBIT Margin (%): 0.046429045446166085
    EV/EBITDA-Capex vs YOY_Gross_Profit_Change: 0.0585464740805827
    EV/EBITDA-Capex vs ROIC: 0.0007374792593324196
    EV/EBITDA-Capex vs FCF_Positive: -0.0544372823078999
    EV/EBITDA-Capex vs Gross_Margin: -0.06973869958916736
    EV/EBITDA-Capex vs Quick_Ratio: 0.05497667790843299
    EV/EBITDA-Capex vs Current_Ratio: 0.047654405684030995
    EV/EBITDA-Capex vs Debt_to_Equity: 0.007936125403540278
    EV/EBITDA-Capex vs Revenue per Employee: 0.02432212372036977
    EV/EBITDA-Capex vs YOY_Revenue_Change: 0.16188050084256012
    EV/EBITDA-Capex vs YOY_EBIT_Change: 0.0318333529353954
    --- Services ---
    EV/EBITDA vs Debt_Coverage_Ratio: -0.1863024441576512
    EV/EBITDA vs ROE: -0.01965835967158571
    EV/EBITDA vs EBIT Margin (%): 0.0881155539456184
    EV/EBITDA vs YOY_Gross_Profit_Change: -0.08315106981651368
    EV/EBITDA vs ROIC: -0.03277461056644822
    EV/EBITDA vs FCF_Positive: 0.018643496998715633
    EV/EBITDA vs Gross_Margin: 0.0952335634752951
    EV/EBITDA vs Quick_Ratio: 0.030010834053315522
    EV/EBITDA vs Current_Ratio: 0.027477402911173367
    EV/EBITDA vs Debt_to_Equity: 0.0002563288628313085
    EV/EBITDA vs Revenue per Employee: -0.030390607297598893
    EV/EBITDA vs YOY_Revenue_Change: -0.04600041073929421
    EV/EBITDA vs YOY_EBIT_Change: -0.012569298524499934
    P/E vs Debt_Coverage_Ratio: -0.170572898308364
    P/E vs ROE: -0.02314578739824416
    P/E vs EBIT Margin (%): 0.115512299313094
    P/E vs YOY_Gross_Profit_Change: -0.07526298466454434
    P/E vs ROIC: -0.02365396121149276
    P/E vs FCF_Positive: 0.03862993863019573
    P/E vs Gross_Margin: 0.15754075299982398
    P/E vs Quick_Ratio: 0.007650019596158596
    P/E vs Current_Ratio: 0.005702267754926608
    P/E vs Debt_to_Equity: -0.007647390736270606
    P/E vs Revenue per Employee: -0.026274819957699175
    P/E vs YOY_Revenue_Change: -0.04862936347040557
    P/E vs YOY_EBIT_Change: -0.0035359327052225747
    EV/GP vs Debt_Coverage_Ratio: -0.19553732931455006
    EV/GP vs ROE: 0.0374630289109726
    EV/GP vs EBIT Margin (%): 0.003047359819212509
    EV/GP vs YOY_Gross_Profit_Change: -0.032051653229487234
    EV/GP vs ROIC: -0.07803268011931941
    EV/GP vs FCF_Positive: -0.036786939339888254
    EV/GP vs Gross_Margin: -0.4167166313810165
    EV/GP vs Quick_Ratio: 0.1153554572716875
    EV/GP vs Current_Ratio: 0.11694115520267831
    EV/GP vs Debt_to_Equity: 0.05000830867245282
    EV/GP vs Revenue per Employee: -0.10557355060578322
    EV/GP vs YOY_Revenue_Change: -0.02986154359060379
    EV/GP vs YOY_EBIT_Change: 0.0018747544126838194
    EV_EBIT vs Debt_Coverage_Ratio: 0.06281974867183979
    EV_EBIT vs ROE: 0.006809708684516872
    EV_EBIT vs EBIT Margin (%): -0.200448903500731
    EV_EBIT vs YOY_Gross_Profit_Change: 0.09987705368103994
    EV_EBIT vs ROIC: -0.18261486111149397
    EV_EBIT vs FCF_Positive: -0.0867303695131029
    EV_EBIT vs Gross_Margin: -0.08749804819102579
    EV_EBIT vs Quick_Ratio: -0.03149255873429653
    EV_EBIT vs Current_Ratio: -0.034812284810478954
    EV_EBIT vs Debt_to_Equity: -0.017314282226392395
    EV_EBIT vs Revenue per Employee: -0.08802104675946991
    EV_EBIT vs YOY_Revenue_Change: 0.056521635293521104
    EV_EBIT vs YOY_EBIT_Change: -0.041162164122851654
    FCF Yield vs Debt_Coverage_Ratio: 0.08051944644723077
    FCF Yield vs ROE: 0.13234925608383807
    FCF Yield vs EBIT Margin (%): 0.006648288012312571
    FCF Yield vs YOY_Gross_Profit_Change: -0.04239727733618023
    FCF Yield vs ROIC: 0.058863655948313
    FCF Yield vs FCF_Positive: 0.5032062134275097
    FCF Yield vs Gross_Margin: -0.2293818236076124
    FCF Yield vs Quick_Ratio: 0.07493868252698689
    FCF Yield vs Current_Ratio: 0.08758928411225014
    FCF Yield vs Debt_to_Equity: 0.1403421529390853
    FCF Yield vs Revenue per Employee: -0.19454464315673986
    FCF Yield vs YOY_Revenue_Change: -0.04919666441364333
    FCF Yield vs YOY_EBIT_Change: -0.007118677268336037
    EV/EBITDA-Capex vs Debt_Coverage_Ratio: 0.004829110561196852
    EV/EBITDA-Capex vs ROE: 0.0015256677234443579
    EV/EBITDA-Capex vs EBIT Margin (%): -0.05988982067339699
    EV/EBITDA-Capex vs YOY_Gross_Profit_Change: -0.002681029993665895
    EV/EBITDA-Capex vs ROIC: -0.023157524596254433
    EV/EBITDA-Capex vs FCF_Positive: -0.08892627138479159
    EV/EBITDA-Capex vs Gross_Margin: -0.12601206898453268
    EV/EBITDA-Capex vs Quick_Ratio: 0.06367951090761297
    EV/EBITDA-Capex vs Current_Ratio: 0.0625964136070127
    EV/EBITDA-Capex vs Debt_to_Equity: 0.0001769814395032019
    EV/EBITDA-Capex vs Revenue per Employee: -0.004937159420302055
    EV/EBITDA-Capex vs YOY_Revenue_Change: -0.0033962318424133166
    EV/EBITDA-Capex vs YOY_EBIT_Change: 0.003757269123031581
    --- Unknown_Nonclassifiable ---
    EV/EBITDA vs Debt_Coverage_Ratio: -0.1526056890375154
    EV/EBITDA vs ROE: -0.2662271147161148
    EV/EBITDA vs EBIT Margin (%): 0.033572907777702554
    EV/EBITDA vs YOY_Gross_Profit_Change: -0.10566693996887642
    EV/EBITDA vs ROIC: 0.3255114532985711
    EV/EBITDA vs FCF_Positive: -0.21434731946906102
    EV/EBITDA vs Gross_Margin: -0.2398582869263802
    EV/EBITDA vs Quick_Ratio: -0.2019145477477061
    EV/EBITDA vs Current_Ratio: -0.21310784634035637
    EV/EBITDA vs Debt_to_Equity: -0.231820007805482
    EV/EBITDA vs Revenue per Employee: -0.03421265490923506
    EV/EBITDA vs YOY_Revenue_Change: -0.15104780078214097
    EV/EBITDA vs YOY_EBIT_Change: -0.07898683569484037
    P/E vs Debt_Coverage_Ratio: 0.05895958689137138
    P/E vs ROE: -0.41337002749511725
    P/E vs EBIT Margin (%): 0.058913072540967844
    P/E vs YOY_Gross_Profit_Change: -0.16777474958506927
    P/E vs ROIC: 0.3682350207727263
    P/E vs FCF_Positive: 0.008317799208845874
    P/E vs Gross_Margin: -0.13690366965688486
    P/E vs Quick_Ratio: -0.1845776701633525
    P/E vs Current_Ratio: -0.18405360698538323
    P/E vs Debt_to_Equity: -0.39196568308818286
    P/E vs Revenue per Employee: -0.0059592422698792604
    P/E vs YOY_Revenue_Change: -0.11966461171415924
    P/E vs YOY_EBIT_Change: -0.10008642713144407
    EV/GP vs Debt_Coverage_Ratio: -0.05618874820460691
    EV/GP vs ROE: 0.006157440513897728
    EV/GP vs EBIT Margin (%): 0.15501279418621908
    EV/GP vs YOY_Gross_Profit_Change: 0.2233151838641182
    EV/GP vs ROIC: 0.05464586853659127
    EV/GP vs FCF_Positive: -0.2917336330326486
    EV/GP vs Gross_Margin: -0.28806374830939346
    EV/GP vs Quick_Ratio: -0.05955757691190454
    EV/GP vs Current_Ratio: -0.08197068568840281
    EV/GP vs Debt_to_Equity: 0.03515148168487499
    EV/GP vs Revenue per Employee: 0.029073492804237242
    EV/GP vs YOY_Revenue_Change: 0.08623447470034817
    EV/GP vs YOY_EBIT_Change: 0.03466977760399959
    EV_EBIT vs Debt_Coverage_Ratio: 0.00482808103770972
    EV_EBIT vs ROE: -0.1247950341429605
    EV_EBIT vs EBIT Margin (%): -0.34340648586269
    EV_EBIT vs YOY_Gross_Profit_Change: -0.19655855871829972
    EV_EBIT vs ROIC: -0.33434773354900466
    EV_EBIT vs FCF_Positive: 0.0875477423406188
    EV_EBIT vs Gross_Margin: 0.06859751278116266
    EV_EBIT vs Quick_Ratio: -0.0949670278963045
    EV_EBIT vs Current_Ratio: -0.07629473571145214
    EV_EBIT vs Debt_to_Equity: -0.09903775094742795
    EV_EBIT vs Revenue per Employee: -0.12946248584555584
    EV_EBIT vs YOY_Revenue_Change: -0.14559274112300333
    EV_EBIT vs YOY_EBIT_Change: -0.09295891931262505
    FCF Yield vs Debt_Coverage_Ratio: -0.02084877247785283
    FCF Yield vs ROE: 0.2173846819963624
    FCF Yield vs EBIT Margin (%): 0.25285823666757495
    FCF Yield vs YOY_Gross_Profit_Change: -0.14903449443923272
    FCF Yield vs ROIC: -0.08109986349060029
    FCF Yield vs FCF_Positive: 0.3816102903713165
    FCF Yield vs Gross_Margin: 0.5366637542457964
    FCF Yield vs Quick_Ratio: 0.7609264456310928
    FCF Yield vs Current_Ratio: 0.7618725473696331
    FCF Yield vs Debt_to_Equity: 0.1926659512056959
    FCF Yield vs Revenue per Employee: 0.5041398526642962
    FCF Yield vs YOY_Revenue_Change: -0.09091668810417285
    FCF Yield vs YOY_EBIT_Change: -0.10835779872377051
    EV/EBITDA-Capex vs Debt_Coverage_Ratio: -0.035260247888111544
    EV/EBITDA-Capex vs ROE: -0.014875273842983431
    EV/EBITDA-Capex vs EBIT Margin (%): -0.06990721752551321
    EV/EBITDA-Capex vs YOY_Gross_Profit_Change: 0.03177747019614112
    EV/EBITDA-Capex vs ROIC: -0.2222698224309893
    EV/EBITDA-Capex vs FCF_Positive: 0.06661178774364622
    EV/EBITDA-Capex vs Gross_Margin: -0.02881217682418564
    EV/EBITDA-Capex vs Quick_Ratio: -0.05029226365540777
    EV/EBITDA-Capex vs Current_Ratio: -0.04536994780785337
    EV/EBITDA-Capex vs Debt_to_Equity: 0.014949851439987186
    EV/EBITDA-Capex vs Revenue per Employee: -0.055388014776854406
    EV/EBITDA-Capex vs YOY_Revenue_Change: -0.01790544890347901
    EV/EBITDA-Capex vs YOY_EBIT_Change: -0.038258834941891445
    --- Wholesale Trade ---
    EV/EBITDA vs Debt_Coverage_Ratio: -0.39791502813862795
    EV/EBITDA vs ROE: -0.06418929843492173
    EV/EBITDA vs EBIT Margin (%): -0.09407340207500794
    EV/EBITDA vs YOY_Gross_Profit_Change: -0.17092970995885826
    EV/EBITDA vs ROIC: -0.09755373015362112
    EV/EBITDA vs FCF_Positive: 0.0536943826318509
    EV/EBITDA vs Gross_Margin: -0.08943695244127843
    EV/EBITDA vs Quick_Ratio: 0.14419507172790208
    EV/EBITDA vs Current_Ratio: 0.09140502445057012
    EV/EBITDA vs Debt_to_Equity: -0.047513115350374044
    EV/EBITDA vs Revenue per Employee: -0.1870754148679237
    EV/EBITDA vs YOY_Revenue_Change: -0.028547147418331434
    EV/EBITDA vs YOY_EBIT_Change: 0.1074363696498715
    P/E vs Debt_Coverage_Ratio: 0.09498811722035
    P/E vs ROE: -0.08466391263156389
    P/E vs EBIT Margin (%): -0.031391308871870686
    P/E vs YOY_Gross_Profit_Change: -0.13799652980626453
    P/E vs ROIC: -0.052686286811508075
    P/E vs FCF_Positive: 0.11331788046528132
    P/E vs Gross_Margin: 0.24661008430661677
    P/E vs Quick_Ratio: 0.24935804107866183
    P/E vs Current_Ratio: 0.24782200491016187
    P/E vs Debt_to_Equity: -0.08492709420748708
    P/E vs Revenue per Employee: -0.25628743905251594
    P/E vs YOY_Revenue_Change: -0.026650953789912002
    P/E vs YOY_EBIT_Change: 0.02453571127924996
    EV/GP vs Debt_Coverage_Ratio: 0.0032634414387582925
    EV/GP vs ROE: 0.0608636193232529
    EV/GP vs EBIT Margin (%): -0.05035524064629322
    EV/GP vs YOY_Gross_Profit_Change: -0.10765969155160518
    EV/GP vs ROIC: -0.09334113776620358
    EV/GP vs FCF_Positive: -0.06202395586316193
    EV/GP vs Gross_Margin: -0.1624642475411034
    EV/GP vs Quick_Ratio: 0.48117433751816224
    EV/GP vs Current_Ratio: 0.4141225146313788
    EV/GP vs Debt_to_Equity: 0.06388305590102174
    EV/GP vs Revenue per Employee: -0.2671710046823629
    EV/GP vs YOY_Revenue_Change: 0.010984235751574265
    EV/GP vs YOY_EBIT_Change: 0.007998754884041476
    EV_EBIT vs Debt_Coverage_Ratio: -0.13013055775050347
    EV_EBIT vs ROE: -0.020571410183906763
    EV_EBIT vs EBIT Margin (%): -0.2142613595380801
    EV_EBIT vs YOY_Gross_Profit_Change: -0.07955478123585485
    EV_EBIT vs ROIC: -0.2261051274117716
    EV_EBIT vs FCF_Positive: -0.05535488361486886
    EV_EBIT vs Gross_Margin: -0.06649153955825048
    EV_EBIT vs Quick_Ratio: 0.03875027710393314
    EV_EBIT vs Current_Ratio: -0.013085655333156008
    EV_EBIT vs Debt_to_Equity: -0.014637781511120093
    EV_EBIT vs Revenue per Employee: 0.006691394575570909
    EV_EBIT vs YOY_Revenue_Change: -0.002609407627550128
    EV_EBIT vs YOY_EBIT_Change: 0.02142171924326835
    FCF Yield vs Debt_Coverage_Ratio: -0.0309379705170796
    FCF Yield vs ROE: -0.08686640504273678
    FCF Yield vs EBIT Margin (%): 0.11305520869374104
    FCF Yield vs YOY_Gross_Profit_Change: -0.07392211464622313
    FCF Yield vs ROIC: 0.1313853181076312
    FCF Yield vs FCF_Positive: 0.194055082265809
    FCF Yield vs Gross_Margin: -0.2672015676691491
    FCF Yield vs Quick_Ratio: -0.22802128875283148
    FCF Yield vs Current_Ratio: -0.11682850297062013
    FCF Yield vs Debt_to_Equity: -0.09208759278368636
    FCF Yield vs Revenue per Employee: 0.4770285322220833
    FCF Yield vs YOY_Revenue_Change: -0.11406754402907143
    FCF Yield vs YOY_EBIT_Change: -0.08844190457066525
    EV/EBITDA-Capex vs Debt_Coverage_Ratio: -0.06834227022187804
    EV/EBITDA-Capex vs ROE: -0.0045169349624387895
    EV/EBITDA-Capex vs EBIT Margin (%): -0.025330494845238315
    EV/EBITDA-Capex vs YOY_Gross_Profit_Change: 0.014109318690938503
    EV/EBITDA-Capex vs ROIC: -0.029259389936670092
    EV/EBITDA-Capex vs FCF_Positive: -0.018074301369230467
    EV/EBITDA-Capex vs Gross_Margin: 0.04827617210063475
    EV/EBITDA-Capex vs Quick_Ratio: -0.0735977746334454
    EV/EBITDA-Capex vs Current_Ratio: -0.07293418194524466
    EV/EBITDA-Capex vs Debt_to_Equity: 0.0005178222850221422
    EV/EBITDA-Capex vs Revenue per Employee: -0.005032377674458902
    EV/EBITDA-Capex vs YOY_Revenue_Change: 0.02725230853657669
    EV/EBITDA-Capex vs YOY_EBIT_Change: -0.007490682390115752



```python
import seaborn as sns
import matplotlib.pyplot as plt
# Correlation Analysis

columns_to_drop = ['Ticker'] + ['Division']

# Create a new dataframe without the specified columns
corr_df = selected_df.drop(columns=columns_to_drop)
corr = corr_df.corr()
plt.figure(figsize=(10, 8))
sns.heatmap(corr, cmap='coolwarm', annot=False)
plt.show()
```


    
![png](output_13_0.png)
    



```python

```


```python
# Define the multiples and metrics
multiples = ['EV/EBITDA', 'P/E', 'EV/GP','EV_EBIT','FCF Yield','EV/EBITDA-Capex']
metrics = ['Debt_Coverage_Ratio', 'ROE', 'EBIT Margin (%)',
           'YOY_Gross_Profit_Change','ROIC','FCF_Positive',
           'Gross_Margin','Quick_Ratio','Current_Ratio','Debt_to_Equity',
           'Revenue per Employee','FCF_Positive','YOY_Revenue_Change','YOY_EBIT_Change']

# Drop the specified non-numeric columns
columns_to_drop = ['Ticker', 'Division']

# Iterate over each unique Division in the dataset
grouped_data = selected_df.groupby('Division')
for division, group in grouped_data:
    # Drop the non-numeric columns
    group = group.drop(columns=columns_to_drop, errors='ignore')
    
    # Keep only the columns that are multiples or metrics
    subset = group[multiples + metrics].select_dtypes(include='number')
    
    # Calculate the correlation matrix
    corr = subset.corr()
    
    # Plot the correlation matrix using seaborn heatmap
    plt.figure(figsize=(10, 8))
    sns.heatmap(corr, cmap='coolwarm', annot=True)
    plt.title(f'Correlation Matrix for Division: {division}')
    plt.show()
```


    
![png](output_15_0.png)
    



    
![png](output_15_1.png)
    



    
![png](output_15_2.png)
    



    
![png](output_15_3.png)
    



    
![png](output_15_4.png)
    



    
![png](output_15_5.png)
    



    
![png](output_15_6.png)
    



    
![png](output_15_7.png)
    



```python
import seaborn as sns
import matplotlib.pyplot as plt
from scipy.stats import linregress

# Define the multiples and metrics
multiples = ['EV/EBITDA', 'P/E', 'EV/GP','EV_EBIT','FCF Yield','EV/EBITDA-Capex']
metrics = ['Debt_Coverage_Ratio', 'ROE', 'EBIT Margin (%)',
           'YOY_Gross_Profit_Change','ROIC','FCF_Positive',
           'Gross_Margin','Quick_Ratio','Current_Ratio','Debt_to_Equity',
           'Revenue per Employee','FCF_Positive','YOY_Revenue_Change','YOY_EBIT_Change']

# Group data by sector
grouped_data = selected_df.groupby('Division')

# Calculate correlation between multiples and metrics for each sector
correlation_results = {}
for sector, group in grouped_data:
    correlation_results[sector] = {}
    for multiple in multiples:
        for metric in metrics:
            correlation = group[multiple].corr(group[metric])
            correlation_results[sector][(multiple, metric)] = correlation

# Sort correlation results and select top 5 correlations
top_correlations = {}
for sector, result in correlation_results.items():
    top_correlations[sector] = sorted(result.items(), key=lambda x: abs(x[1]), reverse=True)[:5]

# Plot scatter plots for top 5 correlations
for sector, correlations in top_correlations.items():
    print(f"--- {sector} ---")
    for (multiple, metric), correlation in correlations:
        plt.figure(figsize=(8, 6))
        sns.scatterplot(data=selected_df, x=metric, y=multiple, hue='Division', palette='viridis')
        plt.title(f'Scatter Plot of {metric} vs {multiple} ({sector})')
        plt.xlabel(metric)
        plt.ylabel(multiple)
        plt.legend()
        plt.grid(True)
        plt.tight_layout()
        plt.show()

```

    --- Construction ---



    
![png](output_16_1.png)
    



    
![png](output_16_2.png)
    



    
![png](output_16_3.png)
    



    
![png](output_16_4.png)
    



    
![png](output_16_5.png)
    


    --- Finance, Insurance and Real Estate ---



    
![png](output_16_7.png)
    



    
![png](output_16_8.png)
    



    
![png](output_16_9.png)
    



    
![png](output_16_10.png)
    



    
![png](output_16_11.png)
    


    --- Manufacturing ---



    
![png](output_16_13.png)
    



    
![png](output_16_14.png)
    



    
![png](output_16_15.png)
    



    
![png](output_16_16.png)
    



    
![png](output_16_17.png)
    


    --- Mining_Trans_Comm_Gas_Sanitary ---



    
![png](output_16_19.png)
    



    
![png](output_16_20.png)
    



    
![png](output_16_21.png)
    



    
![png](output_16_22.png)
    



    
![png](output_16_23.png)
    


    --- Retail Trade ---



    
![png](output_16_25.png)
    



    
![png](output_16_26.png)
    



    
![png](output_16_27.png)
    



    
![png](output_16_28.png)
    



    
![png](output_16_29.png)
    


    --- Services ---



    
![png](output_16_31.png)
    



    
![png](output_16_32.png)
    



    
![png](output_16_33.png)
    



    
![png](output_16_34.png)
    



    
![png](output_16_35.png)
    


    --- Unknown_Nonclassifiable ---



    
![png](output_16_37.png)
    



    
![png](output_16_38.png)
    



    
![png](output_16_39.png)
    



    
![png](output_16_40.png)
    



    
![png](output_16_41.png)
    


    --- Wholesale Trade ---



    
![png](output_16_43.png)
    



    
![png](output_16_44.png)
    



    
![png](output_16_45.png)
    



    
![png](output_16_46.png)
    



    
![png](output_16_47.png)
    



```python
import statsmodels.api as sm

# Assuming 'selected_df' is the DataFrame containing the data

# Define the multiples (dependent variables) and metrics (independent variables)
multiples = ['EV/EBITDA', 'P/E', 'EV/GP','EV_EBIT','FCF Yield','EV/EBITDA-Capex']
metrics = ['Debt_Coverage_Ratio', 'ROE', 'EBIT Margin (%)',
           'YOY_Gross_Profit_Change','ROIC','FCF_Positive',
           'Gross_Margin','Quick_Ratio','Current_Ratio','Debt_to_Equity',
           'Revenue per Employee','FCF_Positive','YOY_Revenue_Change','YOY_EBIT_Change']

# Group data by Division
grouped_data = selected_df.groupby('Division')

# Perform MLR for each multiple by each industry
for division, group in grouped_data:
    print(f'\nDivision: {division}')
    
    # Drop non-numeric columns and keep only columns with multiples and metrics
    group = group[multiples + metrics].select_dtypes(include='number')
    
    for multiple in multiples:
        # Prepare the dependent (y) and independent (X) variables
        if multiple in group.columns:
            y = group[multiple].dropna()  # Drop missing values
            X = group.loc[y.index, metrics].dropna()
            
            # Add a constant to the model (intercept term)
            X = sm.add_constant(X)
            
            # Fit the model
            model = sm.OLS(y, X).fit()
            
            # Print the summary of the model
            print(f'\nMultiple: {multiple}')
            print(model.summary())
```

    
    Division: Construction
    
    Multiple: EV/EBITDA
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              EV/EBITDA   R-squared:                       0.699
    Model:                            OLS   Adj. R-squared:                  0.662
    Method:                 Least Squares   F-statistic:                     18.76
    Date:                Sun, 05 May 2024   Prob (F-statistic):           8.54e-22
    Time:                        19:16:55   Log-Likelihood:                -334.51
    No. Observations:                 119   AIC:                             697.0
    Df Residuals:                     105   BIC:                             735.9
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      16.4562      3.841      4.284      0.000       8.840      24.072
    Debt_Coverage_Ratio        -7.2383      5.291     -1.368      0.174     -17.729       3.252
    ROE                       -18.8543      4.862     -3.878      0.000     -28.494      -9.214
    EBIT Margin (%)            -2.0618      1.919     -1.075      0.285      -5.866       1.742
    YOY_Gross_Profit_Change   -11.3433      3.366     -3.370      0.001     -18.017      -4.669
    ROIC                        1.3264      1.008      1.315      0.191      -0.673       3.326
    FCF_Positive               -1.9021      0.565     -3.368      0.001      -3.022      -0.782
    FCF_Positive               -1.9021      0.565     -3.368      0.001      -3.022      -0.782
    Gross_Margin                8.2427     14.562      0.566      0.573     -20.630      37.116
    Quick_Ratio                -4.3678      3.181     -1.373      0.173     -10.675       1.939
    Current_Ratio               5.5941      3.051      1.833      0.070      -0.456      11.645
    Debt_to_Equity              3.0080      0.780      3.858      0.000       1.462       4.554
    Revenue per Employee        0.0008      0.001      0.785      0.434      -0.001       0.003
    FCF_Positive               -1.9021      0.565     -3.368      0.001      -3.022      -0.782
    FCF_Positive               -1.9021      0.565     -3.368      0.001      -3.022      -0.782
    YOY_Revenue_Change         12.6295      4.374      2.887      0.005       3.957      21.302
    YOY_EBIT_Change             2.3348      1.611      1.449      0.150      -0.859       5.529
    ==============================================================================
    Omnibus:                       33.615   Durbin-Watson:                   1.841
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               81.242
    Skew:                           1.081   Prob(JB):                     2.28e-18
    Kurtosis:                       6.422   Cond. No.                     2.55e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 5.68e-37. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: P/E
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    P/E   R-squared:                       0.545
    Model:                            OLS   Adj. R-squared:                  0.488
    Method:                 Least Squares   F-statistic:                     9.656
    Date:                Sun, 05 May 2024   Prob (F-statistic):           6.31e-13
    Time:                        19:16:55   Log-Likelihood:                -306.54
    No. Observations:                 119   AIC:                             641.1
    Df Residuals:                     105   BIC:                             680.0
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       1.9036      3.036      0.627      0.532      -4.117       7.924
    Debt_Coverage_Ratio        -0.4615      4.183     -0.110      0.912      -8.755       7.832
    ROE                       -10.2654      3.843     -2.671      0.009     -17.886      -2.645
    EBIT Margin (%)            -2.0383      1.517     -1.344      0.182      -5.046       0.969
    YOY_Gross_Profit_Change    -9.3030      2.661     -3.496      0.001     -14.579      -4.027
    ROIC                        1.5400      0.797      1.932      0.056      -0.040       3.120
    FCF_Positive               -0.3477      0.446     -0.779      0.438      -1.233       0.537
    FCF_Positive               -0.3477      0.446     -0.779      0.438      -1.233       0.537
    Gross_Margin               11.4031     11.511      0.991      0.324     -11.422      34.228
    Quick_Ratio                -5.3687      2.514     -2.135      0.035     -10.354      -0.383
    Current_Ratio               6.5661      2.412      2.722      0.008       1.783      11.349
    Debt_to_Equity              1.6225      0.616      2.632      0.010       0.400       2.845
    Revenue per Employee        0.0013      0.001      1.630      0.106      -0.000       0.003
    FCF_Positive               -0.3477      0.446     -0.779      0.438      -1.233       0.537
    FCF_Positive               -0.3477      0.446     -0.779      0.438      -1.233       0.537
    YOY_Revenue_Change         10.4224      3.458      3.014      0.003       3.566      17.279
    YOY_EBIT_Change             2.3300      1.274      1.830      0.070      -0.195       4.855
    ==============================================================================
    Omnibus:                       14.465   Durbin-Watson:                   1.716
    Prob(Omnibus):                  0.001   Jarque-Bera (JB):               22.680
    Skew:                           0.574   Prob(JB):                     1.19e-05
    Kurtosis:                       4.804   Cond. No.                     2.55e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 5.68e-37. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/GP
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                  EV/GP   R-squared:                       0.636
    Model:                            OLS   Adj. R-squared:                  0.591
    Method:                 Least Squares   F-statistic:                     14.12
    Date:                Sun, 05 May 2024   Prob (F-statistic):           1.08e-17
    Time:                        19:16:55   Log-Likelihood:                -246.68
    No. Observations:                 119   AIC:                             521.4
    Df Residuals:                     105   BIC:                             560.3
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       3.2357      1.836      1.762      0.081      -0.405       6.876
    Debt_Coverage_Ratio         1.7976      2.529      0.711      0.479      -3.217       6.813
    ROE                        -9.8138      2.324     -4.223      0.000     -14.422      -5.205
    EBIT Margin (%)             2.3328      0.917      2.544      0.012       0.514       4.151
    YOY_Gross_Profit_Change    -2.8312      1.609     -1.760      0.081      -6.022       0.359
    ROIC                       -0.7968      0.482     -1.653      0.101      -1.752       0.159
    FCF_Positive               -0.3140      0.270     -1.163      0.247      -0.849       0.221
    FCF_Positive               -0.3140      0.270     -1.163      0.247      -0.849       0.221
    Gross_Margin                0.2013      6.961      0.029      0.977     -13.601      14.004
    Quick_Ratio                -3.0924      1.520     -2.034      0.044      -6.107      -0.078
    Current_Ratio               3.7893      1.459      2.598      0.011       0.897       6.682
    Debt_to_Equity              1.5993      0.373      4.291      0.000       0.860       2.338
    Revenue per Employee        0.0007      0.000      1.359      0.177      -0.000       0.002
    FCF_Positive               -0.3140      0.270     -1.163      0.247      -0.849       0.221
    FCF_Positive               -0.3140      0.270     -1.163      0.247      -0.849       0.221
    YOY_Revenue_Change          4.6184      2.091      2.209      0.029       0.473       8.764
    YOY_EBIT_Change             0.0815      0.770      0.106      0.916      -1.446       1.608
    ==============================================================================
    Omnibus:                       21.741   Durbin-Watson:                   1.217
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               31.898
    Skew:                           0.898   Prob(JB):                     1.18e-07
    Kurtosis:                       4.792   Cond. No.                     2.55e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 5.68e-37. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV_EBIT
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                EV_EBIT   R-squared:                       0.583
    Model:                            OLS   Adj. R-squared:                  0.532
    Method:                 Least Squares   F-statistic:                     11.30
    Date:                Sun, 05 May 2024   Prob (F-statistic):           8.69e-15
    Time:                        19:16:55   Log-Likelihood:                -266.26
    No. Observations:                 119   AIC:                             560.5
    Df Residuals:                     105   BIC:                             599.4
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      -5.7016      2.165     -2.634      0.010      -9.994      -1.409
    Debt_Coverage_Ratio        -7.2117      2.982     -2.419      0.017     -13.124      -1.299
    ROE                        -3.0594      2.740     -1.117      0.267      -8.492       2.373
    EBIT Margin (%)            -4.8529      1.081     -4.488      0.000      -6.997      -2.709
    YOY_Gross_Profit_Change    -2.4652      1.897     -1.300      0.197      -6.227       1.296
    ROIC                        1.8352      0.568      3.230      0.002       0.709       2.962
    FCF_Positive                0.2390      0.318      0.751      0.454      -0.392       0.870
    FCF_Positive                0.2390      0.318      0.751      0.454      -0.392       0.870
    Gross_Margin               46.4234      8.206      5.657      0.000      30.151      62.695
    Quick_Ratio                -0.8440      1.793     -0.471      0.639      -4.398       2.710
    Current_Ratio               1.5873      1.720      0.923      0.358      -1.823       4.997
    Debt_to_Equity              0.4907      0.439      1.117      0.267      -0.381       1.362
    Revenue per Employee        0.0001      0.001      0.249      0.804      -0.001       0.001
    FCF_Positive                0.2390      0.318      0.751      0.454      -0.392       0.870
    FCF_Positive                0.2390      0.318      0.751      0.454      -0.392       0.870
    YOY_Revenue_Change          2.0031      2.465      0.813      0.418      -2.885       6.891
    YOY_EBIT_Change             0.0765      0.908      0.084      0.933      -1.724       1.877
    ==============================================================================
    Omnibus:                       37.935   Durbin-Watson:                   0.756
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              116.163
    Skew:                           1.122   Prob(JB):                     5.96e-26
    Kurtosis:                       7.288   Cond. No.                     2.55e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 5.68e-37. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: FCF Yield
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              FCF Yield   R-squared:                       0.250
    Model:                            OLS   Adj. R-squared:                  0.157
    Method:                 Least Squares   F-statistic:                     2.691
    Date:                Sun, 05 May 2024   Prob (F-statistic):            0.00264
    Time:                        19:16:55   Log-Likelihood:                -63.679
    No. Observations:                 119   AIC:                             155.4
    Df Residuals:                     105   BIC:                             194.3
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       0.4404      0.395      1.116      0.267      -0.342       1.223
    Debt_Coverage_Ratio         0.6451      0.543      1.187      0.238      -0.432       1.723
    ROE                        -0.1492      0.499     -0.299      0.766      -1.139       0.841
    EBIT Margin (%)             0.4850      0.197      2.461      0.015       0.094       0.876
    YOY_Gross_Profit_Change     0.4799      0.346      1.388      0.168      -0.206       1.165
    ROIC                       -0.2382      0.104     -2.300      0.023      -0.443      -0.033
    FCF_Positive                0.0881      0.058      1.520      0.132      -0.027       0.203
    FCF_Positive                0.0881      0.058      1.520      0.132      -0.027       0.203
    Gross_Margin               -1.7919      1.496     -1.198      0.234      -4.757       1.174
    Quick_Ratio                 0.1267      0.327      0.388      0.699      -0.521       0.774
    Current_Ratio              -0.1753      0.313     -0.559      0.577      -0.797       0.446
    Debt_to_Equity              0.0361      0.080      0.450      0.654      -0.123       0.195
    Revenue per Employee       -0.0002      0.000     -2.071      0.041      -0.000   -9.18e-06
    FCF_Positive                0.0881      0.058      1.520      0.132      -0.027       0.203
    FCF_Positive                0.0881      0.058      1.520      0.132      -0.027       0.203
    YOY_Revenue_Change         -0.5698      0.449     -1.268      0.207      -1.461       0.321
    YOY_EBIT_Change            -0.3911      0.165     -2.364      0.020      -0.719      -0.063
    ==============================================================================
    Omnibus:                      172.805   Durbin-Watson:                   1.315
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):             9119.804
    Skew:                           5.499   Prob(JB):                         0.00
    Kurtosis:                      44.453   Cond. No.                     2.55e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 5.68e-37. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/EBITDA-Capex
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:        EV/EBITDA-Capex   R-squared:                       0.134
    Model:                            OLS   Adj. R-squared:                  0.026
    Method:                 Least Squares   F-statistic:                     1.246
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.258
    Time:                        19:16:55   Log-Likelihood:                -674.40
    No. Observations:                 119   AIC:                             1377.
    Df Residuals:                     105   BIC:                             1416.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                     120.2188     66.818      1.799      0.075     -12.269     252.707
    Debt_Coverage_Ratio        26.4618     92.041      0.288      0.774    -156.038     208.962
    ROE                       -83.9230     84.576     -0.992      0.323    -251.622      83.776
    EBIT Margin (%)           -38.1291     33.375     -1.142      0.256    -104.307      28.048
    YOY_Gross_Profit_Change    34.6633     58.555      0.592      0.555     -81.441     150.768
    ROIC                       -6.6817     17.540     -0.381      0.704     -41.461      28.097
    FCF_Positive                7.0781      9.824      0.720      0.473     -12.401      26.557
    FCF_Positive                7.0781      9.824      0.720      0.473     -12.401      26.557
    Gross_Margin             -273.8108    253.316     -1.081      0.282    -776.089     228.467
    Quick_Ratio                40.4397     55.332      0.731      0.466     -69.273     150.153
    Current_Ratio             -41.5915     53.084     -0.784      0.435    -146.847      63.664
    Debt_to_Equity             12.6536     13.564      0.933      0.353     -14.241      39.548
    Revenue per Employee       -0.0246      0.018     -1.391      0.167      -0.060       0.010
    FCF_Positive                7.0781      9.824      0.720      0.473     -12.401      26.557
    FCF_Positive                7.0781      9.824      0.720      0.473     -12.401      26.557
    YOY_Revenue_Change         57.9492     76.090      0.762      0.448     -92.923     208.822
    YOY_EBIT_Change           -38.8915     28.025     -1.388      0.168     -94.459      16.676
    ==============================================================================
    Omnibus:                      220.934   Durbin-Watson:                   2.163
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):            31563.006
    Skew:                           8.113   Prob(JB):                         0.00
    Kurtosis:                      81.118   Cond. No.                     2.55e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 5.68e-37. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Division: Finance, Insurance and Real Estate
    
    Multiple: EV/EBITDA
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              EV/EBITDA   R-squared:                       0.365
    Model:                            OLS   Adj. R-squared:                  0.163
    Method:                 Least Squares   F-statistic:                     1.811
    Date:                Sun, 05 May 2024   Prob (F-statistic):             0.0742
    Time:                        19:16:56   Log-Likelihood:                -221.85
    No. Observations:                  55   AIC:                             471.7
    Df Residuals:                      41   BIC:                             499.8
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      32.0787      9.288      3.454      0.001      13.322      50.836
    Debt_Coverage_Ratio       -32.7677     29.253     -1.120      0.269     -91.846      26.310
    ROE                        -3.4598      1.510     -2.292      0.027      -6.509      -0.411
    EBIT Margin (%)             6.1338      4.348      1.411      0.166      -2.648      14.916
    YOY_Gross_Profit_Change    -6.3487     10.698     -0.593      0.556     -27.954      15.257
    ROIC                        4.4187     49.914      0.089      0.930     -96.386     105.223
    FCF_Positive               -4.5011      2.294     -1.962      0.057      -9.134       0.131
    FCF_Positive               -4.5011      2.294     -1.962      0.057      -9.134       0.131
    Gross_Margin                7.2021     17.202      0.419      0.678     -27.538      41.943
    Quick_Ratio               -18.1231     45.804     -0.396      0.694    -110.625      74.379
    Current_Ratio              19.9893     45.457      0.440      0.662     -71.814     111.792
    Debt_to_Equity              0.4468      0.210      2.127      0.039       0.023       0.871
    Revenue per Employee        0.0005      0.002      0.239      0.812      -0.004       0.005
    FCF_Positive               -4.5011      2.294     -1.962      0.057      -9.134       0.131
    FCF_Positive               -4.5011      2.294     -1.962      0.057      -9.134       0.131
    YOY_Revenue_Change         -7.2781     17.860     -0.408      0.686     -43.347      28.791
    YOY_EBIT_Change             1.9217      4.222      0.455      0.651      -6.606      10.449
    ==============================================================================
    Omnibus:                       40.800   Durbin-Watson:                   1.675
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              163.408
    Skew:                           1.945   Prob(JB):                     3.28e-36
    Kurtosis:                      10.495   Cond. No.                     1.34e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 9.81e-37. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: P/E
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    P/E   R-squared:                       0.727
    Model:                            OLS   Adj. R-squared:                  0.641
    Method:                 Least Squares   F-statistic:                     8.401
    Date:                Sun, 05 May 2024   Prob (F-statistic):           6.65e-08
    Time:                        19:16:56   Log-Likelihood:                -142.83
    No. Observations:                  55   AIC:                             313.7
    Df Residuals:                      41   BIC:                             341.8
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       2.8136      2.207      1.275      0.210      -1.644       7.272
    Debt_Coverage_Ratio         7.5323      6.953      1.083      0.285      -6.509      21.574
    ROE                         0.7998      0.359      2.229      0.031       0.075       1.524
    EBIT Margin (%)             0.1913      1.034      0.185      0.854      -1.896       2.279
    YOY_Gross_Profit_Change    -2.5868      2.543     -1.017      0.315      -7.722       2.548
    ROIC                        7.1018     11.863      0.599      0.553     -16.857      31.060
    FCF_Positive               -0.2769      0.545     -0.508      0.614      -1.378       0.824
    FCF_Positive               -0.2769      0.545     -0.508      0.614      -1.378       0.824
    Gross_Margin                4.2864      4.089      1.048      0.301      -3.970      12.543
    Quick_Ratio               -32.1140     10.886     -2.950      0.005     -54.099     -10.129
    Current_Ratio              32.7319     10.804      3.030      0.004      10.913      54.551
    Debt_to_Equity             -0.1434      0.050     -2.874      0.006      -0.244      -0.043
    Revenue per Employee    -8.256e-06      0.000     -0.017      0.987      -0.001       0.001
    FCF_Positive               -0.2769      0.545     -0.508      0.614      -1.378       0.824
    FCF_Positive               -0.2769      0.545     -0.508      0.614      -1.378       0.824
    YOY_Revenue_Change         -0.1058      4.245     -0.025      0.980      -8.679       8.467
    YOY_EBIT_Change             1.4822      1.004      1.477      0.147      -0.545       3.509
    ==============================================================================
    Omnibus:                       32.859   Durbin-Watson:                   1.707
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               84.916
    Skew:                           1.716   Prob(JB):                     3.64e-19
    Kurtosis:                       8.027   Cond. No.                     1.34e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 9.81e-37. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/GP
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                  EV/GP   R-squared:                       0.483
    Model:                            OLS   Adj. R-squared:                  0.319
    Method:                 Least Squares   F-statistic:                     2.945
    Date:                Sun, 05 May 2024   Prob (F-statistic):            0.00416
    Time:                        19:16:56   Log-Likelihood:                -214.72
    No. Observations:                  55   AIC:                             457.4
    Df Residuals:                      41   BIC:                             485.5
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      34.7823      8.157      4.264      0.000      18.308      51.256
    Debt_Coverage_Ratio       -13.0805     25.693     -0.509      0.613     -64.968      38.807
    ROE                        -3.3930      1.326     -2.559      0.014      -6.071      -0.715
    EBIT Margin (%)             8.9168      3.819      2.335      0.025       1.204      16.630
    YOY_Gross_Profit_Change    -4.8671      9.396     -0.518      0.607     -23.843      14.109
    ROIC                       -0.5254     43.839     -0.012      0.990     -89.061      88.010
    FCF_Positive               -4.4167      2.015     -2.192      0.034      -8.485      -0.348
    FCF_Positive               -4.4167      2.015     -2.192      0.034      -8.485      -0.348
    Gross_Margin               -9.6960     15.108     -0.642      0.525     -40.208      20.816
    Quick_Ratio                19.3466     40.229      0.481      0.633     -61.897     100.590
    Current_Ratio             -18.9436     39.925     -0.474      0.638     -99.573      61.686
    Debt_to_Equity              0.4460      0.184      2.418      0.020       0.073       0.819
    Revenue per Employee        0.0016      0.002      0.905      0.371      -0.002       0.005
    FCF_Positive               -4.4167      2.015     -2.192      0.034      -8.485      -0.348
    FCF_Positive               -4.4167      2.015     -2.192      0.034      -8.485      -0.348
    YOY_Revenue_Change         -3.9686     15.686     -0.253      0.802     -35.648      27.711
    YOY_EBIT_Change             1.6910      3.709      0.456      0.651      -5.798       9.180
    ==============================================================================
    Omnibus:                       37.260   Durbin-Watson:                   1.263
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              199.447
    Skew:                           1.560   Prob(JB):                     4.90e-44
    Kurtosis:                      11.792   Cond. No.                     1.34e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 9.81e-37. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV_EBIT
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                EV_EBIT   R-squared:                       0.612
    Model:                            OLS   Adj. R-squared:                  0.488
    Method:                 Least Squares   F-statistic:                     4.967
    Date:                Sun, 05 May 2024   Prob (F-statistic):           3.81e-05
    Time:                        19:16:56   Log-Likelihood:                -252.96
    No. Observations:                  55   AIC:                             533.9
    Df Residuals:                      41   BIC:                             562.0
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      72.3173     16.351      4.423      0.000      39.296     105.339
    Debt_Coverage_Ratio       -34.6494     51.500     -0.673      0.505    -138.656      69.357
    ROE                        -2.2472      2.658     -0.846      0.403      -7.615       3.120
    EBIT Margin (%)           -13.8818      7.655     -1.813      0.077     -29.342       1.579
    YOY_Gross_Profit_Change   -32.9638     18.834     -1.750      0.088     -71.000       5.073
    ROIC                       69.9437     87.874      0.796      0.431    -107.521     247.408
    FCF_Positive              -14.5566      4.038     -3.605      0.001     -22.712      -6.401
    FCF_Positive              -14.5566      4.038     -3.605      0.001     -22.712      -6.401
    Gross_Margin               36.8306     30.284      1.216      0.231     -24.329      97.991
    Quick_Ratio               113.3788     80.637      1.406      0.167     -49.470     276.228
    Current_Ratio            -110.6565     80.027     -1.383      0.174    -272.275      50.962
    Debt_to_Equity             -0.2527      0.370     -0.683      0.498      -0.999       0.494
    Revenue per Employee        0.0020      0.004      0.545      0.589      -0.005       0.009
    FCF_Positive              -14.5566      4.038     -3.605      0.001     -22.712      -6.401
    FCF_Positive              -14.5566      4.038     -3.605      0.001     -22.712      -6.401
    YOY_Revenue_Change         50.8350     31.443      1.617      0.114     -12.665     114.335
    YOY_EBIT_Change             3.3283      7.434      0.448      0.657     -11.684      18.341
    ==============================================================================
    Omnibus:                        3.887   Durbin-Watson:                   1.650
    Prob(Omnibus):                  0.143   Jarque-Bera (JB):                3.438
    Skew:                           0.258   Prob(JB):                        0.179
    Kurtosis:                       4.111   Cond. No.                     1.34e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 9.81e-37. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: FCF Yield
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              FCF Yield   R-squared:                       0.483
    Model:                            OLS   Adj. R-squared:                  0.319
    Method:                 Least Squares   F-statistic:                     2.948
    Date:                Sun, 05 May 2024   Prob (F-statistic):            0.00413
    Time:                        19:16:56   Log-Likelihood:                 46.895
    No. Observations:                  55   AIC:                            -65.79
    Df Residuals:                      41   BIC:                            -37.69
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      -0.0644      0.070     -0.919      0.364      -0.206       0.077
    Debt_Coverage_Ratio         0.1041      0.221      0.471      0.640      -0.342       0.550
    ROE                        -0.0264      0.011     -2.315      0.026      -0.049      -0.003
    EBIT Margin (%)            -0.0348      0.033     -1.061      0.295      -0.101       0.031
    YOY_Gross_Profit_Change     0.0384      0.081      0.476      0.637      -0.125       0.202
    ROIC                       -0.3398      0.377     -0.902      0.372      -1.101       0.421
    FCF_Positive                0.0742      0.017      4.283      0.000       0.039       0.109
    FCF_Positive                0.0742      0.017      4.283      0.000       0.039       0.109
    Gross_Margin               -0.1104      0.130     -0.850      0.400      -0.373       0.152
    Quick_Ratio                 0.1523      0.346      0.441      0.662      -0.546       0.851
    Current_Ratio              -0.1479      0.343     -0.431      0.669      -0.841       0.545
    Debt_to_Equity              0.0036      0.002      2.283      0.028       0.000       0.007
    Revenue per Employee    -1.492e-05   1.56e-05     -0.958      0.344   -4.64e-05    1.65e-05
    FCF_Positive                0.0742      0.017      4.283      0.000       0.039       0.109
    FCF_Positive                0.0742      0.017      4.283      0.000       0.039       0.109
    YOY_Revenue_Change          0.0941      0.135      0.698      0.489      -0.178       0.366
    YOY_EBIT_Change            -0.0304      0.032     -0.953      0.346      -0.095       0.034
    ==============================================================================
    Omnibus:                        5.600   Durbin-Watson:                   1.580
    Prob(Omnibus):                  0.061   Jarque-Bera (JB):                6.387
    Skew:                           0.307   Prob(JB):                       0.0410
    Kurtosis:                       4.553   Cond. No.                     1.34e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 9.81e-37. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/EBITDA-Capex
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:        EV/EBITDA-Capex   R-squared:                       0.559
    Model:                            OLS   Adj. R-squared:                  0.420
    Method:                 Least Squares   F-statistic:                     4.005
    Date:                Sun, 05 May 2024   Prob (F-statistic):           0.000323
    Time:                        19:16:56   Log-Likelihood:                -263.01
    No. Observations:                  55   AIC:                             554.0
    Df Residuals:                      41   BIC:                             582.1
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                     128.4046     19.627      6.542      0.000      88.767     168.042
    Debt_Coverage_Ratio       -63.7480     61.818     -1.031      0.308    -188.592      61.096
    ROE                        -8.6554      3.190     -2.713      0.010     -15.098      -2.212
    EBIT Margin (%)            -0.5041      9.189     -0.055      0.957     -19.062      18.054
    YOY_Gross_Profit_Change   -33.7454     22.608     -1.493      0.143     -79.403      11.912
    ROIC                       48.8579    105.479      0.463      0.646    -164.162     261.878
    FCF_Positive              -25.4530      4.847     -5.251      0.000     -35.243     -15.663
    FCF_Positive              -25.4530      4.847     -5.251      0.000     -35.243     -15.663
    Gross_Margin               -4.1441     36.352     -0.114      0.910     -77.558      69.270
    Quick_Ratio               -28.5654     96.792     -0.295      0.769    -224.042     166.911
    Current_Ratio              27.0276     96.061      0.281      0.780    -166.971     221.026
    Debt_to_Equity              0.9887      0.444      2.228      0.031       0.092       1.885
    Revenue per Employee       -0.0036      0.004     -0.825      0.414      -0.012       0.005
    FCF_Positive              -25.4530      4.847     -5.251      0.000     -35.243     -15.663
    FCF_Positive              -25.4530      4.847     -5.251      0.000     -35.243     -15.663
    YOY_Revenue_Change         66.7360     37.742      1.768      0.084      -9.486     142.958
    YOY_EBIT_Change             3.9642      8.923      0.444      0.659     -14.056      21.984
    ==============================================================================
    Omnibus:                       14.754   Durbin-Watson:                   1.706
    Prob(Omnibus):                  0.001   Jarque-Bera (JB):               37.877
    Skew:                           0.588   Prob(JB):                     5.96e-09
    Kurtosis:                       6.891   Cond. No.                     1.34e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 9.81e-37. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Division: Manufacturing
    
    Multiple: EV/EBITDA
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              EV/EBITDA   R-squared:                       0.016
    Model:                            OLS   Adj. R-squared:                 -0.001
    Method:                 Least Squares   F-statistic:                    0.9171
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.535
    Time:                        19:16:56   Log-Likelihood:                -4691.2
    No. Observations:                 753   AIC:                             9410.
    Df Residuals:                     739   BIC:                             9475.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       6.7887     36.968      0.184      0.854     -65.786      79.363
    Debt_Coverage_Ratio       -25.9830     15.363     -1.691      0.091     -56.143       4.177
    ROE                        -7.3439      9.041     -0.812      0.417     -25.094      10.406
    EBIT Margin (%)             5.1253      8.224      0.623      0.533     -11.019      21.270
    YOY_Gross_Profit_Change   -32.5782     37.608     -0.866      0.387    -106.410      41.254
    ROIC                       -3.5850     12.666     -0.283      0.777     -28.451      21.281
    FCF_Positive                3.7461      8.453      0.443      0.658     -12.849      20.341
    FCF_Positive                3.7461      8.453      0.443      0.658     -12.849      20.341
    Gross_Margin               30.2925     38.271      0.792      0.429     -44.840     105.425
    Quick_Ratio                 6.4231      7.298      0.880      0.379      -7.905      20.751
    Current_Ratio              -6.6106      6.691     -0.988      0.323     -19.746       6.525
    Debt_to_Equity              0.3709      0.521      0.711      0.477      -0.653       1.395
    Revenue per Employee        0.0374      0.026      1.419      0.156      -0.014       0.089
    FCF_Positive                3.7461      8.453      0.443      0.658     -12.849      20.341
    FCF_Positive                3.7461      8.453      0.443      0.658     -12.849      20.341
    YOY_Revenue_Change         15.9588     48.489      0.329      0.742     -79.234     111.151
    YOY_EBIT_Change             0.1634      1.776      0.092      0.927      -3.323       3.650
    ==============================================================================
    Omnibus:                     1740.777   Durbin-Watson:                   1.964
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):          7018017.629
    Skew:                          20.326   Prob(JB):                         0.00
    Kurtosis:                     474.200   Cond. No.                     2.24e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 2.19e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: P/E
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    P/E   R-squared:                       0.012
    Model:                            OLS   Adj. R-squared:                 -0.006
    Method:                 Least Squares   F-statistic:                    0.6718
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.792
    Time:                        19:16:56   Log-Likelihood:                -4661.6
    No. Observations:                 753   AIC:                             9351.
    Df Residuals:                     739   BIC:                             9416.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      -5.4397     35.546     -0.153      0.878     -75.222      64.343
    Debt_Coverage_Ratio       -18.4670     14.772     -1.250      0.212     -47.466      10.532
    ROE                        -5.5720      8.693     -0.641      0.522     -22.639      11.495
    EBIT Margin (%)             5.3248      7.907      0.673      0.501     -10.199      20.848
    YOY_Gross_Profit_Change   -21.5882     36.161     -0.597      0.551     -92.580      49.403
    ROIC                       -5.8825     12.179     -0.483      0.629     -29.792      18.027
    FCF_Positive                4.4771      8.128      0.551      0.582     -11.480      20.434
    FCF_Positive                4.4771      8.128      0.551      0.582     -11.480      20.434
    Gross_Margin               25.1636     36.798      0.684      0.494     -47.078      97.405
    Quick_Ratio                 6.5393      7.018      0.932      0.352      -7.237      20.316
    Current_Ratio              -6.2331      6.433     -0.969      0.333     -18.863       6.397
    Debt_to_Equity              0.2869      0.501      0.572      0.567      -0.697       1.271
    Revenue per Employee        0.0401      0.025      1.581      0.114      -0.010       0.090
    FCF_Positive                4.4771      8.128      0.551      0.582     -11.480      20.434
    FCF_Positive                4.4771      8.128      0.551      0.582     -11.480      20.434
    YOY_Revenue_Change          5.7633     46.623      0.124      0.902     -85.767      97.293
    YOY_EBIT_Change             0.4014      1.708      0.235      0.814      -2.951       3.754
    ==============================================================================
    Omnibus:                     1827.723   Durbin-Watson:                   1.957
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):         10301280.216
    Skew:                          22.762   Prob(JB):                         0.00
    Kurtosis:                     574.188   Cond. No.                     2.24e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 2.19e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/GP
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                  EV/GP   R-squared:                       0.259
    Model:                            OLS   Adj. R-squared:                  0.246
    Method:                 Least Squares   F-statistic:                     19.88
    Date:                Sun, 05 May 2024   Prob (F-statistic):           2.30e-40
    Time:                        19:16:56   Log-Likelihood:                -2164.6
    No. Observations:                 753   AIC:                             4357.
    Df Residuals:                     739   BIC:                             4422.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       6.5248      1.290      5.058      0.000       3.992       9.057
    Debt_Coverage_Ratio        -0.5267      0.536     -0.982      0.326      -1.579       0.526
    ROE                         2.1501      0.316      6.815      0.000       1.531       2.770
    EBIT Margin (%)             1.8503      0.287      6.448      0.000       1.287       2.414
    YOY_Gross_Profit_Change    -4.3005      1.312     -3.277      0.001      -6.877      -1.724
    ROIC                       -1.4345      0.442     -3.245      0.001      -2.302      -0.567
    FCF_Positive               -0.5167      0.295     -1.752      0.080      -1.096       0.062
    FCF_Positive               -0.5167      0.295     -1.752      0.080      -1.096       0.062
    Gross_Margin               -3.8435      1.336     -2.878      0.004      -6.465      -1.222
    Quick_Ratio                 0.9476      0.255      3.721      0.000       0.448       1.448
    Current_Ratio              -0.5368      0.233     -2.299      0.022      -0.995      -0.078
    Debt_to_Equity             -0.0783      0.018     -4.305      0.000      -0.114      -0.043
    Revenue per Employee        0.0036      0.001      3.899      0.000       0.002       0.005
    FCF_Positive               -0.5167      0.295     -1.752      0.080      -1.096       0.062
    FCF_Positive               -0.5167      0.295     -1.752      0.080      -1.096       0.062
    YOY_Revenue_Change          6.3500      1.692      3.753      0.000       3.028       9.672
    YOY_EBIT_Change             0.0131      0.062      0.211      0.833      -0.109       0.135
    ==============================================================================
    Omnibus:                      797.173   Durbin-Watson:                   1.290
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):            60638.845
    Skew:                           4.849   Prob(JB):                         0.00
    Kurtosis:                      45.879   Cond. No.                     2.24e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 2.19e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV_EBIT
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                EV_EBIT   R-squared:                       0.021
    Model:                            OLS   Adj. R-squared:                  0.004
    Method:                 Least Squares   F-statistic:                     1.232
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.251
    Time:                        19:16:56   Log-Likelihood:                -4453.0
    No. Observations:                 753   AIC:                             8934.
    Df Residuals:                     739   BIC:                             8999.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                     -28.3562     26.943     -1.052      0.293     -81.250      24.538
    Debt_Coverage_Ratio        -7.8420     11.197     -0.700      0.484     -29.823      14.139
    ROE                        -1.1840      6.589     -0.180      0.857     -14.120      11.752
    EBIT Margin (%)            -3.7594      5.994     -0.627      0.531     -15.526       8.007
    YOY_Gross_Profit_Change   -10.0553     27.410     -0.367      0.714     -63.865      43.755
    ROIC                        5.5378      9.231      0.600      0.549     -12.585      23.661
    FCF_Positive               -1.0305      6.161     -0.167      0.867     -13.125      11.064
    FCF_Positive               -1.0305      6.161     -0.167      0.867     -13.125      11.064
    Gross_Margin               35.6310     27.892      1.277      0.202     -19.127      90.389
    Quick_Ratio                 3.6218      5.319      0.681      0.496      -6.821      14.064
    Current_Ratio              -0.6504      4.876     -0.133      0.894     -10.224       8.923
    Debt_to_Equity              0.0323      0.380      0.085      0.932      -0.714       0.778
    Revenue per Employee        0.0441      0.019      2.294      0.022       0.006       0.082
    FCF_Positive               -1.0305      6.161     -0.167      0.867     -13.125      11.064
    FCF_Positive               -1.0305      6.161     -0.167      0.867     -13.125      11.064
    YOY_Revenue_Change         17.6344     35.340      0.499      0.618     -51.744      87.013
    YOY_EBIT_Change            -0.1226      1.294     -0.095      0.925      -2.664       2.418
    ==============================================================================
    Omnibus:                      705.624   Durbin-Watson:                   1.986
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):          1891572.479
    Skew:                           2.807   Prob(JB):                         0.00
    Kurtosis:                     248.474   Cond. No.                     2.24e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 2.19e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: FCF Yield
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              FCF Yield   R-squared:                       0.255
    Model:                            OLS   Adj. R-squared:                  0.242
    Method:                 Least Squares   F-statistic:                     19.51
    Date:                Sun, 05 May 2024   Prob (F-statistic):           1.25e-39
    Time:                        19:16:56   Log-Likelihood:                 40.387
    No. Observations:                 753   AIC:                            -52.77
    Df Residuals:                     739   BIC:                             11.96
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       0.1654      0.069      2.396      0.017       0.030       0.301
    Debt_Coverage_Ratio        -0.0886      0.029     -3.091      0.002      -0.145      -0.032
    ROE                        -0.0291      0.017     -1.724      0.085      -0.062       0.004
    EBIT Margin (%)             0.0188      0.015      1.227      0.220      -0.011       0.049
    YOY_Gross_Profit_Change     0.1763      0.070      2.512      0.012       0.038       0.314
    ROIC                       -0.0648      0.024     -2.740      0.006      -0.111      -0.018
    FCF_Positive                0.0924      0.016      5.855      0.000       0.061       0.123
    FCF_Positive                0.0924      0.016      5.855      0.000       0.061       0.123
    Gross_Margin               -0.4451      0.071     -6.231      0.000      -0.585      -0.305
    Quick_Ratio                -0.1140      0.014     -8.365      0.000      -0.141      -0.087
    Current_Ratio               0.1039      0.012      8.319      0.000       0.079       0.128
    Debt_to_Equity              0.0016      0.001      1.628      0.104      -0.000       0.003
    Revenue per Employee    -2.621e-05   4.92e-05     -0.533      0.594      -0.000    7.03e-05
    FCF_Positive                0.0924      0.016      5.855      0.000       0.061       0.123
    FCF_Positive                0.0924      0.016      5.855      0.000       0.061       0.123
    YOY_Revenue_Change         -0.2907      0.091     -3.212      0.001      -0.468      -0.113
    YOY_EBIT_Change            -0.0046      0.003     -1.374      0.170      -0.011       0.002
    ==============================================================================
    Omnibus:                      377.652   Durbin-Watson:                   1.097
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):             2923.100
    Skew:                           2.129   Prob(JB):                         0.00
    Kurtosis:                      11.662   Cond. No.                     2.24e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 2.19e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/EBITDA-Capex
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:        EV/EBITDA-Capex   R-squared:                       0.010
    Model:                            OLS   Adj. R-squared:                 -0.007
    Method:                 Least Squares   F-statistic:                    0.5706
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.878
    Time:                        19:16:56   Log-Likelihood:                -8357.5
    No. Observations:                 753   AIC:                         1.674e+04
    Df Residuals:                     739   BIC:                         1.681e+04
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                    -842.5406   4812.837     -0.175      0.861   -1.03e+04    8605.921
    Debt_Coverage_Ratio       569.9181   2000.065      0.285      0.776   -3356.569    4496.405
    ROE                       573.5398   1177.084      0.487      0.626   -1737.287    2884.366
    EBIT Margin (%)          -358.4965   1070.645     -0.335      0.738   -2460.365    1743.372
    YOY_Gross_Profit_Change   494.3734   4896.214      0.101      0.920   -9117.773    1.01e+04
    ROIC                      824.3086   1649.022      0.500      0.617   -2413.016    4061.634
    FCF_Positive             -373.0821   1100.514     -0.339      0.735   -2533.589    1787.425
    FCF_Positive             -373.0821   1100.514     -0.339      0.735   -2533.589    1787.425
    Gross_Margin             6648.7653   4982.435      1.334      0.182   -3132.647    1.64e+04
    Quick_Ratio             -1231.1593    950.170     -1.296      0.195   -3096.514     634.195
    Current_Ratio            1192.3270    871.073      1.369      0.171    -517.744    2902.399
    Debt_to_Equity            -27.8672     67.885     -0.411      0.682    -161.138     105.403
    Revenue per Employee       -6.8412      3.430     -1.994      0.046     -13.575      -0.107
    FCF_Positive             -373.0821   1100.514     -0.339      0.735   -2533.589    1787.425
    FCF_Positive             -373.0821   1100.514     -0.339      0.735   -2533.589    1787.425
    YOY_Revenue_Change       1608.5516   6312.747      0.255      0.799   -1.08e+04     1.4e+04
    YOY_EBIT_Change           -18.4876    231.206     -0.080      0.936    -472.386     435.411
    ==============================================================================
    Omnibus:                     1958.249   Durbin-Watson:                   1.987
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):         16849396.497
    Skew:                         -26.914   Prob(JB):                         0.00
    Kurtosis:                     733.845   Cond. No.                     2.24e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 2.19e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Division: Mining_Trans_Comm_Gas_Sanitary
    
    Multiple: EV/EBITDA
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              EV/EBITDA   R-squared:                       0.618
    Model:                            OLS   Adj. R-squared:                  0.484
    Method:                 Least Squares   F-statistic:                     4.613
    Date:                Sun, 05 May 2024   Prob (F-statistic):           0.000121
    Time:                        19:16:56   Log-Likelihood:                -184.47
    No. Observations:                  51   AIC:                             396.9
    Df Residuals:                      37   BIC:                             424.0
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      36.8044      7.439      4.947      0.000      21.731      51.878
    Debt_Coverage_Ratio       -19.7657     23.795     -0.831      0.411     -67.978      28.447
    ROE                       -55.3904     27.590     -2.008      0.052    -111.293       0.512
    EBIT Margin (%)            -5.0273      2.980     -1.687      0.100     -11.066       1.012
    YOY_Gross_Profit_Change     1.7479      4.965      0.352      0.727      -8.313      11.809
    ROIC                        9.9092      8.893      1.114      0.272      -8.110      27.928
    FCF_Positive               -3.2541      1.373     -2.369      0.023      -6.037      -0.471
    FCF_Positive               -3.2541      1.373     -2.369      0.023      -6.037      -0.471
    Gross_Margin               -9.3699     14.524     -0.645      0.523     -38.799      20.059
    Quick_Ratio                24.9881     12.436      2.009      0.052      -0.211      50.187
    Current_Ratio             -24.0822     12.442     -1.936      0.061     -49.292       1.128
    Debt_to_Equity              5.9856      3.328      1.798      0.080      -0.758      12.730
    Revenue per Employee     3.862e-05      0.000      0.108      0.915      -0.001       0.001
    FCF_Positive               -3.2541      1.373     -2.369      0.023      -6.037      -0.471
    FCF_Positive               -3.2541      1.373     -2.369      0.023      -6.037      -0.471
    YOY_Revenue_Change         -3.7874      2.721     -1.392      0.172      -9.300       1.725
    YOY_EBIT_Change            -0.4092      3.601     -0.114      0.910      -7.706       6.888
    ==============================================================================
    Omnibus:                       16.615   Durbin-Watson:                   1.680
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               21.716
    Skew:                           1.150   Prob(JB):                     1.93e-05
    Kurtosis:                       5.220   Cond. No.                     6.12e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.2e-36. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: P/E
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    P/E   R-squared:                       0.499
    Model:                            OLS   Adj. R-squared:                  0.324
    Method:                 Least Squares   F-statistic:                     2.840
    Date:                Sun, 05 May 2024   Prob (F-statistic):            0.00637
    Time:                        19:16:56   Log-Likelihood:                -168.28
    No. Observations:                  51   AIC:                             364.6
    Df Residuals:                      37   BIC:                             391.6
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      22.9406      5.416      4.236      0.000      11.967      33.914
    Debt_Coverage_Ratio       -11.0970     17.323     -0.641      0.526     -46.196      24.002
    ROE                       -28.3744     20.086     -1.413      0.166     -69.072      12.324
    EBIT Margin (%)            -1.7285      2.170     -0.797      0.431      -6.125       2.668
    YOY_Gross_Profit_Change     0.7796      3.615      0.216      0.830      -6.545       8.104
    ROIC                        1.3784      6.474      0.213      0.833     -11.740      14.497
    FCF_Positive                0.8175      1.000      0.818      0.419      -1.208       2.843
    FCF_Positive                0.8175      1.000      0.818      0.419      -1.208       2.843
    Gross_Margin              -11.2164     10.574     -1.061      0.296     -32.641      10.208
    Quick_Ratio                20.2259      9.054      2.234      0.032       1.881      38.571
    Current_Ratio             -20.6257      9.058     -2.277      0.029     -38.979      -2.273
    Debt_to_Equity              1.9230      2.423      0.794      0.432      -2.987       6.833
    Revenue per Employee        0.0002      0.000      0.677      0.503      -0.000       0.001
    FCF_Positive                0.8175      1.000      0.818      0.419      -1.208       2.843
    FCF_Positive                0.8175      1.000      0.818      0.419      -1.208       2.843
    YOY_Revenue_Change         -1.9821      1.981     -1.001      0.323      -5.995       2.031
    YOY_EBIT_Change            -0.1587      2.622     -0.061      0.952      -5.471       5.154
    ==============================================================================
    Omnibus:                       19.081   Durbin-Watson:                   1.160
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               30.197
    Skew:                           1.184   Prob(JB):                     2.77e-07
    Kurtosis:                       5.934   Cond. No.                     6.12e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.2e-36. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/GP
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                  EV/GP   R-squared:                       0.628
    Model:                            OLS   Adj. R-squared:                  0.497
    Method:                 Least Squares   F-statistic:                     4.796
    Date:                Sun, 05 May 2024   Prob (F-statistic):           8.28e-05
    Time:                        19:16:56   Log-Likelihood:                -140.66
    No. Observations:                  51   AIC:                             309.3
    Df Residuals:                      37   BIC:                             336.4
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      15.9531      3.151      5.063      0.000       9.569      22.337
    Debt_Coverage_Ratio        -9.3899     10.078     -0.932      0.358     -29.810      11.030
    ROE                       -12.0539     11.686     -1.032      0.309     -35.731      11.624
    EBIT Margin (%)            -0.0552      1.262     -0.044      0.965      -2.613       2.503
    YOY_Gross_Profit_Change     2.6382      2.103      1.254      0.218      -1.623       6.899
    ROIC                        1.5717      3.767      0.417      0.679      -6.060       9.204
    FCF_Positive               -1.2821      0.582     -2.204      0.034      -2.461      -0.103
    FCF_Positive               -1.2821      0.582     -2.204      0.034      -2.461      -0.103
    Gross_Margin              -14.3644      6.152     -2.335      0.025     -26.829      -1.900
    Quick_Ratio                 8.3405      5.267      1.583      0.122      -2.332      19.013
    Current_Ratio              -7.7764      5.270     -1.476      0.148     -18.454       2.901
    Debt_to_Equity              1.3240      1.410      0.939      0.354      -1.532       4.180
    Revenue per Employee     4.682e-05      0.000      0.308      0.760      -0.000       0.000
    FCF_Positive               -1.2821      0.582     -2.204      0.034      -2.461      -0.103
    FCF_Positive               -1.2821      0.582     -2.204      0.034      -2.461      -0.103
    YOY_Revenue_Change         -2.2067      1.152     -1.915      0.063      -4.542       0.128
    YOY_EBIT_Change             0.2439      1.525      0.160      0.874      -2.847       3.335
    ==============================================================================
    Omnibus:                       18.420   Durbin-Watson:                   1.522
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               24.489
    Skew:                           1.281   Prob(JB):                     4.81e-06
    Kurtosis:                       5.228   Cond. No.                     6.12e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.2e-36. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV_EBIT
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                EV_EBIT   R-squared:                       0.555
    Model:                            OLS   Adj. R-squared:                  0.398
    Method:                 Least Squares   F-statistic:                     3.548
    Date:                Sun, 05 May 2024   Prob (F-statistic):            0.00122
    Time:                        19:16:56   Log-Likelihood:                -115.06
    No. Observations:                  51   AIC:                             258.1
    Df Residuals:                      37   BIC:                             285.2
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       6.0728      1.907      3.184      0.003       2.208       9.937
    Debt_Coverage_Ratio         3.5120      6.101      0.576      0.568      -8.849      15.873
    ROE                        -2.0334      7.074     -0.287      0.775     -16.366      12.300
    EBIT Margin (%)             0.3132      0.764      0.410      0.684      -1.235       1.862
    YOY_Gross_Profit_Change    -1.3122      1.273     -1.031      0.309      -3.892       1.267
    ROIC                       -5.5347      2.280     -2.427      0.020     -10.155      -0.915
    FCF_Positive                0.2388      0.352      0.678      0.502      -0.475       0.952
    FCF_Positive                0.2388      0.352      0.678      0.502      -0.475       0.952
    Gross_Margin                0.3534      3.724      0.095      0.925      -7.192       7.899
    Quick_Ratio                 3.2429      3.189      1.017      0.316      -3.218       9.704
    Current_Ratio              -3.3947      3.190     -1.064      0.294      -9.858       3.069
    Debt_to_Equity              0.5630      0.853      0.660      0.513      -1.166       2.292
    Revenue per Employee    -6.924e-05   9.19e-05     -0.753      0.456      -0.000       0.000
    FCF_Positive                0.2388      0.352      0.678      0.502      -0.475       0.952
    FCF_Positive                0.2388      0.352      0.678      0.502      -0.475       0.952
    YOY_Revenue_Change          1.6058      0.698      2.302      0.027       0.192       3.019
    YOY_EBIT_Change            -0.5025      0.923     -0.544      0.590      -2.373       1.368
    ==============================================================================
    Omnibus:                       31.945   Durbin-Watson:                   1.911
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               78.077
    Skew:                           1.771   Prob(JB):                     1.11e-17
    Kurtosis:                       7.919   Cond. No.                     6.12e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.2e-36. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: FCF Yield
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              FCF Yield   R-squared:                       0.668
    Model:                            OLS   Adj. R-squared:                  0.552
    Method:                 Least Squares   F-statistic:                     5.738
    Date:                Sun, 05 May 2024   Prob (F-statistic):           1.32e-05
    Time:                        19:16:56   Log-Likelihood:                -54.894
    No. Observations:                  51   AIC:                             137.8
    Df Residuals:                      37   BIC:                             164.8
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      -2.1745      0.586     -3.709      0.001      -3.362      -0.987
    Debt_Coverage_Ratio         3.9954      1.875      2.131      0.040       0.196       7.795
    ROE                        -3.4249      2.174     -1.575      0.124      -7.831       0.981
    EBIT Margin (%)             0.0966      0.235      0.411      0.683      -0.379       0.572
    YOY_Gross_Profit_Change    -0.3016      0.391     -0.771      0.446      -1.094       0.491
    ROIC                       -0.3642      0.701     -0.520      0.606      -1.784       1.056
    FCF_Positive                0.3895      0.108      3.598      0.001       0.170       0.609
    FCF_Positive                0.3895      0.108      3.598      0.001       0.170       0.609
    Gross_Margin               -1.4854      1.145     -1.298      0.202      -3.805       0.834
    Quick_Ratio                 1.0238      0.980      1.045      0.303      -0.962       3.010
    Current_Ratio              -0.9661      0.981     -0.985      0.331      -2.953       1.021
    Debt_to_Equity              0.9673      0.262      3.687      0.001       0.436       1.499
    Revenue per Employee     1.429e-05   2.83e-05      0.506      0.616    -4.3e-05    7.15e-05
    FCF_Positive                0.3895      0.108      3.598      0.001       0.170       0.609
    FCF_Positive                0.3895      0.108      3.598      0.001       0.170       0.609
    YOY_Revenue_Change          0.0498      0.214      0.232      0.818      -0.385       0.484
    YOY_EBIT_Change             0.1073      0.284      0.378      0.708      -0.468       0.682
    ==============================================================================
    Omnibus:                       25.872   Durbin-Watson:                   1.875
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               89.538
    Skew:                          -1.166   Prob(JB):                     3.61e-20
    Kurtosis:                       9.058   Cond. No.                     6.12e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.2e-36. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/EBITDA-Capex
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:        EV/EBITDA-Capex   R-squared:                       0.274
    Model:                            OLS   Adj. R-squared:                  0.019
    Method:                 Least Squares   F-statistic:                     1.076
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.408
    Time:                        19:16:56   Log-Likelihood:                -384.88
    No. Observations:                  51   AIC:                             797.8
    Df Residuals:                      37   BIC:                             824.8
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                    -808.0671    378.546     -2.135      0.039   -1575.075     -41.060
    Debt_Coverage_Ratio     -1056.7189   1210.806     -0.873      0.388   -3510.045    1396.607
    ROE                      -754.7667   1403.943     -0.538      0.594   -3599.425    2089.891
    EBIT Margin (%)          -309.7235    151.657     -2.042      0.048    -617.011      -2.436
    YOY_Gross_Profit_Change   197.7724    252.665      0.783      0.439    -314.176     709.721
    ROIC                      813.6877    452.535      1.798      0.080    -103.235    1730.610
    FCF_Positive              155.9717     69.888      2.232      0.032      14.365     297.579
    FCF_Positive              155.9717     69.888      2.232      0.032      14.365     297.579
    Gross_Margin             1116.5471    739.069      1.511      0.139    -380.948    2614.043
    Quick_Ratio               640.8731    632.839      1.013      0.318    -641.381    1923.127
    Current_Ratio            -618.6524    633.119     -0.977      0.335   -1901.472     664.168
    Debt_to_Equity              7.7409    169.370      0.046      0.964    -335.435     350.916
    Revenue per Employee        0.0379      0.018      2.074      0.045       0.001       0.075
    FCF_Positive              155.9717     69.888      2.232      0.032      14.365     297.579
    FCF_Positive              155.9717     69.888      2.232      0.032      14.365     297.579
    YOY_Revenue_Change        -26.8173    138.443     -0.194      0.847    -307.329     253.695
    YOY_EBIT_Change           -30.9007    183.259     -0.169      0.867    -402.219     340.417
    ==============================================================================
    Omnibus:                       75.391   Durbin-Watson:                   2.331
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):             1072.005
    Skew:                          -3.813   Prob(JB):                    1.65e-233
    Kurtosis:                      24.126   Cond. No.                     6.12e+22
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.2e-36. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Division: Retail Trade
    
    Multiple: EV/EBITDA
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              EV/EBITDA   R-squared:                       0.045
    Model:                            OLS   Adj. R-squared:                  0.014
    Method:                 Least Squares   F-statistic:                     1.444
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.136
    Time:                        19:16:56   Log-Likelihood:                -2578.7
    No. Observations:                 412   AIC:                             5185.
    Df Residuals:                     398   BIC:                             5242.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      64.7411     22.545      2.872      0.004      20.419     109.063
    Debt_Coverage_Ratio      -129.3227     50.417     -2.565      0.011    -228.439     -30.206
    ROE                         0.2613      0.681      0.384      0.701      -1.078       1.601
    EBIT Margin (%)          -675.8440    338.690     -1.995      0.047   -1341.690      -9.998
    YOY_Gross_Profit_Change   -18.3181     42.086     -0.435      0.664    -101.056      64.420
    ROIC                      333.8206    203.753      1.638      0.102     -66.747     734.388
    FCF_Positive               -4.2211      4.966     -0.850      0.396     -13.984       5.542
    FCF_Positive               -4.2211      4.966     -0.850      0.396     -13.984       5.542
    Gross_Margin              -16.1869     47.871     -0.338      0.735    -110.298      77.924
    Quick_Ratio                -2.5837     14.799     -0.175      0.861     -31.677      26.510
    Current_Ratio               5.5887     15.134      0.369      0.712     -24.163      35.341
    Debt_to_Equity             -0.0605      0.134     -0.451      0.652      -0.324       0.203
    Revenue per Employee       -0.0086      0.014     -0.610      0.542      -0.036       0.019
    FCF_Positive               -4.2211      4.966     -0.850      0.396     -13.984       5.542
    FCF_Positive               -4.2211      4.966     -0.850      0.396     -13.984       5.542
    YOY_Revenue_Change         42.7090     51.544      0.829      0.408     -58.624     144.042
    YOY_EBIT_Change             0.1711      2.371      0.072      0.943      -4.491       4.833
    ==============================================================================
    Omnibus:                      847.708   Durbin-Watson:                   1.955
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):           953959.872
    Skew:                          14.456   Prob(JB):                         0.00
    Kurtosis:                     236.954   Cond. No.                     2.86e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.72e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: P/E
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    P/E   R-squared:                       0.052
    Model:                            OLS   Adj. R-squared:                  0.021
    Method:                 Least Squares   F-statistic:                     1.682
    Date:                Sun, 05 May 2024   Prob (F-statistic):             0.0623
    Time:                        19:16:56   Log-Likelihood:                -2351.6
    No. Observations:                 412   AIC:                             4731.
    Df Residuals:                     398   BIC:                             4787.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      20.5644     12.991      1.583      0.114      -4.975      46.104
    Debt_Coverage_Ratio       -76.2800     29.051     -2.626      0.009    -133.392     -19.168
    ROE                         0.1670      0.393      0.425      0.671      -0.605       0.939
    EBIT Margin (%)          -494.6326    195.158     -2.535      0.012    -878.301    -110.964
    YOY_Gross_Profit_Change    -5.8952     24.250     -0.243      0.808     -53.570      41.779
    ROIC                      250.8274    117.405      2.136      0.033      20.016     481.639
    FCF_Positive               -0.8313      2.862     -0.291      0.772      -6.457       4.794
    FCF_Positive               -0.8313      2.862     -0.291      0.772      -6.457       4.794
    Gross_Margin                1.6344     27.584      0.059      0.953     -52.594      55.862
    Quick_Ratio                -3.5645      8.527     -0.418      0.676     -20.328      13.199
    Current_Ratio               6.7360      8.720      0.772      0.440     -10.407      23.880
    Debt_to_Equity             -0.0372      0.077     -0.481      0.631      -0.189       0.115
    Revenue per Employee       -0.0032      0.008     -0.388      0.698      -0.019       0.013
    FCF_Positive               -0.8313      2.862     -0.291      0.772      -6.457       4.794
    FCF_Positive               -0.8313      2.862     -0.291      0.772      -6.457       4.794
    YOY_Revenue_Change         29.7493     29.700      1.002      0.317     -28.640      88.138
    YOY_EBIT_Change            -0.1603      1.366     -0.117      0.907      -2.847       2.526
    ==============================================================================
    Omnibus:                      760.558   Durbin-Watson:                   1.904
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):           401168.200
    Skew:                          11.707   Prob(JB):                         0.00
    Kurtosis:                     154.066   Cond. No.                     2.86e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.72e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/GP
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                  EV/GP   R-squared:                       0.511
    Model:                            OLS   Adj. R-squared:                  0.496
    Method:                 Least Squares   F-statistic:                     32.06
    Date:                Sun, 05 May 2024   Prob (F-statistic):           5.22e-54
    Time:                        19:16:56   Log-Likelihood:                -1243.3
    No. Observations:                 412   AIC:                             2515.
    Df Residuals:                     398   BIC:                             2571.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       8.9599      0.882     10.162      0.000       7.226      10.693
    Debt_Coverage_Ratio        -1.4228      1.972     -0.722      0.471      -5.299       2.454
    ROE                         0.0044      0.027      0.166      0.868      -0.048       0.057
    EBIT Margin (%)           154.6339     13.246     11.674      0.000     128.593     180.675
    YOY_Gross_Profit_Change    -0.5794      1.646     -0.352      0.725      -3.815       2.656
    ROIC                      -86.6357      7.969    -10.872      0.000    -102.302     -70.970
    FCF_Positive               -0.0745      0.194     -0.383      0.702      -0.456       0.307
    FCF_Positive               -0.0745      0.194     -0.383      0.702      -0.456       0.307
    Gross_Margin              -12.6135      1.872     -6.737      0.000     -16.294      -8.933
    Quick_Ratio                 2.2089      0.579      3.817      0.000       1.071       3.347
    Current_Ratio              -1.8891      0.592     -3.192      0.002      -3.053      -0.726
    Debt_to_Equity             -0.0006      0.005     -0.119      0.905      -0.011       0.010
    Revenue per Employee       -0.0007      0.001     -1.343      0.180      -0.002       0.000
    FCF_Positive               -0.0745      0.194     -0.383      0.702      -0.456       0.307
    FCF_Positive               -0.0745      0.194     -0.383      0.702      -0.456       0.307
    YOY_Revenue_Change          4.1796      2.016      2.073      0.039       0.216       8.143
    YOY_EBIT_Change            -0.0587      0.093     -0.633      0.527      -0.241       0.124
    ==============================================================================
    Omnibus:                      383.132   Durbin-Watson:                   1.237
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):            14474.076
    Skew:                           3.854   Prob(JB):                         0.00
    Kurtosis:                      30.995   Cond. No.                     2.86e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.72e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV_EBIT
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                EV_EBIT   R-squared:                       0.036
    Model:                            OLS   Adj. R-squared:                  0.004
    Method:                 Least Squares   F-statistic:                     1.127
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.334
    Time:                        19:16:56   Log-Likelihood:                -3247.8
    No. Observations:                 412   AIC:                             6524.
    Df Residuals:                     398   BIC:                             6580.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                    -234.3966    114.390     -2.049      0.041    -459.280      -9.513
    Debt_Coverage_Ratio       111.9073    255.806      0.437      0.662    -390.993     614.807
    ROE                        -0.4377      3.457     -0.127      0.899      -7.233       6.358
    EBIT Margin (%)          -400.4381   1718.454     -0.233      0.816   -3778.819    2977.942
    YOY_Gross_Profit_Change   -66.3410    213.535     -0.311      0.756    -486.138     353.456
    ROIC                       97.1300   1033.807      0.094      0.925   -1935.275    2129.535
    FCF_Positive               67.4833     25.197      2.678      0.008      17.947     117.019
    FCF_Positive               67.4833     25.197      2.678      0.008      17.947     117.019
    Gross_Margin              118.8014    242.888      0.489      0.625    -358.702     596.305
    Quick_Ratio               119.9077     75.085      1.597      0.111     -27.706     267.521
    Current_Ratio            -106.3305     76.786     -1.385      0.167    -257.287      44.626
    Debt_to_Equity              0.1596      0.681      0.234      0.815      -1.179       1.498
    Revenue per Employee        0.0723      0.072      1.011      0.312      -0.068       0.213
    FCF_Positive               67.4833     25.197      2.678      0.008      17.947     117.019
    FCF_Positive               67.4833     25.197      2.678      0.008      17.947     117.019
    YOY_Revenue_Change        173.4369    261.525      0.663      0.508    -340.706     687.580
    YOY_EBIT_Change             1.7855     12.032      0.148      0.882     -21.868      25.440
    ==============================================================================
    Omnibus:                      175.772   Durbin-Watson:                   2.012
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):            57409.795
    Skew:                          -0.343   Prob(JB):                         0.00
    Kurtosis:                      60.826   Cond. No.                     2.86e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.72e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: FCF Yield
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              FCF Yield   R-squared:                       0.413
    Model:                            OLS   Adj. R-squared:                  0.394
    Method:                 Least Squares   F-statistic:                     21.53
    Date:                Sun, 05 May 2024   Prob (F-statistic):           1.26e-38
    Time:                        19:16:56   Log-Likelihood:                -45.867
    No. Observations:                 412   AIC:                             119.7
    Df Residuals:                     398   BIC:                             176.0
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      -0.1973      0.048     -4.093      0.000      -0.292      -0.103
    Debt_Coverage_Ratio         0.0054      0.108      0.050      0.960      -0.207       0.217
    ROE                         0.0015      0.001      0.998      0.319      -0.001       0.004
    EBIT Margin (%)            -2.2400      0.724     -3.093      0.002      -3.664      -0.816
    YOY_Gross_Profit_Change     0.1816      0.090      2.018      0.044       0.005       0.358
    ROIC                        1.0695      0.436      2.455      0.015       0.213       1.926
    FCF_Positive                0.0743      0.011      6.999      0.000       0.053       0.095
    FCF_Positive                0.0743      0.011      6.999      0.000       0.053       0.095
    Gross_Margin                0.4127      0.102      4.031      0.000       0.211       0.614
    Quick_Ratio                -0.1420      0.032     -4.486      0.000      -0.204      -0.080
    Current_Ratio               0.1396      0.032      4.313      0.000       0.076       0.203
    Debt_to_Equity             -0.0004      0.000     -1.221      0.223      -0.001       0.000
    Revenue per Employee    -2.006e-05   3.01e-05     -0.665      0.506   -7.93e-05    3.92e-05
    FCF_Positive                0.0743      0.011      6.999      0.000       0.053       0.095
    FCF_Positive                0.0743      0.011      6.999      0.000       0.053       0.095
    YOY_Revenue_Change         -0.3933      0.110     -3.568      0.000      -0.610      -0.177
    YOY_EBIT_Change             0.0059      0.005      1.159      0.247      -0.004       0.016
    ==============================================================================
    Omnibus:                      249.005   Durbin-Watson:                   1.227
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):             2739.678
    Skew:                           2.399   Prob(JB):                         0.00
    Kurtosis:                      14.687   Cond. No.                     2.86e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.72e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/EBITDA-Capex
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:        EV/EBITDA-Capex   R-squared:                       0.044
    Model:                            OLS   Adj. R-squared:                  0.013
    Method:                 Least Squares   F-statistic:                     1.421
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.146
    Time:                        19:16:56   Log-Likelihood:                -2766.0
    No. Observations:                 412   AIC:                             5560.
    Df Residuals:                     398   BIC:                             5616.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      32.3146     35.518      0.910      0.363     -37.512     102.141
    Debt_Coverage_Ratio        40.2487     79.428      0.507      0.613    -115.902     196.399
    ROE                        -0.2463      1.073     -0.230      0.819      -2.356       1.864
    EBIT Margin (%)           585.2668    533.580      1.097      0.273    -463.720    1634.254
    YOY_Gross_Profit_Change  -103.9778     66.303     -1.568      0.118    -234.325      26.369
    ROIC                     -342.1680    320.997     -1.066      0.287    -973.230     288.894
    FCF_Positive               -0.8783      7.824     -0.112      0.911     -16.259      14.503
    FCF_Positive               -0.8783      7.824     -0.112      0.911     -16.259      14.503
    Gross_Margin              -70.6973     75.417     -0.937      0.349    -218.962      77.568
    Quick_Ratio                16.5271     23.314      0.709      0.479     -29.307      62.361
    Current_Ratio             -15.6114     23.842     -0.655      0.513     -62.483      31.261
    Debt_to_Equity              0.0545      0.211      0.258      0.797      -0.361       0.470
    Revenue per Employee        0.0137      0.022      0.617      0.538      -0.030       0.057
    FCF_Positive               -0.8783      7.824     -0.112      0.911     -16.259      14.503
    FCF_Positive               -0.8783      7.824     -0.112      0.911     -16.259      14.503
    YOY_Revenue_Change        220.8145     81.203      2.719      0.007      61.173     380.456
    YOY_EBIT_Change             1.3599      3.736      0.364      0.716      -5.985       8.704
    ==============================================================================
    Omnibus:                      578.414   Durbin-Watson:                   1.980
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):           339240.226
    Skew:                           6.463   Prob(JB):                         0.00
    Kurtosis:                     142.980   Cond. No.                     2.86e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.72e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Division: Services
    
    Multiple: EV/EBITDA
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              EV/EBITDA   R-squared:                       0.096
    Model:                            OLS   Adj. R-squared:                  0.057
    Method:                 Least Squares   F-statistic:                     2.464
    Date:                Sun, 05 May 2024   Prob (F-statistic):            0.00337
    Time:                        19:16:56   Log-Likelihood:                -2033.0
    No. Observations:                 317   AIC:                             4094.
    Df Residuals:                     303   BIC:                             4147.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      50.4699     36.410      1.386      0.167     -21.178     122.118
    Debt_Coverage_Ratio      -231.8618     76.229     -3.042      0.003    -381.867     -81.857
    ROE                       -10.3972      8.654     -1.201      0.231     -27.426       6.632
    EBIT Margin (%)            35.8724     13.304      2.696      0.007       9.692      62.053
    YOY_Gross_Profit_Change  -104.9760     59.254     -1.772      0.077    -221.577      11.625
    ROIC                      -34.9696     14.329     -2.441      0.015     -63.166      -6.773
    FCF_Positive                5.4283      6.404      0.848      0.397      -7.174      18.030
    FCF_Positive                5.4283      6.404      0.848      0.397      -7.174      18.030
    Gross_Margin               54.1312     47.337      1.144      0.254     -39.020     147.282
    Quick_Ratio                15.9173     34.429      0.462      0.644     -51.832      83.667
    Current_Ratio             -16.0762     34.304     -0.469      0.640     -83.581      51.429
    Debt_to_Equity              0.8861      0.757      1.170      0.243      -0.604       2.376
    Revenue per Employee       -0.0291      0.030     -0.980      0.328      -0.087       0.029
    FCF_Positive                5.4283      6.404      0.848      0.397      -7.174      18.030
    FCF_Positive                5.4283      6.404      0.848      0.397      -7.174      18.030
    YOY_Revenue_Change         71.8924     57.792      1.244      0.214     -41.832     185.617
    YOY_EBIT_Change            -3.4545      5.587     -0.618      0.537     -14.450       7.540
    ==============================================================================
    Omnibus:                      531.738   Durbin-Watson:                   1.646
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):           136406.146
    Skew:                           9.324   Prob(JB):                         0.00
    Kurtosis:                     102.898   Cond. No.                     5.36e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.74e-36. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: P/E
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    P/E   R-squared:                       0.111
    Model:                            OLS   Adj. R-squared:                  0.073
    Method:                 Least Squares   F-statistic:                     2.919
    Date:                Sun, 05 May 2024   Prob (F-statistic):           0.000515
    Time:                        19:16:56   Log-Likelihood:                -1888.6
    No. Observations:                 317   AIC:                             3805.
    Df Residuals:                     303   BIC:                             3858.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      13.4201     23.088      0.581      0.561     -32.013      58.853
    Debt_Coverage_Ratio      -141.0680     48.337     -2.918      0.004    -236.188     -45.948
    ROE                        -4.3030      5.487     -0.784      0.434     -15.101       6.495
    EBIT Margin (%)            26.4778      8.436      3.139      0.002       9.876      43.079
    YOY_Gross_Profit_Change   -47.9287     37.573     -1.276      0.203    -121.867      26.009
    ROIC                      -24.3107      9.086     -2.676      0.008     -42.190      -6.431
    FCF_Positive                5.8479      4.061      1.440      0.151      -2.143      13.839
    FCF_Positive                5.8479      4.061      1.440      0.151      -2.143      13.839
    Gross_Margin               68.4131     30.017      2.279      0.023       9.345     127.481
    Quick_Ratio                 5.1751     21.831      0.237      0.813     -37.785      48.136
    Current_Ratio              -6.0472     21.753     -0.278      0.781     -48.853      36.758
    Debt_to_Equity              0.3598      0.480      0.749      0.454      -0.585       1.305
    Revenue per Employee       -0.0187      0.019     -0.996      0.320      -0.056       0.018
    FCF_Positive                5.8479      4.061      1.440      0.151      -2.143      13.839
    FCF_Positive                5.8479      4.061      1.440      0.151      -2.143      13.839
    YOY_Revenue_Change         29.5121     36.646      0.805      0.421     -42.602     101.626
    YOY_EBIT_Change            -1.3012      3.543     -0.367      0.714      -8.273       5.671
    ==============================================================================
    Omnibus:                      527.725   Durbin-Watson:                   1.837
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):           142858.487
    Skew:                           9.142   Prob(JB):                         0.00
    Kurtosis:                     105.379   Cond. No.                     5.36e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.74e-36. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/GP
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                  EV/GP   R-squared:                       0.313
    Model:                            OLS   Adj. R-squared:                  0.283
    Method:                 Least Squares   F-statistic:                     10.60
    Date:                Sun, 05 May 2024   Prob (F-statistic):           1.50e-18
    Time:                        19:16:56   Log-Likelihood:                -911.77
    No. Observations:                 317   AIC:                             1852.
    Df Residuals:                     303   BIC:                             1904.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      16.3017      1.060     15.383      0.000      14.216      18.387
    Debt_Coverage_Ratio        -5.2835      2.219     -2.381      0.018      -9.649      -0.918
    ROE                        -0.1813      0.252     -0.720      0.472      -0.677       0.314
    EBIT Margin (%)             1.8277      0.387      4.720      0.000       1.066       2.590
    YOY_Gross_Profit_Change    -1.0813      1.725     -0.627      0.531      -4.475       2.312
    ROIC                       -2.2630      0.417     -5.426      0.000      -3.084      -1.442
    FCF_Positive               -0.4715      0.186     -2.530      0.012      -0.838      -0.105
    FCF_Positive               -0.4715      0.186     -2.530      0.012      -0.838      -0.105
    Gross_Margin              -13.9015      1.378    -10.090      0.000     -16.613     -11.190
    Quick_Ratio                -0.3843      1.002     -0.384      0.702      -2.356       1.588
    Current_Ratio               0.4476      0.998      0.448      0.654      -1.517       2.412
    Debt_to_Equity              0.0173      0.022      0.787      0.432      -0.026       0.061
    Revenue per Employee       -0.0012      0.001     -1.409      0.160      -0.003       0.000
    FCF_Positive               -0.4715      0.186     -2.530      0.012      -0.838      -0.105
    FCF_Positive               -0.4715      0.186     -2.530      0.012      -0.838      -0.105
    YOY_Revenue_Change          0.5152      1.682      0.306      0.760      -2.795       3.825
    YOY_EBIT_Change            -0.2020      0.163     -1.242      0.215      -0.522       0.118
    ==============================================================================
    Omnibus:                      117.376   Durbin-Watson:                   1.123
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              436.074
    Skew:                           1.590   Prob(JB):                     2.03e-95
    Kurtosis:                       7.785   Cond. No.                     5.36e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.74e-36. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV_EBIT
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                EV_EBIT   R-squared:                       0.111
    Model:                            OLS   Adj. R-squared:                  0.073
    Method:                 Least Squares   F-statistic:                     2.901
    Date:                Sun, 05 May 2024   Prob (F-statistic):           0.000557
    Time:                        19:16:56   Log-Likelihood:                -1836.1
    No. Observations:                 317   AIC:                             3700.
    Df Residuals:                     303   BIC:                             3753.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      90.2832     19.567      4.614      0.000      51.778     128.788
    Debt_Coverage_Ratio        61.5106     40.967      1.501      0.134     -19.105     142.126
    ROE                         7.7245      4.651      1.661      0.098      -1.427      16.876
    EBIT Margin (%)            -0.4377      7.150     -0.061      0.951     -14.508      13.632
    YOY_Gross_Profit_Change    52.2354     31.844      1.640      0.102     -10.428     114.899
    ROIC                      -16.3736      7.700     -2.126      0.034     -31.527      -1.221
    FCF_Positive               -4.3236      3.442     -1.256      0.210     -11.096       2.449
    FCF_Positive               -4.3236      3.442     -1.256      0.210     -11.096       2.449
    Gross_Margin              -68.4224     25.440     -2.690      0.008    -118.483     -18.362
    Quick_Ratio                22.0136     18.502      1.190      0.235     -14.396      58.423
    Current_Ratio             -24.5223     18.436     -1.330      0.184     -60.800      11.756
    Debt_to_Equity             -0.7013      0.407     -1.724      0.086      -1.502       0.099
    Revenue per Employee       -0.0238      0.016     -1.495      0.136      -0.055       0.008
    FCF_Positive               -4.3236      3.442     -1.256      0.210     -11.096       2.449
    FCF_Positive               -4.3236      3.442     -1.256      0.210     -11.096       2.449
    YOY_Revenue_Change        -37.1181     31.058     -1.195      0.233     -98.235      23.999
    YOY_EBIT_Change            -2.0203      3.003     -0.673      0.502      -7.929       3.889
    ==============================================================================
    Omnibus:                      132.103   Durbin-Watson:                   1.503
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):            12876.879
    Skew:                          -0.647   Prob(JB):                         0.00
    Kurtosis:                      34.197   Cond. No.                     5.36e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.74e-36. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: FCF Yield
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              FCF Yield   R-squared:                       0.329
    Model:                            OLS   Adj. R-squared:                  0.300
    Method:                 Least Squares   F-statistic:                     11.43
    Date:                Sun, 05 May 2024   Prob (F-statistic):           4.98e-20
    Time:                        19:16:56   Log-Likelihood:                 13.664
    No. Observations:                 317   AIC:                            0.6721
    Df Residuals:                     303   BIC:                             53.30
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      -0.0711      0.057     -1.244      0.215      -0.184       0.041
    Debt_Coverage_Ratio        -0.0939      0.120     -0.784      0.434      -0.330       0.142
    ROE                         0.0091      0.014      0.672      0.502      -0.018       0.036
    EBIT Margin (%)            -0.0317      0.021     -1.518      0.130      -0.073       0.009
    YOY_Gross_Profit_Change     0.0255      0.093      0.274      0.784      -0.158       0.209
    ROIC                        0.0188      0.023      0.837      0.403      -0.025       0.063
    FCF_Positive                0.0903      0.010      8.980      0.000       0.071       0.110
    FCF_Positive                0.0903      0.010      8.980      0.000       0.071       0.110
    Gross_Margin               -0.1242      0.074     -1.670      0.096      -0.271       0.022
    Quick_Ratio                -0.1697      0.054     -3.137      0.002      -0.276      -0.063
    Current_Ratio               0.1703      0.054      3.160      0.002       0.064       0.276
    Debt_to_Equity             -0.0001      0.001     -0.116      0.908      -0.002       0.002
    Revenue per Employee       -0.0001   4.66e-05     -2.264      0.024      -0.000   -1.38e-05
    FCF_Positive                0.0903      0.010      8.980      0.000       0.071       0.110
    FCF_Positive                0.0903      0.010      8.980      0.000       0.071       0.110
    YOY_Revenue_Change         -0.0797      0.091     -0.878      0.380      -0.258       0.099
    YOY_EBIT_Change            -0.0030      0.009     -0.347      0.729      -0.020       0.014
    ==============================================================================
    Omnibus:                      179.978   Durbin-Watson:                   1.280
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):             1463.940
    Skew:                           2.237   Prob(JB):                         0.00
    Kurtosis:                      12.530   Cond. No.                     5.36e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.74e-36. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/EBITDA-Capex
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:        EV/EBITDA-Capex   R-squared:                       0.039
    Model:                            OLS   Adj. R-squared:                 -0.002
    Method:                 Least Squares   F-statistic:                    0.9569
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.494
    Time:                        19:16:56   Log-Likelihood:                -2428.2
    No. Observations:                 317   AIC:                             4884.
    Df Residuals:                     303   BIC:                             4937.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                     252.0202    126.699      1.989      0.048       2.699     501.341
    Debt_Coverage_Ratio       138.6454    265.261      0.523      0.602    -383.341     660.632
    ROE                        -8.3655     30.113     -0.278      0.781     -67.623      50.892
    EBIT Margin (%)           -29.3212     46.296     -0.633      0.527    -120.424      61.782
    YOY_Gross_Profit_Change   -22.3539    206.191     -0.108      0.914    -428.102     383.395
    ROIC                       18.7761     49.860      0.377      0.707     -79.341     116.893
    FCF_Positive              -46.6015     22.285     -2.091      0.037     -90.454      -2.749
    FCF_Positive              -46.6015     22.285     -2.091      0.037     -90.454      -2.749
    Gross_Margin             -400.5628    164.723     -2.432      0.016    -724.709     -76.417
    Quick_Ratio                38.5355    119.804      0.322      0.748    -197.218     274.289
    Current_Ratio             -27.2504    119.372     -0.228      0.820    -262.153     207.652
    Debt_to_Equity              0.6427      2.635      0.244      0.807      -4.542       5.827
    Revenue per Employee        0.0139      0.103      0.134      0.893      -0.189       0.217
    FCF_Positive              -46.6015     22.285     -2.091      0.037     -90.454      -2.749
    FCF_Positive              -46.6015     22.285     -2.091      0.037     -90.454      -2.749
    YOY_Revenue_Change         13.3121    201.104      0.066      0.947    -382.425     409.050
    YOY_EBIT_Change            -3.0422     19.443     -0.156      0.876     -41.302      35.218
    ==============================================================================
    Omnibus:                      387.131   Durbin-Watson:                   1.939
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):           165389.189
    Skew:                          -4.692   Prob(JB):                         0.00
    Kurtosis:                     114.506   Cond. No.                     5.36e+21
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 1.74e-36. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Division: Unknown_Nonclassifiable
    
    Multiple: EV/EBITDA
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              EV/EBITDA   R-squared:                       0.374
    Model:                            OLS   Adj. R-squared:                  0.176
    Method:                 Least Squares   F-statistic:                     1.888
    Date:                Sun, 05 May 2024   Prob (F-statistic):             0.0612
    Time:                        19:16:57   Log-Likelihood:                -215.15
    No. Observations:                  55   AIC:                             458.3
    Df Residuals:                      41   BIC:                             486.4
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      25.6354      7.473      3.430      0.001      10.543      40.728
    Debt_Coverage_Ratio        -2.5755      5.383     -0.478      0.635     -13.447       8.296
    ROE                        -5.7160      6.296     -0.908      0.369     -18.431       6.998
    EBIT Margin (%)            -7.9273      4.069     -1.948      0.058     -16.145       0.291
    YOY_Gross_Profit_Change     5.2907     15.521      0.341      0.735     -26.055      36.636
    ROIC                       16.6498      6.453      2.580      0.014       3.618      29.681
    FCF_Positive               -1.6827      1.349     -1.247      0.219      -4.407       1.041
    FCF_Positive               -1.6827      1.349     -1.247      0.219      -4.407       1.041
    Gross_Margin               -5.1690     15.178     -0.341      0.735     -35.821      25.483
    Quick_Ratio                 3.8559      3.723      1.036      0.306      -3.664      11.375
    Current_Ratio              -3.7730      3.694     -1.021      0.313     -11.234       3.688
    Debt_to_Equity              0.1540      0.557      0.276      0.784      -0.971       1.279
    Revenue per Employee        0.0054      0.005      1.083      0.285      -0.005       0.016
    FCF_Positive               -1.6827      1.349     -1.247      0.219      -4.407       1.041
    FCF_Positive               -1.6827      1.349     -1.247      0.219      -4.407       1.041
    YOY_Revenue_Change        -19.6364     18.166     -1.081      0.286     -56.323      17.050
    YOY_EBIT_Change            -1.0566      1.191     -0.887      0.380      -3.462       1.349
    ==============================================================================
    Omnibus:                       36.565   Durbin-Watson:                   2.015
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              119.277
    Skew:                           1.803   Prob(JB):                     1.26e-26
    Kurtosis:                       9.249   Cond. No.                     9.23e+20
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 3.02e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: P/E
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    P/E   R-squared:                       0.430
    Model:                            OLS   Adj. R-squared:                  0.250
    Method:                 Least Squares   F-statistic:                     2.384
    Date:                Sun, 05 May 2024   Prob (F-statistic):             0.0173
    Time:                        19:16:57   Log-Likelihood:                -184.46
    No. Observations:                  55   AIC:                             396.9
    Df Residuals:                      41   BIC:                             425.0
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       8.1974      4.277      1.917      0.062      -0.440      16.835
    Debt_Coverage_Ratio         2.9790      3.081      0.967      0.339      -3.243       9.201
    ROE                        -2.9039      3.603     -0.806      0.425     -10.181       4.373
    EBIT Margin (%)            -3.9991      2.329     -1.717      0.094      -8.703       0.704
    YOY_Gross_Profit_Change    -5.9966      8.883     -0.675      0.503     -23.937      11.943
    ROIC                       10.6306      3.693      2.878      0.006       3.172      18.089
    FCF_Positive                0.0048      0.772      0.006      0.995      -1.554       1.564
    FCF_Positive                0.0048      0.772      0.006      0.995      -1.554       1.564
    Gross_Margin               -1.0176      8.687     -0.117      0.907     -18.561      16.526
    Quick_Ratio                 1.6009      2.131      0.751      0.457      -2.703       5.905
    Current_Ratio              -1.6768      2.114     -0.793      0.432      -5.947       2.593
    Debt_to_Equity             -0.0304      0.319     -0.095      0.925      -0.674       0.614
    Revenue per Employee        0.0043      0.003      1.501      0.141      -0.001       0.010
    FCF_Positive                0.0048      0.772      0.006      0.995      -1.554       1.564
    FCF_Positive                0.0048      0.772      0.006      0.995      -1.554       1.564
    YOY_Revenue_Change         -1.4432     10.397     -0.139      0.890     -22.440      19.554
    YOY_EBIT_Change            -0.3603      0.682     -0.528      0.600      -1.737       1.017
    ==============================================================================
    Omnibus:                       26.374   Durbin-Watson:                   1.937
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               58.237
    Skew:                           1.401   Prob(JB):                     2.26e-13
    Kurtosis:                       7.190   Cond. No.                     9.23e+20
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 3.02e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/GP
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                  EV/GP   R-squared:                       0.399
    Model:                            OLS   Adj. R-squared:                  0.208
    Method:                 Least Squares   F-statistic:                     2.092
    Date:                Sun, 05 May 2024   Prob (F-statistic):             0.0364
    Time:                        19:16:57   Log-Likelihood:                -165.51
    No. Observations:                  55   AIC:                             359.0
    Df Residuals:                      41   BIC:                             387.1
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      15.7496      3.031      5.196      0.000       9.629      21.871
    Debt_Coverage_Ratio         2.9604      2.183      1.356      0.183      -1.449       7.369
    ROE                         0.6606      2.553      0.259      0.797      -4.496       5.817
    EBIT Margin (%)             4.1831      1.650      2.535      0.015       0.850       7.516
    YOY_Gross_Profit_Change     8.9381      6.295      1.420      0.163      -3.775      21.651
    ROIC                       -6.2225      2.617     -2.378      0.022     -11.508      -0.937
    FCF_Positive               -0.5863      0.547     -1.072      0.290      -1.691       0.519
    FCF_Positive               -0.5863      0.547     -1.072      0.290      -1.691       0.519
    Gross_Margin              -18.5169      6.156     -3.008      0.004     -30.949      -6.085
    Quick_Ratio                 2.5959      1.510      1.719      0.093      -0.454       5.646
    Current_Ratio              -2.6206      1.498     -1.749      0.088      -5.647       0.405
    Debt_to_Equity             -0.1459      0.226     -0.646      0.522      -0.602       0.310
    Revenue per Employee        0.0003      0.002      0.150      0.882      -0.004       0.004
    FCF_Positive               -0.5863      0.547     -1.072      0.290      -1.691       0.519
    FCF_Positive               -0.5863      0.547     -1.072      0.290      -1.691       0.519
    YOY_Revenue_Change         -9.3145      7.367     -1.264      0.213     -24.193       5.564
    YOY_EBIT_Change            -0.0147      0.483     -0.030      0.976      -0.990       0.961
    ==============================================================================
    Omnibus:                       58.369   Durbin-Watson:                   1.766
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              471.098
    Skew:                           2.680   Prob(JB):                    5.04e-103
    Kurtosis:                      16.298   Cond. No.                     9.23e+20
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 3.02e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV_EBIT
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                EV_EBIT   R-squared:                       0.276
    Model:                            OLS   Adj. R-squared:                  0.046
    Method:                 Least Squares   F-statistic:                     1.199
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.314
    Time:                        19:16:57   Log-Likelihood:                -286.18
    No. Observations:                  55   AIC:                             600.4
    Df Residuals:                      41   BIC:                             628.5
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      42.6167     27.190      1.567      0.125     -12.294      97.527
    Debt_Coverage_Ratio       -19.2432     19.585     -0.983      0.332     -58.796      20.309
    ROE                       -30.6771     22.906     -1.339      0.188     -76.937      15.582
    EBIT Margin (%)           -12.4601     14.806     -0.842      0.405     -42.361      17.440
    YOY_Gross_Profit_Change   -52.1101     56.471     -0.923      0.362    -166.155      61.935
    ROIC                      -17.9854     23.477     -0.766      0.448     -65.398      29.427
    FCF_Positive                0.8026      4.908      0.164      0.871      -9.109      10.714
    FCF_Positive                0.8026      4.908      0.164      0.871      -9.109      10.714
    Gross_Margin               51.2939     55.222      0.929      0.358     -60.229     162.816
    Quick_Ratio                -8.3304     13.547     -0.615      0.542     -35.689      19.028
    Current_Ratio               8.1214     13.442      0.604      0.549     -19.025      35.267
    Debt_to_Equity              2.3321      2.027      1.150      0.257      -1.762       6.426
    Revenue per Employee       -0.0189      0.018     -1.033      0.308      -0.056       0.018
    FCF_Positive                0.8026      4.908      0.164      0.871      -9.109      10.714
    FCF_Positive                0.8026      4.908      0.164      0.871      -9.109      10.714
    YOY_Revenue_Change         23.4586     66.092      0.355      0.724    -110.018     156.935
    YOY_EBIT_Change            -1.1541      4.334     -0.266      0.791      -9.907       7.599
    ==============================================================================
    Omnibus:                       68.682   Durbin-Watson:                   2.244
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              586.597
    Skew:                           3.413   Prob(JB):                    4.19e-128
    Kurtosis:                      17.469   Cond. No.                     9.23e+20
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 3.02e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: FCF Yield
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              FCF Yield   R-squared:                       0.862
    Model:                            OLS   Adj. R-squared:                  0.819
    Method:                 Least Squares   F-statistic:                     19.76
    Date:                Sun, 05 May 2024   Prob (F-statistic):           1.29e-13
    Time:                        19:16:57   Log-Likelihood:                -37.897
    No. Observations:                  55   AIC:                             103.8
    Df Residuals:                      41   BIC:                             131.9
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      -1.5057      0.298     -5.056      0.000      -2.107      -0.904
    Debt_Coverage_Ratio        -1.0404      0.214     -4.850      0.000      -1.474      -0.607
    ROE                         0.0918      0.251      0.366      0.716      -0.415       0.598
    EBIT Margin (%)            -0.4687      0.162     -2.890      0.006      -0.796      -0.141
    YOY_Gross_Profit_Change    -1.0357      0.618     -1.675      0.102      -2.285       0.213
    ROIC                        0.7240      0.257      2.816      0.007       0.205       1.243
    FCF_Positive                0.2139      0.054      3.979      0.000       0.105       0.322
    FCF_Positive                0.2139      0.054      3.979      0.000       0.105       0.322
    Gross_Margin                0.8441      0.605      1.396      0.170      -0.377       2.065
    Quick_Ratio                -0.0847      0.148     -0.571      0.571      -0.384       0.215
    Current_Ratio               0.2099      0.147      1.426      0.162      -0.087       0.507
    Debt_to_Equity              0.0146      0.022      0.657      0.515      -0.030       0.059
    Revenue per Employee        0.0005      0.000      2.314      0.026    5.88e-05       0.001
    FCF_Positive                0.2139      0.054      3.979      0.000       0.105       0.322
    FCF_Positive                0.2139      0.054      3.979      0.000       0.105       0.322
    YOY_Revenue_Change          1.5472      0.724      2.138      0.039       0.085       3.009
    YOY_EBIT_Change            -0.0824      0.047     -1.736      0.090      -0.178       0.013
    ==============================================================================
    Omnibus:                        5.705   Durbin-Watson:                   2.205
    Prob(Omnibus):                  0.058   Jarque-Bera (JB):                5.332
    Skew:                          -0.457   Prob(JB):                       0.0695
    Kurtosis:                       4.220   Cond. No.                     9.23e+20
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 3.02e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/EBITDA-Capex
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:        EV/EBITDA-Capex   R-squared:                       0.144
    Model:                            OLS   Adj. R-squared:                 -0.127
    Method:                 Least Squares   F-statistic:                    0.5316
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.891
    Time:                        19:16:57   Log-Likelihood:                -291.60
    No. Observations:                  55   AIC:                             611.2
    Df Residuals:                      41   BIC:                             639.3
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      49.2798     30.002      1.643      0.108     -11.311     109.870
    Debt_Coverage_Ratio        -3.3610     21.611     -0.156      0.877     -47.005      40.283
    ROE                       -13.4589     25.276     -0.532      0.597     -64.504      37.586
    EBIT Margin (%)            24.5613     16.337      1.503      0.140      -8.432      57.555
    YOY_Gross_Profit_Change    20.0789     62.312      0.322      0.749    -105.763     145.921
    ROIC                      -57.6441     25.906     -2.225      0.032    -109.961      -5.327
    FCF_Positive                3.2335      5.415      0.597      0.554      -7.703      14.170
    FCF_Positive                3.2335      5.415      0.597      0.554      -7.703      14.170
    Gross_Margin              -37.6288     60.934     -0.618      0.540    -160.688      85.431
    Quick_Ratio                -0.7966     14.948     -0.053      0.958     -30.985      29.392
    Current_Ratio               0.1286     14.832      0.009      0.993     -29.826      30.083
    Debt_to_Equity              0.8802      2.237      0.394      0.696      -3.637       5.397
    Revenue per Employee       -0.0190      0.020     -0.941      0.352      -0.060       0.022
    FCF_Positive                3.2335      5.415      0.597      0.554      -7.703      14.170
    FCF_Positive                3.2335      5.415      0.597      0.554      -7.703      14.170
    YOY_Revenue_Change        -28.5998     72.930     -0.392      0.697    -175.884     118.684
    YOY_EBIT_Change             0.7270      4.783      0.152      0.880      -8.932      10.386
    ==============================================================================
    Omnibus:                       47.245   Durbin-Watson:                   1.889
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              402.023
    Skew:                           1.915   Prob(JB):                     5.03e-88
    Kurtosis:                      15.679   Cond. No.                     9.23e+20
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 3.02e-35. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Division: Wholesale Trade
    
    Multiple: EV/EBITDA
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              EV/EBITDA   R-squared:                       0.308
    Model:                            OLS   Adj. R-squared:                  0.207
    Method:                 Least Squares   F-statistic:                     3.052
    Date:                Sun, 05 May 2024   Prob (F-statistic):           0.000924
    Time:                        19:16:57   Log-Likelihood:                -316.68
    No. Observations:                 103   AIC:                             661.4
    Df Residuals:                      89   BIC:                             698.2
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       8.6250      5.221      1.652      0.102      -1.749      18.999
    Debt_Coverage_Ratio       -10.8287      8.130     -1.332      0.186     -26.983       5.325
    ROE                       -11.3560      4.866     -2.334      0.022     -21.024      -1.688
    EBIT Margin (%)           -15.9390     19.983     -0.798      0.427     -55.645      23.767
    YOY_Gross_Profit_Change    -4.7974      6.179     -0.776      0.440     -17.075       7.480
    ROIC                        9.2691     14.178      0.654      0.515     -18.903      37.441
    FCF_Positive                1.5275      1.041      1.467      0.146      -0.541       3.597
    FCF_Positive                1.5275      1.041      1.467      0.146      -0.541       3.597
    Gross_Margin                6.1713      7.344      0.840      0.403      -8.422      20.764
    Quick_Ratio                -0.5511      1.481     -0.372      0.711      -3.495       2.392
    Current_Ratio               1.0651      1.372      0.776      0.440      -1.662       3.792
    Debt_to_Equity              1.5792      0.685      2.304      0.024       0.217       2.941
    Revenue per Employee       -0.0013      0.002     -0.648      0.519      -0.005       0.003
    FCF_Positive                1.5275      1.041      1.467      0.146      -0.541       3.597
    FCF_Positive                1.5275      1.041      1.467      0.146      -0.541       3.597
    YOY_Revenue_Change         -1.0536      5.039     -0.209      0.835     -11.066       8.958
    YOY_EBIT_Change             0.2889      0.266      1.084      0.281      -0.241       0.818
    ==============================================================================
    Omnibus:                       25.663   Durbin-Watson:                   1.527
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               38.351
    Skew:                           1.150   Prob(JB):                     4.70e-09
    Kurtosis:                       4.909   Cond. No.                     1.14e+23
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 6.58e-39. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: P/E
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    P/E   R-squared:                       0.214
    Model:                            OLS   Adj. R-squared:                  0.100
    Method:                 Least Squares   F-statistic:                     1.868
    Date:                Sun, 05 May 2024   Prob (F-statistic):             0.0448
    Time:                        19:16:57   Log-Likelihood:                -302.20
    No. Observations:                 103   AIC:                             632.4
    Df Residuals:                      89   BIC:                             669.3
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      -1.6049      4.537     -0.354      0.724     -10.619       7.409
    Debt_Coverage_Ratio         4.2665      7.064      0.604      0.547      -9.769      18.302
    ROE                        -2.5712      4.228     -0.608      0.545     -10.972       5.829
    EBIT Margin (%)            -2.9748     17.363     -0.171      0.864     -37.475      31.525
    YOY_Gross_Profit_Change    -5.3287      5.369     -0.993      0.324     -15.996       5.339
    ROIC                        0.5459     12.319      0.044      0.965     -23.932      25.023
    FCF_Positive                1.5950      0.905      1.763      0.081      -0.203       3.393
    FCF_Positive                1.5950      0.905      1.763      0.081      -0.203       3.393
    Gross_Margin               10.7198      6.381      1.680      0.096      -1.960      23.399
    Quick_Ratio                 1.1719      1.287      0.910      0.365      -1.386       3.729
    Current_Ratio              -0.4528      1.192     -0.380      0.705      -2.822       1.916
    Debt_to_Equity              0.3425      0.595      0.575      0.567      -0.841       1.526
    Revenue per Employee       -0.0012      0.002     -0.692      0.491      -0.005       0.002
    FCF_Positive                1.5950      0.905      1.763      0.081      -0.203       3.393
    FCF_Positive                1.5950      0.905      1.763      0.081      -0.203       3.393
    YOY_Revenue_Change          0.0701      4.378      0.016      0.987      -8.629       8.769
    YOY_EBIT_Change             0.2077      0.232      0.897      0.372      -0.252       0.668
    ==============================================================================
    Omnibus:                       39.751   Durbin-Watson:                   1.283
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               86.832
    Skew:                           1.508   Prob(JB):                     1.40e-19
    Kurtosis:                       6.337   Cond. No.                     1.14e+23
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 6.58e-39. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/GP
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                  EV/GP   R-squared:                       0.340
    Model:                            OLS   Adj. R-squared:                  0.244
    Method:                 Least Squares   F-statistic:                     3.526
    Date:                Sun, 05 May 2024   Prob (F-statistic):           0.000189
    Time:                        19:16:57   Log-Likelihood:                -192.12
    No. Observations:                 103   AIC:                             412.2
    Df Residuals:                      89   BIC:                             449.1
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       4.0152      1.558      2.577      0.012       0.919       7.111
    Debt_Coverage_Ratio         3.8280      2.426      1.578      0.118      -0.993       8.649
    ROE                        -0.0283      1.452     -0.019      0.984      -2.914       2.857
    EBIT Margin (%)             8.9107      5.964      1.494      0.139      -2.939      20.760
    YOY_Gross_Profit_Change    -1.2475      1.844     -0.677      0.500      -4.911       2.416
    ROIC                       -6.8956      4.231     -1.630      0.107     -15.303       1.512
    FCF_Positive                0.0528      0.311      0.170      0.865      -0.565       0.670
    FCF_Positive                0.0528      0.311      0.170      0.865      -0.565       0.670
    Gross_Margin               -4.3222      2.192     -1.972      0.052      -8.677       0.033
    Quick_Ratio                 1.2145      0.442      2.747      0.007       0.336       2.093
    Current_Ratio              -0.7940      0.410     -1.939      0.056      -1.608       0.020
    Debt_to_Equity             -0.0008      0.205     -0.004      0.997      -0.407       0.406
    Revenue per Employee       -0.0006      0.001     -1.016      0.313      -0.002       0.001
    FCF_Positive                0.0528      0.311      0.170      0.865      -0.565       0.670
    FCF_Positive                0.0528      0.311      0.170      0.865      -0.565       0.670
    YOY_Revenue_Change          0.3880      1.504      0.258      0.797      -2.600       3.376
    YOY_EBIT_Change             0.0335      0.080      0.422      0.674      -0.124       0.192
    ==============================================================================
    Omnibus:                       26.413   Durbin-Watson:                   0.968
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               42.248
    Skew:                           1.134   Prob(JB):                     6.70e-10
    Kurtosis:                       5.169   Cond. No.                     1.14e+23
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 6.58e-39. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV_EBIT
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                EV_EBIT   R-squared:                       0.088
    Model:                            OLS   Adj. R-squared:                 -0.045
    Method:                 Least Squares   F-statistic:                    0.6644
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.792
    Time:                        19:16:57   Log-Likelihood:                -624.01
    No. Observations:                 103   AIC:                             1276.
    Df Residuals:                      89   BIC:                             1313.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      87.9897    103.183      0.853      0.396    -117.033     293.012
    Debt_Coverage_Ratio        84.5840    160.668      0.526      0.600    -234.660     403.828
    ROE                       -84.3795     96.162     -0.877      0.383    -275.451     106.692
    EBIT Margin (%)            86.2472    394.918      0.218      0.828    -698.446     870.940
    YOY_Gross_Profit_Change   -89.4102    122.108     -0.732      0.466    -332.036     153.215
    ROIC                     -165.8184    280.194     -0.592      0.555    -722.559     390.922
    FCF_Positive               -3.7264     20.578     -0.181      0.857     -44.615      37.162
    FCF_Positive               -3.7264     20.578     -0.181      0.857     -44.615      37.162
    Gross_Margin               -9.3793    145.140     -0.065      0.949    -297.770     279.011
    Quick_Ratio                18.5853     29.277      0.635      0.527     -39.587      76.758
    Current_Ratio             -17.7007     27.120     -0.653      0.516     -71.587      36.186
    Debt_to_Equity             11.7877     13.544      0.870      0.386     -15.125      38.700
    Revenue per Employee        0.0099      0.039      0.256      0.799      -0.067       0.087
    FCF_Positive               -3.7264     20.578     -0.181      0.857     -44.615      37.162
    FCF_Positive               -3.7264     20.578     -0.181      0.857     -44.615      37.162
    YOY_Revenue_Change         38.8559     99.578      0.390      0.697    -159.004     236.716
    YOY_EBIT_Change             1.6553      5.266      0.314      0.754      -8.808      12.119
    ==============================================================================
    Omnibus:                      195.687   Durbin-Watson:                   2.031
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):            22541.744
    Skew:                           7.940   Prob(JB):                         0.00
    Kurtosis:                      73.713   Cond. No.                     1.14e+23
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 6.58e-39. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: FCF Yield
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:              FCF Yield   R-squared:                       0.457
    Model:                            OLS   Adj. R-squared:                  0.377
    Method:                 Least Squares   F-statistic:                     5.752
    Date:                Sun, 05 May 2024   Prob (F-statistic):           1.52e-07
    Time:                        19:16:57   Log-Likelihood:                -39.533
    No. Observations:                 103   AIC:                             107.1
    Df Residuals:                      89   BIC:                             144.0
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                       0.2373      0.354      0.670      0.505      -0.466       0.941
    Debt_Coverage_Ratio        -1.4627      0.551     -2.652      0.009      -2.558      -0.367
    ROE                         0.5613      0.330      1.701      0.093      -0.095       1.217
    EBIT Margin (%)             0.5697      1.356      0.420      0.675      -2.124       3.263
    YOY_Gross_Profit_Change    -0.3829      0.419     -0.914      0.363      -1.216       0.450
    ROIC                       -0.2045      0.962     -0.213      0.832      -2.116       1.706
    FCF_Positive                0.0656      0.071      0.929      0.355      -0.075       0.206
    FCF_Positive                0.0656      0.071      0.929      0.355      -0.075       0.206
    Gross_Margin               -0.8998      0.498     -1.806      0.074      -1.890       0.090
    Quick_Ratio                -0.4120      0.100     -4.100      0.000      -0.612      -0.212
    Current_Ratio               0.3837      0.093      4.122      0.000       0.199       0.569
    Debt_to_Equity             -0.0789      0.046     -1.696      0.093      -0.171       0.014
    Revenue per Employee        0.0003      0.000      2.495      0.014    6.76e-05       0.001
    FCF_Positive                0.0656      0.071      0.929      0.355      -0.075       0.206
    FCF_Positive                0.0656      0.071      0.929      0.355      -0.075       0.206
    YOY_Revenue_Change          0.2255      0.342      0.660      0.511      -0.454       0.905
    YOY_EBIT_Change            -0.0308      0.018     -1.707      0.091      -0.067       0.005
    ==============================================================================
    Omnibus:                       74.548   Durbin-Watson:                   1.488
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              596.656
    Skew:                           2.235   Prob(JB):                    2.74e-130
    Kurtosis:                      13.911   Cond. No.                     1.14e+23
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 6.58e-39. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.
    
    Multiple: EV/EBITDA-Capex
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:        EV/EBITDA-Capex   R-squared:                       0.043
    Model:                            OLS   Adj. R-squared:                 -0.097
    Method:                 Least Squares   F-statistic:                    0.3058
    Date:                Sun, 05 May 2024   Prob (F-statistic):              0.990
    Time:                        19:16:57   Log-Likelihood:                -561.74
    No. Observations:                 103   AIC:                             1151.
    Df Residuals:                      89   BIC:                             1188.
    Df Model:                          13                                         
    Covariance Type:            nonrobust                                         
    ===========================================================================================
                                  coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------------------
    const                      -2.4300     56.373     -0.043      0.966    -114.441     109.581
    Debt_Coverage_Ratio         5.1911     87.779      0.059      0.953    -169.224     179.606
    ROE                       -72.6887     52.537     -1.384      0.170    -177.078      31.701
    EBIT Margin (%)            11.0808    215.758      0.051      0.959    -417.626     439.788
    YOY_Gross_Profit_Change    19.2851     66.712      0.289      0.773    -113.270     151.841
    ROIC                      -18.2682    153.081     -0.119      0.905    -322.436     285.900
    FCF_Positive               -2.0830     11.243     -0.185      0.853     -24.422      20.256
    FCF_Positive               -2.0830     11.243     -0.185      0.853     -24.422      20.256
    Gross_Margin               74.4972     79.296      0.939      0.350     -83.061     232.056
    Quick_Ratio                -8.4499     15.995     -0.528      0.599     -40.232      23.332
    Current_Ratio               7.3189     14.817      0.494      0.623     -22.121      36.759
    Debt_to_Equity             10.2942      7.400      1.391      0.168      -4.409      24.998
    Revenue per Employee        0.0103      0.021      0.486      0.628      -0.032       0.052
    FCF_Positive               -2.0830     11.243     -0.185      0.853     -24.422      20.256
    FCF_Positive               -2.0830     11.243     -0.185      0.853     -24.422      20.256
    YOY_Revenue_Change         -8.7841     54.403     -0.161      0.872    -116.883      99.314
    YOY_EBIT_Change            -0.5077      2.877     -0.176      0.860      -6.224       5.209
    ==============================================================================
    Omnibus:                       80.111   Durbin-Watson:                   1.883
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):             2530.185
    Skew:                          -1.833   Prob(JB):                         0.00
    Kurtosis:                      27.002   Cond. No.                     1.14e+23
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The smallest eigenvalue is 6.58e-39. This might indicate that there are
    strong multicollinearity problems or that the design matrix is singular.



```python
from sklearn.model_selection import train_test_split
from interpret.glassbox import ExplainableBoostingRegressor 
from interpret import show
```


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


```python
from sklearn.model_selection import train_test_split
from interpret.glassbox import ExplainableBoostingRegressor
from interpret import show

# Adjust the data by replacing the division mapping
# This assumes you have already run the division grouping mapping mentioned earlier

# Loop through each unique Division and compute feature importance
for division, group in selected_df.groupby('Division'):
    print(f"\nDivision: {division}")
    
    # Prepare features (X) and target (y)
    X = group.drop(columns=['Ticker', 'Division','EV/EBITDA', 'P/E', 'EV/GP','EV_EBIT','FCF Yield','EV/EBITDA-Capex'])
    y = group['EV/EBITDA']

    # Check if there are enough samples to perform a split and modeling
    if len(y) < 2:
        print(f"Not enough samples to perform feature selection for {division}")
        continue
    
    # Split the dataset into training and testing sets
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.20, random_state=42)

    # Initialize the ExplainableBoostingRegressor
    ebm = ExplainableBoostingRegressor(random_state=42)

    # Fit the model
    ebm.fit(X_train, y_train)

    # Get the global feature importances from the model
    ebm_global = ebm.explain_global()
    show(ebm_global)
```

    
    Division: Construction



<!-- http://127.0.0.1:7001/140191826074160/ -->
<iframe src="http://127.0.0.1:7001/140191826074160/" width=100% height=800 frameBorder="0"></iframe>


    
    Division: Finance, Insurance and Real Estate



<!-- http://127.0.0.1:7001/140191851993792/ -->
<iframe src="http://127.0.0.1:7001/140191851993792/" width=100% height=800 frameBorder="0"></iframe>


    
    Division: Manufacturing



<!-- http://127.0.0.1:7001/140191825955760/ -->
<iframe src="http://127.0.0.1:7001/140191825955760/" width=100% height=800 frameBorder="0"></iframe>


    
    Division: Mining_Trans_Comm_Gas_Sanitary



<!-- http://127.0.0.1:7001/140191794564880/ -->
<iframe src="http://127.0.0.1:7001/140191794564880/" width=100% height=800 frameBorder="0"></iframe>


    
    Division: Retail Trade



<!-- http://127.0.0.1:7001/140191811128144/ -->
<iframe src="http://127.0.0.1:7001/140191811128144/" width=100% height=800 frameBorder="0"></iframe>


    
    Division: Services



<!-- http://127.0.0.1:7001/140191860285936/ -->
<iframe src="http://127.0.0.1:7001/140191860285936/" width=100% height=800 frameBorder="0"></iframe>


    
    Division: Unknown_Nonclassifiable



<!-- http://127.0.0.1:7001/140191825891088/ -->
<iframe src="http://127.0.0.1:7001/140191825891088/" width=100% height=800 frameBorder="0"></iframe>


    
    Division: Wholesale Trade



<!-- http://127.0.0.1:7001/140191824686096/ -->
<iframe src="http://127.0.0.1:7001/140191824686096/" width=100% height=800 frameBorder="0"></iframe>



```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.preprocessing import StandardScaler
import seaborn as sns
import matplotlib.pyplot as plt

# Group the data by 'Division'
for division, group in selected_df.groupby('Division'):
    print(f"\nDivision: {division}")

    # Prepare the features (X) and target (y)
    X = group.drop(columns=['Ticker', 'Division', 'EV/EBITDA', 'P/E', 'EV/GP', 'EV_EBIT', 'FCF Yield', 'EV/EBITDA-Capex'])
    y = group['EV/EBITDA']

    # Check if there are enough samples to train the model
    if len(y) < 2:
        print(f"Not enough samples to perform feature selection for {division}")
        continue

    # Scale the features
    scaler = StandardScaler()
    X_scaled = scaler.fit_transform(X)

    # Use RandomForestRegressor to get feature importances
    rf = RandomForestRegressor(random_state=42)
    rf.fit(X_scaled, y)
    feature_importances = rf.feature_importances_

    # Plot feature importances
    features = pd.DataFrame({'Feature': X.columns, 'Importance': feature_importances})
    features = features.sort_values(by='Importance', ascending=False)
    
    plt.figure(figsize=(10, 6))
    sns.barplot(x='Importance', y='Feature', data=features.head(20))
    plt.title(f'Top 20 Important Features according to Random Forest for {division}')
    plt.show()
```

    
    Division: Construction



    
![png](output_21_1.png)
    


    
    Division: Finance, Insurance and Real Estate



    
![png](output_21_3.png)
    


    
    Division: Manufacturing



    
![png](output_21_5.png)
    


    
    Division: Mining_Trans_Comm_Gas_Sanitary



    
![png](output_21_7.png)
    


    
    Division: Retail Trade



    
![png](output_21_9.png)
    


    
    Division: Services



    
![png](output_21_11.png)
    


    
    Division: Unknown_Nonclassifiable



    
![png](output_21_13.png)
    


    
    Division: Wholesale Trade



    
![png](output_21_15.png)
    



```python
from sklearn.feature_selection import RFE

# Recursive Feature Elimination (RFE)
rfe = RFE(estimator=rf, n_features_to_select=10)
rfe.fit(X_scaled, y)

# Features selected by RFE
selected_features = X.columns[rfe.support_]
print("Features selected by RFE:", selected_features)
```

    Features selected by RFE: Index(['ROE', 'ROIC', 'Debt_Coverage_Ratio', 'Interest_Coverage_Ratio',
           'Gross_Margin', 'Revenue per Employee', 'Operating_Margin',
           'EBIT Margin (%)', 'Price_Range_Ratio', 'YOY_Operating_Margin_Change'],
          dtype='object')

