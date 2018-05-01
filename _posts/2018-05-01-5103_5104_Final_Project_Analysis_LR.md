---
layout: post
title: Analysis LR
---

```python
#Mathew Suran
#DSSA-5103-91 Data Visualization
#DSSA-5104-91 Data Analysis
#Final Project
#04/14/18

import sys
import os
from pprint import pprint
from tqdm import tqdm
import threading
from pandas.core import datetools

import statsmodels.api as sm
import pandas as pd
import numpy as np
import codecs

import matplotlib.pyplot as plt
import seaborn as sns
sns.set(color_codes=True)
```


```python
#Load in slope data for each profile line to run linear regression
```


```python
#Load Final Beach Replenishment Data
# Assign spreadsheet filename to `NJBPN`
df_beach_el_merge_final4 = pd.ExcelFile('df_beach_el_merge_final4.xlsx')
# Convert Excel file to dataframe
df_beach_el_merge_final4 = df_beach_el_merge_final4.parse('DataFrame')
# Check column types
df_beach_el_merge_final4.dtypes
```




    MUN            object
    Year            int64
    Line            int64
    Latitude      float64
    Longitude     float64
    Total_CY        int64
    Costin2016      int64
    Z             float64
    dtype: object




```python
df_beach_el_merge_final4
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
      <th>MUN</th>
      <th>Year</th>
      <th>Line</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Total_CY</th>
      <th>Costin2016</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Asbury Park</td>
      <td>2001</td>
      <td>167</td>
      <td>40.210737</td>
      <td>-74.002733</td>
      <td>3100000</td>
      <td>49494739</td>
      <td>-5.7200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Asbury Park</td>
      <td>2014</td>
      <td>167</td>
      <td>40.210737</td>
      <td>-74.002733</td>
      <td>1200000</td>
      <td>18410462</td>
      <td>-4.3830</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Atlantic City</td>
      <td>1986</td>
      <td>130</td>
      <td>39.357595</td>
      <td>-74.421816</td>
      <td>1000000</td>
      <td>15184381</td>
      <td>-2.6000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Atlantic City</td>
      <td>2004</td>
      <td>130</td>
      <td>39.357595</td>
      <td>-74.421816</td>
      <td>4000000</td>
      <td>34532931</td>
      <td>-5.7350</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Atlantic City</td>
      <td>2011</td>
      <td>130</td>
      <td>39.357595</td>
      <td>-74.421816</td>
      <td>1003000</td>
      <td>7944450</td>
      <td>-9.4500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Atlantic City</td>
      <td>2012</td>
      <td>130</td>
      <td>39.357595</td>
      <td>-74.421816</td>
      <td>1325000</td>
      <td>21800793</td>
      <td>-5.7875</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Atlantic City</td>
      <td>2013</td>
      <td>130</td>
      <td>39.357595</td>
      <td>-74.421816</td>
      <td>760000</td>
      <td>11526704</td>
      <td>-6.2000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Avalon</td>
      <td>1987</td>
      <td>116</td>
      <td>39.098428</td>
      <td>-74.711459</td>
      <td>1305000</td>
      <td>6037689</td>
      <td>-0.5700</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Avalon</td>
      <td>1990</td>
      <td>116</td>
      <td>39.098428</td>
      <td>-74.711459</td>
      <td>404000</td>
      <td>1050788</td>
      <td>4.2500</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Avalon</td>
      <td>1992</td>
      <td>116</td>
      <td>39.098428</td>
      <td>-74.711459</td>
      <td>410000</td>
      <td>2020408</td>
      <td>-4.5900</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Avalon</td>
      <td>1993</td>
      <td>116</td>
      <td>39.098428</td>
      <td>-74.711459</td>
      <td>239000</td>
      <td>2932661</td>
      <td>-3.6500</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Avalon</td>
      <td>2010</td>
      <td>116</td>
      <td>39.098428</td>
      <td>-74.711459</td>
      <td>500000</td>
      <td>4912663</td>
      <td>-8.1000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Avalon</td>
      <td>2011</td>
      <td>116</td>
      <td>39.098428</td>
      <td>-74.711459</td>
      <td>450000</td>
      <td>9686721</td>
      <td>-5.3200</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Avalon</td>
      <td>2013</td>
      <td>116</td>
      <td>39.098428</td>
      <td>-74.711459</td>
      <td>121359</td>
      <td>2627328</td>
      <td>-5.0350</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Barnegat Light</td>
      <td>1991</td>
      <td>145</td>
      <td>39.764626</td>
      <td>-74.105426</td>
      <td>75000</td>
      <td>571080</td>
      <td>-4.9200</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Beach Haven</td>
      <td>2010</td>
      <td>136</td>
      <td>39.557398</td>
      <td>-74.239254</td>
      <td>2000</td>
      <td>515283</td>
      <td>-6.6800</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Brant Beach</td>
      <td>2012</td>
      <td>139</td>
      <td>39.620367</td>
      <td>-74.194772</td>
      <td>1250000</td>
      <td>17323651</td>
      <td>-6.2250</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Brant Beach</td>
      <td>2014</td>
      <td>139</td>
      <td>39.620367</td>
      <td>-74.194772</td>
      <td>1060000</td>
      <td>10959764</td>
      <td>-4.1970</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Brigantine</td>
      <td>1997</td>
      <td>133</td>
      <td>39.405826</td>
      <td>-74.362421</td>
      <td>1200000</td>
      <td>8875739</td>
      <td>-6.0900</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Brigantine</td>
      <td>1999</td>
      <td>133</td>
      <td>39.405826</td>
      <td>-74.362421</td>
      <td>999827</td>
      <td>7110157</td>
      <td>-3.1750</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Brigantine</td>
      <td>2006</td>
      <td>133</td>
      <td>39.405826</td>
      <td>-74.362421</td>
      <td>672000</td>
      <td>17709563</td>
      <td>-6.3350</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Brigantine</td>
      <td>2011</td>
      <td>133</td>
      <td>39.405826</td>
      <td>-74.362421</td>
      <td>175000</td>
      <td>3132780</td>
      <td>-7.0050</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Brigantine</td>
      <td>2013</td>
      <td>133</td>
      <td>39.405826</td>
      <td>-74.362421</td>
      <td>757000</td>
      <td>6009764</td>
      <td>-7.2550</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Cape May</td>
      <td>1986</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>15000</td>
      <td>590021</td>
      <td>-1.3000</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Cape May</td>
      <td>1989</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>465000</td>
      <td>6061420</td>
      <td>0.3500</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Cape May</td>
      <td>1991</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>1365000</td>
      <td>18434325</td>
      <td>-0.0400</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Cape May</td>
      <td>1992</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>242000</td>
      <td>764293</td>
      <td>-6.6000</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Cape May</td>
      <td>1993</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>1015000</td>
      <td>11113861</td>
      <td>-2.4000</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Cape May</td>
      <td>1995</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>330000</td>
      <td>4063962</td>
      <td>-2.4150</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Cape May</td>
      <td>1997</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>366000</td>
      <td>3550295</td>
      <td>-6.9850</td>
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
    </tr>
    <tr>
      <th>58</th>
      <td>Ocean City</td>
      <td>1995</td>
      <td>124</td>
      <td>39.264158</td>
      <td>-74.589958</td>
      <td>1771000</td>
      <td>10892898</td>
      <td>-3.1500</td>
    </tr>
    <tr>
      <th>59</th>
      <td>Ocean City</td>
      <td>1997</td>
      <td>124</td>
      <td>39.264158</td>
      <td>-74.589958</td>
      <td>800000</td>
      <td>7315088</td>
      <td>-6.1700</td>
    </tr>
    <tr>
      <th>60</th>
      <td>Ocean City</td>
      <td>2000</td>
      <td>124</td>
      <td>39.264158</td>
      <td>-74.589958</td>
      <td>1351000</td>
      <td>9576551</td>
      <td>-5.5400</td>
    </tr>
    <tr>
      <th>61</th>
      <td>Ocean City</td>
      <td>2004</td>
      <td>124</td>
      <td>39.264158</td>
      <td>-74.589958</td>
      <td>1600000</td>
      <td>10484237</td>
      <td>-6.6900</td>
    </tr>
    <tr>
      <th>62</th>
      <td>Ocean City</td>
      <td>2010</td>
      <td>124</td>
      <td>39.264158</td>
      <td>-74.589958</td>
      <td>1400000</td>
      <td>15091703</td>
      <td>-8.3400</td>
    </tr>
    <tr>
      <th>63</th>
      <td>Ocean City</td>
      <td>2013</td>
      <td>124</td>
      <td>39.264158</td>
      <td>-74.589958</td>
      <td>1836200</td>
      <td>18978220</td>
      <td>-7.6700</td>
    </tr>
    <tr>
      <th>64</th>
      <td>Port Monmouth</td>
      <td>2012</td>
      <td>185</td>
      <td>40.439500</td>
      <td>-74.093714</td>
      <td>800000</td>
      <td>13381742</td>
      <td>-5.3050</td>
    </tr>
    <tr>
      <th>65</th>
      <td>Port Monmouth</td>
      <td>2015</td>
      <td>185</td>
      <td>40.439500</td>
      <td>-74.093714</td>
      <td>391000</td>
      <td>17820351</td>
      <td>-5.6165</td>
    </tr>
    <tr>
      <th>66</th>
      <td>Sandy Hook</td>
      <td>1990</td>
      <td>184</td>
      <td>40.455046</td>
      <td>-73.989172</td>
      <td>3302273</td>
      <td>2364273</td>
      <td>-4.2600</td>
    </tr>
    <tr>
      <th>67</th>
      <td>Sea Bright</td>
      <td>1996</td>
      <td>180</td>
      <td>40.346152</td>
      <td>-73.973207</td>
      <td>3800000</td>
      <td>36941781</td>
      <td>-10.7150</td>
    </tr>
    <tr>
      <th>68</th>
      <td>Sea Bright</td>
      <td>2013</td>
      <td>180</td>
      <td>40.346152</td>
      <td>-73.973207</td>
      <td>2460000</td>
      <td>26166462</td>
      <td>-10.9975</td>
    </tr>
    <tr>
      <th>69</th>
      <td>Sea Isle City</td>
      <td>1987</td>
      <td>118</td>
      <td>39.141178</td>
      <td>-74.699750</td>
      <td>158000</td>
      <td>1109756</td>
      <td>0.9000</td>
    </tr>
    <tr>
      <th>70</th>
      <td>Sea Isle City</td>
      <td>2009</td>
      <td>118</td>
      <td>39.141178</td>
      <td>-74.699750</td>
      <td>394797</td>
      <td>4011064</td>
      <td>-4.0350</td>
    </tr>
    <tr>
      <th>71</th>
      <td>Sea Isle City</td>
      <td>2010</td>
      <td>118</td>
      <td>39.141178</td>
      <td>-74.699750</td>
      <td>700000</td>
      <td>6550218</td>
      <td>-6.6450</td>
    </tr>
    <tr>
      <th>72</th>
      <td>Sea Isle City</td>
      <td>2012</td>
      <td>118</td>
      <td>39.141178</td>
      <td>-74.699750</td>
      <td>394797</td>
      <td>5186721</td>
      <td>-5.9000</td>
    </tr>
    <tr>
      <th>73</th>
      <td>Spring Lake</td>
      <td>1994</td>
      <td>160</td>
      <td>40.150144</td>
      <td>-74.022303</td>
      <td>70000</td>
      <td>559096</td>
      <td>-6.7300</td>
    </tr>
    <tr>
      <th>74</th>
      <td>Stone Harbor</td>
      <td>2009</td>
      <td>113</td>
      <td>39.050752</td>
      <td>-74.756134</td>
      <td>319670</td>
      <td>1664816</td>
      <td>-6.2650</td>
    </tr>
    <tr>
      <th>75</th>
      <td>Stone Harbor</td>
      <td>2011</td>
      <td>113</td>
      <td>39.050752</td>
      <td>-74.756134</td>
      <td>580000</td>
      <td>9686721</td>
      <td>-7.1700</td>
    </tr>
    <tr>
      <th>76</th>
      <td>Stone Harbor</td>
      <td>2013</td>
      <td>113</td>
      <td>39.050752</td>
      <td>-74.756134</td>
      <td>365000</td>
      <td>5687065</td>
      <td>-7.5550</td>
    </tr>
    <tr>
      <th>77</th>
      <td>Strathmere</td>
      <td>1992</td>
      <td>121</td>
      <td>39.194613</td>
      <td>-74.657435</td>
      <td>23000</td>
      <td>174624</td>
      <td>-4.5300</td>
    </tr>
    <tr>
      <th>78</th>
      <td>Strathmere</td>
      <td>2009</td>
      <td>121</td>
      <td>39.194613</td>
      <td>-74.657435</td>
      <td>891000</td>
      <td>6689034</td>
      <td>-3.5600</td>
    </tr>
    <tr>
      <th>79</th>
      <td>Strathmere</td>
      <td>2012</td>
      <td>121</td>
      <td>39.194613</td>
      <td>-74.657435</td>
      <td>450000</td>
      <td>4356846</td>
      <td>-5.8900</td>
    </tr>
    <tr>
      <th>80</th>
      <td>Surf City</td>
      <td>2007</td>
      <td>241</td>
      <td>39.625788</td>
      <td>-74.194107</td>
      <td>880000</td>
      <td>81515499</td>
      <td>-5.1350</td>
    </tr>
    <tr>
      <th>81</th>
      <td>Surf City</td>
      <td>2011</td>
      <td>241</td>
      <td>39.625788</td>
      <td>-74.194107</td>
      <td>300000</td>
      <td>6273858</td>
      <td>-6.8850</td>
    </tr>
    <tr>
      <th>82</th>
      <td>Surf City</td>
      <td>2014</td>
      <td>241</td>
      <td>39.625788</td>
      <td>-74.194107</td>
      <td>415000</td>
      <td>5383156</td>
      <td>-3.5495</td>
    </tr>
    <tr>
      <th>83</th>
      <td>Ventnor</td>
      <td>2004</td>
      <td>128</td>
      <td>39.337484</td>
      <td>-74.475292</td>
      <td>3000000</td>
      <td>12028325</td>
      <td>-6.1000</td>
    </tr>
    <tr>
      <th>84</th>
      <td>Ventnor</td>
      <td>2011</td>
      <td>128</td>
      <td>39.337484</td>
      <td>-74.475292</td>
      <td>175000</td>
      <td>2767168</td>
      <td>-6.6750</td>
    </tr>
    <tr>
      <th>85</th>
      <td>Ventnor</td>
      <td>2012</td>
      <td>128</td>
      <td>39.337484</td>
      <td>-74.475292</td>
      <td>325000</td>
      <td>7085256</td>
      <td>-4.7500</td>
    </tr>
    <tr>
      <th>86</th>
      <td>Ventnor</td>
      <td>2014</td>
      <td>128</td>
      <td>39.337484</td>
      <td>-74.475292</td>
      <td>340000</td>
      <td>6097729</td>
      <td>-3.8530</td>
    </tr>
    <tr>
      <th>87</th>
      <td>Wildwood</td>
      <td>1991</td>
      <td>110</td>
      <td>38.978995</td>
      <td>-74.817971</td>
      <td>100000</td>
      <td>761441</td>
      <td>-0.2300</td>
    </tr>
  </tbody>
</table>
<p>88 rows × 8 columns</p>
</div>




```python
X = df_beach_el_merge_final4["Total_CY"]
y = df_beach_el_merge_final4["Z"]

