```python
import pandas as pd
import numpy as np 
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline
```


```python
from sklearn.datasets import fetch_openml
cal = fetch_openml(name="house_prices", version=1, parser='liac-arff')
```


```python
type(cal)
```




    sklearn.utils._bunch.Bunch




```python
# transform the dataset into a pandas dataframe
housingdf =cal.frame
```


```python
#check the data type
type(housingdf)
```




    pandas.core.frame.DataFrame




```python
#call the data 
housingdf.head()
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>MSZoning</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>Street</th>
      <th>Alley</th>
      <th>LotShape</th>
      <th>LandContour</th>
      <th>Utilities</th>
      <th>...</th>
      <th>PoolArea</th>
      <th>PoolQC</th>
      <th>Fence</th>
      <th>MiscFeature</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SaleType</th>
      <th>SaleCondition</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
      <td>RL</td>
      <td>65.0</td>
      <td>8450</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>208500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>20</td>
      <td>RL</td>
      <td>80.0</td>
      <td>9600</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>5</td>
      <td>2007</td>
      <td>WD</td>
      <td>Normal</td>
      <td>181500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>60</td>
      <td>RL</td>
      <td>68.0</td>
      <td>11250</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>9</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>223500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>70</td>
      <td>RL</td>
      <td>60.0</td>
      <td>9550</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2006</td>
      <td>WD</td>
      <td>Abnorml</td>
      <td>140000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>60</td>
      <td>RL</td>
      <td>84.0</td>
      <td>14260</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>250000</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 81 columns</p>
</div>




```python
housingdf.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1460 entries, 0 to 1459
    Data columns (total 81 columns):
     #   Column         Non-Null Count  Dtype  
    ---  ------         --------------  -----  
     0   Id             1460 non-null   int64  
     1   MSSubClass     1460 non-null   int64  
     2   MSZoning       1460 non-null   object 
     3   LotFrontage    1201 non-null   float64
     4   LotArea        1460 non-null   int64  
     5   Street         1460 non-null   object 
     6   Alley          91 non-null     object 
     7   LotShape       1460 non-null   object 
     8   LandContour    1460 non-null   object 
     9   Utilities      1460 non-null   object 
     10  LotConfig      1460 non-null   object 
     11  LandSlope      1460 non-null   object 
     12  Neighborhood   1460 non-null   object 
     13  Condition1     1460 non-null   object 
     14  Condition2     1460 non-null   object 
     15  BldgType       1460 non-null   object 
     16  HouseStyle     1460 non-null   object 
     17  OverallQual    1460 non-null   int64  
     18  OverallCond    1460 non-null   int64  
     19  YearBuilt      1460 non-null   int64  
     20  YearRemodAdd   1460 non-null   int64  
     21  RoofStyle      1460 non-null   object 
     22  RoofMatl       1460 non-null   object 
     23  Exterior1st    1460 non-null   object 
     24  Exterior2nd    1460 non-null   object 
     25  MasVnrType     1452 non-null   object 
     26  MasVnrArea     1452 non-null   float64
     27  ExterQual      1460 non-null   object 
     28  ExterCond      1460 non-null   object 
     29  Foundation     1460 non-null   object 
     30  BsmtQual       1423 non-null   object 
     31  BsmtCond       1423 non-null   object 
     32  BsmtExposure   1422 non-null   object 
     33  BsmtFinType1   1423 non-null   object 
     34  BsmtFinSF1     1460 non-null   int64  
     35  BsmtFinType2   1422 non-null   object 
     36  BsmtFinSF2     1460 non-null   int64  
     37  BsmtUnfSF      1460 non-null   int64  
     38  TotalBsmtSF    1460 non-null   int64  
     39  Heating        1460 non-null   object 
     40  HeatingQC      1460 non-null   object 
     41  CentralAir     1460 non-null   object 
     42  Electrical     1459 non-null   object 
     43  1stFlrSF       1460 non-null   int64  
     44  2ndFlrSF       1460 non-null   int64  
     45  LowQualFinSF   1460 non-null   int64  
     46  GrLivArea      1460 non-null   int64  
     47  BsmtFullBath   1460 non-null   int64  
     48  BsmtHalfBath   1460 non-null   int64  
     49  FullBath       1460 non-null   int64  
     50  HalfBath       1460 non-null   int64  
     51  BedroomAbvGr   1460 non-null   int64  
     52  KitchenAbvGr   1460 non-null   int64  
     53  KitchenQual    1460 non-null   object 
     54  TotRmsAbvGrd   1460 non-null   int64  
     55  Functional     1460 non-null   object 
     56  Fireplaces     1460 non-null   int64  
     57  FireplaceQu    770 non-null    object 
     58  GarageType     1379 non-null   object 
     59  GarageYrBlt    1379 non-null   float64
     60  GarageFinish   1379 non-null   object 
     61  GarageCars     1460 non-null   int64  
     62  GarageArea     1460 non-null   int64  
     63  GarageQual     1379 non-null   object 
     64  GarageCond     1379 non-null   object 
     65  PavedDrive     1460 non-null   object 
     66  WoodDeckSF     1460 non-null   int64  
     67  OpenPorchSF    1460 non-null   int64  
     68  EnclosedPorch  1460 non-null   int64  
     69  3SsnPorch      1460 non-null   int64  
     70  ScreenPorch    1460 non-null   int64  
     71  PoolArea       1460 non-null   int64  
     72  PoolQC         7 non-null      object 
     73  Fence          281 non-null    object 
     74  MiscFeature    54 non-null     object 
     75  MiscVal        1460 non-null   int64  
     76  MoSold         1460 non-null   int64  
     77  YrSold         1460 non-null   int64  
     78  SaleType       1460 non-null   object 
     79  SaleCondition  1460 non-null   object 
     80  SalePrice      1460 non-null   int64  
    dtypes: float64(3), int64(35), object(43)
    memory usage: 924.0+ KB
    


```python
#check if there a missing values
housingdf.isnull()
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>MSZoning</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>Street</th>
      <th>Alley</th>
      <th>LotShape</th>
      <th>LandContour</th>
      <th>Utilities</th>
      <th>...</th>
      <th>PoolArea</th>
      <th>PoolQC</th>
      <th>Fence</th>
      <th>MiscFeature</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SaleType</th>
      <th>SaleCondition</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
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
    </tr>
    <tr>
      <th>1455</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1456</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1457</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1458</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1459</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
<p>1460 rows × 81 columns</p>
</div>




```python
housingdf.isnull().values.any() #missing values
```




    True




```python
housingdf.isnull().sum() #missing values Lot Frontage column
```




    Id                 0
    MSSubClass         0
    MSZoning           0
    LotFrontage      259
    LotArea            0
                    ... 
    MoSold             0
    YrSold             0
    SaleType           0
    SaleCondition      0
    SalePrice          0
    Length: 81, dtype: int64




```python
housingdf[housingdf.isnull().any(axis=1)]
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>MSZoning</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>Street</th>
      <th>Alley</th>
      <th>LotShape</th>
      <th>LandContour</th>
      <th>Utilities</th>
      <th>...</th>
      <th>PoolArea</th>
      <th>PoolQC</th>
      <th>Fence</th>
      <th>MiscFeature</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SaleType</th>
      <th>SaleCondition</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
      <td>RL</td>
      <td>65.0</td>
      <td>8450</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>208500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>20</td>
      <td>RL</td>
      <td>80.0</td>
      <td>9600</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>5</td>
      <td>2007</td>
      <td>WD</td>
      <td>Normal</td>
      <td>181500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>60</td>
      <td>RL</td>
      <td>68.0</td>
      <td>11250</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>9</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>223500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>70</td>
      <td>RL</td>
      <td>60.0</td>
      <td>9550</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2006</td>
      <td>WD</td>
      <td>Abnorml</td>
      <td>140000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>60</td>
      <td>RL</td>
      <td>84.0</td>
      <td>14260</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>250000</td>
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
    </tr>
    <tr>
      <th>1455</th>
      <td>1456</td>
      <td>60</td>
      <td>RL</td>
      <td>62.0</td>
      <td>7917</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>8</td>
      <td>2007</td>
      <td>WD</td>
      <td>Normal</td>
      <td>175000</td>
    </tr>
    <tr>
      <th>1456</th>
      <td>1457</td>
      <td>20</td>
      <td>RL</td>
      <td>85.0</td>
      <td>13175</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>MnPrv</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
      <td>210000</td>
    </tr>
    <tr>
      <th>1457</th>
      <td>1458</td>
      <td>70</td>
      <td>RL</td>
      <td>66.0</td>
      <td>9042</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>GdPrv</td>
      <td>Shed</td>
      <td>2500</td>
      <td>5</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
      <td>266500</td>
    </tr>
    <tr>
      <th>1458</th>
      <td>1459</td>
      <td>20</td>
      <td>RL</td>
      <td>68.0</td>
      <td>9717</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>4</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
      <td>142125</td>
    </tr>
    <tr>
      <th>1459</th>
      <td>1460</td>
      <td>20</td>
      <td>RL</td>
      <td>75.0</td>
      <td>9937</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>6</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>147500</td>
    </tr>
  </tbody>
</table>
<p>1460 rows × 81 columns</p>
</div>




