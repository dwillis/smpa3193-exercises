
### Agate Exercise

  1. Download the [mdcounty2014.csv](https://raw.githubusercontent.com/SMPA3193/python/master/mdcounty2014.csv) file to the directory where we've been working on Python in class (with the virtualenv already activated). If you have a Python session running, exit it using Control-D.
  2. Start your notebook by typing `jupyter notebook`; it should open http://localhost:8888/ in a browser.
  3. Using the `New` drop-down, choose `Python 2` notebook.
  4. Name your notebook by clicking on `Untitled` and typing in "agate" and hitting the OK button.
  5. Type in the following commands, clicking the Cells -> Run Cells drop-down selection after each line:

  ```python
  import agate
  results = agate.Table.from_csv("mdcounty2014.csv")
  print(results)
  row = results.rows[0]
  row['jurisdiction']
  by_county = results.group_by('jurisdiction')
  totals = by_county.aggregate([('county_total', agate.Sum('votes'))])
  totals = totals.order_by('county_total', reverse=True)
  totals.limit(10).print_bars('jurisdiction', 'county_total', width=80)
  ```

  6. Let's do the same with candidates (`name_raw` is candidate name)
  7. Make sure to save your notebook.
  8. Shut down the notebook in terminal by hitting `Ctrl-C`
  9. Using git from Terminal, add your notebook file (`agate.ipynb`), commit it and push to your repository.
