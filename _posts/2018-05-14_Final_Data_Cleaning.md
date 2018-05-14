---
layout: post
title: Cleaning in Jupyter Notebook
---

<div tabindex="-1" id="notebook" class="border-box-sizing">

<div class="container" id="notebook-container">

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [2]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Mathew Suran</span>
<span class="c1">#DSSA-5103-91 Data Visualization</span>
<span class="c1">#DSSA-5104-91 Data Analysis</span>
<span class="c1">#Final Project</span>
<span class="c1">#05/12/18</span>

<span class="kn">import</span> <span class="nn">sys</span>
<span class="kn">import</span> <span class="nn">os</span>
<span class="kn">from</span> <span class="nn">pprint</span> <span class="k">import</span> <span class="n">pprint</span>
<span class="kn">from</span> <span class="nn">tqdm</span> <span class="k">import</span> <span class="n">tqdm</span>
<span class="kn">import</span> <span class="nn">threading</span>

<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">codecs</span>

<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="n">sns</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">color_codes</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

Load the Data

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [3]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Load Beach Replenishment Data</span>
<span class="c1"># Assign spreadsheet filename to `NJBPN`</span>
<span class="n">df_beach</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">ExcelFile</span><span class="p">(</span><span class="s1">'NJData.xlsx'</span><span class="p">)</span>
<span class="c1"># Convert Excel file to dataframe</span>
<span class="n">df_beach</span> <span class="o">=</span> <span class="n">df_beach</span><span class="o">.</span><span class="n">parse</span><span class="p">(</span><span class="s1">'Sheet1'</span><span class="p">)</span>
<span class="c1"># Check column types</span>
<span class="n">df_beach</span><span class="o">.</span><span class="n">dtypes</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[3]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>Beach Location              object
State                       object
Year Completed               int64
Latitude                   float64
Longitude                  float64
Primary Funding Source      object
Justification               object
Length (ft)                float64
Volume (CY)                  int64
Nominal Cost               float64
2016 CF$                   float64
Cost in 2016               float64
dtype: object</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [4]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Display info</span>
<span class="n">df_beach</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre><class 'pandas.core.frame.DataFrame'>
RangeIndex: 322 entries, 0 to 321
Data columns (total 12 columns):
Beach Location             322 non-null object
State                      322 non-null object
Year Completed             322 non-null int64
Latitude                   322 non-null float64
Longitude                  322 non-null float64
Primary Funding Source     322 non-null object
Justification              322 non-null object
Length (ft)                308 non-null float64
Volume (CY)                322 non-null int64
Nominal Cost               320 non-null float64
2016 CF$                   322 non-null float64
Cost in 2016               322 non-null float64
dtypes: float64(6), int64(2), object(4)
memory usage: 30.3+ KB
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [5]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Check the df</span>
<span class="n">df_beach</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[5]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>Beach Location</th>

<th>State</th>

<th>Year Completed</th>

<th>Latitude</th>

<th>Longitude</th>

<th>Primary Funding Source</th>

<th>Justification</th>

<th>Length (ft)</th>

<th>Volume (CY)</th>

<th>Nominal Cost</th>

<th>2016 CF$</th>

<th>Cost in 2016</th>

</tr>

</thead>

<tbody>

<tr>

<th>0</th>

<td>Atlantic City</td>

<td>NJ</td>

<td>1936</td>

<td>39.357595</td>

<td>-74.421816</td>

<td>Unknown</td>

<td>Unknown</td>

<td>0.0</td>

<td>792000</td>

<td>157832.0</td>

<td>0.058</td>

<td>2.721241e+06</td>

</tr>

<tr>

<th>1</th>

<td>Atlantic City</td>

<td>NJ</td>

<td>1936</td>

<td>39.357595</td>

<td>-74.421816</td>

<td>Federal</td>

<td>Shore Protection</td>

<td>0.0</td>

<td>191447</td>

<td>0.0</td>

<td>0.058</td>

<td>0.000000e+00</td>

</tr>

<tr>

<th>2</th>

<td>Atlantic City</td>

<td>NJ</td>

<td>1937</td>

<td>39.357595</td>

<td>-74.421816</td>

<td>Unknown</td>

<td>Unknown</td>

<td>0.0</td>

<td>900000</td>

<td>204638.0</td>

<td>0.060</td>

<td>3.410633e+06</td>

</tr>

<tr>

<th>3</th>

<td>Atlantic City</td>

<td>NJ</td>

<td>1938</td>

<td>39.357595</td>

<td>-74.421816</td>

<td>Unknown</td>

<td>Unknown</td>

<td>0.0</td>

<td>500000</td>

<td>114207.0</td>

<td>0.059</td>

<td>1.935712e+06</td>

</tr>

<tr>

<th>4</th>

<td>Atlantic City</td>

<td>NJ</td>

<td>1942</td>

<td>39.357595</td>

<td>-74.421816</td>

<td>Federal</td>

<td>Shore Protection</td>

<td>0.0</td>

<td>1362000</td>

<td>364366.0</td>

<td>0.068</td>

<td>5.358324e+06</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [6]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Load Beach Replenishment Data</span>
<span class="c1"># Assign spreadsheet filename to `NJBPN`</span>
<span class="n">df_NJBPN</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">ExcelFile</span><span class="p">(</span><span class="s1">'NJBPN_Profiles_F17.xlsx'</span><span class="p">)</span>
<span class="c1"># Convert Excel file to dataframe</span>
<span class="n">df_NJBPN</span> <span class="o">=</span> <span class="n">df_NJBPN</span><span class="o">.</span><span class="n">parse</span><span class="p">(</span><span class="s1">'Sheet1'</span><span class="p">)</span>
<span class="c1"># Check column types</span>
<span class="n">df_NJBPN</span><span class="o">.</span><span class="n">dtypes</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[6]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>Line                 int64
Distance           float64
Z                  float64
Survey               int64
Season              object
Year                 int64
Date        datetime64[ns]
Name                object
County              object
MUN                 object
dtype: object</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [7]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Display info</span>
<span class="n">df_NJBPN</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre><class 'pandas.core.frame.DataFrame'>
RangeIndex: 284971 entries, 0 to 284970
Data columns (total 10 columns):
Line        284971 non-null int64
Distance    284971 non-null float64
Z           284971 non-null float64
Survey      284971 non-null int64
Season      284971 non-null object
Year        284971 non-null int64
Date        284971 non-null datetime64[ns]
Name        280286 non-null object
County      284971 non-null object
MUN         284971 non-null object
dtypes: datetime64[ns](1), float64(2), int64(3), object(4)
memory usage: 21.7+ MB
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [8]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Check the df</span>
<span class="n">df_NJBPN</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[8]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>Line</th>

<th>Distance</th>

<th>Z</th>

<th>Survey</th>

<th>Season</th>

<th>Year</th>

<th>Date</th>

<th>Name</th>

<th>County</th>

<th>MUN</th>

</tr>

</thead>

<tbody>

<tr>

<th>0</th>

<td>168</td>

<td>-27.9</td>

<td>21.02</td>

<td>21</td>

<td>Fall</td>

<td>2000</td>

<td>2000-01-19</td>

<td>Corlies Avenue</td>

<td>MONMOUTH</td>

<td>Allenhurst</td>

</tr>

<tr>

<th>1</th>

<td>168</td>

<td>-26.0</td>

<td>20.83</td>

<td>21</td>

<td>Fall</td>

<td>2000</td>

<td>2000-01-19</td>

<td>Corlies Avenue</td>

<td>MONMOUTH</td>

<td>Allenhurst</td>

</tr>

<tr>

<th>2</th>

<td>168</td>

<td>-25.9</td>

<td>20.49</td>

<td>21</td>

<td>Fall</td>

<td>2000</td>

<td>2000-01-19</td>

<td>Corlies Avenue</td>

<td>MONMOUTH</td>

<td>Allenhurst</td>

</tr>

<tr>

<th>3</th>

<td>168</td>

<td>-25.5</td>

<td>20.52</td>

<td>21</td>

<td>Fall</td>

<td>2000</td>

<td>2000-01-19</td>

<td>Corlies Avenue</td>

<td>MONMOUTH</td>

<td>Allenhurst</td>