```python
#option 1
housingdf.dropna()
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>MSZoning</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>Street</th>
      <th>Alley</th>
      <th>LotShape</th>
      <th>LandContour</th>
      <th>Utilities</th>
      <th>...</th>
      <th>PoolArea</th>
      <th>PoolQC</th>
      <th>Fence</th>
      <th>MiscFeature</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SaleType</th>
      <th>SaleCondition</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
<p>0 rows × 81 columns</p>
</div>




```python
housingdf.columns
```




    Index(['Id', 'MSSubClass', 'MSZoning', 'LotFrontage', 'LotArea', 'Street',
           'Alley', 'LotShape', 'LandContour', 'Utilities', 'LotConfig',
           'LandSlope', 'Neighborhood', 'Condition1', 'Condition2', 'BldgType',
           'HouseStyle', 'OverallQual', 'OverallCond', 'YearBuilt', 'YearRemodAdd',
           'RoofStyle', 'RoofMatl', 'Exterior1st', 'Exterior2nd', 'MasVnrType',
           'MasVnrArea', 'ExterQual', 'ExterCond', 'Foundation', 'BsmtQual',
           'BsmtCond', 'BsmtExposure', 'BsmtFinType1', 'BsmtFinSF1',
           'BsmtFinType2', 'BsmtFinSF2', 'BsmtUnfSF', 'TotalBsmtSF', 'Heating',
           'HeatingQC', 'CentralAir', 'Electrical', '1stFlrSF', '2ndFlrSF',
           'LowQualFinSF', 'GrLivArea', 'BsmtFullBath', 'BsmtHalfBath', 'FullBath',
           'HalfBath', 'BedroomAbvGr', 'KitchenAbvGr', 'KitchenQual',
           'TotRmsAbvGrd', 'Functional', 'Fireplaces', 'FireplaceQu', 'GarageType',
           'GarageYrBlt', 'GarageFinish', 'GarageCars', 'GarageArea', 'GarageQual',
           'GarageCond', 'PavedDrive', 'WoodDeckSF', 'OpenPorchSF',
           'EnclosedPorch', '3SsnPorch', 'ScreenPorch', 'PoolArea', 'PoolQC',
           'Fence', 'MiscFeature', 'MiscVal', 'MoSold', 'YrSold', 'SaleType',
           'SaleCondition', 'SalePrice'],
          dtype='object')




```python
#option 2 fill it with the mean values of the LotFrontage serie
housingdf['LotFrontage'].fillna(value=housingdf['LotFrontage'].mean())
```




    0       65.0
    1       80.0
    2       68.0
    3       60.0
    4       84.0
            ... 
    1455    62.0
    1456    85.0
    1457    66.0
    1458    68.0
    1459    75.0
    Name: LotFrontage, Length: 1460, dtype: float64




```python
#store it 
housingdf['LotFrontage'] = housingdf['LotFrontage'].fillna(value=housingdf['LotFrontage'].mean())
```


```python
housingdf.describe()
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>OverallQual</th>
      <th>OverallCond</th>
      <th>YearBuilt</th>
      <th>YearRemodAdd</th>
      <th>MasVnrArea</th>
      <th>BsmtFinSF1</th>
      <th>...</th>
      <th>WoodDeckSF</th>
      <th>OpenPorchSF</th>
      <th>EnclosedPorch</th>
      <th>3SsnPorch</th>
      <th>ScreenPorch</th>
      <th>PoolArea</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1452.000000</td>
      <td>1460.000000</td>
      <td>...</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>730.500000</td>
      <td>56.897260</td>
      <td>70.049958</td>
      <td>10516.828082</td>
      <td>6.099315</td>
      <td>5.575342</td>
      <td>1971.267808</td>
      <td>1984.865753</td>
      <td>103.685262</td>
      <td>443.639726</td>
      <td>...</td>
      <td>94.244521</td>
      <td>46.660274</td>
      <td>21.954110</td>
      <td>3.409589</td>
      <td>15.060959</td>
      <td>2.758904</td>
      <td>43.489041</td>
      <td>6.321918</td>
      <td>2007.815753</td>
      <td>180921.195890</td>
    </tr>
    <tr>
      <th>std</th>
      <td>421.610009</td>
      <td>42.300571</td>
      <td>22.024023</td>
      <td>9981.264932</td>
      <td>1.382997</td>
      <td>1.112799</td>
      <td>30.202904</td>
      <td>20.645407</td>
      <td>181.066207</td>
      <td>456.098091</td>
      <td>...</td>
      <td>125.338794</td>
      <td>66.256028</td>
      <td>61.119149</td>
      <td>29.317331</td>
      <td>55.757415</td>
      <td>40.177307</td>
      <td>496.123024</td>
      <td>2.703626</td>
      <td>1.328095</td>
      <td>79442.502883</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>20.000000</td>
      <td>21.000000</td>
      <td>1300.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1872.000000</td>
      <td>1950.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2006.000000</td>
      <td>34900.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>365.750000</td>
      <td>20.000000</td>
      <td>60.000000</td>
      <td>7553.500000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>1954.000000</td>
      <td>1967.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>5.000000</td>
      <td>2007.000000</td>
      <td>129975.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>730.500000</td>
      <td>50.000000</td>
      <td>70.049958</td>
      <td>9478.500000</td>
      <td>6.000000</td>
      <td>5.000000</td>
      <td>1973.000000</td>
      <td>1994.000000</td>
      <td>0.000000</td>
      <td>383.500000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>25.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>6.000000</td>
      <td>2008.000000</td>
      <td>163000.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1095.250000</td>
      <td>70.000000</td>
      <td>79.000000</td>
      <td>11601.500000</td>
      <td>7.000000</td>
      <td>6.000000</td>
      <td>2000.000000</td>
      <td>2004.000000</td>
      <td>166.000000</td>
      <td>712.250000</td>
      <td>...</td>
      <td>168.000000</td>
      <td>68.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>8.000000</td>
      <td>2009.000000</td>
      <td>214000.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1460.000000</td>
      <td>190.000000</td>
      <td>313.000000</td>
      <td>215245.000000</td>
      <td>10.000000</td>
      <td>9.000000</td>
      <td>2010.000000</td>
      <td>2010.000000</td>
      <td>1600.000000</td>
      <td>5644.000000</td>
      <td>...</td>
      <td>857.000000</td>
      <td>547.000000</td>
      <td>552.000000</td>
      <td>508.000000</td>
      <td>480.000000</td>
      <td>738.000000</td>
      <td>15500.000000</td>
      <td>12.000000</td>
      <td>2010.000000</td>
      <td>755000.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 38 columns</p>
</div>




```python
#check again missing values
housingdf.isnull().sum() # bingo!  LotFrontage has no missing values! 
```




    Id               0
    MSSubClass       0
    MSZoning         0
    LotFrontage      0
    LotArea          0
                    ..
    MoSold           0
    YrSold           0
    SaleType         0
    SaleCondition    0
    SalePrice        0
    Length: 81, dtype: int64




```python
housingdf.isnull().values.any() #missing values
```




    True




```python
housingdf # Nan values :(
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>MSZoning</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>Street</th>
      <th>Alley</th>
      <th>LotShape</th>
      <th>LandContour</th>
      <th>Utilities</th>
      <th>...</th>
      <th>PoolArea</th>
      <th>PoolQC</th>
      <th>Fence</th>
      <th>MiscFeature</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SaleType</th>
      <th>SaleCondition</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
      <td>RL</td>
      <td>65.0</td>
      <td>8450</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>208500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>20</td>
      <td>RL</td>
      <td>80.0</td>
      <td>9600</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>5</td>
      <td>2007</td>
      <td>WD</td>
      <td>Normal</td>
      <td>181500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>60</td>
      <td>RL</td>
      <td>68.0</td>
      <td>11250</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>9</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>223500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>70</td>
      <td>RL</td>
      <td>60.0</td>
      <td>9550</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2006</td>
      <td>WD</td>
      <td>Abnorml</td>
      <td>140000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>60</td>
      <td>RL</td>
      <td>84.0</td>
      <td>14260</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>250000</td>
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
    </tr>
    <tr>
      <th>1455</th>
      <td>1456</td>
      <td>60</td>
      <td>RL</td>
      <td>62.0</td>
      <td>7917</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>8</td>
      <td>2007</td>
      <td>WD</td>
      <td>Normal</td>
      <td>175000</td>
    </tr>
    <tr>
      <th>1456</th>
      <td>1457</td>
      <td>20</td>
      <td>RL</td>
      <td>85.0</td>
      <td>13175</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>MnPrv</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
      <td>210000</td>
    </tr>
    <tr>
      <th>1457</th>
      <td>1458</td>
      <td>70</td>
      <td>RL</td>
      <td>66.0</td>
      <td>9042</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>GdPrv</td>
      <td>Shed</td>
      <td>2500</td>
      <td>5</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
      <td>266500</td>
    </tr>
    <tr>
      <th>1458</th>
      <td>1459</td>
      <td>20</td>
      <td>RL</td>
      <td>68.0</td>
      <td>9717</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>4</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
      <td>142125</td>
    </tr>
    <tr>
      <th>1459</th>
      <td>1460</td>
      <td>20</td>
      <td>RL</td>
      <td>75.0</td>
      <td>9937</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>6</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>147500</td>
    </tr>
  </tbody>
</table>
<p>1460 rows × 81 columns</p>
</div>




```python
print(housingdf.loc[:, ['Alley', 'PoolQC', 'Fence', 'MiscFeature']])
```

         Alley PoolQC  Fence MiscFeature
    0      NaN    NaN    NaN         NaN
    1      NaN    NaN    NaN         NaN
    2      NaN    NaN    NaN         NaN
    3      NaN    NaN    NaN         NaN
    4      NaN    NaN    NaN         NaN
    ...    ...    ...    ...         ...
    1455   NaN    NaN    NaN         NaN
    1456   NaN    NaN  MnPrv         NaN
    1457   NaN    NaN  GdPrv        Shed
    1458   NaN    NaN    NaN         NaN
    1459   NaN    NaN    NaN         NaN
    
    [1460 rows x 4 columns]
    


```python
#fill it out with None values 
housingdf = housingdf.fillna('None')
```


```python
print(housingdf)
```

            Id  MSSubClass MSZoning  LotFrontage  LotArea Street Alley LotShape  \
    0        1          60       RL         65.0     8450   Pave  None      Reg   
    1        2          20       RL         80.0     9600   Pave  None      Reg   
    2        3          60       RL         68.0    11250   Pave  None      IR1   
    3        4          70       RL         60.0     9550   Pave  None      IR1   
    4        5          60       RL         84.0    14260   Pave  None      IR1   
    ...    ...         ...      ...          ...      ...    ...   ...      ...   
    1455  1456          60       RL         62.0     7917   Pave  None      Reg   
    1456  1457          20       RL         85.0    13175   Pave  None      Reg   
    1457  1458          70       RL         66.0     9042   Pave  None      Reg   
    1458  1459          20       RL         68.0     9717   Pave  None      Reg   
    1459  1460          20       RL         75.0     9937   Pave  None      Reg   
    
         LandContour Utilities  ... PoolArea PoolQC  Fence MiscFeature MiscVal  \
    0            Lvl    AllPub  ...        0   None   None        None       0   
    1            Lvl    AllPub  ...        0   None   None        None       0   
    2            Lvl    AllPub  ...        0   None   None        None       0   
    3            Lvl    AllPub  ...        0   None   None        None       0   
    4            Lvl    AllPub  ...        0   None   None        None       0   
    ...          ...       ...  ...      ...    ...    ...         ...     ...   
    1455         Lvl    AllPub  ...        0   None   None        None       0   
    1456         Lvl    AllPub  ...        0   None  MnPrv        None       0   
    1457         Lvl    AllPub  ...        0   None  GdPrv        Shed    2500   
    1458         Lvl    AllPub  ...        0   None   None        None       0   
    1459         Lvl    AllPub  ...        0   None   None        None       0   
    
         MoSold YrSold  SaleType  SaleCondition  SalePrice  
    0         2   2008        WD         Normal     208500  
    1         5   2007        WD         Normal     181500  
    2         9   2008        WD         Normal     223500  
    3         2   2006        WD        Abnorml     140000  
    4        12   2008        WD         Normal     250000  
    ...     ...    ...       ...            ...        ...  
    1455      8   2007        WD         Normal     175000  
    1456      2   2010        WD         Normal     210000  
    1457      5   2010        WD         Normal     266500  
    1458      4   2010        WD         Normal     142125  
    1459      6   2008        WD         Normal     147500  
    
    [1460 rows x 81 columns]
    


```python
housingdf.isnull().values.any() #missing values bingo! No missing values
```




    False




```python
housingdf.columns
```




    Index(['Id', 'MSSubClass', 'MSZoning', 'LotFrontage', 'LotArea', 'Street',
           'Alley', 'LotShape', 'LandContour', 'Utilities', 'LotConfig',
           'LandSlope', 'Neighborhood', 'Condition1', 'Condition2', 'BldgType',
           'HouseStyle', 'OverallQual', 'OverallCond', 'YearBuilt', 'YearRemodAdd',
           'RoofStyle', 'RoofMatl', 'Exterior1st', 'Exterior2nd', 'MasVnrType',
           'MasVnrArea', 'ExterQual', 'ExterCond', 'Foundation', 'BsmtQual',
           'BsmtCond', 'BsmtExposure', 'BsmtFinType1', 'BsmtFinSF1',
           'BsmtFinType2', 'BsmtFinSF2', 'BsmtUnfSF', 'TotalBsmtSF', 'Heating',
           'HeatingQC', 'CentralAir', 'Electrical', '1stFlrSF', '2ndFlrSF',
           'LowQualFinSF', 'GrLivArea', 'BsmtFullBath', 'BsmtHalfBath', 'FullBath',
           'HalfBath', 'BedroomAbvGr', 'KitchenAbvGr', 'KitchenQual',
           'TotRmsAbvGrd', 'Functional', 'Fireplaces', 'FireplaceQu', 'GarageType',
           'GarageYrBlt', 'GarageFinish', 'GarageCars', 'GarageArea', 'GarageQual',
           'GarageCond', 'PavedDrive', 'WoodDeckSF', 'OpenPorchSF',
           'EnclosedPorch', '3SsnPorch', 'ScreenPorch', 'PoolArea', 'PoolQC',
           'Fence', 'MiscFeature', 'MiscVal', 'MoSold', 'YrSold', 'SaleType',
           'SaleCondition', 'SalePrice'],
          dtype='object')




```python
housingdf.isnull().sum()
```




    Id               0
    MSSubClass       0
    MSZoning         0
    LotFrontage      0
    LotArea          0
                    ..
    MoSold           0
    YrSold           0
    SaleType         0
    SaleCondition    0
    SalePrice        0
    Length: 81, dtype: int64




```python
# check missing values per columns : Alley
print(housingdf['Alley'].isnull().sum())
```

    0
    


```python
# check missing values per columns : PoolQC
print(housingdf['PoolQC'].isnull().sum())
```

    0
    


```python
# check missing values per columns : Fence
print(housingdf['Fence'].isnull().sum())
```

    0
    


```python
# check missing values per columns : MiscFeature
print(housingdf['MiscFeature'].isnull().sum())
```

    0
    

#### Data Visualization


```python
housingdf.describe()
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>OverallQual</th>
      <th>OverallCond</th>
      <th>YearBuilt</th>
      <th>YearRemodAdd</th>
      <th>BsmtFinSF1</th>
      <th>BsmtFinSF2</th>
      <th>...</th>
      <th>WoodDeckSF</th>
      <th>OpenPorchSF</th>
      <th>EnclosedPorch</th>
      <th>3SsnPorch</th>
      <th>ScreenPorch</th>
      <th>PoolArea</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>...</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
      <td>1460.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>730.500000</td>
      <td>56.897260</td>
      <td>70.049958</td>
      <td>10516.828082</td>
      <td>6.099315</td>
      <td>5.575342</td>
      <td>1971.267808</td>
      <td>1984.865753</td>
      <td>443.639726</td>
      <td>46.549315</td>
      <td>...</td>
      <td>94.244521</td>
      <td>46.660274</td>
      <td>21.954110</td>
      <td>3.409589</td>
      <td>15.060959</td>
      <td>2.758904</td>
      <td>43.489041</td>
      <td>6.321918</td>
      <td>2007.815753</td>
      <td>180921.195890</td>
    </tr>
    <tr>
      <th>std</th>
      <td>421.610009</td>
      <td>42.300571</td>
      <td>22.024023</td>
      <td>9981.264932</td>
      <td>1.382997</td>
      <td>1.112799</td>
      <td>30.202904</td>
      <td>20.645407</td>
      <td>456.098091</td>
      <td>161.319273</td>
      <td>...</td>
      <td>125.338794</td>
      <td>66.256028</td>
      <td>61.119149</td>
      <td>29.317331</td>
      <td>55.757415</td>
      <td>40.177307</td>
      <td>496.123024</td>
      <td>2.703626</td>
      <td>1.328095</td>
      <td>79442.502883</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>20.000000</td>
      <td>21.000000</td>
      <td>1300.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1872.000000</td>
      <td>1950.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2006.000000</td>
      <td>34900.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>365.750000</td>
      <td>20.000000</td>
      <td>60.000000</td>
      <td>7553.500000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>1954.000000</td>
      <td>1967.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>5.000000</td>
      <td>2007.000000</td>
      <td>129975.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>730.500000</td>
      <td>50.000000</td>
      <td>70.049958</td>
      <td>9478.500000</td>
      <td>6.000000</td>
      <td>5.000000</td>
      <td>1973.000000</td>
      <td>1994.000000</td>
      <td>383.500000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>25.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>6.000000</td>
      <td>2008.000000</td>
      <td>163000.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1095.250000</td>
      <td>70.000000</td>
      <td>79.000000</td>
      <td>11601.500000</td>
      <td>7.000000</td>
      <td>6.000000</td>
      <td>2000.000000</td>
      <td>2004.000000</td>
      <td>712.250000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>168.000000</td>
      <td>68.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>8.000000</td>
      <td>2009.000000</td>
      <td>214000.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1460.000000</td>
      <td>190.000000</td>
      <td>313.000000</td>
      <td>215245.000000</td>
      <td>10.000000</td>
      <td>9.000000</td>
      <td>2010.000000</td>
      <td>2010.000000</td>
      <td>5644.000000</td>
      <td>1474.000000</td>
      <td>...</td>
      <td>857.000000</td>
      <td>547.000000</td>
      <td>552.000000</td>
      <td>508.000000</td>
      <td>480.000000</td>
      <td>738.000000</td>
      <td>15500.000000</td>
      <td>12.000000</td>
      <td>2010.000000</td>
      <td>755000.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 36 columns</p>