# Note the difference in argument order
model = sm.OLS(y, X).fit()
predictions = model.predict(X) # make the predictions by the model

# Print out the statistics
model.summary()
```




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>            <td>Z</td>        <th>  R-squared:         </th> <td>   0.445</td>
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th> <td>   0.438</td>
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th> <td>   69.64</td>
</tr>
<tr>
  <th>Date:</th>             <td>Tue, 01 May 2018</td> <th>  Prob (F-statistic):</th> <td>9.81e-13</td>
</tr>
<tr>
  <th>Time:</th>                 <td>01:19:04</td>     <th>  Log-Likelihood:    </th> <td> -264.69</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td>    88</td>      <th>  AIC:               </th> <td>   531.4</td>
</tr>
<tr>
  <th>Df Residuals:</th>          <td>    87</td>      <th>  BIC:               </th> <td>   533.9</td>
</tr>
<tr>
  <th>Df Model:</th>              <td>     1</td>      <th>                     </th>     <td> </td>   
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>     <td> </td>   
</tr>
</table>
<table class="simpletable">
<tr>
      <td></td>        <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>Total_CY</th> <td>-2.799e-06</td> <td> 3.35e-07</td> <td>   -8.345</td> <td> 0.000</td> <td>-3.47e-06</td> <td>-2.13e-06</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td> 2.635</td> <th>  Durbin-Watson:     </th> <td>   1.080</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.268</td> <th>  Jarque-Bera (JB):  </th> <td>   2.557</td>
</tr>
<tr>
  <th>Skew:</th>          <td> 0.407</td> <th>  Prob(JB):          </th> <td>   0.279</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 2.816</td> <th>  Cond. No.          </th> <td>    1.00</td>
</tr>
</table>




```python
y = df_beach_el_merge_final4["Total_CY"]
X = df_beach_el_merge_final4["Z"]

