# 📱 Google Play Store Data Analysis

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import warnings

warnings.filterwarnings("ignore")

%matplotlib inline


```

```python
df=pd.read_csv('https://raw.githubusercontent.com/krishnaik06/playstore-Dataset/main/googleplaystore.csv')
df.head()
```

```python
df.info()
```

```python
df.describe()
```

```python
df.isnull().sum()
```

```python
df['Reviews'].unique()
```

```python
# checking the numeric value in that string  so by checking we found that there is only one 
# one value that is not numeric so we will find by writing another code by this 

df['Reviews'].str.isnumeric().sum()
```

```python
# now we find what is not numeric 
df[~df['Reviews'].str.isnumeric()]

```

```python
df_copy=df.copy()
```

```python
df_copy = df_copy.drop(df_copy.index[10472])
```

```python
df_copy.index[10472]
```

```python
df_copy['Reviews']= df_copy['Reviews'].astype(int)

```

```python
df_copy.info()
df_copy.describe()
```

```python
df_copy['Size'].unique()
```

```python
df_copy.isnull().sum()
```

```python
# 19000k =19M
df_copy['Size']=df_copy['Size'].str.replace('M','000')
df_copy['Size']=df_copy['Size'].str.replace('k','')

```

```python
df_copy['Size']=df_copy['Size'].replace('Varies with device',np.nan)
```

```python
df_copy['Size'].unique
```

```python
df_copy['Size']= df_copy['Size'].astype(float)
```

```python
df_copy['Installs'].unique()
```

```python
df_copy['Price'].unique()
```

```python
chars_to_remove=['+',',','$']
cols_to_clean=['Installs','Price']

for item in chars_to_remove:
  for cols in cols_to_clean:
    df_copy[cols]= df_copy[cols].str.replace(item,'')
         
```

```python
df_copy['Installs']=df_copy['Installs'].astype(int)
df_copy['Price']=df_copy['Price'].astype(float)
```

```python
df_copy.info()
```

```python
# last update feature
df_copy['Last Updated'].unique()
```

```python
df_copy['Last Updated']=pd.to_datetime(df_copy['Last Updated'])
df_copy.info()

```

```python
df_copy['Day'] = df_copy['Last Updated'].dt.day
df_copy['Month'] = df_copy['Last Updated'].dt.month
df_copy['Year'] = df_copy['Last Updated'].dt.year
```

```python
df_copy.info()
```

```python
df_copy['Size'].unique()
```

```python

df_copy.to_csv('python/playstore.csv', index=False)
```

```python
import os
```

```python
os.makedirs('python', exist_ok=True)

# Now save the file
df_copy.to_csv('python/playstore.csv', index=False)
```

```python
import pandas as pd

# Reload to verify
df_test = pd.read_csv('python/playstore.csv')
df_test.head()
```
