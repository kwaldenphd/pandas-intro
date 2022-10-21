# Getting Started With `pandas` (in Python)

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>This tutorial was written by Katherine Walden and is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Overview & Goals

This lab covers the core components of `pandas`, including `Series` and `DataFrame` objects. It covers how to manually create and interact with `Series` and `DataFrame` objects in the Python programming environment. It covers loading a structured data file (CSV and JSON) as a `DataFrame`, and sorting, selecting, and filtering the resulting `DataFrame`. The lab also covers common data parsing and wrangling challenges like duplicate entries and missing data.

By the end of this lab, students will be able to;
- Understand the basic components of `Series` and `DataFrame` objects in `pandas`
- Manually create `Series` and `DataFrame` objects in Python using `pandas`
- Load a structured data file as a `DataFrame` in Python using `pandas`
- Interact with a `DataFrame` using sorting, selecting, and filtering operations
- Remove duplicate rows from a `DataFrame`
- Understand how to approach common `DataFrame` parsing and loading errors using `pandas`
- Understand the basic components of how to handle missing values in a `DataFrame`

## Acknowledgements

Information and exercises in this lab were developed in consultation with the following resources:
- `pandas` package ["Getting started"](https://pandas.pydata.org/pandas-docs/stable/getting_started/intro_tutorials/) documentation.
- Wes McKinney's [*Python for Data Analysis: Data Wrangling With pandas, Numpy, and IPython*](https://www.oreilly.com/library/view/python-for-data/9781491957653/) (O'Reilly, 2017)
  * Chapter 5 "Getting Started with pandas" (125-168)
  * Chapter 7 "Data Cleaning and Preparation" (195-224)
  * Chapter 8 "Data Wrangling: Join, Combine, and Reshape" (225-256)
  * Chapter 10 "Data Aggregation and Group Operations" (293-322)

# Table of Contents