# Note the difference in argument order
model = sm.OLS(y, X).fit()
predictions = model.predict(X) # make the predictions by the model

# Print out the statistics
model.summary()
```




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>        <td>Total_CY</td>     <th>  R-squared:         </th> <td>   0.445</td>
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th> <td>   0.438</td>
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th> <td>   69.64</td>
</tr>
<tr>
  <th>Date:</th>             <td>Tue, 01 May 2018</td> <th>  Prob (F-statistic):</th> <td>9.81e-13</td>
</tr>
<tr>
  <th>Time:</th>                 <td>01:19:13</td>     <th>  Log-Likelihood:    </th> <td> -1354.2</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td>    88</td>      <th>  AIC:               </th> <td>   2710.</td>
</tr>
<tr>
  <th>Df Residuals:</th>          <td>    87</td>      <th>  BIC:               </th> <td>   2713.</td>
</tr>
<tr>
  <th>Df Model:</th>              <td>     1</td>      <th>                     </th>     <td> </td>   
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>     <td> </td>   
</tr>
</table>
<table class="simpletable">
<tr>
  <td></td>     <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>Z</th> <td>-1.588e+05</td> <td>  1.9e+04</td> <td>   -8.345</td> <td> 0.000</td> <td>-1.97e+05</td> <td>-1.21e+05</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>16.685</td> <th>  Durbin-Watson:     </th> <td>   1.725</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td> <th>  Jarque-Bera (JB):  </th> <td>  19.321</td>
</tr>
<tr>
  <th>Skew:</th>          <td> 1.098</td> <th>  Prob(JB):          </th> <td>6.37e-05</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 3.669</td> <th>  Cond. No.          </th> <td>    1.00</td>
</tr>
</table>




```python
# Find most beach replenishments at location
df_beach_el_merge_final4['MUN'].describe()
```




    count          103
    unique          28
    top       Cape May
    freq            19
    Name: MUN, dtype: object




```python
# Use Cape May as df and run Linear Regression
# Find just a row based on value you select-loc is used for labels, iloc for integer
df_Cape_May = df_beach_el_merge_final4.loc[df_beach_el_merge_final4['MUN'] == "Cape May"]
df_Cape_May
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
      <th>MUN</th>
      <th>Year</th>
      <th>Line</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Total_CY</th>
      <th>Costin2016</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>23</th>
      <td>Cape May</td>
      <td>1986</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>15000</td>
      <td>590021</td>
      <td>-1.3000</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Cape May</td>
      <td>1989</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>465000</td>
      <td>6061420</td>
      <td>0.3500</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Cape May</td>
      <td>1991</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>1365000</td>
      <td>18434325</td>
      <td>-0.0400</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Cape May</td>
      <td>1992</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>242000</td>
      <td>764293</td>
      <td>-6.6000</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Cape May</td>
      <td>1993</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>1015000</td>
      <td>11113861</td>
      <td>-2.4000</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Cape May</td>
      <td>1995</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>330000</td>
      <td>4063962</td>
      <td>-2.4150</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Cape May</td>
      <td>1997</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>366000</td>
      <td>3550295</td>
      <td>-6.9850</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Cape May</td>
      <td>1999</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>2772000</td>
      <td>110115879</td>
      <td>-6.7800</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Cape May</td>
      <td>2003</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>267000</td>
      <td>3141935</td>
      <td>-11.3500</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Cape May</td>
      <td>2004</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>290000</td>
      <td>2981084</td>
      <td>-10.6050</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Cape May</td>
      <td>2007</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>230000</td>
      <td>4587256</td>
      <td>-9.8700</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Cape May</td>
      <td>2009</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>1225000</td>
      <td>12069920</td>
      <td>-11.1600</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Cape May</td>
      <td>2012</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>770000</td>
      <td>9336099</td>
      <td>-9.3300</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Cape May</td>
      <td>2014</td>
      <td>106</td>
      <td>38.929502</td>
      <td>-74.924212</td>
      <td>585000</td>
      <td>9803319</td>
      <td>-8.6235</td>
    </tr>
  </tbody>
