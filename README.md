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

For this section of the lab, we're going to work with data about *Titanic* passengers.

Navigate to https://raw.githubusercontent.com/kwaldenphd/pandas-intro/main/data/titanic.csv in a web browser to see the dataset.

We can load structured data into Python from a file located on our computer or from a URL, using `pd.read_csv()`.
```Python
# import pandas
import pandas as pd

# load titanic data from csv file
titanic_file = pd.read_csv("titanic.csv")

# show first 5 rows of newly-loaded dataframe
titanic_file.head(5)

# load titanic data from url
titanic = pd.read_csv("https://raw.githubusercontent.com/kwaldenphd/pandas-intro/main/titanic.csv)

# show first 5 rows of newly-loaded dataframe
titanic.head(5)
```

`pandas` provides the `read_csv()` function which stores `.csv` data as a `pandas` `DataFrame`.

This `read_` prefix can be used with other structured data file formats, as we'll explore with JSON later.

Other parsing functions in `pandas`:
- `read_fwf`: fixed-width data with no delimiter
- `read_clipboard`: reads in data from clipboard
- `read_excel`: reads in data from `.xls` or `.xlsx` files
- `read_html`: reads in any tables contained in an HTML document
- `read_json`: reads in JSON data
- `read_sql`: reads in results of an SQL query as a pandas dataframe
- `read_sas`: reads in SAS dataset
- `read_stata`: reads in Stata file format

To check the first and last five rows of the `titanic` data frame:
```Python
titanic
```

We can also check the data type for each column using `.dtypes`.
```Python
titanic.dtypes
```

From this output, we know we have integers (`int64`), floats (`float64`), and strings (`object`).

Maybe we want a more technical summary of this `DataFrame`.
```Python
titanic.info()
```

`.info()` returns row numbers, the number of entries, column names, column data types, and the number of non-null values in each column. 

We can see from the `Non-Null Count` values that some columns do have null or missing values.

`.info()` also tells us how much memory (RAM) is used to store this `DataFrame`.

Let's go through these same steps with JSON data scraped from Twitter.

To learn more about scraping Twitter data with Python, [visit the `twarc` package documentation](https://github.com/DocNow/twarc).

```Python
import pandas as pd

# load data from JSON file
ND_Twitter_file = read_json("ND_Twitter.json")

# show first and last five  rows of new data frame
ND_Twitter_file

# load data from url
ND_Twitter = read_json("https://raw.githubusercontent.com/kwaldenphd/pandas-intro/main/data/ND_Twitter.json")

# show first and last five rows 
ND_Twitter

# check data type
ND_Twitter.dtypes

# check technical summary
ND_Twitter.info()
```


In the titanic data example, the `read` operation was fairly straightforward. 

The data being loaded contained headers and was formatted in a way we would expect for a `.csv` file.

But in many situations, data being loaded to a `DataFrame` will not conform to these formatting conventions.

Let's say we have a file that does not include a header row.

`pandas` can assign default column names, or you can set them manually.

The `titanic_no_header` file contains the same original data with the first row of column names removed.

```Python
# import pandas 
import pandas as pd

# load headless titanic data
headless_titanic_default = read_csv("https://raw.githubusercontent.com/kwaldenphd/pandas-intro/main/data/titanic_no_header.csv", header=None)

# shows us the default column names assigned by pandas
headless_titanic_default

# load headless titanic data and manually assign column names
headless_titanic = read_csv("https://raw.githubusercontent.com/kwaldenphd/pandas-intro/main/data/titanic_no_header.csv", names=['PassengerID', 'Survived', 'Pclass', 'Name', 'Sex', 'Age', 'SibSp', 'Parch', 'Ticket', 'Fare' ,'Cabin', 'Embarked'])

# shows data frame with manually assigned column names
headless_titanic
```

Let's say you have a `.txt` file that does not incldue a character delimiter.

`titanic.txt` is the same titanic data this time as tab-delimited values.

We would need to specify how `pandas` should parse this data as rows and columns.

```Python
# import pandas
import pandas as pd

# load titanic txt data
titanic_txt = pd.read_csv("https://raw.githubusercontent.com/kwaldenphd/pandas-intro/main/data/titanic.txt", sep="\t")

# shows first and last five rows of data frame
titanic_txt
```

We can also run into situations where the data we are loading into Python has missing values.

Just trying to load a file with missing data will return error messages.

We can specify what characters representing missing data when we create the `DataFrame`.

```Python
# import pandas
import pandas as pd

# load data where missing values are represented by NA or Null
sample = pd.read_csv("file_name.csv", na_values=['NA', 'Null'])

# for a situation where missing values in one column are represented by NA and another column's missing data are represented by Null
# first step is to create a dictionary for these column names and null values
null_symbols = {'column1': ['NA'], 'column2': ['Null']}

# load data where with column-specific missing values
sample2 = pd.read_csv("file_2_name.csv", na_values=null_symbols)
```

`pd.read_csv` includes other function arguments that can help with other common data formatting issues.

Argument | Description
--- | ---
`sep` or `delimiter` | Specifies the character sequence or regular expression used as a separator or delimiter
`header` | Specifies the row number to use as column names; `0` is default (does not need to be specified); `header=None` if no header
`index_col` | Specifies the column numbers or names to use as row index 
`names` | Specifies list of column names for result
`skiprows` | Row numbers (starting at 0) for rows to skip
`na_values` | Sequence of characters that represent missing or NA data
`comment` | Characters used to mark or split off comments that occur at end of lines of data
`parse_dates` | Specifies how date and time data will be parsed; `False` by default; `True` will attempt to parse all columns as `datetime` format; can also apply to select columns
`dayfirst` | Specifies international date format (DD/MM/YYYY); `False` by default
`date_parser` | Function used to parse dates
`nrows` | Number of rows to read starting at the beginning of the file; especially helpful when only needing part of a large file
`skip_footer` | Number of lines to ignore at the end of the file
`encoding` | Specifies encoding schema
`thousands` | Specifies `,` or `.` separater for thousands

Other elements of `.csv` dialect we might encounter when loading a file to a `DataFrame`:

Argument | Description
--- | ---
`delimiter` | One character string used to separate fields; default is `,`
`quotechar` | Quote character for fields with specific characters or fields that inclde the delimiter character
`skippinitialspace` | Instructs program to ignore whitespace after delimiter; default is `False`
`doublequote` | Specifies how to handle quoting character within a field
`escapechar` | Specifies the string used to escape the delimiter character if `quoting` is set to `QUOTE_NONE`

### From `DataFrame` to data file

Let's say we have data in a `DataFrame` and want to write that to a file.

While `.read_` loads data, `.to_` writes data.

To save the titanic data as an Excel file:
```Python
titanic.to_excel("titanic.xlsx", sheet_name="passengers", index=False)
```

In this example, we create a new Excel file with a single sheet (`passengers`) that stores the data from our `titanic` `DataFrame`.

`index=False` means that row index labels are not included in the new spreadsheet.

We could load back in the new Excel file and write it to a `.csv` file, dropping the header row:
```Python

# load Excel file as dataframe
titanic_excel = pd.read_excel("titanic.xlsx", sheet_name="passengers")

# write dataframe to CSV file with no header
titanic_excel.to_csv("titanic_no_head.csv", header=False)
```

# Practice Problems



# Lab Notebook Questions
