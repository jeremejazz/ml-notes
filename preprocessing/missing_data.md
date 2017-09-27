


First section in the tutorial class was about loading the data csv data in spyder

Here we have a file (Data.csv) that contains the following data 

**Country**|**Age**|**Salary**|**Purchased**
:-----:|:-----:|:-----:|:-----:
France|44.0|72000.0|No
Spain|27.0|48000.0|Yes
Germany|30.0|54000.0|No
Spain|38.0|61000.0|No
Germany|40.0| |Yes
France|35.0|58000.0|Yes
Spain| |52000.0|No
France|48.0|79000.0|Yes
Germany|50.0|83000.0|No
France|37.0|67000.0|Yes

As you can see we have two missing data for Age column in Spain and the Salary column in Germany.

We can compute for the missing data by getting the means which uses the average of the other rows.


Using spyder we will need the to import the following libraries to prepare our code

```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd

```

`numpy` will be the array storage for data. `matplotlib` and `pandas` is needed for visualization 


Next we need to import the data. It is best to save the file along with `Data.csv` in order to easily do a relative path


```python
dataset = pd.read_csv('Data.csv')`
```

******************************************
**Tip:**
In spyder you can execute part of your code by highlighting it and clicking **run current cell** (Ctrl + Enter in Linux). 
******************************************
We can double click `dataset` in the variable explorer to see the imported data as displayed earlier. 

*Jereme: Using `type(dataset)` I have noticed that this is a **pandas.core.frame.DataFrame** object which can be also seen in the Variable explorer. BRB for elaboration. As of this point I don't know what X and Y ... I'll have to discuss with the intructor about this. I Might be too early for the exposition plot*

Using python's list slicing, we then assign the columns to X and Y


```python
X = dataset.iloc[:, :-1].values
Y = dataset.iloc[:,3].values
```


Here we are excluding the last column from X which is Purchased and assign to Y instead.

****************************************
**Tip:**
You might encounter an ellipsis when viewing the array. To view the full `numpy` array, you will need to enter `np.set_printoptions(threshold=np.nan)` into the console. 
****************************************

Next thing we will be needing is to import the Imputer module. You don't necessarily need to put this in the beginning and selecting and running it would be fine. We will have to assign the imputer object as well

```python
from sklearn.preprocessing import Imputer

imputer = Imputer(missing_values="NaN", strategy='median', axis=0)
```

As an explanation for the code above we set the configuration to look for missing values using the **median** strategy. The **axis** parameter set to **0** pertains to process the column while **1**  is for the rows. Since we need to compute for the column we will be using 0.

****************************************
**Tip:**
Spyder provides a quick documentation when you highlight a function/module (say Imputer) then press Ctrl+i that becomes displayed in the Help window. You can use this to view other available strategies and experiment on them
****************************************

Now to compute for the missing values: 

```python
imputer = imputer.fit(X[:, 1:3])
X[:,1:3] = imputer.transform(X[:,1:3])
```

Since we don't need the Country column we will just use the 2nd and 3rd column using python's slicing method. 

If we view X in the compiler, we can now see that the missing data has been filled out with the average. This can be verified by manually computing the average of the other rows.


