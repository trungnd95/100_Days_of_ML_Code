## Pandas Noted

##### Trung Ng - 18/06/2019

-------------------------------------------------

#### 1. Why use Pandas?

- Large dataset don't come ready to be fed into ml learning algorithms. More often than not, large dataset will often have missing values, outliers, incorrect data, ... **=> Cannot put those data straight into ML algorithms**. We need  look at the data first and make sure it is well suited for ML algorithms. This is where Pandas come in. 

- Two main objects in Pandas are **Series** and **DataFrame** 

#### 2. Series
> Pandas series is a one-dimensional array-like object that can hold many datatypes such as number or string. 

**One of the main differences between Pandas series and numpy array is that Pandas series can hold data of different datatype and asign an index label to each element**

- Creation 
```Python
import pandas as pd 
ser = pd.Series(data, index, ...)
```
There are 2 important arguments when creating pandas series are data and index (It both are list (numpy array)). Or we can create pd series shortly from python dictionary instead. 
```Python 
labels = ['a','b','c']
my_list = [10,20,30]
arr = np.array([10,20,30])
d = {'a':10,'b':20,'c':30}
serie =  pd.Series(data=my_list/arr , index = lables)
or 
serie = pd.Series(d)
```
- Interaction
    - Select data from Series by index: 
        - serie['a']
        - Using loc: serie.loc['a'] - The same way above
        - Using iloc to select pandas series by index: serie.iloc[0]
    - Change pandas series data
        - serie['a'] = 50 
    - Drop pandas series data
        - serie.drop('a', inplace=True) // Inplace set to True to change in place of serie, actually change serie after run this command

#### 3. DataFrame
> DataFrame is two-dimensional data structure with labeled rows and columns
> **DataFrame inlcudes bunch of Pandas Series. Imagine that DataFrame like a sheet table, and Series like a row / column of that table**

- Creation
    ```Python
    # df = pd.DataFrame(data, index, columns, ...)
    
    Ex1:
    # We create a dictionary of Pandas Series 
    items = {'Bob' : pd.Series(data = [245, 25, 55], index = ['bike', 'pants', 'watch']),
             'Alice' : pd.Series(data = [40, 110, 500, 45], index = ['book', 'glasses', 'bike', 'pants'])}
    shopping_carts = pd.DataFrame(items)
    
    Ex2:
    # We create a list of Python dictionaries
    items2 = [{'bikes': 20, 'pants': 30, 'watches': 35}, 
              {'watches': 10, 'glasses': 50, 'bikes': 15, 'pants':5}]
    store_items = pd.DataFrame(items2)
    
    Ex3:
    df = pd.DataFrame(randn(5,4),index='A B C D E'.split(),columns='W X Y Z'.split())
    ```
- Interaction
    - Selection: There are 3 ways to retreive dataframe value like series:
        - Select columns: Using the column name - items[['Bob', 'Alice']]
        - Select rows: 
            - Using _loc_ to select index name - items.loc['bike']
            - Using _iloc_ to select index sequence - items.iloc[1]
        - Select condition
            - items[items['bike']>300]
    - Add new column to end of 
        - Set new columns with value directly. items['new_col'] = [5,10,15]
        - Using insert API to insert column: insert(loc,label,data)
    - Add new row
        - Using **append**: create new row as DataFrame, add new DataFrame to existing one. 
    - Delete row / column
        - Using pop API to remove column
        - Using drop with axis to remove row / column follow axis value set.
    - Rename columns
        - items.columns = new_columns
        - items.rename(columns = {}, inplace=True)
        - ...
    - Set index / Reset index
        - items.set_index(index_array)
        - items.reset_index() => The current index will change to one column of dataframe, the index is default numerical index
    
    - Dealing with NaN
        - Check with isnull() method
        - Drop NaN with dropna(axis=0/1) method
        - Fill NaN with fillna(method='ffill/bfill/linear/..', axis=0/1, ...)
    - Groupby 
    - Merging, joining and concatenating
    
    