</tr>

<tr>

<th>4</th>

<td>168</td>

<td>-2.3</td>

<td>20.94</td>

<td>21</td>

<td>Fall</td>

<td>2000</td>

<td>2000-01-19</td>

<td>Corlies Avenue</td>

<td>MONMOUTH</td>

<td>Allenhurst</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Load Beach Replenishment Data</span>
<span class="c1"># Assign spreadsheet filename to `NJBPN`</span>
<span class="n">df_prof_el</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">ExcelFile</span><span class="p">(</span><span class="s1">'ProfZ_per_SLdist.xls'</span><span class="p">)</span>
<span class="c1"># Convert Excel file to dataframe</span>
<span class="n">df_prof_el</span> <span class="o">=</span> <span class="n">df_prof_el</span><span class="o">.</span><span class="n">parse</span><span class="p">(</span><span class="s1">'Sheet1'</span><span class="p">)</span>
<span class="c1"># Check column types</span>
<span class="n">df_prof_el</span><span class="o">.</span><span class="n">dtypes</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [10]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Display info</span>
<span class="n">df_prof_el</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre><class 'pandas.core.frame.DataFrame'>
RangeIndex: 55 entries, 0 to 54
Columns: 113 entries, 0 to 385
dtypes: float64(112), int64(1)
memory usage: 48.6 KB
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [11]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Check the df</span>
<span class="n">df_prof_el</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[11]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>0</th>

<th>100</th>

<th>101</th>

<th>102</th>

<th>103</th>

<th>104</th>

<th>105</th>

<th>106</th>

<th>107</th>

<th>108</th>

<th>...</th>

<th>248</th>

<th>256</th>

<th>267</th>

<th>272</th>

<th>282</th>

<th>284</th>

<th>285</th>

<th>286</th>

<th>347</th>

<th>385</th>

</tr>

</thead>

<tbody>

<tr>

<th>0</th>

<td>1</td>

<td>-4.43</td>

<td>-0.02</td>

<td>-0.45</td>

<td>-4.00</td>

<td>-0.98</td>

<td>-1.250</td>

<td>-1.30</td>

<td>-1.61</td>

<td>-1.94</td>

<td>...</td>

<td>NaN</td>

<td>NaN</td>

<td>-3.17</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

</tr>

<tr>

<th>1</th>

<td>2</td>

<td>-0.50</td>

<td>0.04</td>

<td>-2.29</td>

<td>-3.91</td>

<td>-1.36</td>

<td>-1.150</td>

<td>-0.83</td>

<td>-0.16</td>

<td>-3.96</td>

<td>...</td>

<td>NaN</td>

<td>NaN</td>

<td>4.36</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

</tr>

<tr>

<th>2</th>

<td>3</td>

<td>-4.93</td>

<td>-0.80</td>

<td>-3.57</td>

<td>-3.01</td>

<td>-3.14</td>

<td>-1.140</td>

<td>-2.01</td>

<td>-2.44</td>

<td>-3.35</td>

<td>...</td>

<td>NaN</td>

<td>NaN</td>

<td>0.00</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

</tr>

<tr>

<th>3</th>

<td>4</td>

<td>-0.70</td>

<td>-0.70</td>

<td>-3.13</td>

<td>-4.00</td>

<td>-2.80</td>

<td>-2.055</td>

<td>0.35</td>

<td>-0.28</td>

<td>-0.16</td>

<td>...</td>

<td>NaN</td>

<td>NaN</td>

<td>-0.97</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

</tr>

<tr>

<th>4</th>

<td>5</td>

<td>-5.23</td>

<td>-1.31</td>

<td>-2.67</td>

<td>-1.16</td>

<td>-2.69</td>

<td>-0.420</td>

<td>0.43</td>

<td>-0.44</td>

<td>-2.29</td>

<td>...</td>

<td>NaN</td>

<td>NaN</td>

<td>-4.59</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

</tr>

</tbody>

</table>

5 rows × 113 columns

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [12]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Load Beach Replenishment Data</span>
<span class="c1"># Assign spreadsheet filename to `NJBPN`</span>
<span class="n">df_ref_lines</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">ExcelFile</span><span class="p">(</span><span class="s1">'Ref_Lines_v3.xlsx'</span><span class="p">)</span>
<span class="c1"># Convert Excel file to dataframe</span>
<span class="n">df_ref_lines</span> <span class="o">=</span> <span class="n">df_ref_lines</span><span class="o">.</span><span class="n">parse</span><span class="p">(</span><span class="s1">'DataFrame'</span><span class="p">)</span>
<span class="c1"># Check column types</span>
<span class="n">df_ref_lines</span><span class="o">.</span><span class="n">dtypes</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[12]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>X       float64
Y       float64
Line      int64
dtype: object</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [13]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Display info</span>
<span class="n">df_ref_lines</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre><class 'pandas.core.frame.DataFrame'>
Float64Index: 114 entries, 5.0 to 170.0
Data columns (total 3 columns):
X       114 non-null float64
Y       114 non-null float64
Line    114 non-null int64
dtypes: float64(2), int64(1)
memory usage: 3.6 KB
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [14]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Check the df</span>
<span class="n">df_ref_lines</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[14]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>X</th>

<th>Y</th>

<th>Line</th>

</tr>

</thead>

<tbody>

<tr>

<th>5.0</th>

<td>381279.90</td>

<td>104858.48</td>

<td>100</td>

</tr>

<tr>

<th>NaN</th>

<td>367262.69</td>

<td>72499.01</td>

<td>101</td>

</tr>

<tr>

<th>7.0</th>

<td>361392.71</td>

<td>54266.72</td>

<td>102</td>

</tr>

<tr>

<th>8.0</th>

<td>360486.95</td>

<td>46870.38</td>

<td>103</td>

</tr>

<tr>

<th>9.0</th>

<td>359579.73</td>

<td>36977.98</td>

<td>104</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

Transform/clean Data

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [15]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#remove whitespaces in column names</span>
<span class="n">df_beach</span><span class="o">.</span><span class="n">columns</span><span class="o">=</span><span class="n">df_beach</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">str</span><span class="o">.</span><span class="n">replace</span><span class="p">(</span><span class="s1">'\s+'</span><span class="p">,</span> <span class="s1">''</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [16]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#select the columns you want</span>
<span class="n">df_beach</span> <span class="o">=</span> <span class="n">df_beach</span><span class="p">[[</span><span class="s1">'BeachLocation'</span><span class="p">,</span><span class="s1">'YearCompleted'</span><span class="p">,</span><span class="s1">'Latitude'</span><span class="p">,</span><span class="s1">'Longitude'</span><span class="p">,</span><span class="s1">'Volume(CY)'</span><span class="p">,</span><span class="s1">'Costin2016'</span><span class="p">]]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [17]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#rename column names</span>
<span class="n">df_beach</span> <span class="o">=</span> <span class="n">df_beach</span><span class="o">.</span><span class="n">rename</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="p">{</span><span class="s1">'Volume(CY)'</span><span class="p">:</span> <span class="s1">'Total_CY'</span><span class="p">,</span> <span class="s1">'BeachLocation'</span><span class="p">:</span> <span class="s1">'MUN'</span><span class="p">,</span> <span class="s1">'YearCompleted'</span><span class="p">:</span> <span class="s1">'Year'</span><span class="p">})</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [18]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">df_beach</span><span class="o">.</span><span class="n">dtypes</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[18]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>MUN            object
Year            int64
Latitude      float64
Longitude     float64
Total_CY        int64
Costin2016    float64
dtype: object</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [19]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Convert column to int to convert float scientifc notation</span>
<span class="n">df_beach</span><span class="o">.</span><span class="n">Costin2016</span> <span class="o">=</span> <span class="n">df_beach</span><span class="o">.</span><span class="n">Costin2016</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [20]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#**(Might not need)Find all years beach replenishment took place and sort</span>
<span class="n">df_beach_uniqueyears</span><span class="o">=</span><span class="n">df_beach</span><span class="o">.</span><span class="n">Year</span><span class="o">.</span><span class="n">unique</span><span class="p">()</span>
<span class="n">df_beach_uniqueyears</span><span class="o">.</span><span class="n">sort</span><span class="p">()</span>
<span class="n">df_beach_uniqueyears</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[20]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>array([1936, 1937, 1938, 1940, 1942, 1943, 1945, 1947, 1948, 1949, 1950,
       1952, 1953, 1954, 1955, 1956, 1957, 1958, 1959, 1960, 1961, 1962,
       1963, 1964, 1965, 1966, 1967, 1968, 1969, 1970, 1971, 1972, 1973,
       1974, 1975, 1976, 1977, 1978, 1979, 1980, 1981, 1982, 1983, 1984,
       1985, 1986, 1987, 1988, 1989, 1990, 1991, 1992, 1993, 1994, 1995,
       1996, 1997, 1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006,
       2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015])</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [21]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Check the df</span>
