# customer-personality-data-cleaning
Data cleaning and preprocessing of the Customer Personality Analysis dataset from Kaggle, including missing value treatment, standardization, and data type correction.
#Check data types of all columns
print(df.dtypes)

#converting year into age 
from datetime import datetime

current_year = datetime.now().year

df['age'] = current_year - df['year_birth']

df['age'] = df['age'].astype(int)


#converting binary column to int not necessary as they are already in int datatype
binary_cols = ['acceptedcmp1', 'acceptedcmp2', 'acceptedcmp3', 'acceptedcmp4',
               'acceptedcmp5', 'response', 'complain']

for col in binary_cols:
    df[col] = df[col].astype(int)
    
#converting object into category to save memory

cat_cols = ['education', 'marital_status']

df[cat_cols] = df[cat_cols].astype('category')

print(df.dtypes)

#### 2. **Marital_Status**
- Converted to lowercase and stripped whitespace
- Standardized values using a mapping dictionary:

#### 3. **Dt_Customer**
- Converted from string to `datetime` using format `%d-%m-%Y`
- Handled errors with `errors='coerce'`

#### 4. **Column Renaming**
- Renamed all column names to lowercase with underscores
- Fixed specific confusing names:
- `mntwines` → `mnt_wines`
- `mntfishproducts` → `mnt_fish_products`
- `numdealspurchases` → `num_deals_purchases`

---

### 📊 Feature Engineering

#### 5. **Age Calculation**
- Created a new column `age` from `year_birth`:
```python
df['age'] = current_year - df['year_birth']
customer-personality-data-cleaning/
│
├── data/
│   └── marketing_campaign.csv         # Raw dataset
│
├── notebooks/
│   └── 01_data_cleaning.ipynb         # Jupyter notebook with all steps
│
├── README.md                          # Project documentation
└── requirements.txt                   # (optional) Python dependencies