</table>
</div>




```python
X = df_Cape_May["Total_CY"]
y = df_Cape_May["Z"]

# Note the difference in argument order
model = sm.OLS(y, X).fit()
predictions = model.predict(X) # make the predictions by the model

# Print out the statistics
model.summary()
```

    /home/m/anaconda3/lib/python3.6/site-packages/scipy/stats/stats.py:1390: UserWarning: kurtosistest only valid for n>=20 ... continuing anyway, n=14
      "anyway, n=%i" % int(n))





<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>            <td>Z</td>        <th>  R-squared:         </th> <td>   0.342</td>
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th> <td>   0.291</td>
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th> <td>   6.746</td>
</tr>
<tr>
  <th>Date:</th>             <td>Tue, 01 May 2018</td> <th>  Prob (F-statistic):</th>  <td>0.0221</td> 
</tr>
<tr>
  <th>Time:</th>                 <td>01:21:50</td>     <th>  Log-Likelihood:    </th> <td> -45.048</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td>    14</td>      <th>  AIC:               </th> <td>   92.10</td>
</tr>
<tr>
  <th>Df Residuals:</th>          <td>    13</td>      <th>  BIC:               </th> <td>   92.74</td>
</tr>
<tr>
  <th>Df Model:</th>              <td>     1</td>      <th>                     </th>     <td> </td>   
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>     <td> </td>   
</tr>
</table>
<table class="simpletable">
<tr>
      <td></td>        <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>Total_CY</th> <td>-4.394e-06</td> <td> 1.69e-06</td> <td>   -2.597</td> <td> 0.022</td> <td>-8.05e-06</td> <td>-7.39e-07</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td> 1.801</td> <th>  Durbin-Watson:     </th> <td>   1.200</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.406</td> <th>  Jarque-Bera (JB):  </th> <td>   1.127</td>