</div>




```python
housingdf.head()
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>MSZoning</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>Street</th>
      <th>Alley</th>
      <th>LotShape</th>
      <th>LandContour</th>
      <th>Utilities</th>
      <th>...</th>
      <th>PoolArea</th>
      <th>PoolQC</th>
      <th>Fence</th>
      <th>MiscFeature</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SaleType</th>
      <th>SaleCondition</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
      <td>RL</td>
      <td>65.0</td>
      <td>8450</td>
      <td>Pave</td>
      <td>None</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>0</td>
      <td>2</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>208500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>20</td>
      <td>RL</td>
      <td>80.0</td>
      <td>9600</td>
      <td>Pave</td>
      <td>None</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>0</td>
      <td>5</td>
      <td>2007</td>
      <td>WD</td>
      <td>Normal</td>
      <td>181500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>60</td>
      <td>RL</td>
      <td>68.0</td>
      <td>11250</td>
      <td>Pave</td>
      <td>None</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>0</td>
      <td>9</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>223500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>70</td>
      <td>RL</td>
      <td>60.0</td>
      <td>9550</td>
      <td>Pave</td>
      <td>None</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>0</td>
      <td>2</td>
      <td>2006</td>
      <td>WD</td>
      <td>Abnorml</td>
      <td>140000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>60</td>
      <td>RL</td>
      <td>84.0</td>
      <td>14260</td>
      <td>Pave</td>
      <td>None</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>0</td>
      <td>12</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>250000</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 81 columns</p>
</div>




```python
print(housingdf.dtypes)
```

    Id                 int64
    MSSubClass         int64
    MSZoning          object
    LotFrontage      float64
    LotArea            int64
                      ...   
    MoSold             int64
    YrSold             int64
    SaleType          object
    SaleCondition     object
    SalePrice          int64
    Length: 81, dtype: object
    


```python
# Select only those columns that contain numeric data
numeric_cols = housingdf.select_dtypes(include=['int64', 'float64']).columns.tolist()
```


```python
# Create a new DF just with numeric data
numeric_df = housingdf[numeric_cols]
```


```python
#call the data
print(numeric_df)
```

            Id  MSSubClass  LotFrontage  LotArea  OverallQual  OverallCond  \
    0        1          60         65.0     8450            7            5   
    1        2          20         80.0     9600            6            8   
    2        3          60         68.0    11250            7            5   
    3        4          70         60.0     9550            7            5   
    4        5          60         84.0    14260            8            5   
    ...    ...         ...          ...      ...          ...          ...   
    1455  1456          60         62.0     7917            6            5   
    1456  1457          20         85.0    13175            6            6   
    1457  1458          70         66.0     9042            7            9   
    1458  1459          20         68.0     9717            5            6   
    1459  1460          20         75.0     9937            5            6   
    
          YearBuilt  YearRemodAdd  BsmtFinSF1  BsmtFinSF2  ...  WoodDeckSF  \
    0          2003          2003         706           0  ...           0   
    1          1976          1976         978           0  ...         298   
    2          2001          2002         486           0  ...           0   
    3          1915          1970         216           0  ...           0   
    4          2000          2000         655           0  ...         192   
    ...         ...           ...         ...         ...  ...         ...   
    1455       1999          2000           0           0  ...           0   
    1456       1978          1988         790         163  ...         349   
    1457       1941          2006         275           0  ...           0   
    1458       1950          1996          49        1029  ...         366   
    1459       1965          1965         830         290  ...         736   
    
          OpenPorchSF  EnclosedPorch  3SsnPorch  ScreenPorch  PoolArea  MiscVal  \
    0              61              0          0            0         0        0   
    1               0              0          0            0         0        0   
    2              42              0          0            0         0        0   
    3              35            272          0            0         0        0   
    4              84              0          0            0         0        0   
    ...           ...            ...        ...          ...       ...      ...   
    1455           40              0          0            0         0        0   
    1456            0              0          0            0         0        0   
    1457           60              0          0            0         0     2500   
    1458            0            112          0            0         0        0   
    1459           68              0          0            0         0        0   
    
          MoSold  YrSold  SalePrice  
    0          2    2008     208500  
    1          5    2007     181500  
    2          9    2008     223500  
    3          2    2006     140000  
    4         12    2008     250000  
    ...      ...     ...        ...  
    1455       8    2007     175000  
    1456       2    2010     210000  
    1457       5    2010     266500  
    1458       4    2010     142125  
    1459       6    2008     147500  
    
    [1460 rows x 36 columns]
    


```python
numeric_df.head()
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>OverallQual</th>
      <th>OverallCond</th>
      <th>YearBuilt</th>
      <th>YearRemodAdd</th>
      <th>BsmtFinSF1</th>
      <th>BsmtFinSF2</th>
      <th>...</th>
      <th>WoodDeckSF</th>
      <th>OpenPorchSF</th>
      <th>EnclosedPorch</th>
      <th>3SsnPorch</th>
      <th>ScreenPorch</th>
      <th>PoolArea</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
      <td>65.0</td>
      <td>8450</td>
      <td>7</td>
      <td>5</td>
      <td>2003</td>
      <td>2003</td>
      <td>706</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>61</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2008</td>
      <td>208500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>20</td>
      <td>80.0</td>
      <td>9600</td>
      <td>6</td>
      <td>8</td>
      <td>1976</td>
      <td>1976</td>
      <td>978</td>
      <td>0</td>
      <td>...</td>
      <td>298</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>2007</td>
      <td>181500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>60</td>
      <td>68.0</td>
      <td>11250</td>
      <td>7</td>
      <td>5</td>
      <td>2001</td>
      <td>2002</td>
      <td>486</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>42</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>9</td>
      <td>2008</td>
      <td>223500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>70</td>
      <td>60.0</td>
      <td>9550</td>
      <td>7</td>
      <td>5</td>
      <td>1915</td>
      <td>1970</td>
      <td>216</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>35</td>
      <td>272</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2006</td>
      <td>140000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>60</td>
      <td>84.0</td>
      <td>14260</td>
      <td>8</td>
      <td>5</td>
      <td>2000</td>
      <td>2000</td>
      <td>655</td>
      <td>0</td>
      <td>...</td>
      <td>192</td>
      <td>84</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>12</td>
      <td>2008</td>
      <td>250000</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 36 columns</p>
</div>




```python
numeric_df.isnull().values.any() #missing values bingo! No missing values
```




    False




```python
numeric_df.columns
```




    Index(['Id', 'MSSubClass', 'LotFrontage', 'LotArea', 'OverallQual',
           'OverallCond', 'YearBuilt', 'YearRemodAdd', 'BsmtFinSF1', 'BsmtFinSF2',
           'BsmtUnfSF', 'TotalBsmtSF', '1stFlrSF', '2ndFlrSF', 'LowQualFinSF',
           'GrLivArea', 'BsmtFullBath', 'BsmtHalfBath', 'FullBath', 'HalfBath',
           'BedroomAbvGr', 'KitchenAbvGr', 'TotRmsAbvGrd', 'Fireplaces',
           'GarageCars', 'GarageArea', 'WoodDeckSF', 'OpenPorchSF',
           'EnclosedPorch', '3SsnPorch', 'ScreenPorch', 'PoolArea', 'MiscVal',
           'MoSold', 'YrSold', 'SalePrice'],
          dtype='object')




