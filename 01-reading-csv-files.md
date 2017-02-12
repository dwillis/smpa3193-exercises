### Reading CSV files (offline and online)

#### Setup

  1. Open your PythonAnywhere account, go to the Files tab and upload the `baby_names_nyc.csv` to your account.
  2. Switch to your Consoles tab and then your already started bash console.
  3. Type `ls` to see that your baby names csv file is there.

#### Working with local CSV file

  1. Start up a Python session by typing `python`
  2. Let's import the tool we'll need to read in a CSV file: Python's [csv module](https://docs.python.org/2/library/csv.html), open the CSV file and then print out each row:
  ```python
  import csv
  file = open('baby_names_nyc.csv')
  csv_data = csv.reader(file)
  for row in csv_data:
    print row
  ```

  3. Try the last two lines again.

#### Working with an online CSV file

  Exit the Python session using Control-D and let's setup what we need to grab a file from the Web, including the library that handles [making web requests](http://docs.python-requests.org/en/master/). Copy the following command:

  `pip install urllib3[secure] pyopenssl ndg-httpsclient pyasn1 requests`

  Then type `python` to start a new session:

  ```python
  import csv
  import requests
  url = ""
  r = requests.get(url)
  csv_data = csv.reader(r.text)
  for row in csv_data:
    print row
  ```