<span class="n">df_NJBPN</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[21]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>Line</th>

<th>Distance</th>

<th>Z</th>

<th>Survey</th>

<th>Season</th>

<th>Year</th>

<th>Date</th>

<th>Name</th>

<th>County</th>

<th>MUN</th>

</tr>

</thead>

<tbody>

<tr>

<th>0</th>

<td>168</td>

<td>-27.9</td>

<td>21.02</td>

<td>21</td>

<td>Fall</td>

<td>2000</td>

<td>2000-01-19</td>

<td>Corlies Avenue</td>

<td>MONMOUTH</td>

<td>Allenhurst</td>

</tr>

<tr>

<th>1</th>

<td>168</td>

<td>-26.0</td>

<td>20.83</td>

<td>21</td>

<td>Fall</td>

<td>2000</td>

<td>2000-01-19</td>

<td>Corlies Avenue</td>

<td>MONMOUTH</td>

<td>Allenhurst</td>

</tr>

<tr>

<th>2</th>

<td>168</td>

<td>-25.9</td>

<td>20.49</td>

<td>21</td>

<td>Fall</td>

<td>2000</td>

<td>2000-01-19</td>

<td>Corlies Avenue</td>

<td>MONMOUTH</td>

<td>Allenhurst</td>

</tr>

<tr>

<th>3</th>

<td>168</td>

<td>-25.5</td>

<td>20.52</td>

<td>21</td>

<td>Fall</td>

<td>2000</td>

<td>2000-01-19</td>

<td>Corlies Avenue</td>

<td>MONMOUTH</td>

<td>Allenhurst</td>

</tr>

<tr>

<th>4</th>

<td>168</td>

<td>-2.3</td>

<td>20.94</td>

<td>21</td>

<td>Fall</td>

<td>2000</td>

<td>2000-01-19</td>

<td>Corlies Avenue</td>

<td>MONMOUTH</td>

<td>Allenhurst</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [22]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Select the columns you want</span>
<span class="n">df_NJBPN</span> <span class="o">=</span> <span class="n">df_NJBPN</span><span class="p">[[</span><span class="s1">'Line'</span><span class="p">,</span><span class="s1">'Survey'</span><span class="p">,</span><span class="s1">'Year'</span><span class="p">,</span><span class="s1">'MUN'</span><span class="p">]]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop duplicates, keep the first</span>
<span class="n">df_NJBPN</span> <span class="o">=</span> <span class="n">df_NJBPN</span><span class="o">.</span><span class="n">drop_duplicates</span><span class="p">(</span><span class="n">keep</span><span class="o">=</span><span class="s1">'first'</span><span class="p">)</span>
<span class="c1">#df_NJBPN</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [24]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Check the df</span>
<span class="n">df_ref_lines</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[24]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>X</th>

<th>Y</th>

<th>Line</th>

</tr>

</thead>

<tbody>

<tr>

<th>5.0</th>

<td>381279.90</td>

<td>104858.48</td>

<td>100</td>

</tr>

<tr>

<th>NaN</th>

<td>367262.69</td>

<td>72499.01</td>

<td>101</td>

</tr>

<tr>

<th>7.0</th>

<td>361392.71</td>

<td>54266.72</td>

<td>102</td>

</tr>

<tr>

<th>8.0</th>

<td>360486.95</td>

<td>46870.38</td>

<td>103</td>

</tr>

<tr>

<th>9.0</th>

<td>359579.73</td>

<td>36977.98</td>

<td>104</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Sort all values of df by column name-specify ascending order, etc</span>
<span class="n">df_ref_lines</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="p">[</span><span class="s1">'Line'</span><span class="p">],</span> <span class="n">ascending</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [26]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Merge NJBPN df with ref_lines for X & Y values based on Line-how defines which side to merge on</span>
<span class="n">df_NJBPN</span> <span class="o">=</span> <span class="n">df_NJBPN</span><span class="o">.</span><span class="n">merge</span><span class="p">(</span><span class="n">df_ref_lines</span><span class="p">,</span> <span class="n">how</span><span class="o">=</span><span class="s1">'left'</span><span class="p">,</span> <span class="n">on</span><span class="o">=</span><span class="s1">'Line'</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Sort df by column values</span>
<span class="n">df_NJBPN</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="p">[</span><span class="s1">'Line'</span><span class="p">],</span> <span class="n">ascending</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [28]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Check the df for NaNs by any row and return those rows</span>
<span class="n">df_NJBPN_NAN</span> <span class="o">=</span> <span class="n">df_NJBPN</span><span class="p">[</span><span class="n">df_NJBPN</span><span class="o">.</span><span class="n">isna</span><span class="p">()</span><span class="o">.</span><span class="n">any</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)]</span>
<span class="n">df_NJBPN_NAN</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[28]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>Line</th>

<th>Survey</th>

<th>Year</th>

<th>MUN</th>

<th>X</th>

<th>Y</th>

</tr>

</thead>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [29]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Find unique values in MUN column-this will be our merge key</span>
<span class="n">df_NJBPN_uniqueMUN</span><span class="o">=</span><span class="n">df_NJBPN</span><span class="o">.</span><span class="n">MUN</span><span class="o">.</span><span class="n">unique</span><span class="p">()</span>
<span class="n">df_NJBPN_uniqueMUN</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[29]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>array(['Allenhurst', 'Asbury Park', 'Atlantic City', 'Avalon',
       'Avon By The Sea', 'Barnegat Light', 'Bay Head', 'Beach Haven',
       'Belmar', 'Bradley Beach', 'Brick Township', 'Brigantine',
       'Cape May', 'Cape May Point', 'Cliffwood Beach', 'Deal', 'Elberon',
       'Harvey Cedars', 'Island Beach State Park', 'Lavallette',
       'Long Beach Township', 'Long Branch', 'Longport', 'Loveladies',
       'Lower Township', 'Manasquan', 'Mantoloking', 'Margate',
       'Midway Beach', 'Monmouth Beach', 'Normandy Beach',
       'North Cape May', 'North Wildwood', 'Ocean City', 'Ocean Grove',
       'Ortley Beach', 'Point Pleasant', 'Port Monmouth', 'Sandy Hook',
       'Sea Bright', 'Sea Girt', 'Sea Isle City', 'Seaside Heights',
       'Seaside Park', 'Ship Bottom', 'Spring Lake', 'Stone Harbor',
       'Strathmere', 'Surf City', 'Union Beach', 'Ventnor', 'Villas',
       'Wildwood', 'Monmouth Beach Borough', 'Middle Township'],
      dtype=object)</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [30]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># # Find unique values in MUN column-this will be our merge key</span>