```python
numeric_df.corr()
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>OverallQual</th>
      <th>OverallCond</th>
      <th>YearBuilt</th>
      <th>YearRemodAdd</th>
      <th>BsmtFinSF1</th>
      <th>BsmtFinSF2</th>
      <th>...</th>
      <th>WoodDeckSF</th>
      <th>OpenPorchSF</th>
      <th>EnclosedPorch</th>
      <th>3SsnPorch</th>
      <th>ScreenPorch</th>
      <th>PoolArea</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Id</th>
      <td>1.000000</td>
      <td>0.011156</td>
      <td>-0.009601</td>
      <td>-0.033226</td>
      <td>-0.028365</td>
      <td>0.012609</td>
      <td>-0.012713</td>
      <td>-0.021998</td>
      <td>-0.005024</td>
      <td>-0.005968</td>
      <td>...</td>
      <td>-0.029643</td>
      <td>-0.000477</td>
      <td>0.002889</td>
      <td>-0.046635</td>
      <td>0.001330</td>
      <td>0.057044</td>
      <td>-0.006242</td>
      <td>0.021172</td>
      <td>0.000712</td>
      <td>-0.021917</td>
    </tr>
    <tr>
      <th>MSSubClass</th>
      <td>0.011156</td>
      <td>1.000000</td>
      <td>-0.357056</td>
      <td>-0.139781</td>
      <td>0.032628</td>
      <td>-0.059316</td>
      <td>0.027850</td>
      <td>0.040581</td>
      <td>-0.069836</td>
      <td>-0.065649</td>
      <td>...</td>
      <td>-0.012579</td>
      <td>-0.006100</td>
      <td>-0.012037</td>
      <td>-0.043825</td>
      <td>-0.026030</td>
      <td>0.008283</td>
      <td>-0.007683</td>
      <td>-0.013585</td>
      <td>-0.021407</td>
      <td>-0.084284</td>
    </tr>
    <tr>
      <th>LotFrontage</th>
      <td>-0.009601</td>
      <td>-0.357056</td>
      <td>1.000000</td>
      <td>0.306795</td>
      <td>0.234196</td>
      <td>-0.052820</td>
      <td>0.117598</td>
      <td>0.082746</td>
      <td>0.215828</td>
      <td>0.043340</td>
      <td>...</td>
      <td>0.077106</td>
      <td>0.137454</td>
      <td>0.009790</td>
      <td>0.062335</td>
      <td>0.037684</td>
      <td>0.180868</td>
      <td>0.001168</td>
      <td>0.010158</td>
      <td>0.006768</td>
      <td>0.334901</td>
    </tr>
    <tr>
      <th>LotArea</th>
      <td>-0.033226</td>
      <td>-0.139781</td>
      <td>0.306795</td>
      <td>1.000000</td>
      <td>0.105806</td>
      <td>-0.005636</td>
      <td>0.014228</td>
      <td>0.013788</td>
      <td>0.214103</td>
      <td>0.111170</td>
      <td>...</td>
      <td>0.171698</td>
      <td>0.084774</td>
      <td>-0.018340</td>
      <td>0.020423</td>
      <td>0.043160</td>
      <td>0.077672</td>
      <td>0.038068</td>
      <td>0.001205</td>
      <td>-0.014261</td>
      <td>0.263843</td>
    </tr>
    <tr>
      <th>OverallQual</th>
      <td>-0.028365</td>
      <td>0.032628</td>
      <td>0.234196</td>
      <td>0.105806</td>
      <td>1.000000</td>
      <td>-0.091932</td>
      <td>0.572323</td>
      <td>0.550684</td>
      <td>0.239666</td>
      <td>-0.059119</td>
      <td>...</td>
      <td>0.238923</td>
      <td>0.308819</td>
      <td>-0.113937</td>
      <td>0.030371</td>
      <td>0.064886</td>
      <td>0.065166</td>
      <td>-0.031406</td>
      <td>0.070815</td>
      <td>-0.027347</td>
      <td>0.790982</td>
    </tr>
    <tr>
      <th>OverallCond</th>
      <td>0.012609</td>
      <td>-0.059316</td>
      <td>-0.052820</td>
      <td>-0.005636</td>
      <td>-0.091932</td>
      <td>1.000000</td>
      <td>-0.375983</td>
      <td>0.073741</td>
      <td>-0.046231</td>
      <td>0.040229</td>
      <td>...</td>
      <td>-0.003334</td>
      <td>-0.032589</td>
      <td>0.070356</td>
      <td>0.025504</td>
      <td>0.054811</td>
      <td>-0.001985</td>
      <td>0.068777</td>
      <td>-0.003511</td>
      <td>0.043950</td>
      <td>-0.077856</td>
    </tr>
    <tr>
      <th>YearBuilt</th>
      <td>-0.012713</td>
      <td>0.027850</td>
      <td>0.117598</td>
      <td>0.014228</td>
      <td>0.572323</td>
      <td>-0.375983</td>
      <td>1.000000</td>
      <td>0.592855</td>
      <td>0.249503</td>
      <td>-0.049107</td>
      <td>...</td>
      <td>0.224880</td>
      <td>0.188686</td>
      <td>-0.387268</td>
      <td>0.031355</td>
      <td>-0.050364</td>
      <td>0.004950</td>
      <td>-0.034383</td>
      <td>0.012398</td>
      <td>-0.013618</td>
      <td>0.522897</td>
    </tr>
    <tr>
      <th>YearRemodAdd</th>
      <td>-0.021998</td>
      <td>0.040581</td>
      <td>0.082746</td>
      <td>0.013788</td>
      <td>0.550684</td>
      <td>0.073741</td>
      <td>0.592855</td>
      <td>1.000000</td>
      <td>0.128451</td>
      <td>-0.067759</td>
      <td>...</td>
      <td>0.205726</td>
      <td>0.226298</td>
      <td>-0.193919</td>
      <td>0.045286</td>
      <td>-0.038740</td>
      <td>0.005829</td>
      <td>-0.010286</td>
      <td>0.021490</td>
      <td>0.035743</td>
      <td>0.507101</td>
    </tr>
    <tr>
      <th>BsmtFinSF1</th>
      <td>-0.005024</td>
      <td>-0.069836</td>
      <td>0.215828</td>
      <td>0.214103</td>
      <td>0.239666</td>
      <td>-0.046231</td>
      <td>0.249503</td>
      <td>0.128451</td>
      <td>1.000000</td>
      <td>-0.050117</td>
      <td>...</td>
      <td>0.204306</td>
      <td>0.111761</td>
      <td>-0.102303</td>
      <td>0.026451</td>
      <td>0.062021</td>
      <td>0.140491</td>
      <td>0.003571</td>
      <td>-0.015727</td>
      <td>0.014359</td>
      <td>0.386420</td>
    </tr>
    <tr>
      <th>BsmtFinSF2</th>
      <td>-0.005968</td>
      <td>-0.065649</td>
      <td>0.043340</td>
      <td>0.111170</td>
      <td>-0.059119</td>
      <td>0.040229</td>
      <td>-0.049107</td>
      <td>-0.067759</td>
      <td>-0.050117</td>
      <td>1.000000</td>
      <td>...</td>
      <td>0.067898</td>
      <td>0.003093</td>
      <td>0.036543</td>
      <td>-0.029993</td>
      <td>0.088871</td>
      <td>0.041709</td>
      <td>0.004940</td>
      <td>-0.015211</td>
      <td>0.031706</td>
      <td>-0.011378</td>
    </tr>
    <tr>
      <th>BsmtUnfSF</th>
      <td>-0.007940</td>
      <td>-0.140759</td>
      <td>0.122156</td>
      <td>-0.002618</td>
      <td>0.308159</td>
      <td>-0.136841</td>
      <td>0.149040</td>
      <td>0.181133</td>
      <td>-0.495251</td>
      <td>-0.209294</td>
      <td>...</td>
      <td>-0.005316</td>
      <td>0.129005</td>
      <td>-0.002538</td>
      <td>0.020764</td>
      <td>-0.012579</td>
      <td>-0.035092</td>
      <td>-0.023837</td>
      <td>0.034888</td>
      <td>-0.041258</td>
      <td>0.214479</td>
    </tr>
    <tr>
      <th>TotalBsmtSF</th>
      <td>-0.015415</td>
      <td>-0.238518</td>
      <td>0.363358</td>
      <td>0.260833</td>
      <td>0.537808</td>
      <td>-0.171098</td>
      <td>0.391452</td>
      <td>0.291066</td>
      <td>0.522396</td>
      <td>0.104810</td>
      <td>...</td>
      <td>0.232019</td>
      <td>0.247264</td>
      <td>-0.095478</td>
      <td>0.037384</td>
      <td>0.084489</td>
      <td>0.126053</td>
      <td>-0.018479</td>
      <td>0.013196</td>
      <td>-0.014969</td>
      <td>0.613581</td>
    </tr>
    <tr>
      <th>1stFlrSF</th>
      <td>0.010496</td>
      <td>-0.251758</td>
      <td>0.414266</td>
      <td>0.299475</td>
      <td>0.476224</td>
      <td>-0.144203</td>
      <td>0.281986</td>
      <td>0.240379</td>
      <td>0.445863</td>
      <td>0.097117</td>
      <td>...</td>
      <td>0.235459</td>
      <td>0.211671</td>
      <td>-0.065292</td>
      <td>0.056104</td>
      <td>0.088758</td>
      <td>0.131525</td>
      <td>-0.021096</td>
      <td>0.031372</td>
      <td>-0.013604</td>
      <td>0.605852</td>
    </tr>
    <tr>
      <th>2ndFlrSF</th>
      <td>0.005590</td>
      <td>0.307886</td>
      <td>0.072483</td>
      <td>0.050986</td>
      <td>0.295493</td>
      <td>0.028942</td>
      <td>0.010308</td>
      <td>0.140024</td>
      <td>-0.137079</td>
      <td>-0.099260</td>
      <td>...</td>
      <td>0.092165</td>
      <td>0.208026</td>
      <td>0.061989</td>
      <td>-0.024358</td>
      <td>0.040606</td>
      <td>0.081487</td>
      <td>0.016197</td>
      <td>0.035164</td>
      <td>-0.028700</td>
      <td>0.319334</td>
    </tr>
    <tr>
      <th>LowQualFinSF</th>
      <td>-0.044230</td>
      <td>0.046474</td>
      <td>0.036849</td>
      <td>0.004779</td>
      <td>-0.030429</td>
      <td>0.025494</td>
      <td>-0.183784</td>
      <td>-0.062419</td>
      <td>-0.064503</td>
      <td>0.014807</td>
      <td>...</td>
      <td>-0.025444</td>
      <td>0.018251</td>
      <td>0.061081</td>
      <td>-0.004296</td>
      <td>0.026799</td>
      <td>0.062157</td>
      <td>-0.003793</td>
      <td>-0.022174</td>
      <td>-0.028921</td>
      <td>-0.025606</td>
    </tr>
    <tr>
      <th>GrLivArea</th>
      <td>0.008273</td>
      <td>0.074853</td>
      <td>0.368392</td>
      <td>0.263116</td>
      <td>0.593007</td>
      <td>-0.079686</td>
      <td>0.199010</td>
      <td>0.287389</td>
      <td>0.208171</td>
      <td>-0.009640</td>
      <td>...</td>
      <td>0.247433</td>
      <td>0.330224</td>
      <td>0.009113</td>
      <td>0.020643</td>
      <td>0.101510</td>
      <td>0.170205</td>
      <td>-0.002416</td>
      <td>0.050240</td>
      <td>-0.036526</td>
      <td>0.708624</td>
    </tr>
    <tr>
      <th>BsmtFullBath</th>
      <td>0.002289</td>
      <td>0.003491</td>
      <td>0.091481</td>
      <td>0.158155</td>
      <td>0.111098</td>
      <td>-0.054942</td>
      <td>0.187599</td>
      <td>0.119470</td>
      <td>0.649212</td>
      <td>0.158678</td>
      <td>...</td>
      <td>0.175315</td>
      <td>0.067341</td>
      <td>-0.049911</td>
      <td>-0.000106</td>
      <td>0.023148</td>
      <td>0.067616</td>
      <td>-0.023047</td>
      <td>-0.025361</td>
      <td>0.067049</td>
      <td>0.227122</td>
    </tr>
    <tr>
      <th>BsmtHalfBath</th>
      <td>-0.020155</td>
      <td>-0.002333</td>
      <td>-0.006419</td>
      <td>0.048046</td>
      <td>-0.040150</td>
      <td>0.117821</td>
      <td>-0.038162</td>
      <td>-0.012337</td>
      <td>0.067418</td>
      <td>0.070948</td>
      <td>...</td>
      <td>0.040161</td>
      <td>-0.025324</td>
      <td>-0.008555</td>
      <td>0.035114</td>
      <td>0.032121</td>
      <td>0.020025</td>
      <td>-0.007367</td>
      <td>0.032873</td>
      <td>-0.046524</td>
      <td>-0.016844</td>
    </tr>
    <tr>
      <th>FullBath</th>
      <td>0.005587</td>
      <td>0.131608</td>
      <td>0.180424</td>
      <td>0.126031</td>
      <td>0.550600</td>
      <td>-0.194149</td>
      <td>0.468271</td>
      <td>0.439046</td>
      <td>0.058543</td>
      <td>-0.076444</td>
      <td>...</td>
      <td>0.187703</td>
      <td>0.259977</td>
      <td>-0.115093</td>
      <td>0.035353</td>
      <td>-0.008106</td>
      <td>0.049604</td>
      <td>-0.014290</td>
      <td>0.055872</td>
      <td>-0.019669</td>
      <td>0.560664</td>
    </tr>
    <tr>
      <th>HalfBath</th>
      <td>0.006784</td>
      <td>0.177354</td>
      <td>0.048258</td>
      <td>0.014259</td>
      <td>0.273458</td>
      <td>-0.060769</td>
      <td>0.242656</td>
      <td>0.183331</td>
      <td>0.004262</td>
      <td>-0.032148</td>
      <td>...</td>
      <td>0.108080</td>
      <td>0.199740</td>
      <td>-0.095317</td>
      <td>-0.004972</td>
      <td>0.072426</td>
      <td>0.022381</td>
      <td>0.001290</td>
      <td>-0.009050</td>
      <td>-0.010269</td>
      <td>0.284108</td>
    </tr>
    <tr>
      <th>BedroomAbvGr</th>
      <td>0.037719</td>
      <td>-0.023438</td>
      <td>0.237023</td>
      <td>0.119690</td>
      <td>0.101676</td>
      <td>0.012980</td>
      <td>-0.070651</td>
      <td>-0.040581</td>
      <td>-0.107355</td>
      <td>-0.015728</td>
      <td>...</td>
      <td>0.046854</td>
      <td>0.093810</td>
      <td>0.041570</td>
      <td>-0.024478</td>
      <td>0.044300</td>
      <td>0.070703</td>
      <td>0.007767</td>
      <td>0.046544</td>
      <td>-0.036014</td>
      <td>0.168213</td>
    </tr>
    <tr>
      <th>KitchenAbvGr</th>
      <td>0.002951</td>
      <td>0.281721</td>
      <td>-0.005805</td>
      <td>-0.017784</td>
      <td>-0.183882</td>
      <td>-0.087001</td>
      <td>-0.174800</td>
      <td>-0.149598</td>
      <td>-0.081007</td>
      <td>-0.040751</td>
      <td>...</td>
      <td>-0.090130</td>
      <td>-0.070091</td>
      <td>0.037312</td>
      <td>-0.024600</td>
      <td>-0.051613</td>
      <td>-0.014525</td>
      <td>0.062341</td>
      <td>0.026589</td>
      <td>0.031687</td>
      <td>-0.135907</td>
    </tr>
    <tr>
      <th>TotRmsAbvGrd</th>
      <td>0.027239</td>
      <td>0.040380</td>
      <td>0.320146</td>
      <td>0.190015</td>
      <td>0.427452</td>
      <td>-0.057583</td>
      <td>0.095589</td>
      <td>0.191740</td>
      <td>0.044316</td>
      <td>-0.035227</td>
      <td>...</td>
      <td>0.165984</td>
      <td>0.234192</td>
      <td>0.004151</td>
      <td>-0.006683</td>
      <td>0.059383</td>
      <td>0.083757</td>
      <td>0.024763</td>
      <td>0.036907</td>
      <td>-0.034516</td>
      <td>0.533723</td>
    </tr>
    <tr>
      <th>Fireplaces</th>
      <td>-0.019772</td>
      <td>-0.045569</td>
      <td>0.235755</td>
      <td>0.271364</td>
      <td>0.396765</td>
      <td>-0.023820</td>
      <td>0.147716</td>
      <td>0.112581</td>
      <td>0.260011</td>
      <td>0.046921</td>
      <td>...</td>
      <td>0.200019</td>
      <td>0.169405</td>
      <td>-0.024822</td>
      <td>0.011257</td>
      <td>0.184530</td>
      <td>0.095074</td>
      <td>0.001409</td>
      <td>0.046357</td>
      <td>-0.024096</td>
      <td>0.466929</td>
    </tr>
    <tr>
      <th>GarageCars</th>
      <td>0.016570</td>
      <td>-0.040110</td>
      <td>0.269729</td>
      <td>0.154871</td>
      <td>0.600671</td>
      <td>-0.185758</td>
      <td>0.537850</td>
      <td>0.420622</td>
      <td>0.224054</td>
      <td>-0.038264</td>
      <td>...</td>
      <td>0.226342</td>
      <td>0.213569</td>
      <td>-0.151434</td>
      <td>0.035765</td>
      <td>0.050494</td>
      <td>0.020934</td>
      <td>-0.043080</td>
      <td>0.040522</td>
      <td>-0.039117</td>
      <td>0.640409</td>
    </tr>
    <tr>
      <th>GarageArea</th>
      <td>0.017634</td>
      <td>-0.098672</td>
      <td>0.323663</td>
      <td>0.180403</td>
      <td>0.562022</td>
      <td>-0.151521</td>
      <td>0.478954</td>
      <td>0.371600</td>
      <td>0.296970</td>
      <td>-0.018227</td>
      <td>...</td>
      <td>0.224666</td>
      <td>0.241435</td>
      <td>-0.121777</td>
      <td>0.035087</td>
      <td>0.051412</td>
      <td>0.061047</td>
      <td>-0.027400</td>
      <td>0.027974</td>
      <td>-0.027378</td>
      <td>0.623431</td>
    </tr>
    <tr>
      <th>WoodDeckSF</th>
      <td>-0.029643</td>
      <td>-0.012579</td>
      <td>0.077106</td>
      <td>0.171698</td>
      <td>0.238923</td>
      <td>-0.003334</td>
      <td>0.224880</td>
      <td>0.205726</td>
      <td>0.204306</td>
      <td>0.067898</td>
      <td>...</td>
      <td>1.000000</td>
      <td>0.058661</td>
      <td>-0.125989</td>
      <td>-0.032771</td>
      <td>-0.074181</td>
      <td>0.073378</td>
      <td>-0.009551</td>
      <td>0.021011</td>
      <td>0.022270</td>
      <td>0.324413</td>
    </tr>
    <tr>
      <th>OpenPorchSF</th>
      <td>-0.000477</td>
      <td>-0.006100</td>
      <td>0.137454</td>
      <td>0.084774</td>
      <td>0.308819</td>
      <td>-0.032589</td>
      <td>0.188686</td>
      <td>0.226298</td>
      <td>0.111761</td>
      <td>0.003093</td>
      <td>...</td>
      <td>0.058661</td>
      <td>1.000000</td>
      <td>-0.093079</td>
      <td>-0.005842</td>
      <td>0.074304</td>
      <td>0.060762</td>
      <td>-0.018584</td>
      <td>0.071255</td>
      <td>-0.057619</td>
      <td>0.315856</td>
    </tr>
    <tr>
      <th>EnclosedPorch</th>
      <td>0.002889</td>
      <td>-0.012037</td>
      <td>0.009790</td>
      <td>-0.018340</td>
      <td>-0.113937</td>
      <td>0.070356</td>
      <td>-0.387268</td>
      <td>-0.193919</td>
      <td>-0.102303</td>
      <td>0.036543</td>
      <td>...</td>
      <td>-0.125989</td>
      <td>-0.093079</td>
      <td>1.000000</td>
      <td>-0.037305</td>
      <td>-0.082864</td>
      <td>0.054203</td>
      <td>0.018361</td>
      <td>-0.028887</td>
      <td>-0.009916</td>
      <td>-0.128578</td>
    </tr>
    <tr>
      <th>3SsnPorch</th>
      <td>-0.046635</td>
      <td>-0.043825</td>
      <td>0.062335</td>
      <td>0.020423</td>
      <td>0.030371</td>
      <td>0.025504</td>
      <td>0.031355</td>
      <td>0.045286</td>
      <td>0.026451</td>
      <td>-0.029993</td>
      <td>...</td>
      <td>-0.032771</td>
      <td>-0.005842</td>
      <td>-0.037305</td>
      <td>1.000000</td>
      <td>-0.031436</td>
      <td>-0.007992</td>
      <td>0.000354</td>
      <td>0.029474</td>
      <td>0.018645</td>
      <td>0.044584</td>
    </tr>
    <tr>
      <th>ScreenPorch</th>
      <td>0.001330</td>
      <td>-0.026030</td>
      <td>0.037684</td>
      <td>0.043160</td>
      <td>0.064886</td>
      <td>0.054811</td>
      <td>-0.050364</td>
      <td>-0.038740</td>
      <td>0.062021</td>
      <td>0.088871</td>
      <td>...</td>
      <td>-0.074181</td>
      <td>0.074304</td>
      <td>-0.082864</td>
      <td>-0.031436</td>
      <td>1.000000</td>
      <td>0.051307</td>
      <td>0.031946</td>
      <td>0.023217</td>
      <td>0.010694</td>
      <td>0.111447</td>
    </tr>
    <tr>
      <th>PoolArea</th>
      <td>0.057044</td>
      <td>0.008283</td>
      <td>0.180868</td>
      <td>0.077672</td>
      <td>0.065166</td>
      <td>-0.001985</td>
      <td>0.004950</td>
      <td>0.005829</td>
      <td>0.140491</td>
      <td>0.041709</td>
      <td>...</td>
      <td>0.073378</td>
      <td>0.060762</td>
      <td>0.054203</td>
      <td>-0.007992</td>
      <td>0.051307</td>
      <td>1.000000</td>
      <td>0.029669</td>
      <td>-0.033737</td>
      <td>-0.059689</td>
      <td>0.092404</td>
    </tr>
    <tr>
      <th>MiscVal</th>
      <td>-0.006242</td>
      <td>-0.007683</td>
      <td>0.001168</td>
      <td>0.038068</td>
      <td>-0.031406</td>
      <td>0.068777</td>
      <td>-0.034383</td>
      <td>-0.010286</td>
      <td>0.003571</td>
      <td>0.004940</td>
      <td>...</td>
      <td>-0.009551</td>
      <td>-0.018584</td>
      <td>0.018361</td>
      <td>0.000354</td>
      <td>0.031946</td>
      <td>0.029669</td>
      <td>1.000000</td>
      <td>-0.006495</td>
      <td>0.004906</td>
      <td>-0.021190</td>
    </tr>
    <tr>
      <th>MoSold</th>
      <td>0.021172</td>
      <td>-0.013585</td>
      <td>0.010158</td>
      <td>0.001205</td>
      <td>0.070815</td>
      <td>-0.003511</td>
      <td>0.012398</td>
      <td>0.021490</td>
      <td>-0.015727</td>
      <td>-0.015211</td>
      <td>...</td>
      <td>0.021011</td>
      <td>0.071255</td>
      <td>-0.028887</td>
      <td>0.029474</td>
      <td>0.023217</td>
      <td>-0.033737</td>
      <td>-0.006495</td>
      <td>1.000000</td>
      <td>-0.145721</td>
      <td>0.046432</td>
    </tr>
    <tr>
      <th>YrSold</th>
      <td>0.000712</td>
      <td>-0.021407</td>
      <td>0.006768</td>
      <td>-0.014261</td>
      <td>-0.027347</td>
      <td>0.043950</td>
      <td>-0.013618</td>
      <td>0.035743</td>
      <td>0.014359</td>
      <td>0.031706</td>
      <td>...</td>
      <td>0.022270</td>
      <td>-0.057619</td>
      <td>-0.009916</td>
      <td>0.018645</td>
      <td>0.010694</td>
      <td>-0.059689</td>
      <td>0.004906</td>
      <td>-0.145721</td>
      <td>1.000000</td>
      <td>-0.028923</td>
    </tr>
    <tr>
      <th>SalePrice</th>
      <td>-0.021917</td>
      <td>-0.084284</td>
      <td>0.334901</td>
      <td>0.263843</td>
      <td>0.790982</td>
      <td>-0.077856</td>
      <td>0.522897</td>
      <td>0.507101</td>
      <td>0.386420</td>
      <td>-0.011378</td>
      <td>...</td>
      <td>0.324413</td>
      <td>0.315856</td>
      <td>-0.128578</td>
      <td>0.044584</td>
      <td>0.111447</td>
      <td>0.092404</td>
      <td>-0.021190</td>
      <td>0.046432</td>
      <td>-0.028923</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
<p>36 rows × 36 columns</p>
</div>




```python
sns.heatmap(numeric_df.corr())
```




    <Axes: >




    
![png](output_40_1.png)
    



```python
plt.figure(figsize=(12,6))
sns.heatmap(numeric_df.corr(),annot=True)
```




    <Axes: >




    
![png](output_41_1.png)
    



```python
plt.figure(figsize=(14, 10))
sns.set(font_scale=0.8)
heatmap = sns.heatmap(numeric_df.corr(), annot=True, cmap='bwr', xticklabels=numeric_df.corr().columns, yticklabels=numeric_df.corr().columns, fmt='.2g')
heatmap.set_xticklabels(heatmap.get_xticklabels(), rotation=45, ha='right')
plt.show()
```


    
![png](output_42_0.png)
    



```python
plt.figure(figsize=(14, 10))
sns.set(font_scale=0.8)
heatmap = sns.heatmap(numeric_df.corr(), annot=True, cmap='bwr', xticklabels=numeric_df.corr().columns, yticklabels=numeric_df.corr().columns, fmt='.2g')
heatmap.set_xticklabels(heatmap.get_xticklabels(), rotation=45, ha='right')
plt.show()
```


    
![png](output_43_0.png)
    



```python
plt.figure(figsize=(14, 10))
sns.set(font_scale=0.8)
heatmap = sns.heatmap(numeric_df.corr(), annot=True, cmap='coolwarm', xticklabels=numeric_df.corr().columns, yticklabels=numeric_df.corr().columns, fmt='.2g', vmin=-1, vmax=1)
heatmap.set_xticklabels(heatmap.get_xticklabels(), rotation=45, ha='right')
heatmap.set_yticklabels(heatmap.get_yticklabels(), rotation=0, ha='right')
heatmap.tick_params(axis='both', which='major', pad=2)
plt.show()
```


    
![png](output_44_0.png)
    



```python
sns.distplot(numeric_df['SalePrice'])
```

#### Training the model


```python
numeric_df.head()
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>OverallQual</th>
      <th>OverallCond</th>
      <th>YearBuilt</th>
      <th>YearRemodAdd</th>
      <th>BsmtFinSF1</th>
      <th>BsmtFinSF2</th>
      <th>...</th>
      <th>WoodDeckSF</th>
      <th>OpenPorchSF</th>
      <th>EnclosedPorch</th>
      <th>3SsnPorch</th>
      <th>ScreenPorch</th>
      <th>PoolArea</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
      <td>65.0</td>
      <td>8450</td>
      <td>7</td>
      <td>5</td>
      <td>2003</td>
      <td>2003</td>
      <td>706</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>61</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2008</td>
      <td>208500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>20</td>
      <td>80.0</td>
      <td>9600</td>
      <td>6</td>
      <td>8</td>
      <td>1976</td>
      <td>1976</td>
      <td>978</td>
      <td>0</td>
      <td>...</td>
      <td>298</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>2007</td>
      <td>181500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>60</td>
      <td>68.0</td>
      <td>11250</td>
      <td>7</td>
      <td>5</td>
      <td>2001</td>
      <td>2002</td>
      <td>486</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>42</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>9</td>
      <td>2008</td>
      <td>223500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>70</td>
      <td>60.0</td>
      <td>9550</td>
      <td>7</td>
      <td>5</td>
      <td>1915</td>
      <td>1970</td>
      <td>216</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>35</td>
      <td>272</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2006</td>
      <td>140000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>60</td>
      <td>84.0</td>
      <td>14260</td>
      <td>8</td>
      <td>5</td>
      <td>2000</td>
      <td>2000</td>
      <td>655</td>
      <td>0</td>
      <td>...</td>
      <td>192</td>
      <td>84</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>12</td>
      <td>2008</td>
      <td>250000</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 36 columns</p>