</tr>
<tr>
  <th>Skew:</th>          <td> 0.409</td> <th>  Prob(JB):          </th> <td>   0.569</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 1.877</td> <th>  Cond. No.          </th> <td>    1.00</td>
</tr>
</table>




```python
y = df_Cape_May["Total_CY"]
X = df_Cape_May["Z"]

# Note the difference in argument order
model = sm.OLS(y, X).fit()
predictions = model.predict(X) # make the predictions by the model

# Print out the statistics
model.summary()
```

    /home/m/anaconda3/lib/python3.6/site-packages/scipy/stats/stats.py:1390: UserWarning: kurtosistest only valid for n>=20 ... continuing anyway, n=14
      "anyway, n=%i" % int(n))





<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>        <td>Total_CY</td>     <th>  R-squared:         </th> <td>   0.342</td>
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th> <td>   0.291</td>
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th> <td>   6.746</td>
</tr>
<tr>
  <th>Date:</th>             <td>Tue, 01 May 2018</td> <th>  Prob (F-statistic):</th>  <td>0.0221</td> 
</tr>
<tr>
  <th>Time:</th>                 <td>01:22:17</td>     <th>  Log-Likelihood:    </th> <td> -210.22</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td>    14</td>      <th>  AIC:               </th> <td>   422.4</td>
