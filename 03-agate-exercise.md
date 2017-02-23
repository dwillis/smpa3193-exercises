### Agate Exercise

#### Data Smells

  Any time you are given a dataset from anyone, you should immediately be suspicious. Is this data what I think it is? Does it include what I expect? Is there anything I need to know about it? Will it produce the information I expect?

  One of the first things you should do is give it the smell test. Agate is a great tool for doing it, because it leaves a record of your work.

  Failure to give data the smell test can lead you to miss stories and get your butt kicked on a competitive story. Let's look at arrest data for Fairfax County, Va.

  The easiest way to do this is to use the same terminal window that you used in class. If you closed it, using Terminal cd to the directory of your class repository and type `workon exercises` to turn on the virtualenv.

  1. Download the [arrest.csv](https://raw.githubusercontent.com/dwillis/smpa3193-exercises/master/arrest.csv) file to the directory where we've been working on Python in class (with the virtualenv already activated). If you have a Python session running, exit it using Control-D.
  2. Start your notebook by typing `jupyter notebook`; it should open http://localhost:8888/ in a browser.
  3. Using the `New` drop-down, choose `Python 2` notebook.
  4. Name your notebook by clicking on `Untitled` and typing in "arrest" and hitting the OK button.
  5. Type in the following commands, clicking the Cells -> Run Cells drop-down selection after each line:

  ```python
  import agate
  results = agate.Table.from_csv("arrest.csv")
  ```

  With data smells, we're trying to find common mistakes in data. For more on data smells, read the GitHub wiki post that started it all. The common mistakes we're looking for are:

  * Missing data
  * Gaps in data
  * Wrong type of data
  * Outliers
  * Sharp curves
  * Conflicting information within a dataset
  * Conflicting information across datasets
  * Wrongly derived data
  * External inconsistency
  * Wrong spatial data
  * Unusable data, including non-standard abbreviations, ambigious data, extraneous data, inconsistent data

  But with several of these data smells, we can do them first, before we do anything else. First, let's look at Wrong Type Of Data. We can sniff that out by simply printing the table structure that Agate has discovered for us.

  ```python
  print arrests
  ```

  Here are the other checks we want to make. In each case, write some Python code using Agate's functions to accomplish the tasks below (see the [cookbook](http://agate.readthedocs.io/en/1.5.5/cookbook.html) for examples, including Agate versions of common SQL ans Excel tasks).

  1. Missing Data - let's start with `Charge Descrip` and see whether every row has a charge description.
  2. Outliers - let's look at `Age` and count the number of times each age appears, sorting from most to least.
  3. Outliers - can you calculate the average (median) age for each charge description?
  4. Inconsistent data - how many rows have addresses with Alexandria (or versions of Alexandria, including abbreviations)?

  Don't worry too much about getting these perfect, and don't worry about running into errors. Use the examples from your earlier Agate work and from the cookbook, adapting them with the fields our arrest data has. If you get stuck on something, exit the jupyter notebook using Control-C and push the arrest.ipynb file to your Github repository and send me an email with your question and a link to your file.