</div>




```python
# first, separate all the columns from SalePrice column
```


```python
#Lets create a col df
numeric_df.columns
```




    Index(['Id', 'MSSubClass', 'LotFrontage', 'LotArea', 'OverallQual',
           'OverallCond', 'YearBuilt', 'YearRemodAdd', 'BsmtFinSF1', 'BsmtFinSF2',
           'BsmtUnfSF', 'TotalBsmtSF', '1stFlrSF', '2ndFlrSF', 'LowQualFinSF',
           'GrLivArea', 'BsmtFullBath', 'BsmtHalfBath', 'FullBath', 'HalfBath',
           'BedroomAbvGr', 'KitchenAbvGr', 'TotRmsAbvGrd', 'Fireplaces',
           'GarageCars', 'GarageArea', 'WoodDeckSF', 'OpenPorchSF',
           'EnclosedPorch', '3SsnPorch', 'ScreenPorch', 'PoolArea', 'MiscVal',
           'MoSold', 'YrSold', 'SalePrice'],
          dtype='object')




```python
#df columns
X = numeric_df[['Id', 'MSSubClass', 'LotFrontage', 'LotArea', 'OverallQual',
       'OverallCond', 'YearBuilt', 'YearRemodAdd', 'BsmtFinSF1', 'BsmtFinSF2',
       'BsmtUnfSF', 'TotalBsmtSF', '1stFlrSF', '2ndFlrSF', 'LowQualFinSF',
       'GrLivArea', 'BsmtFullBath', 'BsmtHalfBath', 'FullBath', 'HalfBath',
       'BedroomAbvGr', 'KitchenAbvGr', 'TotRmsAbvGrd', 'Fireplaces',
       'GarageCars', 'GarageArea', 'WoodDeckSF', 'OpenPorchSF',
       'EnclosedPorch', '3SsnPorch', 'ScreenPorch', 'PoolArea', 'MiscVal',
       'MoSold', 'YrSold']]
```


