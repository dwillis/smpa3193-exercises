### Agate Exercise

#### Percent Change

Here we will import county population estimates from the Census Bureau, calculate the percent change in population from 2010-2015 and print out the 50 fastest growing counties. You can find the CSV file [here](county_population.csv); download it to your class exercise folder.

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

Well, that seems like an excessive number of numbers after the decimal point. Maybe we can do something about that. Python has a Decimal library that can do the rounding for us. First we'll write a Python method that will do the rounding, and then we'll add the rounded change to our table:

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

Now we sort it.