<span class="n">df_beach_uniqueMUN</span><span class="o">=</span><span class="n">df_beach</span><span class="o">.</span><span class="n">MUN</span><span class="o">.</span><span class="n">unique</span><span class="p">()</span>
<span class="n">df_beach_uniqueMUN</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[30]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>array(['Atlantic City', 'Avalon', 'Avon by the Sea', 'Barnegat Light',
       'Bay Head', 'Beesleys Point', 'Belford', 'Belmar', 'Spring Lake',
       'Bradley Beach', 'Brigantine', 'Cape May', 'Cliffwood Beach',
       'Keansburg', 'Highlands', 'Highlands ', 'Island Beach State Park',
       'Island Heights', 'Laurence Harbor', 'Lavallette', 'Leonardo',
       'Long Beach Island', 'Beach Haven', 'Brant Beach', 'Harvey Cedars',
       'Holgate', 'Long Beach Township', 'Loveladies',
       'Loveladies & Harvey Cedars', 'Ship Bottom', 'Surf City',
       'Long Branch', 'Longport', 'Cape May Point', 'Lower Township',
       'Sea Isle City', 'Strathmere', 'Margate', 'Monmouth Beach',
       'North Wildwood', 'Oakwood Beach', 'Ocean City', 'Ocean City   ',
       'Ocean Gate', 'Pine Beach', 'Port Monmouth', 'Sandy Hook',
       'Asbury Park', 'Manasquan', 'Sea Bright', 'Sea Girt',
       'Seaside Heights', 'Seaside Park', 'Shark River Inlet',
       'South Amboy', 'Stone Harbor', 'Union Beach', 'Ventnor',
       'Wildwood'], dtype=object)</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [31]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Find min year in NJBPN df to define range</span>
<span class="n">df_NJBPN_yearsmin</span><span class="o">=</span><span class="n">df_NJBPN</span><span class="o">.</span><span class="n">Year</span><span class="o">.</span><span class="n">min</span><span class="p">()</span>
<span class="n">df_NJBPN_yearsmin</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[31]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>1986</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [32]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Find max year in NJBPN df to define range</span>
<span class="n">df_NJBPN_yearsmax</span><span class="o">=</span><span class="n">df_NJBPN</span><span class="o">.</span><span class="n">Year</span><span class="o">.</span><span class="n">max</span><span class="p">()</span>
<span class="n">df_NJBPN_yearsmax</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[32]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>2017</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [33]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Find min year in beach df to define range</span>
<span class="n">df_beach_yearsmin</span><span class="o">=</span><span class="n">df_beach</span><span class="o">.</span><span class="n">Year</span><span class="o">.</span><span class="n">min</span><span class="p">()</span>
<span class="n">df_beach_yearsmin</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[33]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>1936</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [34]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Find max year in beach df to define range</span>
<span class="n">df_beach_yearsmax</span><span class="o">=</span><span class="n">df_beach</span><span class="o">.</span><span class="n">Year</span><span class="o">.</span><span class="n">max</span><span class="p">()</span>
<span class="n">df_beach_yearsmax</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[34]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>2015</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Find all beach values between 1986-2017</span>
<span class="n">df_beach_ryr</span> <span class="o">=</span> <span class="n">df_beach</span><span class="p">[(</span><span class="n">df_beach</span><span class="p">[</span><span class="s1">'Year'</span><span class="p">]</span> <span class="o">>=</span> <span class="mi">1986</span><span class="p">)</span> <span class="o">&</span> <span class="p">(</span><span class="n">df_beach</span><span class="p">[</span><span class="s1">'Year'</span><span class="p">]</span> <span class="o"><=</span> <span class="mi">2017</span><span class="p">)]</span>
<span class="n">df_beach_ryr</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Merge beach df with NJBPN for Line # and survey locations-how defines which side to merge on, indicator defines a column to identify where the data merged from</span>
<span class="n">df_beach_ryr_merge</span> <span class="o">=</span> <span class="n">df_beach_ryr</span><span class="o">.</span><span class="n">merge</span><span class="p">(</span><span class="n">df_NJBPN</span><span class="p">,</span> <span class="n">how</span><span class="o">=</span><span class="s1">'left'</span><span class="p">,</span> <span class="n">on</span><span class="o">=</span><span class="p">[</span><span class="s1">'Year'</span><span class="p">,</span><span class="s1">'MUN'</span><span class="p">])</span>
<span class="n">df_beach_ryr_merge</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Remove any replenishments that have a zero either in CY or Cost</span>
<span class="n">df_beach_ryr_merge1</span> <span class="o">=</span> <span class="n">df_beach_ryr_merge</span><span class="p">[(</span><span class="n">df_beach_ryr_merge</span> <span class="o">!=</span> <span class="mi">0</span><span class="p">)</span><span class="o">.</span><span class="n">all</span><span class="p">(</span><span class="mi">1</span><span class="p">)]</span>
<span class="n">df_beach_ryr_merge1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [86]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Check the df for NaNs by any row and return those rows</span>
<span class="n">df_beach_ryr_merge1_NAN</span> <span class="o">=</span> <span class="n">df_beach_ryr_merge1</span><span class="p">[</span><span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">isna</span><span class="p">()</span><span class="o">.</span><span class="n">any</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)]</span>
<span class="n">df_beach_ryr_merge1_NAN</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[86]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>MUN</th>

<th>Year</th>

<th>Latitude</th>

<th>Longitude</th>

<th>Total_CY</th>

<th>Costin2016</th>

<th>Line</th>

<th>Survey</th>

<th>X</th>

<th>Y</th>

</tr>

</thead>

<tbody>

<tr>

<th>419</th>

<td>Oakwood Beach</td>

<td>2014</td>

<td>39.556105</td>

<td>-75.518577</td>

<td>354000</td>

<td>12676056</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

<td>NaN</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Replace column values by index</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">303</span><span class="p">,</span> <span class="s2">"Line"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">185</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">303</span><span class="p">,</span> <span class="s2">"Survey"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">48</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">303</span><span class="p">,</span> <span class="s2">"X"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">605278.02</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">303</span><span class="p">,</span> <span class="s2">"Y"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">585173.15</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">303</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Replace column values by index</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">567</span><span class="p">,</span> <span class="s2">"Line"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">124</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">567</span><span class="p">,</span> <span class="s2">"Survey"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">14</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">567</span><span class="p">,</span> <span class="s2">"X"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">466537.01</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">567</span><span class="p">,</span> <span class="s2">"Y"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">157510.59</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">567</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Replace column values by index</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">309</span><span class="p">,</span> <span class="s2">"Line"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">139</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">309</span><span class="p">,</span> <span class="s2">"Survey"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">44</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">309</span><span class="p">,</span> <span class="s2">"X"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">575784.35</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">309</span><span class="p">,</span> <span class="s2">"Y"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">282576.61</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">309</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Replace column values by index</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">310</span><span class="p">,</span> <span class="s2">"Line"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">139</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">310</span><span class="p">,</span> <span class="s2">"Survey"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">48</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">310</span><span class="p">,</span> <span class="s2">"X"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">575784.35</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">310</span><span class="p">,</span> <span class="s2">"Y"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">282576.61</span>
<span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">310</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [71]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Insert a new indexed row in beach df</span>
<span class="k">def</span> <span class="nf">insert_row</span><span class="p">(</span><span class="n">idx</span><span class="p">,</span> <span class="n">df_beach_ryr_merge1</span><span class="p">,</span> <span class="n">df_beach_ryr_merge1_insert</span><span class="p">):</span>
    <span class="k">return</span> <span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">iloc</span><span class="p">[:</span><span class="n">idx</span><span class="p">,</span> <span class="p">]</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">df_beach_ryr_merge1_insert</span><span class="p">)</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="n">idx</span><span class="p">:,</span> <span class="p">])</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span> <span class="o">=</span> <span class="kc">True</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [72]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Create the new df to be concatinated to the beach df-define values first then columns</span>
<span class="n">df_beach_ryr_merge2</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">([[</span><span class="s1">'Keansburg'</span><span class="p">,</span><span class="mi">2014</span><span class="p">,</span><span class="mf">40.449103</span><span class="p">,</span><span class="o">-</span><span class="mf">74.121923</span><span class="p">,</span><span class="mi">875000</span><span class="p">,</span><span class="mi">37122736</span><span class="p">,</span><span class="mi">185</span><span class="p">,</span><span class="mi">49</span><span class="p">,</span><span class="mf">605278.02</span><span class="p">,</span><span class="mf">585173.15</span><span class="p">]],</span><span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">,</span><span class="s1">'Year'</span><span class="p">,</span><span class="s1">'Latitude'</span><span class="p">,</span><span class="s1">'Longitude'</span><span class="p">,</span><span class="s1">'Total_CY'</span><span class="p">,</span><span class="s1">'Costin2016'</span><span class="p">,</span><span class="s1">'Line'</span><span class="p">,</span><span class="s1">'Survey'</span><span class="p">,</span><span class="s1">'X'</span><span class="p">,</span><span class="s1">'Y'</span><span class="p">])</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Create new df by concatinating df</span>
<span class="n">df_beach_ryr_merge1</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">df_beach_ryr_merge2</span><span class="p">,</span><span class="n">df_beach_ryr_merge1</span><span class="p">])</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">df_beach_ryr_merge1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [88]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Insert a new indexed row in beach df</span>
<span class="k">def</span> <span class="nf">insert_row</span><span class="p">(</span><span class="n">idx</span><span class="p">,</span> <span class="n">df_beach_ryr_merge1</span><span class="p">,</span> <span class="n">df_beach_ryr_merge1_insert</span><span class="p">):</span>
    <span class="k">return</span> <span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">iloc</span><span class="p">[:</span><span class="n">idx</span><span class="p">,</span> <span class="p">]</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">df_beach_ryr_merge1_insert</span><span class="p">)</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="n">idx</span><span class="p">:,</span> <span class="p">])</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span> <span class="o">=</span> <span class="kc">True</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [89]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Create the new df to be concatinated to the beach df-define values first then columns</span>