```python
# y is the target 
y = numeric_df[['SalePrice']]
```


```python
#### Split the data  into two set = training and testing 
```


```python
from sklearn.model_selection import train_test_split
```


```python
# >>> X_train, X_test, y_train, y_test = train_test_split(
# ...     X, y, test_size=0.33, random_state=42)
X_train, X_test, y_train, y_test = train_test_split(X,y,test_size=0.33) # 0.33 person / X variable feature / y the target
X_test #random, its means everytime that we run dif values
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>OverallQual</th>
      <th>OverallCond</th>
      <th>YearBuilt</th>
      <th>YearRemodAdd</th>
      <th>BsmtFinSF1</th>
      <th>BsmtFinSF2</th>
      <th>...</th>
      <th>GarageArea</th>
      <th>WoodDeckSF</th>
      <th>OpenPorchSF</th>
      <th>EnclosedPorch</th>
      <th>3SsnPorch</th>
      <th>ScreenPorch</th>
      <th>PoolArea</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1458</th>
      <td>1459</td>
      <td>20</td>
      <td>68.000000</td>
      <td>9717</td>
      <td>5</td>
      <td>6</td>
      <td>1950</td>
      <td>1996</td>
      <td>49</td>
      <td>1029</td>
      <td>...</td>
      <td>240</td>
      <td>366</td>
      <td>0</td>
      <td>112</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>546</th>
      <td>547</td>
      <td>50</td>
      <td>70.000000</td>
      <td>8737</td>
      <td>6</td>
      <td>7</td>
      <td>1923</td>
      <td>1950</td>
      <td>300</td>
      <td>0</td>
      <td>...</td>
      <td>440</td>
      <td>0</td>
      <td>38</td>
      <td>0</td>
      <td>144</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>1184</th>
      <td>1185</td>
      <td>20</td>
      <td>50.000000</td>
      <td>35133</td>
      <td>5</td>
      <td>4</td>
      <td>1963</td>
      <td>1963</td>
      <td>1159</td>
      <td>0</td>
      <td>...</td>
      <td>995</td>
      <td>0</td>
      <td>263</td>
      <td>0</td>
      <td>0</td>
      <td>263</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>1100</th>
      <td>1101</td>
      <td>30</td>
      <td>60.000000</td>
      <td>8400</td>
      <td>2</td>
      <td>5</td>
      <td>1920</td>
      <td>1950</td>
      <td>290</td>
      <td>0</td>
      <td>...</td>
      <td>246</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>1145</th>
      <td>1146</td>
      <td>50</td>
      <td>52.000000</td>
      <td>6240</td>
      <td>5</td>
      <td>6</td>
      <td>1928</td>
      <td>1950</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>225</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>8</td>
      <td>2006</td>
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
    </tr>
    <tr>
      <th>1383</th>
      <td>1384</td>
      <td>30</td>
      <td>70.049958</td>
      <td>25339</td>
      <td>5</td>
      <td>7</td>
      <td>1918</td>
      <td>2007</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>576</td>
      <td>0</td>
      <td>0</td>
      <td>112</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>8</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>1451</th>
      <td>1452</td>
      <td>20</td>
      <td>78.000000</td>
      <td>9262</td>
      <td>8</td>
      <td>5</td>
      <td>2008</td>
      <td>2009</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>840</td>
      <td>0</td>
      <td>36</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>1273</th>
      <td>1274</td>
      <td>80</td>
      <td>124.000000</td>
      <td>11512</td>
      <td>6</td>
      <td>7</td>
      <td>1959</td>
      <td>2006</td>
      <td>719</td>
      <td>0</td>
      <td>...</td>
      <td>312</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>163</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>2008</td>
    </tr>
    <tr>
      <th>208</th>
      <td>209</td>
      <td>60</td>
      <td>70.049958</td>
      <td>14364</td>
      <td>7</td>
      <td>5</td>
      <td>1988</td>
      <td>1989</td>
      <td>1065</td>
      <td>0</td>
      <td>...</td>
      <td>454</td>
      <td>60</td>
      <td>55</td>
      <td>0</td>
      <td>0</td>
      <td>154</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>763</th>
      <td>764</td>
      <td>60</td>
      <td>82.000000</td>
      <td>9430</td>
      <td>8</td>
      <td>5</td>
      <td>1999</td>
      <td>1999</td>
      <td>1163</td>
      <td>0</td>
      <td>...</td>
      <td>856</td>
      <td>0</td>
      <td>128</td>
      <td>0</td>
      <td>0</td>
      <td>180</td>
      <td>0</td>
      <td>0</td>
      <td>7</td>
      <td>2009</td>
    </tr>
  </tbody>
</table>
<p>482 rows × 35 columns</p>
</div>




```python
#random_state = 100
X_train, X_test, y_train, y_test = train_test_split(X,y,test_size=0.33, random_state=100) # 0.33 person / X variable feature / y the target
X_test #random, its means everytime that we run dif values
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
      <th>Id</th>
      <th>MSSubClass</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>OverallQual</th>
      <th>OverallCond</th>
      <th>YearBuilt</th>
      <th>YearRemodAdd</th>
      <th>BsmtFinSF1</th>
      <th>BsmtFinSF2</th>
      <th>...</th>
      <th>GarageArea</th>
      <th>WoodDeckSF</th>
      <th>OpenPorchSF</th>
      <th>EnclosedPorch</th>
      <th>3SsnPorch</th>
      <th>ScreenPorch</th>
      <th>PoolArea</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1436</th>
      <td>1437</td>
      <td>20</td>
      <td>60.000000</td>
      <td>9000</td>
      <td>4</td>
      <td>6</td>
      <td>1971</td>
      <td>1971</td>
      <td>616</td>
      <td>0</td>
      <td>...</td>
      <td>528</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>57</th>
      <td>58</td>
      <td>60</td>
      <td>89.000000</td>
      <td>11645</td>
      <td>7</td>
      <td>5</td>
      <td>2004</td>
      <td>2004</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>565</td>
      <td>0</td>
      <td>70</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>8</td>
      <td>2006</td>
    </tr>
    <tr>
      <th>780</th>
      <td>781</td>
      <td>20</td>
      <td>63.000000</td>
      <td>7875</td>
      <td>7</td>
      <td>5</td>
      <td>1995</td>
      <td>1996</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>402</td>
      <td>220</td>
      <td>21</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>6</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>382</th>
      <td>383</td>
      <td>60</td>
      <td>79.000000</td>
      <td>9245</td>
      <td>7</td>
      <td>5</td>
      <td>2006</td>
      <td>2006</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>639</td>
      <td>144</td>
      <td>53</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>1170</th>
      <td>1171</td>
      <td>80</td>
      <td>76.000000</td>
      <td>9880</td>
      <td>6</td>
      <td>6</td>
      <td>1977</td>
      <td>1977</td>
      <td>522</td>
      <td>0</td>
      <td>...</td>
      <td>358</td>
      <td>203</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>576</td>
      <td>0</td>
      <td>7</td>
      <td>2008</td>
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
    </tr>
    <tr>
      <th>1037</th>
      <td>1038</td>
      <td>60</td>
      <td>70.049958</td>
      <td>9240</td>
      <td>8</td>
      <td>5</td>
      <td>2001</td>
      <td>2002</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>905</td>
      <td>0</td>
      <td>45</td>
      <td>0</td>
      <td>0</td>
      <td>189</td>
      <td>0</td>
      <td>0</td>
      <td>9</td>
      <td>2008</td>
    </tr>
    <tr>
      <th>106</th>
      <td>107</td>
      <td>30</td>
      <td>60.000000</td>
      <td>10800</td>
      <td>4</td>
      <td>7</td>
      <td>1885</td>
      <td>1995</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>273</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>450</td>
      <td>8</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>1307</th>
      <td>1308</td>
      <td>20</td>
      <td>60.000000</td>
      <td>8072</td>
      <td>5</td>
      <td>5</td>
      <td>1994</td>
      <td>1995</td>
      <td>746</td>
      <td>0</td>
      <td>...</td>
      <td>480</td>
      <td>0</td>
      <td>64</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>876</th>
      <td>877</td>
      <td>20</td>
      <td>94.000000</td>
      <td>25286</td>
      <td>4</td>
      <td>5</td>
      <td>1963</td>
      <td>1963</td>
      <td>633</td>
      <td>0</td>
      <td>...</td>
      <td>648</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>771</th>
      <td>772</td>
      <td>20</td>
      <td>67.000000</td>
      <td>8877</td>
      <td>4</td>
      <td>5</td>
      <td>1951</td>
      <td>1951</td>
      <td>836</td>
      <td>0</td>
      <td>...</td>
      <td>396</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
      <td>2006</td>
    </tr>
  </tbody>
