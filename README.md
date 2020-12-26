# Lab #9: Introduction to Pandas

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

## Acknowledgements

# Table of Contents

# What do we mean by pandas

Some of you may be wondering why we are talking about pandas in a computer science course.

What is a panda?

Figure 1 or 2

Panda: "a large black-and-white mammal (Ailuropoda melanoleuca) of chiefly central China that feeds primarily on bamboo shoots and is now usually classified with the bears (family Ursidae)" ([Merriam-Webster](https://www.merriam-webster.com/dictionary/panda))

Wait that's not right....

`pandas`: "a fast, powerful, flexible and easy to use open source data analysis and manipulation tool, built on top of the Python programming language" ([`pandas` documentation](https://pandas.pydata.org/))

That makes more sense.

If you remember back to our earlier work with `.csv` files in Python, there are limitations to the kinds of things we can do with structured data using the `csv` module.

Particularly if we want to analyze and visualze structured data in a Python programming environment, we aren't going to get very far loading `csv` files as lists or dictionaries.

We need Python to understand or interact with structured data as structured data.

Enter `pandas`.

Software developers at AQR Capital Management began working on a Python-based tool (written in a combination of C and Python) for quantitative data analysis in 2008.

The initial open-source version of `pandas` was released in 2008.

At its core, "`pandas` is a software library written for the Python programming language for data manipulation and analysis. In particular, it offers data structures and operations for manipulating numerical tables and time series" ([Wikipedia](https://en.wikipedia.org/wiki/Pandas_(software)).

The name `pandas` is derived from "panel data," an econometrics term used to describe particular types of datasets.

The name `pandas` is also a play on "Python data analysis."

For more on the history and origins of `pandas`, check out Wes McKinney's "[pandas: a Foundational Python Library for Data Analysis and Statistics]"(https://www.dlr.de/sc/Portaldata/15/Resources/dokumente/pyhpc2011/submissions/pyhpc2011_submission_9.pdf) 2011 paper.

What pandas lets us do

`pandas` is based on and has some similarities with another Python package, `NumPy`.

According to [package documentation](https://numpy.org/doc/stable/user/whatisnumpy.html), "`NumPy` is the fundamental package for scientific computing in Python. It is a Python library that provides a multidimensional array object, various derived objects (such as masked arrays and matrices), and an assortment of routines for fast operations on arrays, including mathematical, logical, shape manipulation, sorting, selecting, I/O, discrete Fourier transforms, basic linear algebra, basic statistical operations, random simulation and much more."

In `NumPy`, data are stored as list-like objects called arrays. 

`NumPy` allows users to access, split, reshape, join, etc. data stored in arrays.

`pandas` takes a similar approach to structured data, or data organized in a tabular (i.e. table-like) format.

"pandas adopts significant parts of NumPy's idiomatic style of array-based computing, especially array-based functions and a preference for data processing without for loops...the biggest difference is that pandas is designed for working with tabular or heterogeneous data. NumPy, by contrast, is best suited for working with homogenous numerical array data" (Wes McKinney, Chapter 5 "Getting Started with Pandas" in *Python for Data Analysis*, pg. 125)

For more on `NumPy`:
- [NumPy website](https://numpy.org/)
- [NumPy documentation](https://numpy.org/doc/stable/)
- ["NumPy Introduction," W3Schools](https://www.w3schools.com/python/numpy_intro.asp)
- ["Introduction to NumPy Tutorial," Software Carpentry](https://software-carpentry.org/blog/2012/06/introduction-to-numpy-tutorial.html)

Getting started with pandas

# Data structures in pandas

`pandas` has two main data structures: `Series` and `DataFrame`.

## `Series`

In `pandas`, "a `Series` is a one-dimensional, array-like object containing a sequence of values...and an associated array of data labels, called its index" (McKinney, 126).

At first glance, a `Series` looks a lot like a Python list.
```Python
# import pandas package
import pandas as pd

# import Series and Data Frame components from pandas
from pandas import Series, DataFrame

# create a Series using pandas
obj = pd.Series([4, 7, -5, 3])

# show obj Series 
obc
```

In this example, we imported the `pandas` package as well as the specific `Series` and `DataFrame` components of the module.

We created a `Series` object containing four integer values.

When working in `pandas`, most commands begin with `pd.`.

We could create a list with these values, but for data analysis we needed the functionality `pandas` provides for working with series.

To verify `obj` is stored as an array-like object, we can use `obj.values` which should return `array([4, 7, -5, 3])`

We can also get the index attributes for `obc` using `obj.index`, which should return `RangeIndex(start=0, stop=4, step=1)`.

The default index attributes assigned to objects in an array are integers `0` through `N-1`, where `N` is the length of the data.

We can create our own index attributes for the data points by manually creating index labels.

```Python
# create obj2 series with index attributes
obj2 = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])

# show obj2 series
obj2
```

The index-value link lets us interact with a `Series` object similar to how we would work with Python dictionary key-value pairs.

```Python
# access Series value using index label
obj2['a'] 

# this returns -5
```

```Python
# assign value for index
obj2['d'] = 6

obj2['d']

# this returns 6, our newly-assigned value for index 'd'
```

```Python
# access multiple values in Series object using index
obj2[['c', 'a', 'd']]

# this returns the index-value pairs for the specified index labels
```

We can also use Python's built-in arithmetic functionality for values in a `Series` object.

```Python
# select values in the Series that meet a specific condition
obj2[obj2 > 0]

# returns index-value pairs for values greater than 0
```

```Python
# multiply all values in Series
obj * 2

# returns modified values
```

```Python
# perform NumPy's exponent calculation functionality on Series values
np.exp(obj2)

# returns exponent float values
```

Try to perform similar mathematical operations on values stored in a Python dictionary or list and you'll run into all kinds of data type errors.

The `Series` object uses a similar data structure and opens up a wide range of analysis possibilities.

To create a `Series` from data in a Python dictionary:
```Python
# create dictionary
sdata = {'Ohio': 35000, 'Texas': 71000, 'Oregon': 16000, 'Utah': 5000}

# create Series from dict dictionary
obj3 = pd.Series(sdata)
```

Let's say we wanted to have the `Series` values appear in a specific order.

We can specify the index (or key) label order when converting a dictionary to a Series.
```Python
# create dictionary
sdata = {'Ohio': 35000, 'Texas': 71000, 'Oregon': 16000, 'Utah': 5000}

# list of index labels
states = ['California', 'Ohio', 'Oregon', 'Texas']

# create Series from dict dictionary
obj4 = pd.Series(sdata, index=states)

# see output for new obj4 series
obj4
```

A few things have happened here.

The `California` index is returning `NaN` for its value, which is "not a number" or "NA".

The `Utah` value in `sdata` is not in the `obj4` series, because the idex label `Utah` was not in the manually assigned list of index values passed to the series through `index=true`.

We can use the `isnull()` or `notnull()` functions in `pandas` to detect missing data.

These functions will return `TRUE` or `FALSE`.

```Python
# test for null values for each index label
pd.isnull(obj4)

# output will be FALSE for all but California
```

```python
# test for not null values
pd.notnull(obj4)

# output will be TRUE for all but California
```

We can assign a name for our `Series` object and its index values using the `name` attribute.

```Python
# assign name to Series object
obj4.name = 'population'

# assign name to index
obj4.index.name = 'state'

# view updated Series
obj4
```

The output for `obj4` now reflects our newly-assigned `name` attribute values.

## `DataFrame`

While a `Series` object is a one-dimensional array, a `DataFrame` includes a tabular data structure "and contains an ordered collection of columns, each of which can be a different value type" (McKinney, 130).

A `pandas` `DataFrame` has a row and column index--we can think of these as Series that all share the same index.

Behold, a two-dimensional data structure. 

In most situations, you'll create a `DataFrame` by reading in a structured data file.

But we're going to manually create a `DataFrame` to better understand how they work in `pandas`.

Let's go back to our state population data example.

Say we have two dictionaries that include equal-length lists:
```Python
# create dictionary with three equal-length lists
data = {'state': [Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', Nevada'], 
        'year': [2000, 2001, 2002, 2001, 2002, 2003],
        'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

# write data dictionary values to data frame
frame = pd.DataFrame(data)

# show newly-created frame
frame
```

Behold, a two-dimensional `DataFrame` object with rows, columns, labels, and values.

The first object from each of the lists in our `data` dictionary now populate the first row of our `frame` DataFrame.

This pattern continues for subsequent rows.

We can start to explore the dimensions or overall characteristics of our DataFrame:
```Python
# shows index labels and values for first 5 rows
frame.head(5)

# shows list of column labels
frame.columns.values

# shows basic statistical information for the data frame
frame.describe()
```

The last command `.describe()` returns some statistical information about values in our dataset, including:
- count
- mean
- standard deviation
- minimum
- 25th percentile
- 50th percentile
- 75th percentile
- maximum

Let's say we want to specify the column sequence or the order in which columns are arranged in the `DataFrame`:
```Python
pd.DataFrame(data, columns=['year', 'state', 'pop']
```

What happens if we specify a column that isn't represented in the data passed to the `DataFrame`? 
```Python
# create new dataframe from data dictionary with specific columns and index labels
frame2 = pd.DataFrame(data, columns=['year', 'state', 'pop', 'debt'], index=['one', 'two', 'three', 'four', 'five', 'six'])

# show frame2 DataFrame
frame2
```

We see only `NaN` missing values for the `debt` column since that column is not represented in the `data` dictionary used to create our `frame2` DataFrame.

We can select columns in our `DataFrame` using their index labels.
```Python
frame2['state']

# returns state column
```

We can also select a column using the `name` attribute.
```Python
frame2.year

# returns year column
```

We can retrieve rows based on their position using the `loc` (location) attribute.
```Python
frame2.loc['three']

# returns the third row in the dataframe
```

```Python
frame2.iloc[0:3, :]

# uses numerical index values to retrieve first four rows
```

Let's say we wanted to manually assign the values in a particular column, for example the `debt` missing data column.
```Python
frame2['debt'] = 16.5

frame2

# returns frame2 DataFrame with newly-assigned 16.5 value for all rows in debt column
```

We could also manually insert values for specific rows using their index labels.

If we wanted to add debt values for rows two, four, and five:
```Python
# variable with Series object
val = pd.Series([-1.2, -1.5, -1.7], index=['two', 'four', 'five'])

# assign val Series object to debt column in frame2 DataFrame
frame2['debt'] = val

# show modified DataFrame
frame2
```

We now see the modified `debt` values for the rows specified in the `index=` portion of our code.

We can remove a column using the `del` keyword.
```Python
del frame2['debt']

# returns updated list of columns
frame2.columns

# result will be 'year', 'state', and 'pop'
```

We can also pass a nested dictionary to a DataFrame.

```Python
# assign nested dictionary to variable
pop = {'Nevada': {2001: 2.4, 2002: 2.9}, 
       'Ohio': {2000: 1.5, 2001: 1.7, 2002: 3.6}}
       
# passing the nested dictionary to a DataFrame
frame3 = pd.DataFrame(pop)

# return new DataFrame
frame3
```

`pandas` interprets the outer dict keys as column names and inner keys as row names.

# From structured data file to `DataFrame`

As mentioned earlier in this lab, it's far more likely that you will load structured data from a file into Python, rather than manually creating a `DataFrame`.




Once within Pandas

How we could do SQL-like things with query/join/filter/etc within pandas

Where do we go from here

# Practice Problems



# Lab Notebook Questions