</tr>
<tr>
  <th>Df Residuals:</th>          <td>    13</td>      <th>  BIC:               </th> <td>   423.1</td>
</tr>
<tr>
  <th>Df Model:</th>              <td>     1</td>      <th>                     </th>     <td> </td>   
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>     <td> </td>   
</tr>
</table>
<table class="simpletable">
<tr>
  <td></td>     <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>Z</th> <td>-7.775e+04</td> <td> 2.99e+04</td> <td>   -2.597</td> <td> 0.022</td> <td>-1.42e+05</td> <td>-1.31e+04</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td> 7.848</td> <th>  Durbin-Watson:     </th> <td>   2.267</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.020</td> <th>  Jarque-Bera (JB):  </th> <td>   4.350</td>
</tr>
<tr>
  <th>Skew:</th>          <td> 1.276</td> <th>  Prob(JB):          </th> <td>   0.114</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 3.974</td> <th>  Cond. No.          </th> <td>    1.00</td>
</tr>
</table>




```python
import matplotlib
 
import matplotlib.pyplot as plt
import numpy as np
from sklearn import datasets, linear_model
import pandas as pd

Y = df_beach_el_merge_final4['Total_CY']
X = df_beach_el_merge_final4['Z']
fit = np.polyfit(X, Y, deg=1)
plot(X, fit[0] * X + fit[1], color='red')
scatter(X, Y)
show()
```


![png](5103_5104_Final_Project_Analysis_LR_files/5103_5104_Final_Project_Analysis_LR_10_0.png)



```python

```