</table>
<p>482 rows × 35 columns</p>
</div>



#### Import the model


```python
from sklearn.linear_model import LinearRegression
```


```python
#create an object of this LR
lr = LinearRegression()
```


```python
#fit the model (most important part)
lr.fit(X,y)
```




<style>#sk-container-id-1 {color: black;}#sk-container-id-1 pre{padding: 0;}#sk-container-id-1 div.sk-toggleable {background-color: white;}#sk-container-id-1 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-1 label.sk-toggleable__label-arrow:before {content: "▸";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-1 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-1 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-1 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: "▾";}#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-1 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-1 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-1 div.sk-parallel-item::after {content: "";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-serial::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-1 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-1 div.sk-item {position: relative;z-index: 1;}#sk-container-id-1 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-1 div.sk-item::before, #sk-container-id-1 div.sk-parallel-item::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-1 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-1 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-1 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-1 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-1 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-1 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-1 div.sk-label-container {text-align: center;}#sk-container-id-1 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-1 div.sk-text-repr-fallback {display: none;}</style><div id="sk-container-id-1" class="sk-top-container"><div class="sk-text-repr-fallback"><pre>LinearRegression()</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden><div class="sk-item"><div class="sk-estimator sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-1" type="checkbox" checked><label for="sk-estimator-id-1" class="sk-toggleable__label sk-toggleable__label-arrow">LinearRegression</label><div class="sk-toggleable__content"><pre>LinearRegression()</pre></div></div></div></div></div>




```python
#check the intercept
lr.intercept_
```




    array([444274.82808234])




```python
#coef
lr.coef_
```




    array([[-1.60947859e+00, -1.71755231e+02, -5.76553799e+01,
             4.12419616e-01,  1.78774986e+04,  4.43539956e+03,
             3.50850687e+02,  1.34851786e+02,  1.19280713e+01,
            -2.74196396e+00,  7.06316233e-01,  9.89242358e+00,
             1.92367543e+01,  1.89583112e+01, -6.00140968e+00,
             3.21936558e+01,  8.49339872e+03,  2.31121702e+03,
             3.37862956e+03, -1.36104959e+03, -1.03561698e+04,
            -1.26787327e+04,  5.18021178e+03,  3.61940345e+03,
             1.06207326e+04,  2.29152474e+00,  2.55130233e+01,
            -5.44230660e+00,  9.27694943e+00,  1.92397302e+01,
             5.72712182e+01, -3.79717537e+01, -9.26896775e-01,
            -1.09914022e+02, -7.28808600e+02]])




```python
# lets create a pandas dataframe from this coef
cdf = pd.DataFrame(lr.coef_.T, index=X.columns, columns=['Coefficient'])
cdf
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
      <th>Coefficient</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Id</th>
      <td>-1.609479</td>
    </tr>
    <tr>
      <th>MSSubClass</th>
      <td>-171.755231</td>
    </tr>
    <tr>
      <th>LotFrontage</th>
      <td>-57.655380</td>
    </tr>
    <tr>
      <th>LotArea</th>
      <td>0.412420</td>
    </tr>
    <tr>
      <th>OverallQual</th>
      <td>17877.498568</td>
    </tr>
    <tr>
      <th>OverallCond</th>
      <td>4435.399561</td>
    </tr>
    <tr>
      <th>YearBuilt</th>
      <td>350.850687</td>
    </tr>
    <tr>
      <th>YearRemodAdd</th>
      <td>134.851786</td>
    </tr>
    <tr>
      <th>BsmtFinSF1</th>
      <td>11.928071</td>
    </tr>
    <tr>
      <th>BsmtFinSF2</th>
      <td>-2.741964</td>
    </tr>
    <tr>
      <th>BsmtUnfSF</th>
      <td>0.706316</td>
    </tr>
    <tr>
      <th>TotalBsmtSF</th>
      <td>9.892424</td>
    </tr>
    <tr>
      <th>1stFlrSF</th>
      <td>19.236754</td>
    </tr>
    <tr>
      <th>2ndFlrSF</th>
      <td>18.958311</td>
    </tr>
    <tr>
      <th>LowQualFinSF</th>
      <td>-6.001410</td>
    </tr>
    <tr>
      <th>GrLivArea</th>
      <td>32.193656</td>
    </tr>
    <tr>
      <th>BsmtFullBath</th>
      <td>8493.398717</td>
    </tr>
    <tr>
      <th>BsmtHalfBath</th>
      <td>2311.217019</td>
    </tr>
    <tr>
      <th>FullBath</th>
      <td>3378.629562</td>
    </tr>
    <tr>
      <th>HalfBath</th>
      <td>-1361.049587</td>
    </tr>
    <tr>
      <th>BedroomAbvGr</th>
      <td>-10356.169849</td>
    </tr>
    <tr>
      <th>KitchenAbvGr</th>
      <td>-12678.732743</td>
    </tr>
    <tr>
      <th>TotRmsAbvGrd</th>
      <td>5180.211775</td>
    </tr>
    <tr>
      <th>Fireplaces</th>
      <td>3619.403449</td>
    </tr>
    <tr>
      <th>GarageCars</th>
      <td>10620.732646</td>
    </tr>
    <tr>
      <th>GarageArea</th>
      <td>2.291525</td>
    </tr>
    <tr>
      <th>WoodDeckSF</th>
      <td>25.513023</td>
    </tr>
    <tr>
      <th>OpenPorchSF</th>
      <td>-5.442307</td>
    </tr>
    <tr>
      <th>EnclosedPorch</th>
      <td>9.276949</td>
    </tr>
    <tr>
      <th>3SsnPorch</th>
      <td>19.239730</td>
    </tr>
    <tr>
      <th>ScreenPorch</th>
      <td>57.271218</td>
    </tr>
    <tr>
      <th>PoolArea</th>
      <td>-37.971754</td>
    </tr>
    <tr>
      <th>MiscVal</th>
      <td>-0.926897</td>
    </tr>
    <tr>
      <th>MoSold</th>
      <td>-109.914022</td>
    </tr>
    <tr>
      <th>YrSold</th>
      <td>-728.808600</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Score
lr.score(X,y)
```




    0.8091353327308902




```python
#lets make some prediction with the test data
#predict function
y_pred = lr.predict(X_test)
```


