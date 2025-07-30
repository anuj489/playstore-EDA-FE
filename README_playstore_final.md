
# 📱 Google Play Store Data Cleaning & EDA with Python

This project involves cleaning and preprocessing raw Google Play Store data to prepare it for further analysis and visualization. It primarily focuses on data cleaning, transformation, and exploratory steps to build a reliable dataset for future modeling and insights.

---

## 📌 Objective

- Clean inconsistent and non-numeric values from the dataset.
- Convert string-based sizes, installs, and prices into numerical formats.
- Handle missing values and erroneous entries.
- Extract features from date columns for temporal analysis.
- Save the cleaned dataset for downstream analysis or modeling.

---

## 🛠️ Tools Used

- **Python**: Core scripting language.
- **Pandas**: Data manipulation.
- **NumPy**: Numerical operations.
- **Matplotlib / Seaborn**: Data visualization (setup only).
- **Jupyter Notebook**: Interactive coding environment.

---

## 🔍 Key Steps in Code

```python
# Importing necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import warnings

warnings.filterwarnings("ignore")
%matplotlib inline

# Loading the dataset
df = pd.read_csv('https://raw.githubusercontent.com/krishnaik06/playstore-Dataset/main/googleplaystore.csv')

# Initial exploration
df.head()
df.info()
df.describe()
df.isnull().sum()

# Identify and handle non-numeric 'Reviews'
df['Reviews'].str.isnumeric().sum()
df[~df['Reviews'].str.isnumeric()]
df_copy = df.copy()
df_copy = df_copy.drop(df_copy.index[10472])
df_copy['Reviews'] = df_copy['Reviews'].astype(int)

# Cleaning 'Size' column
df_copy['Size'] = df_copy['Size'].str.replace('M', '000')
df_copy['Size'] = df_copy['Size'].str.replace('k', '')
df_copy['Size'] = df_copy['Size'].replace('Varies with device', np.nan)
df_copy['Size'] = df_copy['Size'].astype(float)

# Cleaning 'Installs' and 'Price' columns
chars_to_remove = ['+', ',', '$']
cols_to_clean = ['Installs', 'Price']
for item in chars_to_remove:
    for col in cols_to_clean:
        df_copy[col] = df_copy[col].str.replace(item, '')

df_copy['Installs'] = df_copy['Installs'].astype(int)
df_copy['Price'] = df_copy['Price'].astype(float)

# Parsing 'Last Updated' column
df_copy['Last Updated'] = pd.to_datetime(df_copy['Last Updated'])
df_copy['Day'] = df_copy['Last Updated'].dt.day
df_copy['Month'] = df_copy['Last Updated'].dt.month
df_copy['Year'] = df_copy['Last Updated'].dt.year

# Saving the cleaned dataset
import os
os.makedirs('python', exist_ok=True)
df_copy.to_csv('python/playstore.csv', index=False)
```

---

## 💾 Output

The cleaned dataset is saved as:  
📁 `python/playstore.csv`

---

## 👨‍💻 Author

**Anuj Agarwal**  
Data Analyst | Python Enthusiast  
Email: [your-email@example.com]  
GitHub: [your-github-link]  
LinkedIn: [your-linkedin-link]

---

## 📘 License

This project is intended for educational and portfolio purposes.
