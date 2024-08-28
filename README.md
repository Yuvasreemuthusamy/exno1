# Exno:1 Data Cleaning Process
# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding
# Data Cleaning
```
import pandas as pd
df=pd.read_csv("SAMPLEIDS.csv")
df
```
![image](https://github.com/user-attachments/assets/105744d5-2486-4bcf-9430-ebcc6bcc3602)

```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/93d73a93-697a-4cac-b954-669bc1882a52)

```
df.isnull().any()
```
![image](https://github.com/user-attachments/assets/9085f5e3-7607-4202-9e40-f94d855facb2)

```
df.dropna()
```
![image](https://github.com/user-attachments/assets/29d93dc3-0c3e-4de7-85fc-5c4d00ddfdc7)
```
df.fillna(0)
```
![image](https://github.com/user-attachments/assets/07d604bb-7f4d-4601-96e9-a4fb6501a336)

```
df.fillna(method = 'ffill')
```
![image](https://github.com/user-attachments/assets/312de59b-e128-4af5-ba27-fe00fb84ad02)

```
df.fillna(method = 'bfill')
```

```
df_dropped = df.dropna()
df_dropped
```
![image](https://github.com/user-attachments/assets/bc95a021-5417-47e9-b03b-688d67d4415b)
```
df.fillna({'GENDER':'MALE','NAME':'SRI','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![image](https://github.com/user-attachments/assets/e4c8d813-7d2b-4910-88a3-e8ef363ca1de)

# IQR(Inter Quartile Range)
```
import pandas as pd
```
```
ir=pd.read_csv('iris.csv')
ir
```
![image](https://github.com/user-attachments/assets/d4fbe9a9-07ae-4642-ac35-d097527adc93)

```
ir.describe()
```
![image](https://github.com/user-attachments/assets/ebdacf6d-cb89-47ce-ba91-88cd85c5fdc4)

```
sns.boxplot(x='sepal_width',data=ir)
```
![image](https://github.com/user-attachments/assets/3a687961-f889-407d-8573-db7868336d58)

```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![image](https://github.com/user-attachments/assets/88ff49d6-1784-4bdc-81c0-f72446d875ac)

```

rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![image](https://github.com/user-attachments/assets/ff59a40d-49a1-4ca6-9115-18f306956dc2)

```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/user-attachments/assets/1f7724f8-3f29-4534-8431-7ac22210bfb4)

```
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/user-attachments/assets/30e39ac7-98c6-46e7-bfc3-f230895b6e3f)

# Z-Score
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
```
```
dataset=pd.read_csv("heights.csv")
dataset
```
![image](https://github.com/user-attachments/assets/5d3b1a21-01cd-4e2f-b919-8fe00578793a)

```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```
```
iqr = q3-q1
iqr
```
![image](https://github.com/user-attachments/assets/1a5240ae-45c3-4533-9a40-8bbfd6f073a2)

```
low = q1 - 1.5*iqr
low
```
![image](https://github.com/user-attachments/assets/c881c378-079d-4d7c-b9b8-221248617181)

```
high = q3 + 1.5*iqr
high
```
![image](https://github.com/user-attachments/assets/5a51d222-094f-49c4-8782-0e4b7dd08ba4)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![image](https://github.com/user-attachments/assets/b8ef6f82-bc91-46e3-9bf8-dc1ee526bc5f)

```
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/user-attachments/assets/9ac889c2-3793-4935-9219-0f2731613ed2)

```
df1 = df[z<3]
df1
```
![image](https://github.com/user-attachments/assets/77cc6164-2ff1-4cb4-b777-532dc6fc00a4)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