```python
#lets compare the Sales price with the predicted values
#actual prices
y_test
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
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1436</th>
      <td>120500</td>
    </tr>
    <tr>
      <th>57</th>
      <td>196500</td>
    </tr>
    <tr>
      <th>780</th>
      <td>176000</td>
    </tr>
    <tr>
      <th>382</th>
      <td>213500</td>
    </tr>
    <tr>
      <th>1170</th>
      <td>171000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>1037</th>
      <td>287000</td>
    </tr>
    <tr>
      <th>106</th>
      <td>100000</td>
    </tr>
    <tr>
      <th>1307</th>
      <td>138000</td>
    </tr>
    <tr>
      <th>876</th>
      <td>132250</td>
    </tr>
    <tr>
      <th>771</th>
      <td>102000</td>
    </tr>
  </tbody>
</table>
<p>482 rows × 1 columns</p>
</div>




```python
#y_pred predicted prices
y_pred
```




    array([[ 99442.51570293],
           [208746.76792509],
           [195175.53641794],
           [222406.86461851],
           [130783.86416228],
           [233417.05849405],
           [223726.68100078],
           [284384.05347037],
           [104702.92448729],
           [199585.10676779],
           [193332.05094389],
           [201916.60668271],
           [173575.2691768 ],
           [218257.74007457],
           [107653.06740099],
           [125574.97662714],
           [197210.12827553],
           [106915.12715573],
           [118492.14619338],
           [134770.65629359],
           [168952.90459152],
           [ 92504.98579135],
           [121230.61554503],
           [136273.84561438],
           [204106.85059662],
           [152433.48463666],
           [-38887.15845072],
           [ 90785.58111422],
           [182010.22151509],
           [147024.66182504],
           [155386.55325192],
           [222411.21609019],
           [243864.9443067 ],
           [ 55521.53400555],
           [118066.78906204],
           [ 55947.75374158],
           [135761.27670898],
           [ 52460.4519681 ],
           [150598.63107527],
           [117234.55037532],
           [322207.66878636],
           [235006.00870445],
           [139117.93867905],
           [ 72088.14827521],
           [150387.54874578],
           [ 39403.18144075],
           [291856.98632858],
           [170690.33581962],
           [137487.66921476],
           [ 97562.84626159],
           [247404.51038442],
           [ 92936.46331207],
           [342595.52975162],
           [233706.84242453],
           [177826.6701718 ],
           [ 77438.98814384],
           [ 13289.60745011],
           [186390.39705045],
           [132252.65033079],
           [363191.44678175],
           [148316.92994517],
           [235108.00904657],
           [154193.0795777 ],
           [170399.60531641],
           [208926.83031809],
           [250833.79627017],
           [107997.74024806],
           [112969.83464722],
           [215456.90398595],
           [134948.26583355],
           [258045.45116323],
           [282032.89117618],
           [250630.88077192],
           [132094.23171239],
           [199862.79348327],
           [165467.68517763],
           [128524.22585274],
           [251168.34014407],
           [228199.04277064],
           [209425.50065398],
           [116451.82379267],
           [266703.75808804],
           [187372.78050612],
           [203709.52394898],
           [413556.80069191],
           [102899.18084781],
           [116075.67849242],
           [224407.21405484],
           [185201.74647114],
           [127757.07159139],
           [152347.24418455],
           [193715.31505526],
           [206026.58522383],
           [155810.09710654],
           [247466.61243756],
           [ 57945.77872081],
           [215978.83227873],
           [207812.87969727],
           [151947.15231308],
           [209540.99813355],
           [139067.74250707],
           [109342.77208268],
           [239910.21026076],
           [281062.66164521],
           [160211.15441421],
           [ 91844.65013196],
           [196705.6512782 ],
           [117172.08938061],
           [ 70712.95820775],
           [ 66523.7482607 ],
           [297221.73625807],
           [139240.94877825],
           [182022.13556437],
           [ 91443.00357342],
           [168983.45404253],
           [173629.89139994],
           [113882.85397149],
           [188181.75718636],
           [223854.50988847],
           [196217.91057286],
           [174724.54364786],
           [122730.47940003],
           [170468.83471125],
           [112585.92973962],
           [139925.64058088],
           [154530.35049571],
           [157814.08384443],
           [241797.88361623],
           [343607.31762652],
           [200684.6497085 ],
           [118323.91923422],
           [ 59739.42915221],
           [329180.77961218],
           [229877.69510746],
           [ 99681.56995345],
           [105667.14765342],
           [158173.0806242 ],
           [182479.47190554],
           [266315.28940175],
           [ 87461.86602325],
           [168127.94188855],
           [186720.49045892],
           [150678.92023971],
           [259575.51822729],
           [314914.55313303],
           [152189.74343134],
           [172030.95035315],
           [193935.58840276],
           [310308.68540669],
           [153413.92041859],
           [108054.12723326],
           [196844.42501549],
           [105550.54799568],
           [382965.26667038],
           [197342.00223967],
           [156130.81449162],
           [ 37727.50160549],
           [174633.33898207],
           [195210.95224118],
           [207887.15007304],
           [227618.48004244],
           [136750.14837185],
           [176051.33525524],
           [105062.69544007],
           [152982.65993776],
           [ 67054.73732368],
           [277045.33372023],
           [194446.22301526],
           [319903.66654674],
           [184862.37578733],
           [188659.5748205 ],
           [205120.76763914],
           [138642.56025429],
           [209297.69997949],
           [120927.96069238],
           [141610.68190184],
           [231046.31908083],
           [262186.59621293],
           [129408.29838196],
           [125587.32462701],
           [125720.32577083],
           [307499.24114277],
           [ 85873.77726072],
           [ 74508.17310862],
           [177063.60562099],
           [140598.13855849],
           [182730.91549362],
           [240199.66226712],
           [200850.51563673],
           [158335.97823643],
           [241381.71032189],
           [213186.34470394],
           [119229.98199528],
           [202487.6286241 ],
           [359340.99579808],
           [ 83143.47112049],
           [128862.43783465],
           [161524.02176239],
           [237672.98475115],
           [215331.51182908],
           [185013.15099576],
           [259334.74566562],
           [114964.83378722],
           [127171.91812257],
           [185832.59763398],
           [144019.44382516],
           [271318.92144857],
           [184462.15175153],
           [163460.95571933],
           [204254.03316154],
           [151149.26146438],
           [ 90960.46793702],
           [324067.46439752],
           [189109.38780903],
           [144020.74552832],
           [257149.42378738],
           [141363.50329058],
           [ 99788.00696669],
           [185986.94204672],
           [191016.59592145],
           [179203.04529737],
           [117592.36422897],
           [ 97515.4525102 ],
           [ 83747.44460258],
           [223049.11519262],
           [213994.17927725],
           [222289.87724163],
           [ 80132.4888635 ],
           [135655.6761251 ],
           [ 90172.5638681 ],
           [278052.70054546],
           [114784.88929956],
           [259456.2805552 ],
           [283771.43394534],
           [187566.87649431],
           [353001.35633637],
           [195971.09845517],
           [303521.28353438],
           [160842.71225218],
           [149965.24991135],
           [226074.58419086],
           [232558.51891019],
           [223991.04780665],
           [211004.80221005],
           [ 76543.11510033],
           [172597.80670866],
           [245531.68691073],
           [229907.28618335],
           [200730.71511862],
           [213640.33906507],
           [231340.38222928],
           [154326.60920983],
           [211083.57732954],
           [311992.51183419],
           [141317.65365361],
           [ 70998.40952156],
           [186830.77915795],
           [199850.56763941],
           [163565.0917527 ],
           [148563.16008157],
           [128813.83595039],
           [293176.36598009],
           [141942.99846434],
           [119182.34703411],
           [301994.92378099],
           [178801.13685604],
           [201131.50168439],
           [ 84662.33552325],
           [164235.11431527],
           [130547.08316901],
           [194848.46780473],
           [153172.28696113],
           [165265.99408146],
           [220615.6708441 ],
           [193071.72868668],
           [197605.13047507],
           [258500.06222063],
           [127071.14122322],
           [ 96167.6826868 ],
           [128322.80178922],
           [ 85607.47200985],
           [350451.27654628],
           [145095.98895158],
           [288304.50185586],
           [292518.09285056],
           [208365.38620701],
           [363277.45247459],
           [246846.66124715],
           [245403.6017432 ],
           [199180.85453393],
           [336938.50747679],
           [141681.12638534],
           [243182.48451986],
           [248918.26288526],
           [149380.4731333 ],
           [179196.61703862],
           [246024.82706354],
           [218542.2559397 ],
           [109810.26621777],
           [254399.57187038],
           [325645.1752892 ],
           [226772.73522531],
           [165246.92881584],
           [ 70032.28647511],
           [157625.0240282 ],
           [132246.8452876 ],
           [161750.14677511],
           [163960.95345446],
           [ 72354.30568237],
           [184735.73007573],
           [126271.65128741],
           [ 57439.24725932],
           [154269.86649848],
           [133489.76693622],
           [182691.82356189],
           [105624.63862707],
           [164187.19045489],
           [123344.04444779],
           [234415.01001598],
           [186707.2408558 ],
           [226767.99568406],
           [121501.23227993],
           [180818.50397735],
           [207799.79325018],
           [252784.04158117],
           [295912.36166085],
           [113559.08627272],
           [156310.3450874 ],
           [188994.08811948],
           [236011.8375616 ],
           [108135.53303886],
           [212685.79192346],
           [125025.64985106],
           [ 82499.14305291],
           [141931.35366191],
           [266461.87560837],
           [311165.98631713],
           [229502.56401874],
           [203593.53260387],
           [303019.60753169],
           [115012.30073953],
           [272799.64009655],
           [250941.00703035],
           [226989.00686493],
           [366058.42230255],
           [119253.65751774],
           [169105.22649177],
           [212904.85587669],
           [167550.89748661],
           [273449.58053879],
           [137893.01066584],
           [134979.09413907],
           [ 84158.08086214],
           [381631.92987685],
           [123039.49584621],
           [283999.72367588],
           [158572.06692602],
           [218582.68873588],
           [132138.01718862],
           [142188.39900701],
           [ 87683.54922196],
           [ 80982.67796059],
           [146956.89701764],
           [133746.13920744],
           [261453.28146436],
           [292082.15457006],
           [133632.46567076],
           [165690.64072839],
           [227247.17135587],
           [163392.21494229],
           [106634.62737705],
           [287318.22668493],
           [155748.9311987 ],
           [ 71492.07082562],
           [221750.76984989],
           [ 79674.29023139],
           [231675.28405595],
           [180340.24798561],
           [264055.0362727 ],
           [121265.70083775],
           [231802.08923204],
           [313833.79199443],
           [261909.61408424],
           [125026.83240263],
           [ 77347.75591368],
           [271943.14873759],
           [245695.33478029],
           [289510.45462517],
           [199854.719953  ],
           [303297.64315443],
           [135916.25019731],
           [187083.60356569],
           [ 53024.9337798 ],
           [227504.57621155],
           [139218.2969964 ],
           [204344.84438498],
           [175818.65744164],
           [192399.33112928],
           [116898.05088109],
           [141083.00590857],
           [230575.95712092],
           [191047.18322981],
           [168470.86348527],
           [185191.33426398],
           [223096.37871036],
           [123194.67155875],
           [163969.80442456],
           [129091.02106294],
           [127035.5608544 ],
           [129317.97206134],
           [183832.11239536],
           [153051.80649422],
           [186528.71551366],
           [151705.6682543 ],
           [166090.01041055],
           [253637.77584391],
           [169778.67533364],
           [127160.32823998],
           [140556.79356173],
           [165134.61541133],
           [256786.55889787],
           [174858.21097076],
           [212983.5167016 ],
           [201883.54559848],
           [198704.9432465 ],
           [247470.36998829],
           [152073.05650838],
           [148346.18754474],
           [134182.46670124],
           [132057.59267375],
           [217471.48497556],
           [374072.15955272],
           [141688.51504362],
           [133285.44654832],
           [101634.85126891],
           [229159.89571944],
           [254097.03796004],
           [204299.53476603],
           [ 91809.54994059],
           [297217.66128147],
           [134579.14865353],
           [159416.77905065],
           [113930.09683964],
           [112738.32943943],
           [127670.60085797],
           [305117.605134  ],
           [ 50767.63300084],
           [238449.54779653],
           [115475.54194677],
           [115998.1561081 ],
           [ 96387.68352482],
           [ 91913.28034106],
           [122660.32102519],
           [183427.61313422],
           [250754.56214645],
           [ 48154.36831556],
           [127961.61826166],
           [154967.95790743],
           [162079.65826168],
           [114799.73771179],
           [154694.79119253],
           [144091.29074244],
           [130895.67832061],
           [207850.12829253],
           [285297.68029528],
           [155675.94315509],
           [111336.10769568],
           [266529.00073207],
           [ 48048.8736756 ],
           [177707.81825406],
           [272482.44272249],
           [106950.89755916],
           [239080.95895048],
           [102723.0565178 ],
           [182976.48349299],
           [174873.33989688],
           [206712.12015855],
           [267513.30179339],
           [ 81826.71806809],
           [139867.50247312],
           [117349.49507047],
           [122462.92503943]])




```python
#scatter plots with y_test and y_pred
plt.scatter(y_test, y_pred) #most of the point overlap = good prediction and if they are very much scattered then its not a good prediction
```




    <matplotlib.collections.PathCollection at 0x22803570130>




    
![png](output_67_1.png)
    



```python
#Calculate the values of residuals. actual prices - predicted prices
y_test-y_pred

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
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1436</th>
      <td>21057.484297</td>
    </tr>
    <tr>
      <th>57</th>
      <td>-12246.767925</td>
    </tr>
    <tr>
      <th>780</th>
      <td>-19175.536418</td>
    </tr>
    <tr>
      <th>382</th>
      <td>-8906.864619</td>
    </tr>
    <tr>
      <th>1170</th>
      <td>40216.135838</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>1037</th>
      <td>19486.698207</td>
    </tr>
    <tr>
      <th>106</th>
      <td>18173.281932</td>
    </tr>
    <tr>
      <th>1307</th>
      <td>-1867.502473</td>
    </tr>
    <tr>
      <th>876</th>
      <td>14900.504930</td>
    </tr>
    <tr>
      <th>771</th>
      <td>-20462.925039</td>
    </tr>
  </tbody>
</table>
<p>482 rows × 1 columns</p>
</div>




```python
# concatenate y_test and y_pred into a single array
y_concat = np.concatenate((y_test, y_pred))

# create a histogram plot
sns.histplot(data=y_concat, bins=50, kde=True)
```




    <Axes: ylabel='Count'>




    
![png](output_69_1.png)
    



```python
#check the accuracy
from sklearn import metrics 
```


```python
metrics.r2_score(y_test, y_pred)
```




    0.8365919388564145




```python
#mean absolut error = average error that we have / this number should be as low as possible if u are comparing multiple models
metrics.mean_absolute_error(y_test, y_pred)
```




    21361.61234715337




```python
#mean squared error = making square of the error
#benefit = there are two = negativ values will be converted to positive, so there is a fair comparison between ups and downs and as a second benefit
# it punishes larger errors
metrics.mean_squared_error(y_test, y_pred)
```




    1027694985.7301909




```python
#creating root mean square
metrics.mean_squared_error(y_test, y_pred, squared=False)
```




    32057.68216403349




```python

```