<span class="n">df_beach_ryr_merge3</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">([[</span><span class="s1">'Ocean City'</span><span class="p">,</span><span class="mi">1997</span><span class="p">,</span><span class="mf">39.264158</span><span class="p">,</span><span class="o">-</span><span class="mf">74.589958</span><span class="p">,</span><span class="mi">800000</span><span class="p">,</span><span class="mi">7315088</span><span class="p">,</span><span class="mi">124</span><span class="p">,</span><span class="mi">15</span><span class="p">,</span><span class="mf">466537.01</span><span class="p">,</span><span class="mf">157510.59</span><span class="p">]],</span><span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">,</span><span class="s1">'Year'</span><span class="p">,</span><span class="s1">'Latitude'</span><span class="p">,</span><span class="s1">'Longitude'</span><span class="p">,</span><span class="s1">'Total_CY'</span><span class="p">,</span><span class="s1">'Costin2016'</span><span class="p">,</span><span class="s1">'Line'</span><span class="p">,</span><span class="s1">'Survey'</span><span class="p">,</span><span class="s1">'X'</span><span class="p">,</span><span class="s1">'Y'</span><span class="p">])</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Create new df by concatinating df</span>
<span class="n">df_beach_ryr_merge1</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">df_beach_ryr_merge3</span><span class="p">,</span><span class="n">df_beach_ryr_merge1</span><span class="p">])</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">df_beach_ryr_merge1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [91]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Insert a new indexed row in beach df</span>
<span class="k">def</span> <span class="nf">insert_row</span><span class="p">(</span><span class="n">idx</span><span class="p">,</span> <span class="n">df_beach_ryr_merge1</span><span class="p">,</span> <span class="n">df_beach_ryr_merge1_insert</span><span class="p">):</span>
    <span class="k">return</span> <span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">iloc</span><span class="p">[:</span><span class="n">idx</span><span class="p">,</span> <span class="p">]</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">df_beach_ryr_merge1_insert</span><span class="p">)</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="n">idx</span><span class="p">:,</span> <span class="p">])</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span> <span class="o">=</span> <span class="kc">True</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [92]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Create the new df to be concatinated to the beach df-define values first then columns</span>
<span class="n">df_beach_ryr_merge4</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">([[</span><span class="s1">'Brant Beach'</span><span class="p">,</span><span class="mi">2012</span><span class="p">,</span><span class="mf">39.620367</span><span class="p">,</span><span class="o">-</span><span class="mf">74.194772</span><span class="p">,</span><span class="mi">1250000</span><span class="p">,</span><span class="mi">17323651</span><span class="p">,</span><span class="mi">139</span><span class="p">,</span><span class="mi">45</span><span class="p">,</span><span class="mf">575784.35</span><span class="p">,</span><span class="mf">282576.61</span><span class="p">]],</span><span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">,</span><span class="s1">'Year'</span><span class="p">,</span><span class="s1">'Latitude'</span><span class="p">,</span><span class="s1">'Longitude'</span><span class="p">,</span><span class="s1">'Total_CY'</span><span class="p">,</span><span class="s1">'Costin2016'</span><span class="p">,</span><span class="s1">'Line'</span><span class="p">,</span><span class="s1">'Survey'</span><span class="p">,</span><span class="s1">'X'</span><span class="p">,</span><span class="s1">'Y'</span><span class="p">])</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Create new df by concatinating df</span>
<span class="n">df_beach_ryr_merge1</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">df_beach_ryr_merge4</span><span class="p">,</span><span class="n">df_beach_ryr_merge1</span><span class="p">])</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">df_beach_ryr_merge1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [94]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Insert a new indexed row in beach df</span>
<span class="k">def</span> <span class="nf">insert_row</span><span class="p">(</span><span class="n">idx</span><span class="p">,</span> <span class="n">df_beach_ryr_merge1</span><span class="p">,</span> <span class="n">df_beach_ryr_merge1_insert</span><span class="p">):</span>
    <span class="k">return</span> <span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">iloc</span><span class="p">[:</span><span class="n">idx</span><span class="p">,</span> <span class="p">]</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">df_beach_ryr_merge1_insert</span><span class="p">)</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="n">idx</span><span class="p">:,</span> <span class="p">])</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span> <span class="o">=</span> <span class="kc">True</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [95]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Create the new df to be concatinated to the beach df-define values first then columns</span>
<span class="n">df_beach_ryr_merge5</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">([[</span><span class="s1">'Brant Beach'</span><span class="p">,</span><span class="mi">2014</span><span class="p">,</span><span class="mf">39.620367</span><span class="p">,</span><span class="o">-</span><span class="mf">74.194772</span><span class="p">,</span><span class="mi">1060000</span><span class="p">,</span><span class="mi">10959764</span><span class="p">,</span><span class="mi">139</span><span class="p">,</span><span class="mi">49</span><span class="p">,</span><span class="mf">575784.35</span><span class="p">,</span><span class="mf">282576.61</span><span class="p">]],</span><span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">,</span><span class="s1">'Year'</span><span class="p">,</span><span class="s1">'Latitude'</span><span class="p">,</span><span class="s1">'Longitude'</span><span class="p">,</span><span class="s1">'Total_CY'</span><span class="p">,</span><span class="s1">'Costin2016'</span><span class="p">,</span><span class="s1">'Line'</span><span class="p">,</span><span class="s1">'Survey'</span><span class="p">,</span><span class="s1">'X'</span><span class="p">,</span><span class="s1">'Y'</span><span class="p">])</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Create new df by concatinating df</span>
<span class="n">df_beach_ryr_merge1</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">df_beach_ryr_merge5</span><span class="p">,</span><span class="n">df_beach_ryr_merge1</span><span class="p">])</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">df_beach_ryr_merge1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [102]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Check the df for NaNs by any row and return those rows</span>
<span class="n">df_beach_ryr_merge1_NAN</span> <span class="o">=</span> <span class="n">df_beach_ryr_merge1</span><span class="p">[</span><span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">isna</span><span class="p">()</span><span class="o">.</span><span class="n">any</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)]</span>
<span class="n">df_beach_ryr_merge1_NAN</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[102]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>MUN</th>

<th>Year</th>

<th>Latitude</th>

<th>Longitude</th>

<th>Total_CY</th>

<th>Costin2016</th>

<th>Line</th>

<th>Survey</th>

<th>X</th>

<th>Y</th>

</tr>

</thead>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Remove Oakwood Beach by drop index value</span>
<span class="n">df_beach_ryr_merge1</span> <span class="o">=</span> <span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">331</span><span class="p">])</span>
<span class="n">df_beach_ryr_merge1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Set index of 0 column then transpose columns & rows and relabel column as Line</span>
<span class="n">df_prof_el_reindexed</span> <span class="o">=</span> <span class="n">df_prof_el</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span><span class="o">.</span><span class="n">T</span><span class="o">.</span><span class="n">rename_axis</span><span class="p">(</span><span class="kc">None</span><span class="p">,</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">rename_axis</span><span class="p">(</span><span class="s1">'Line'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
<span class="c1"># Set index of Line column then stack and reset index</span>
<span class="n">df_prof_el_stacked</span> <span class="o">=</span> <span class="n">df_prof_el_reindexed</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'Line'</span><span class="p">)</span><span class="o">.</span><span class="n">stack</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
<span class="c1"># Rename new column names to Survey and Z</span>
<span class="n">df_prof_el_stacked</span> <span class="o">=</span><span class="n">df_prof_el_stacked</span><span class="o">.</span><span class="n">rename</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="p">{</span><span class="s1">'level_1'</span><span class="p">:</span><span class="s1">'Survey'</span><span class="p">,</span> <span class="mi">0</span><span class="p">:</span><span class="s1">'Z'</span><span class="p">})</span>
<span class="n">df_prof_el_stacked</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Merge beach df with NJBPN for Line # and survey locations-how defines which side to merge on, indicator defines a column to identify where the data merged from</span>
<span class="n">df_beach_el_merge</span> <span class="o">=</span> <span class="n">df_beach_ryr_merge1</span><span class="o">.</span><span class="n">merge</span><span class="p">(</span><span class="n">df_prof_el_stacked</span><span class="p">,</span> <span class="n">how</span><span class="o">=</span><span class="s1">'left'</span><span class="p">,</span> <span class="n">on</span><span class="o">=</span><span class="p">[</span><span class="s1">'Line'</span><span class="p">,</span><span class="s1">'Survey'</span><span class="p">])</span>
<span class="n">df_beach_el_merge</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Sort values</span>
<span class="n">df_beach_el_merge</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="p">[</span><span class="s1">'Line'</span><span class="p">],</span> <span class="n">ascending</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [108]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Check the df for NaNs by any row and return those rows</span>
<span class="n">df_beach_el_merge_NAN</span> <span class="o">=</span> <span class="n">df_beach_el_merge</span><span class="p">[</span><span class="n">df_beach_el_merge</span><span class="o">.</span><span class="n">isna</span><span class="p">()</span><span class="o">.</span><span class="n">any</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)]</span>
<span class="n">df_beach_el_merge_NAN</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[108]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>MUN</th>

