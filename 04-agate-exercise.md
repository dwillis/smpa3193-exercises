### Agate Exercise

#### Percent Change

Here we will import county population estimates from the Census Bureau, calculate the percent change in population from 2010-2015 and print out the 50 fastest growing counties. You can find the CSV file [here](https://raw.githubusercontent.com/dwillis/smpa3193-exercises/master/county_population.csv); download it to your class exercise folder.

Then, in Terminal, start a jupyter notebook and head to the browser page. Let's call this notebook `population` and instead of calculating percent change in a spreadsheet, we'll do it in Python. For our purpose, percent change is 2016's population compared to 2010.

Let's get started:

```python
import agate
counties = agate.Table.from_csv("county_population.csv")
print counties
```

We'll need to add a column to the `counties` table using Agate's `compute` and `PercentChange` functions:

```python
popchange1016 = counties.compute([
    ('change', agate.PercentChange('estimate_2010', 'estimate_2015'))
])
```

See how you didn't have to type a formula? Agate has it built-in. Let's look at the results!

```python
print popchange1016[0]['change']
```

Well, that seems like an excessive number of numbers after the decimal point. Maybe we can do something about that. Python has a Decimal library that can do the rounding for us. First we'll write a Python method called `round_change` that will do the rounding, and then we'll use that to add the rounded change to our table:

```python
from decimal import Decimal

def round_change(row):
    return row['change'].quantize(Decimal('0.1'))

rounded_change = popchange1016.compute([
    ('change_rounded', agate.Formula(agate.Number(), round_change))
])
```

Let's see what that looks like:

```python
print rounded_change[0]['change_rounded']
```

Now we sort it using `order_by` and then can use `print_table` to display a subset of the columns (county, state and change_rounded):

```python
sorted_counties = rounded_change.order_by('change', reverse=True)
sorted_counties.select(['county', 'state', 'change_rounded']).print_table(max_rows=50)
```

#### Assignment

In your jupyter notebook file, write instructions to do the following:

    1. Show all of the counties in North Dakota, in order of largest change to smallest
    2. Show the bottom 50 counties nationwide in terms of population change (the smallest change)
    3. Show the top 50 counties sorted by 2015 estimated population, with the largest population first
    4. Calculate an average change for all states and show the state and average in descending order
