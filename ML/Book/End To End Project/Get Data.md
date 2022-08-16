## Create the workspace
Create a directory
Create a virtual environment [[Virtual Environments]]
Install dependencies
- jupyter, matplotlib, numpy
- pandas, scipy, scikit-learn
~P.S. if you want to just update use -U for pip~
Register virtual environment to jupyter and name it
`python -m ipykernel install --user --name=myenv`
Fire up jupyter by saying
`jupyter notebook`

With your data inspect it with pandas and matplotlib
If it can be put to a histogram try to make your data more like a bell curve, look for cutoffs, notice scaling needs. 

## Create a test set
```python
def split_train_test(data, test_ratio):
    shuffled_indices = np.random.permutation(len(data))
    test_set_size = int(len(data)*test_ratio)
    test_indices = shuffled_indices[:test_set_size]
    train_indices = shuffled_indices[test_set_size:]
    return data.iloc[train_indices], data.iloc[test_indices]
```
 Unfortunately over time this program will reveal different parts of the data and eventually reveal the whole test set. Two solutions are:
 1. Save the test set and training set
 2. Set random number generator's seed to always generate same shuffle
 But both of these break with an updated dataset
 3.The key solution is to use each instance identifier to decide whether or not it should go in the test or training set, such as through a hash function
 
 ```python
 from zlib import crc32

def test_set_check(identifier, test_ratio):
    return crc32(np.int64(identifier)) < test_ratio * 2**32


def split_train_test_by_id(data, test_ratio, id_column):
    ids = data[id_column]
    in_test_set = ids.apply(lambda _id: test_set_check(_id, test_ratio))
    return data.loc[~in_test_set], data.loc[in_test_set]
```

Your going to need a identifier column which can be done by `df.reset_index()`
If you can't ensure data won't be deleted then use other unique qualities such as latitude and longititude.

While the functions above are great and all, scikit-learn provides the same functionality with split_train_test() with additives. Such as random_state that allows you to set the random generator seed. 
```python
from sklearn.model_selection import train_test_split

train_set, test_set = train_test_split(housing_with_id, test_size=0.2, random_state = 42)
```

While random is great and all, this isn't always the correct way, you should ensure your data represents 100% of the population not part of it. For example if a population is 60% red, and 40% blue then if you sample 500 species from the population you should have 300 red and 200 blue this is called *stratified sampling* and the homogenous groups are *strata*. 

```python
from sklearn.model_selection import StratifiedShuffleSplit
split = StratifiedShuffleSplit(n_splits=1, test_size=0.2, random_state=42)
for train_index, test_index in split.split(housing, housing["income_cat"]):
    strat_train_set = housing.loc[train_index]
    strat_test_set  = housing.loc[test_index]
```
This *ENSURES* the data is representative of the population and not subject to random chance of being wrong