<th>Year</th>

<th>Latitude</th>

<th>Longitude</th>

<th>Total_CY</th>

<th>Costin2016</th>

<th>Line</th>

<th>Survey</th>

<th>X</th>

<th>Y</th>

<th>Z</th>

</tr>

</thead>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Groupby columns values and return mean of Z</span>
<span class="n">df_beach_el_merge1</span> <span class="o">=</span> <span class="n">df_beach_el_merge</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'MUN'</span><span class="p">,</span><span class="s1">'Year'</span><span class="p">,</span><span class="s1">'Line'</span><span class="p">])[</span><span class="s1">'Z'</span><span class="p">]</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
<span class="n">df_beach_el_merge1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Merge beach df with NJBPN for Line # and survey locations-how defines which side to merge on, indicator defines a column to identify where the data merged from</span>
<span class="n">df_beach_el_merge_final</span> <span class="o">=</span> <span class="n">df_beach_el_merge1</span><span class="o">.</span><span class="n">merge</span><span class="p">(</span><span class="n">df_beach_el_merge</span><span class="p">,</span> <span class="n">how</span><span class="o">=</span><span class="s1">'left'</span><span class="p">,</span> <span class="n">on</span><span class="o">=</span><span class="p">[</span><span class="s1">'Line'</span><span class="p">,</span><span class="s1">'Year'</span><span class="p">])</span>
<span class="n">df_beach_el_merge_final</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Select the columns you want</span>
<span class="n">df_beach_el_merge_final1</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final</span><span class="p">[[</span><span class="s1">'MUN_x'</span><span class="p">,</span><span class="s1">'Year'</span><span class="p">,</span><span class="s1">'Line'</span><span class="p">,</span><span class="s1">'Latitude'</span><span class="p">,</span><span class="s1">'Longitude'</span><span class="p">,</span><span class="s1">'X'</span><span class="p">,</span><span class="s1">'Y'</span><span class="p">,</span><span class="s1">'Total_CY'</span><span class="p">,</span><span class="s1">'Costin2016'</span><span class="p">,</span><span class="s1">'Z_x'</span><span class="p">]]</span>
<span class="n">df_beach_el_merge_final1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#rename column names</span>
<span class="n">df_beach_el_merge_final1</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final1</span><span class="o">.</span><span class="n">rename</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="p">{</span><span class="s1">'MUN_x'</span><span class="p">:</span> <span class="s1">'MUN'</span><span class="p">,</span> <span class="s1">'Z_x'</span><span class="p">:</span> <span class="s1">'Z'</span><span class="p">})</span>
<span class="n">df_beach_el_merge_final1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop duplicates, keep the first</span>
<span class="n">df_beach_el_merge_final2</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final1</span><span class="o">.</span><span class="n">drop_duplicates</span><span class="p">(</span><span class="n">keep</span><span class="o">=</span><span class="s1">'first'</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final2</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [124]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Convert X, Y to Lat Long-find nearest to current Lat Long & drop lines at same location</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Convert x,y to Lat, Long</span>
<span class="kn">from</span> <span class="nn">pyproj</span> <span class="k">import</span> <span class="n">Proj</span><span class="p">,</span> <span class="n">transform</span>

<span class="c1"># EPSG Projection 3424 - NAD83 / New Jersey (ft US)</span>
<span class="n">inProj</span> <span class="o">=</span> <span class="n">Proj</span><span class="p">(</span><span class="n">init</span><span class="o">=</span><span class="s1">'epsg:3424'</span><span class="p">,</span> <span class="n">preserve_units</span> <span class="o">=</span> <span class="kc">True</span><span class="p">)</span>
<span class="c1"># EPSG Projection 4326 - WGS 84</span>
<span class="n">outProj</span> <span class="o">=</span> <span class="n">Proj</span><span class="p">(</span><span class="n">init</span><span class="o">=</span><span class="s1">'epsg:4326'</span><span class="p">)</span>
<span class="c1"># Specify the df columns to output(create new columns) run through each row and convert then apply</span>
<span class="n">df_beach_el_merge_final2</span><span class="p">[[</span><span class="s1">'Longitude_cy'</span><span class="p">,</span><span class="s1">'Latitude_cx'</span><span class="p">]]</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final2</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">row</span><span class="p">:</span><span class="n">transform</span><span class="p">(</span><span class="n">inProj</span><span class="p">,</span> <span class="n">outProj</span><span class="p">,</span> <span class="n">row</span><span class="p">[</span><span class="s1">'X'</span><span class="p">],</span> <span class="n">row</span><span class="p">[</span><span class="s1">'Y'</span><span class="p">]),</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final2</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [201]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Write df to Excel file</span>
<span class="n">writer</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">ExcelWriter</span><span class="p">(</span><span class="s1">'df_beach_el_merge_final2.xlsx'</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final2</span><span class="o">.</span><span class="n">to_excel</span><span class="p">(</span><span class="n">writer</span><span class="p">,</span> <span class="s1">'DataFrame'</span><span class="p">)</span>
<span class="n">writer</span><span class="o">.</span><span class="n">save</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Select columns to new df</span>
<span class="n">df_beach_coord</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[[</span><span class="s1">'MUN'</span><span class="p">,</span> <span class="s1">'Line'</span><span class="p">,</span> <span class="s1">'Latitude'</span><span class="p">,</span> <span class="s1">'Longitude'</span><span class="p">,</span> <span class="s1">'Latitude_cx'</span><span class="p">,</span> <span class="s1">'Longitude_cy'</span><span class="p">]]</span>
<span class="n">df_beach_coord</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop duplicates, keep the first</span>
<span class="n">df_beach_coord</span> <span class="o">=</span> <span class="n">df_beach_coord</span><span class="o">.</span><span class="n">drop_duplicates</span><span class="p">(</span><span class="n">keep</span><span class="o">=</span><span class="s1">'first'</span><span class="p">)</span>
<span class="n">df_beach_coord</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Find just a row based on value you select-loc is used for labels, iloc for integer</span>
<span class="n">df_beach_el_merge_final2</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final2</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Avalon"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Create copy of df</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final2</span>
<span class="c1"># Replace column values by index location</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">48</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">8.100</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">56</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">5.320</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">68</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">5.035</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">68</span><span class="p">,</span> <span class="s2">"Total_CY"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">75000</span><span class="o">+</span><span class="mi">46359</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">68</span><span class="p">,</span> <span class="s2">"Costin2016"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">2198919</span><span class="o">+</span><span class="mi">428409</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">70</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">5.035</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">5.720</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">4</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">4.383</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">16</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">9.450</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">22</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">5.7875</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">28</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">6.2000</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">198</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">11.3500</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">211</span><span class="p">,</span> <span class="s2">"Line"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">106</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">211</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">38.929502</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">211</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.924212</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">219</span><span class="p">,</span> <span class="s2">"Line"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">106</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">219</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">38.929502</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">219</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.924212</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">243</span><span class="p">,</span> <span class="s2">"Line"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">106</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">243</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">38.929502</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">243</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.924212</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">251</span><span class="p">,</span> <span class="s2">"Line"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">106</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">251</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">38.929502</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">251</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.924212</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">259</span><span class="p">,</span> <span class="s2">"Line"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">106</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">259</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">38.929502</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">259</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.924212</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">233</span><span class="p">,</span> <span class="s2">"Line"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">106</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">233</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">38.929502</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">233</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.924212</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">233</span><span class="p">,</span> <span class="s2">"Total_CY"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">375000</span><span class="o">+</span><span class="mi">425000</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">233</span><span class="p">,</span> <span class="s2">"Costin2016"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">4578246</span><span class="o">+</span><span class="mi">3745837</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">235</span><span class="p">,</span> <span class="s2">"Line"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">106</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">235</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">38.929502</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">235</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.924212</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">453</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">40.439500</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">453</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.093714</span>
<span class="n">df_beach_el_merge_final3</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Remove rows based on column value</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">129</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">206</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">216</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">267</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">230</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">108</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">114</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">115</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">137</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">131</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">132</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">134</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">105</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">107</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">142</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">173</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">174</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">176</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">177</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">272</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">109</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">256</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">111</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">122</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">123</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">125</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">225</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">223</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">221</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">222</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">181</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">182</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">282</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">117</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">119</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">120</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">161</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">Line</span> <span class="o">!=</span> <span class="mi">212</span><span class="p">]</span>
<span class="n">df_beach_el_merge_final3</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Set index to MUN column</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
<span class="n">df_beach_el_merge_final3</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Find just a row based on value you select-loc is used for labels, iloc for integer</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Cape May"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Remove by index # 14, 41</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">14</span><span class="p">])</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">41</span><span class="p">])</span>
<span class="n">df_beach_el_merge_final3</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Select columns we want</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="p">[[</span><span class="s1">'MUN'</span><span class="p">,</span><span class="s1">'Year'</span><span class="p">,</span><span class="s1">'Line'</span><span class="p">,</span><span class="s1">'Latitude'</span><span class="p">,</span><span class="s1">'Longitude'</span><span class="p">,</span><span class="s1">'Total_CY'</span><span class="p">,</span><span class="s1">'Costin2016'</span><span class="p">,</span><span class="s1">'Z'</span><span class="p">]]</span>
<span class="n">df_beach_el_merge_final3</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [386]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#**(Might not need)Find all years beach replenishment took place and sort</span>
<span class="n">df_beach_el_merge_final3_uniqueMUN</span><span class="o">=</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">MUN</span><span class="o">.</span><span class="n">unique</span><span class="p">()</span>
<span class="n">df_beach_el_merge_final3_uniqueMUN</span><span class="o">.</span><span class="n">sort</span><span class="p">()</span>
<span class="n">df_beach_el_merge_final3_uniqueMUN</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[386]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>array(['Asbury Park', 'Atlantic City', 'Avalon', 'Barnegat Light',
       'Beach Haven', 'Brant Beach', 'Brigantine', 'Cape May',
       'Cape May Point', 'Harvey Cedars', 'Keansburg', 'Long Branch',
       'Longport', 'Lower Township', 'Manasquan', 'Monmouth Beach',
       'Ocean City', 'Ocean City   ', 'Port Monmouth', 'Sandy Hook',
       'Sea Bright', 'Sea Isle City', 'Spring Lake', 'Stone Harbor',
       'Strathmere', 'Surf City', 'Ventnor', 'Wildwood'], dtype=object)</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [387]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Go through each unique MUN to check for final errors</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Avalon"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[387]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

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

