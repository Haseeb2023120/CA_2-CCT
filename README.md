# CA_2-CCT
Ireland Housing Construction Cost 
Statistics for Data Analytics Tasks

Use descriptive statistics and appropriate visualisations in order to summarise the dataset(s) used, and to help justify the chosen models
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
​
# Assuming 'df' is my DataFrame
df = pd.read_csv('/content/sample_data/house/national_house_construction_cost_index_0 (1).csv') 
​
​
​
df
​
Month	1994	1995	1996	1997	1998	1999	2000	2001	2002	...	2007	2008	2009	2010	2011	2012	2013	2014	2015	2016
0	January	109.2	113.5	115.9	118	122.9	126.3	135.8	154.3	169.9	...	198.8	207.4	208	206.9	210.2	202.5	204.1	204.9	206.2	207.4
1	February	109.3	114.1	115.7	118.5	123.1	126.4	136.1	154.7	170	...	198.8	208.2	207.3	207.2	210.5	202.6	204.2	205.4	206	207.1
2	March	109.4	114.1	115.9	118.8	123.8	126.5	136.4	155.6	169.5	...	199.4	208.6	206.8	207.3	200.7	202.7	204.3	205.4	206.5	NaN
3	April	110.3	114.1	115.9	119.8	123.8	130.5	136.5	157.4	169.5	...	200	208.9	206.5	207.9	201	203.4	204.5	205.6	206.8	NaN
4	May	110.1	114.1	115.9	119.8	124.5	130.5	136.8	157.6	169.5	...	200.1	209.4	206.5	208.7	201.2	203.6	204.5	205.9	207.2	NaN
5	June	110.6	114.1	116	119.9	124.5	130.5	136.9	157.7	169.7	...	200.3	209.9	206	208.6	201.4	203.6	204.8	206	207.6	NaN
6	July	110.7	114.5	116	120.8	125.7	131.5	137.2	161.1	173.8	...	203.7	210.4	206	209.4	201.5	204.1	204.8	206	207.4	NaN
7	August	110.9	114.5	116	121	125.7	131.5	137.2	165.9	173.9	...	203.6	210.4	206	209.6	201.9	204.1	205	206.6	207.4	NaN
8	September	112.2	115.7	116.9	121.5	126	134.1	137.7	166	173.9	...	203.7	210.5	206.1	209.5	202.1	203.7	205.1	206.4	207.3	NaN
9	October	112.7	115.8	117.1	122	126.2	134.7	153.8	169.3	173.9	...	203.8	210.1	206.2	209.5	202	203.8	205.4	206.7	207.2	NaN
10	November	112.9	115.9	117.2	122.6	126.2	134.8	153.8	169.4	174	...	203.8	209.9	206.2	209.5	202.2	204	205.4	206.5	207.6	NaN
11	December	113.1	115.9	117.2	122.6	126.1	134.9	153.9	169.3	174.1	...	204.2	209.3	206.2	209.8	202.3	204.2	204.7	206.2	207.4	NaN
12	Yearly average	111	114.7	116.3	120.4	124.9	131	141	161.5	171.8	...	201.7	209.4	206.5	208.7	203.1	203.5	204.7	206	207.1	NaN
13	% Increase on previous year	3.40%	3.30%	1.40%	3.50%	3.70%	4.90%	7.60%	14.50%	6.40%	...	3.90%	3.80%	-1.40%	1.10%	-2.70%	0.20%	0.60%	0.60%	0.50%	NaN
14 rows × 24 columns

df = df.set_index('Month').T.reset_index().rename(columns={'index':'Year'})
​
print(df.describe())
Month   Year January February  March  April    May June July August September  \
count     23      23       23     22     22     22   22   22     22        22   
unique    23      23       23     22     22     22   21   21     22        21   
top     1994   109.2    109.3  109.4  110.3  110.1  206  206  110.9     203.7   
freq       1       1        1      1      1      1    2    2      1         2   

Month  October November December Yearly average % Increase on previous year  
count       22       22       22             22                          22  
unique      21       22       20             22                          20  
top      203.8    112.9    206.2            111                       0.60%  
freq         2        1        2              1                           2  
# Convert all columns to numeric after excluding the 'Year' column
for col in df.columns.drop('Year'):
    df[col] = df[col].str.replace('%','').astype(float)
​
plt.figure(figsize=(10,8))
sns.heatmap(df.drop('Year', axis=1), cmap='coolwarm', annot=True, fmt=".1f")
plt.title('National House Construction Cost Index over Years')
plt.ylabel('Year')
plt.xlabel('Month')
plt.show()
​
​
