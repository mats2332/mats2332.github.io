

```python
%matplotlib inline

import numpy as np
import pandas as pd
import matplotlib as mpl
import matplotlib.pyplot as plt

import seaborn as sns
sns.set(color_codes=True)

np.random.seed(sum(map(ord, "regression")))

#Load Final Beach Replenishment Data
# Assign spreadsheet filename to `NJBPN`
df_beach_el_merge_final4 = pd.ExcelFile('df_beach_el_merge_final4.xlsx')
# Convert Excel file to dataframe
df_beach_el_merge_final4 = df_beach_el_merge_final4.parse('DataFrame')

data=df_beach_el_merge_final4[['Total_CY','Z']]

sns.set_style("darkgrid", {"axes.facecolor": ".9"})
sns.set_context("notebook", font_scale=1, rc={"lines.linewidth": 2})

lmplot=sns.lmplot(x="Z", y="Total_CY", data=data);
lmplot.fig.savefig("output.png")
```


![png](5103_5104_Final_Project_Plot_LR_SNS_files/5103_5104_Final_Project_Plot_LR_SNS_0_0.png)