<th>7</th>

<td>Avalon</td>

<td>1987</td>

<td>116</td>

<td>39.100226</td>

<td>-74.710550</td>

<td>1305000</td>

<td>6037689</td>

<td>-0.570</td>

</tr>

<tr>

<th>8</th>

<td>Avalon</td>

<td>1990</td>

<td>116</td>

<td>39.100226</td>

<td>-74.710550</td>

<td>404000</td>

<td>1050788</td>

<td>4.250</td>

</tr>

<tr>

<th>9</th>

<td>Avalon</td>

<td>1992</td>

<td>116</td>

<td>39.100226</td>

<td>-74.710550</td>

<td>410000</td>

<td>2020408</td>

<td>-4.590</td>

</tr>

<tr>

<th>10</th>

<td>Avalon</td>

<td>1993</td>

<td>116</td>

<td>39.100226</td>

<td>-74.710550</td>

<td>239000</td>

<td>2932661</td>

<td>-3.650</td>

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

<td>-8.100</td>

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

<td>-5.320</td>

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

<td>-5.035</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Updates column values based on index</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">7</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">39.098428</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">7</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.711459</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">8</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">39.098428</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">8</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.711459</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">9</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">39.098428</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">9</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.711459</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">10</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">39.098428</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">10</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.711459</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [389]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Verify updates to Lat Long</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Avalon"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[389]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

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

<th>7</th>

<td>Avalon</td>

<td>1987</td>

<td>116</td>

<td>39.098428</td>

<td>-74.711459</td>

<td>1305000</td>

<td>6037689</td>

<td>-0.570</td>

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

<td>4.250</td>

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

<td>-4.590</td>

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

<td>-3.650</td>

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

<td>-8.100</td>

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

<td>-5.320</td>

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

<td>-5.035</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [390]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Go through each unique MUN to check for final errors</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Brigantine"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[390]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

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

<th>19</th>

<td>Brigantine</td>

<td>1997</td>

<td>133</td>

<td>39.405826</td>

<td>-74.362421</td>

<td>1200000</td>

<td>8875739</td>

<td>-6.090</td>

</tr>

<tr>

<th>20</th>

<td>Brigantine</td>

<td>1999</td>

<td>133</td>

<td>39.405826</td>

<td>-74.362421</td>

<td>999827</td>

<td>7110157</td>

<td>-3.175</td>

</tr>

<tr>

<th>21</th>

<td>Brigantine</td>

<td>2006</td>

<td>133</td>

<td>39.405826</td>

<td>-74.362421</td>

<td>672000</td>

<td>17709563</td>

<td>-6.335</td>

</tr>

<tr>

<th>22</th>

<td>Brigantine</td>

<td>2011</td>

<td>133</td>

<td>39.405826</td>

<td>-74.362421</td>

<td>175000</td>

<td>3132780</td>

<td>-7.005</td>

</tr>

<tr>

<th>23</th>

<td>Brigantine</td>

<td>2013</td>

<td>133</td>

<td>39.405826</td>

<td>-74.362421</td>

<td>667000</td>

<td>4601226</td>

<td>-7.255</td>

</tr>

<tr>

<th>24</th>

<td>Brigantine</td>

<td>2013</td>

<td>133</td>

<td>39.405826</td>

<td>-74.362421</td>

<td>90000</td>

<td>1408538</td>