- [Lab Notebook Template](#lab-notebook-template)
- [Overview](#overview)
- [Data Structures in `pandas`](#data-structures-in-pandas)
- [Creating a `DataFrame`](#creating-a-dataframe)
- [Interacting With a `DataFrame`](#interacting-with-a-dataframe)
- [Other `DataFrame` Tasks](#other-dataframe-tasks)
- [How to submit this lab (and show your work)](#how-to-submit-this-lab-and-show-your-work)
- [Lab Notebook Questions](#lab-notebook-questions)

[Click here](https://colab.research.google.com/drive/1rB4f9NsbjbmOTwriFcdFwqNYlhbQCJjz?usp=sharing) to access the lab procedure as a Jupyter Notebook (Google Colab, ND Users)

## Lab Notebook Template

[Click here](https://colab.research.google.com/drive/1sKrGhGa_uvJw7l4QiKGKP-X_sAMlcQrq?usp=sharing) to access the lab notebook template as a Jupyter Notebook (Google Colab, ND Users)

## How to Submit This Lab (and show your work)

Moving forward, we're going to be submitting lab notebooks using the provide Jupyter Notebook template ([link for this lab's template](https://colab.research.google.com/drive/1sKrGhGa_uvJw7l4QiKGKP-X_sAMlcQrq?usp=sharing)).
- If working in JupyterLab (or another desktop IDE), download the `.ipynb` file to your local computer
  * `File` - `Download` - `Download as .ipynb`
- If working in Google Colaboratory, MAKE SURE you save a copy to your local drive. Otherwise your changes will not be saved.
  * `File` - `Save a copy in Drive`

The lab notebook template includes all of the questions as well as pre-created markdown cells for narrative text answers and pre-created code cells for any programs you may need to create. 
- Double click on these cells to edit and add your own content
- If questions do not require a code component, you can ignore those cells
- If questions to not require a narrative component, you can ignore those cells

If working in JupyterLab or another desktop IDE, upload the lab notebook template `.ipynb` file to Canvas as your lab submission.
- NOTE: This lab also asks you to upload a PDF version of this notebook. You are welcome, but not required, to do that moving forward.

If working in Google Colaboratory, submit the link to your notebook (checking sharing permissions, similar with Google Docs) AS WELL AS the `.ipyb` file

# Overview

<p align="center"><img src="https://github.com/kwaldenphd/pandas-intro/blob/main/images/Peebo.png?raw=true" width="1000"></p>

Some of you may be wondering why we are talking about pandas in a Computer Science course....

Panda: "a large black-and-white mammal (Ailuropoda melanoleuca) of chiefly central China that feeds primarily on bamboo shoots and is now usually classified with the bears (family Ursidae)" ([Merriam-Webster](https://www.merriam-webster.com/dictionary/panda))

Wait that's not right....

`pandas`: "a fast, powerful, flexible and easy to use open source data analysis and manipulation tool, built on top of the Python programming language" ([`pandas` documentation](https://pandas.pydata.org/))

That makes more sense.

If you remember back to our earlier work with `.csv` files in Python, there are limitations to the kinds of things we can do with structured data using the `csv` module. Particularly if we want to analyze and visualze structured data in a Python programming environment, we aren't going to get very far loading `csv` files as lists or dictionaries. We need Python to understand or interact with structured data as structured data.

## Enter `pandas`! 

Software developers at AQR Capital Management began working on a Python-based tool (written in a combination of C and Python) for quantitative data analysis in 2008. The initial open-source version of `pandas` was released in 2008.

At its core, "`pandas` is a software library written for the Python programming language for data manipulation and analysis. In particular, it offers data structures and operations for manipulating numerical tables and time series" ([Wikipedia](https://en.wikipedia.org/wiki/Pandas_(software)). The name `pandas` is derived from "panel data," an econometrics term used to describe particular types of datasets. The name `pandas` is also a play on "Python data analysis."

For more on the history and origins of `pandas`, check out Wes McKinney's ["pandas: a Foundational Python Library for Data Analysis and Statistics"](https://www.dlr.de/sc/Portaldata/15/Resources/dokumente/pyhpc2011/submissions/pyhpc2011_submission_9.pdf) 2011 paper.

`pandas` is based on and has some similarities with another Python package, `NumPy`. According to [package documentation](https://numpy.org/doc/stable/user/whatisnumpy.html), "`NumPy` is the fundamental package for scientific computing in Python. It is a Python library that provides a multidimensional array object, various derived objects (such as masked arrays and matrices), and an assortment of routines for fast operations on arrays, including mathematical, logical, shape manipulation, sorting, selecting, I/O, discrete Fourier transforms, basic linear algebra, basic statistical operations, random simulation and much more."

In `NumPy`, data are stored as list-like objects called arrays. `NumPy` allows users to access, split, reshape, join, etc. data stored in arrays. `pandas` takes a similar approach to structured data, or data organized in a tabular (i.e. table-like) format. "pandas adopts significant parts of NumPy's idiomatic style of array-based computing, especially array-based functions and a preference for data processing without for loops...the biggest difference is that pandas is designed for working with tabular or heterogeneous data. NumPy, by contrast, is best suited for working with homogenous numerical array data" (Wes McKinney, Chapter 5 "Getting Started with Pandas" in *Python for Data Analysis*, pg. 125)

For more on `NumPy`:
- [NumPy website](https://numpy.org/)
- [NumPy documentation](https://numpy.org/doc/stable/)
- ["NumPy Introduction," W3Schools](https://www.w3schools.com/python/numpy_intro.asp)
- ["Introduction to NumPy Tutorial," Software Carpentry](https://software-carpentry.org/blog/2012/06/introduction-to-numpy-tutorial.html)

## Data Structures in `pandas`

<p align="center"><img src="https://github.com/kwaldenphd/pandas-intro/blob/main/images/series_df_diagram.png?raw=true" width="1000"></p>

`pandas` has two main data structures: `Series` and `DataFrame`.
- "A `Series` is a one-dimensional, array-like object containing a sequence of values...and an associated array of data labels, called its index" (McKinney, 126)
- A `DataFrame` includes a tabular data structure "and contains an ordered collection of columns, each of which can be a different value type" (McKinney, 130).

### `Series`

In `pandas`, "a `Series` is a one-dimensional, array-like object containing a sequence of values...and an associated array of data labels, called its index" (McKinney, 126). At first glance, a `Series` looks a lot like a Python list.

```Python
# import pandas package
import pandas as pd

# import Series and Data Frame components from pandas
from pandas import Series, DataFrame

# create a Series using pandas
obj = pd.Series([4, 7, -5, 3])

# show obj Series 
obj
```

A few notes on what's happening in this example:
- We imported the `pandas` package (using the `pd` alias) as well as the specific `Series` and `DataFrame` components.
- We created a `Series` object containing four integer values.

We could create a list with these values, but for data analysis we needed the functionality `pandas` provides for working with series. To verify `obj` is stored as an array-like object, we can use `pd.Series(obj).values` which should return `array([4, 7, -5, 3])`

We can also get the index attributes for `obj` using `pd.Series(obj).index`, which should return `RangeIndex(start=0, stop=4, step=1)`. The default index attributes assigned to objects in an array are integers `0` through `N-1`, where `N` is the length of the data. We can create our own index attributes for the data points by manually creating index labels.

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

Try to perform similar mathematical operations on values stored in a Python dictionary or list and you'll run into all kinds of data type errors. The `Series` object uses a similar data structure and opens up a wide range of analysis possibilities.

To create a `Series` from data in a Python dictionary:

```Python
# create dictionary
sdata = {'Ohio': 35000, 'Texas': 71000, 'Oregon': 16000, 'Utah': 5000}

# create Series from dict dictionary
obj3 = pd.Series(sdata)
```

Let's say we wanted to have the `Series` values appear in a specific order. We can specify the index (or key) label order when converting a dictionary to a Series.

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
- The `California` index is returning `NaN` for its value, which is "not a number" or "NA".
- The `Utah` value in `sdata` is not in the `obj4` series, because the idex label `Utah` was not in the manually assigned list of index values passed to the series through `index=true`.

We can use the `isnull()` or `notnull()` functions in `pandas` to detect missing data. These functions will return `TRUE` or `FALSE`.

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

#### Application

Q1: Describe a `Series` object in your own words.

Q2: Create your own `Series` object. Write code the accomplishes the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.
- Assign unique index attributes for each series value
- Access a series value(s) using the index label
- Perform at least two unique arithmetic operations on the Series
- Test for null values in your series

### `DataFrame`

While a `Series` object is a one-dimensional array, a `DataFrame` includes a tabular data structure "and contains an ordered collection of columns, each of which can be a different value type" (McKinney, 130). A `pandas` `DataFrame` has a row and column index--we can think of these as Series that all share the same index. Behold, a two-dimensional data structure!

In most situations, you'll create a `DataFrame` by reading in a structured data file. But we're going to manually create a `DataFrame` to better understand how they work in `pandas`. Let's go back to our state population data example. Say we have two dictionaries that include equal-length lists:

```Python
# create dictionary with three equal-length lists
data = {'state': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'], 
        'year': [2000, 2001, 2002, 2001, 2002, 2003],
        'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

# write data dictionary values to data frame
frame = pd.DataFrame(data)

# show newly-created frame
frame
```

Behold, a two-dimensional `DataFrame` object with rows, columns, labels, and values. The first object from each of the lists in our `data` dictionary now populate the first row of our `frame` DataFrame. This pattern continues for subsequent rows.

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
pd.DataFrame(data, columns=['year', 'state', 'pop'])
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

We could also manually insert values for specific rows using their index labels. If we wanted to add debt values for rows two, four, and five:

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

#### Application

Q3: Describe a DataFrame in your own words.

Q4: Create your own small DataFrame. Write code that accomplishes the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.
- Change the original column order
- Select a specific column(s) using its index label or name attribute
- Select a specific row(s) using its index label or index value
- Remove a column from the DataFrame
- Determine summary statistics for values in the DataFrame

# From Data File to `DataFrame`

As mentioned earlier in this lab, it's far more likely that you will load structured data from a file into Python, rather than manually creating a `DataFrame`. For this section of the lab, we're going to work with data about *Titanic* passengers. Navigate to https://raw.githubusercontent.com/kwaldenphd/pandas-intro/main/data/titanic.csv in a web browser to see the dataset.

We can load structured data into Python from a file located on our computer or from a URL, using `pd.read_csv()`. An example of how we would load the `titanic.csv` file in Python as a `Pandas` DataFrame:

```Python
# import pandas
import pandas as pd

# load titanic data from csv file
# titanic = pd.read_csv("titanic.csv")

# load titanic data from url
titanic = pd.read_csv("https://raw.githubusercontent.com/kwaldenphd/pandas-intro/main/data/titanic.csv")

# show first 5 rows of newly-loaded dataframe
titanic.head(5)
```

`pandas` provides the `read_csv()` function which stores `.csv` data as a `pandas` `DataFrame`. This `read_` prefix can be used with other structured data file formats, as we'll explore with JSON later.

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

From this output, we know we have integers (`int64`), floats (`float64`), and strings (`object`). Maybe we want a more technical summary of this `DataFrame`.

```Python
titanic.info()
```

`.info()` returns row numbers, the number of entries, column names, column data types, and the number of non-null values in each column. We can see from the `Non-Null Count` values that some columns do have null or missing values. `.info()` also tells us how much memory (RAM) is used to store this `DataFrame`.

## Application

Q5: Write code that loads in a different `.csv` file as a DataFrame and accomplishes each of the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.
- Shows the first five rows
- Shows the last five rows
- Checks the data types for each column
- Returns a technical summary for the DataFrame

## Other Data Loading Challenges

We can also run into situations where the data we are loading into Python has missing values. We can specify what characters representing missing data when we create the `DataFrame`.

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
`skipfooter` | Number of lines to ignore at the end of the file
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

### Application

For Q6-Q9, you do not need to write code that actually loads an existing data file. That is, the lab does not provide data files that include these structures/attributes.

Write sample code that shows the syntax you would use to load a file with the structures/attributes described in the question.

For example, your answers might look something like the sample syntax shown in the previous section of the lab..

HINT: Be prepared to reference and consult the additional pd.read_csv function arguments listed in the previous lab section's tables.

Q6: Write code that loads in a structured data file that uses a pipe symbol (|) as a delimiter. Include code + comments.
 
Q7: Write code that loads in structured data file in which missing data values are represented by "?", "??", and "-" characters. Include code + comments.

Q8: Write code that ignores the last 6 rows of a structured data file. Include code + comments.

Q9: Write code that parses a structured data file in which commas "," are used as a thousands separator. Include code + comments

# Interacting with a `DataFrame`

## Sorting

`pandas` includes a few different built-in sorting operations. We can sort by an index for either axis of our `DataFrame` (i.e. we can sort based on row index labels or by column name). Going back to our Titanic passenger data, let's say we wanted to sort by passenger age.

```Python
# import pandas
import pandas as pd

# load titanic data from url
titanic = pd.read_csv("https://raw.githubusercontent.com/kwaldenphd/eda-pandas/main/data/titanic.csv")

# show first 5 rows of newly-loaded dataframe
titanic.head(5)

# sort by passenger age and show first five rows of the sorted data
titanic.sort_values(by="Age").head()
```

The default for `.sort_values` is to sort in ascending order. We can use `ascending=False` to sort in descending order.

```Python
titanic.sort_values(by=['Age'], ascending=False)
```

NOTE: When sorting, we are returning a sorted `DataFrame`. We ARE NOT updating the `DataFrame` in place. We have a couple of options to sort in place.

```Python
# create new dataframe with sorted results
titanic_by_age = titanic.sort_values(by="Age")

# check newly-created dataframe
titanic_by_age.head()
```

```
# sort values in place
titanic.sort_values(['Age'], inplace=True)

# check newly-created dataframe
titanic.head()
```

We can also sort by multiple fields. To sort by class cabin and age, in descending order:

```Python
titanic.sort_values(by=['Pclass', 'Age'], ascending=False).head()
```

When sorting by fields with string data, `a-z` is considered `ascending` and `z-a` would be `descending`.

## Subsetting

### Select

To review, we can select specific columns from a `DataFrame`. 
```Python
# creates Series object with age values
ages = titanic["Age"]

# show new object
ages
```

We can use `[" "]` to select a specific single column of interest. Python returns this single column's data as a `Series` object. We can also create a new data frame based on multiple columns.

```Python
# selects multiple columns to form new dataframe
age_sex = titanic[["Age", "Sex"]]

# checks first five rows of new dataframe
age_sex.head()
```

When selecting multiple columns, the inner brackets (`[]`) define the column names to subset or select. The outer brackets select data from a dataframe. In this multi-column example, `age_sex` is a `DataFrame` because it is a two-dimensional object.

For more on sorting operations in `pandas`, check out the package's ["Sorting" documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/basics.html#sorting).

### Filter

We can use Python's comparison operators to return rows in our `DataFrame` that meet specific conditions. Let's say we wanted to create a new `DataFrame` only containing data for passengers older than 35 years.

```Python
above_35 = titanic[titanic["Age"] > 35]

# check first five rows of newly-created dataframe
above_35.head()
```

We use brackets (`[]`) to set a condition rows must meet to be assigned to the new dataframe. If we just wanted to see whether rows meet this condition in the original `DataFrame`, we could just test for the condition without creating a new `DataFrame`.

```Python
titanic["Age"] > 35
```

Maybe we want to create a new data frame containing data on passegers in cabin class 2 and 3.
```Python
class_23 = titanic[titanic["Pclass"].isin([2, 3])]

# check first five rows of newly-created dataframe
class_23.head()
```

The `isin()` conditional function on its own would return a `True` or `False` value. By nesting the `isin()` function in brackets (`[]`), we are filtering rows based on rows  that meet the function critera, or return as `True` from this function.

We could also break out the chained or compound conditional statement using an `OR` operator, `|`.
```Python
class_23_alternate =  titanic[(titanic["Pclass"] == 2) | (titanic["Pclass"] == 3)]

class_23_alternate.head()
```

For more on Boolean indexing and the `isin()` function:
- ["Boolean indexing," Pandas documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#indexing-boolean)
- ["Indexing with isin," Pandas documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#indexing-basics-indexing-isin)

We could also create a new dataframe with passenger data for only passengers that have a known age.
```Python
age_known = titanic[titanic["Age"].notna()]

age_known.head()
```

`.notna()` is a conditional function that returns `True` for rows that do not have a `Null` value. For more on missing values and related functions, check out [the "Working with missing data" package documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/missing_data.html#missing-data).

### Selecting specific rows and columns

Selecting lets us isolate columns, and filtering identifies specific rows. But we can imagine a scenario in which we would want to combine these elements. We might want to create a new dataframe containing only the names of passengers who are over 35 years old.
```Python
over_35_names = titanic.loc[titanic["Age"] > 35, "Name"]

over_35_names
```

`.loc` identifies the rows we are writing to the new dataframe. What we are passing to the `loc` operator includes the row filter condition (`titanic["Age"] > 35`) and the column we are writing to the new dataframe (`Name`). 

We can also select rows and columns based on their index position. We could isolate rows 10-25 and columns 3-5 with the following expression:
```Python
titanic.iloc[9:25, 2:5]
```

We can also assign new values to our selection using `loc` or `iloc`. `loc` isolates rows based on their value, while `iloc` isolates rows based on their index position or label. Let's say we wanted to anonymize the first three names in the dataset. We could do this using `titanic.iloc[0:3, 3] = "anonymous"`.

Consult the ["Different choices for indexing"](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#indexing-choice) documentation for more on indexing options.

A few key takeaways:
- We use square brackets `[]` to subset data.
- We can specify single rows or columns, a list of rows/columns, or conditional expression within those brackets
- Select specific rows and/or columns using `loc` when working with row/column names
- Select specific rows and/or columns usign `iloc` when working with index positions
- You can assign new values to selection using `loc` or `iloc`

## From `DataFrame` to Data File

Let's say we have data in a `DataFrame` and want to write that to a file. While `.read_` loads data, `.to_` writes data. 

Let's say we want to save our filtered `DataFrame` as an Excel file.
```Python
df.to_excel("df.xlsx", sheet_name="data", index=False)
```

In this example, we create a new Excel file with a single sheet (`data`) that stores the data from our `df` `DataFrame`. `index=False` means that row index labels are not included in the new spreadsheet.

We could load back in the new Excel file and write it to a `.csv` file, dropping the header row:
```Python
# load Excel file as dataframe
df = pd.read_excel("df.xlsx", sheet_name="data")

# write dataframe to CSV file with no header
df.to_csv("df.csv", header=False, index=False)
```

## Application

Q10A: Using the DataFrame you created for Q5, write code that executes AT LEAST FOUR of the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.
- Sorts a column by ascending values
- Sorts a column by descending values
- Selects a specific column in the DataFrame
- Creates a new DataFrame with select columns from existing DataFrame
- Uses a comparison operator to filter rows in the DataFrame
- Uses an isin statement to filter rows in the DataFrame
- Selects specific rows and columns

Q10B: Write your modified `DataFrame` from Q10A to a `.csv` file. Your answer for these items should include a Python program + comments that document process and explain your code.

# Other `DataFrame` Tasks

## Removing Duplicates

A useful place to start is identifying and removing any duplicate rows in a dataframe. We can do this using a few key functions. `.duplicated()` will return a `True` or `False` value indicating if a row is a duplicate of a previously occuring row.
```Python
data_frame.duplicated()
```

`.drop_duplicates()` will return a dataframe containing only rows that are not duplicated.
```Python
new_data_frame = old_data_frame.drop_duplicates()
```

## Handling Missing Data

As mentioned previously, we can specify how `pandas` handles missing values when working with a data frame object.

### `.dropna()`

We can use `.dropna()` to drop any row containing a missing value:
```Python
no_na = data_frame.dropna()
```

To drop any column containing a missing value, we can specify the axis:
```Python
no_na_columns = data_frame.dropna(axis=1, how='all')
```

### `.fillna()`

But we can imagine a scenario in which you don't want to filter out missing data. The `.fillna()` function will replace missing data with a specified value. The default function will replace all missing data in the dataframe:

```Python
# replaces all missing data with 0
df.fillna(0)
```

We can also specify a different missing fill value for specific columns using a dictionary.

```Python
# replace missing data in column 1 with 0.5 value and in column 2 with 0
df.fillna({1: 0.5, 2: 0})
```

In these examples, `.fillna()` returns a new object, but we can also modify the existing object in-place by setting `inplace` to `True`.
```Python
# modify existing object in-place
df.fillna(0, inplace=True)
```

We can also copy (or propogate) the last valid observation into missing data using specific methods that go along with `.fillna()`.
- Fill Forward (`ffill`) will take the "last known value" and apply it to missing data entries, until you hit the next non-null observation in the data frame.
- Back Fill (`bfill`) goes the other direction, starting from the last row in the dataset. The "last known value" is applied to missing data entries until you hit the next non-null observation.

To use forward fill on all missing values in a dataframe:
```Python
df.fillna(method='ffill')
```

To use back fill on all missing values in a dataframe:
```Python
df.fillna(method='bfill')
```

## Application

Q11A: Using the DataFrame you created for Q5 (and used in Q10), write code that executes AT LEAST ONE of the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.

- Removes duplicate rows
- Removes rows with missing values
- Fills missing values using .fillna, ffill, or bfill

Q11B: Write your modified `DataFrame` from Q11A to a `.csv` file. Your answer for these items should include a Python program + comments that document process and explain your code.

# How to Submit This Lab (and show your work)

Moving forward, we're going to be submitting lab notebooks using the provide Jupyter Notebook template ([link for this lab's template](https://colab.research.google.com/drive/1sKrGhGa_uvJw7l4QiKGKP-X_sAMlcQrq?usp=sharing)).
- If working in JupyterLab (or another desktop IDE), download the `.ipynb` file to your local computer
  * `File` - `Download` - `Download as .ipynb`
- If working in Google Colaboratory, MAKE SURE you save a copy to your local drive. Otherwise your changes will not be saved.
  * `File` - `Save a copy in Drive`

The lab notebook template includes all of the questions as well as pre-created markdown cells for narrative text answers and pre-created code cells for any programs you may need to create. 
- Double click on these cells to edit and add your own content
- If questions do not require a code component, you can ignore those cells
- If questions to not require a narrative component, you can ignore those cells

If working in JupyterLab or another desktop IDE, upload the lab notebook template `.ipynb` file to Canvas as your lab submission.
- NOTE: This lab also asks you to upload a PDF version of this notebook. You are welcome, but not required, to do that moving forward.

If working in Google Colaboratory, submit the link to your notebook (checking sharing permissions, similar with Google Docs) AS WELL AS the `.ipyb` file

# Lab Notebook Questions

[Click here](https://colab.research.google.com/drive/1sKrGhGa_uvJw7l4QiKGKP-X_sAMlcQrq?usp=sharing) to access the lab notebook template as a Jupyter Notebook (Google Colab, ND Users)

Q1: Describe a `Series` object in your own words.

Q2: Create your own `Series` object. Write code the accomplishes the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.
- Assign unique index attributes for each series value
- Access a series value(s) using the index label
- Perform at least two unique arithmetic operations on the Series
- Test for null values in your series

Q3: Describe a DataFrame in your own words.

Q4: Create your own small DataFrame. Write code that accomplishes the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.

- Change the original column order
- Select a specific column(s) using its index label or name attribute
- Select a specific row(s) using its index label or index value
- Remove a column from the DataFrame
- Determine summary statistics for values in the DataFrame

Q5: Write code that loads in a different `.csv` file as a DataFrame and accomplishes each of the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.

- Shows the first five rows
- Shows the last five rows
- Checks the data types for each column
- Returns a technical summary for the DataFrame

For Q6-Q9, you do not need to write code that actually loads an existing data file. That is, the lab does not provide data files that include these structures/attributes.

Write sample code that shows the syntax you would use to load a file with the structures/attributes described in the question.

For example, your answers might look something like the sample syntax shown in the previous section of the lab..

HINT: Be prepared to reference and consult the additional pd.read_csv function arguments listed in the previous lab section's tables.

Q6: Write code that loads in a structured data file that uses a pipe symbol (|) as a delimiter. Include code + comments.
 
Q7: Write code that loads in structured data file in which missing data values are represented by "?", "??", and "-" characters. Include code + comments.

Q8: Write code that ignores the last 6 rows of a structured data file. Include code + comments.

Q9: Write code that parses a structured data file in which commas "," are used as a thousands separator. Include code + comments

Q10: Using the DataFrame you created for Q5, write code that executes AT LEAST FOUR of the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.

- Sorts a column by ascending values
- Sorts a column by descending values
- Selects a specific column in the DataFrame
- Creates a new DataFrame with select columns from existing DataFrame
- Uses a comparison operator to filter rows in the DataFrame
- Uses an isin statement to filter rows in the DataFrame
- Selects specific rows and columns

Q11: Using the DataFrame you created for Q5 (and used in Q10), write code that executes AT LEAST ONE of the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.

- Removes duplicate rows
- Removes rows with missing values
- Fills missing values using .fillna, ffill, or bfill