<td>-7.255</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Updates column values based on index</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">23</span><span class="p">,</span> <span class="s2">"Total_CY"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">667000</span><span class="o">+</span><span class="mi">90000</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">23</span><span class="p">,</span> <span class="s2">"Costin2016"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">4601226</span><span class="o">+</span><span class="mi">1408538</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Set index on MUN</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
<span class="n">df_beach_el_merge_final3</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [393]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">23</span><span class="p">])</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Go through each unique MUN to check for final errors</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Cape May"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [395]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Updates column values based on index</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">27</span><span class="p">,</span> <span class="s2">"Total_CY"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">200000</span><span class="o">+</span><span class="mi">42000</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">27</span><span class="p">,</span> <span class="s2">"Costin2016"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">445416</span><span class="o">+</span><span class="mi">318877</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">29</span><span class="p">,</span> <span class="s2">"Total_CY"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">300000</span><span class="o">+</span><span class="mi">415000</span><span class="o">+</span><span class="mi">300000</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">29</span><span class="p">,</span> <span class="s2">"Costin2016"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">3523102</span><span class="o">+</span><span class="mi">3960396</span><span class="o">+</span><span class="mi">3630363</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">34</span><span class="p">,</span> <span class="s2">"Total_CY"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">2372000</span><span class="o">+</span><span class="mi">400000</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">34</span><span class="p">,</span> <span class="s2">"Costin2016"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">105251788</span><span class="o">+</span><span class="mi">4864091</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">39</span><span class="p">,</span> <span class="s2">"Total_CY"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">800000</span><span class="o">+</span><span class="mi">425000</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">39</span><span class="p">,</span> <span class="s2">"Costin2016"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">8324083</span><span class="o">+</span><span class="mi">3745837</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [397]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Set index on MUN</span>
<span class="n">df_beach_el_merge_final3</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Go through each unique MUN to check for final errors</span>
<span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final3</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Cape May"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [399]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final3</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">27</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Go through each unique MUN to check for final errors</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final4</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Cape May"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [404]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">27</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">28</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">28</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [406]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">31</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [408]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">35</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Go through each unique MUN to check for final errors</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final4</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Cape May"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [410]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Updates column values based on index</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">25</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">38.929502</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">25</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.924212</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">28</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">38.929502</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">28</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.924212</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">29</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">38.929502</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">29</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.924212</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">31</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">38.929502</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">31</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">74.924212</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Go through each unique MUN to check for final errors</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final4</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Ocean City"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [412]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Updates column values based on index</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">56</span><span class="p">,</span> <span class="s2">"Total_CY"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">2727000</span><span class="o">+</span><span class="mi">846000</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">56</span><span class="p">,</span> <span class="s2">"Costin2016"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">24046054</span><span class="o">+</span><span class="mi">4810447</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">59</span><span class="p">,</span> <span class="s2">"Total_CY"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">1411000</span><span class="o">+</span><span class="mi">360000</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">59</span><span class="p">,</span> <span class="s2">"Costin2016"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">8970009</span><span class="o">+</span><span class="mi">1922889</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">65</span><span class="p">,</span> <span class="s2">"Total_CY"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">1000000</span><span class="o">+</span><span class="mi">746200</span><span class="o">+</span><span class="mi">90000</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">65</span><span class="p">,</span> <span class="s2">"Costin2016"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">12262781</span><span class="o">+</span><span class="mi">5590695</span><span class="o">+</span><span class="mi">1124744</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [414]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">57</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [416]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">59</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [418]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">64</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [420]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">64</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [432]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Go through each unique MUN to check for final errors</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final4</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Ocean City   "</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[432]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

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

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [428]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Updates column values based on index</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">59</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">6.17</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [431]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">64</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [448]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Go through each unique MUN to check for final errors</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final4</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Sea Bright"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[448]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

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

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [438]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Updates column values based on index</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">68</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">10.715</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">69</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">10.9975</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [442]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">69</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [446]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Updates column values based on index</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">68</span><span class="p">,</span> <span class="s2">"Z"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">10.9975</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">67</span><span class="p">,</span> <span class="s2">"Line"</span><span class="p">]</span> <span class="o">=</span> <span class="mi">180</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">67</span><span class="p">,</span> <span class="s2">"Latitude"</span><span class="p">]</span> <span class="o">=</span> <span class="mf">40.346152</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">67</span><span class="p">,</span> <span class="s2">"Longitude"</span><span class="p">]</span> <span class="o">=</span> <span class="o">-</span><span class="mf">73.973207</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [453]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Go through each unique MUN to check for final errors</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final4</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Sea Isle City"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[453]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

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

<th>69</th>

<td>Sea Isle City</td>

<td>1987</td>

<td>118</td>

<td>39.141178</td>

<td>-74.69975</td>

<td>158000</td>

<td>1109756</td>

<td>0.900</td>

</tr>

<tr>

<th>70</th>

<td>Sea Isle City</td>

<td>2009</td>

<td>118</td>

<td>39.141178</td>

<td>-74.69975</td>

<td>394797</td>

<td>4011064</td>

<td>-4.035</td>

</tr>

<tr>

<th>71</th>

<td>Sea Isle City</td>

<td>2010</td>

<td>118</td>

<td>39.141178</td>

<td>-74.69975</td>

<td>700000</td>

<td>6550218</td>

<td>-6.645</td>

</tr>

<tr>

<th>72</th>

<td>Sea Isle City</td>

<td>2012</td>

<td>118</td>

<td>39.141178</td>

<td>-74.69975</td>

<td>394797</td>

<td>5186721</td>

<td>-5.900</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [450]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Updates column values based on index</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">70</span><span class="p">,</span> <span class="s2">"Total_CY"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">216630</span><span class="o">+</span><span class="mi">178167</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">70</span><span class="p">,</span> <span class="s2">"Costin2016"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">2206086</span><span class="o">+</span><span class="mi">1804978</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [452]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">71</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [459]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Go through each unique MUN to check for final errors</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final4</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Stone Harbor"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[459]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

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

<th>74</th>

<td>Stone Harbor</td>

<td>2009</td>

<td>113</td>

<td>39.050752</td>

<td>-74.756134</td>

<td>319670</td>

<td>1664816</td>

<td>-6.265</td>

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

<td>-7.170</td>

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

<td>-7.555</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [456]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Updates column values based on index</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">76</span><span class="p">,</span> <span class="s2">"Total_CY"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">265000</span><span class="o">+</span><span class="mi">100000</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">76</span><span class="p">,</span> <span class="s2">"Costin2016"</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">3191922</span><span class="o">+</span><span class="mi">2495143</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [458]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop by index value</span>
<span class="n">df_beach_el_merge_final4</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="mi">77</span><span class="p">])</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">'MUN'</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [463]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Go through each unique MUN to check for final errors</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_beach_el_merge_final4</span><span class="p">[</span><span class="s1">'MUN'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Wildwood"</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[463]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

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

<th>87</th>

<td>Wildwood</td>

<td>1991</td>

<td>110</td>

<td>38.978995</td>

<td>-74.817971</td>

<td>100000</td>

<td>761441</td>

<td>-0.23</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Review df</span>
<span class="n">df_beach_el_merge_final4</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [465]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Write df to Excel file</span>
<span class="n">writer</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">ExcelWriter</span><span class="p">(</span><span class="s1">'df_beach_el_merge_final4.xlsx'</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final4</span><span class="o">.</span><span class="n">to_excel</span><span class="p">(</span><span class="n">writer</span><span class="p">,</span> <span class="s1">'DataFrame'</span><span class="p">)</span>
<span class="n">writer</span><span class="o">.</span><span class="n">save</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Keep columns we want to new df</span>
<span class="n">df_beach_el_merge_final_GIS</span> <span class="o">=</span> <span class="n">df_beach_el_merge_final4</span><span class="p">[[</span><span class="s1">'MUN'</span><span class="p">,</span><span class="s1">'Year'</span><span class="p">,</span><span class="s1">'Latitude'</span><span class="p">,</span><span class="s1">'Longitude'</span><span class="p">,</span><span class="s1">'Total_CY'</span><span class="p">,</span><span class="s1">'Costin2016'</span><span class="p">]]</span>
<span class="n">df_beach_el_merge_final_GIS</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [467]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Write df to Excel file</span>
<span class="n">writer</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">ExcelWriter</span><span class="p">(</span><span class="s1">'NJBR_GIS2.xlsx'</span><span class="p">)</span>
<span class="n">df_beach_el_merge_final_GIS</span><span class="o">.</span><span class="n">to_excel</span><span class="p">(</span><span class="n">writer</span><span class="p">,</span> <span class="s1">'DataFrame'</span><span class="p">)</span>
<span class="n">writer</span><span class="o">.</span><span class="n">save</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

</div>
