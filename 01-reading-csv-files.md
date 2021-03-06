
#### Working with local CSV file

  1. Download [this CSV file](https://raw.githubusercontent.com/dwillis/smpa3193-exercises/master/baby_names_nyc.csv) to your class folder inside your Desktop folder. (Column names [here](https://data.cityofnewyork.us/Health/Most-Popular-Baby-Names-by-Sex-and-Mother-s-Ethnic/25th-nujf))
  2. Open Terminal and start up a Python session by typing `python`
  3. Let's import the tool we'll need to read in a CSV file: Python's [csv module](https://docs.python.org/2/library/csv.html), open the CSV file and then print out each row:
  ```python
  import csv
  file = open('baby_names_nyc.csv')
  csv_data = csv.reader(file)
  for row in csv_data:
      print row
  ```

  4. Try the last two lines again.
  5. Let's loop through again, using a conditional to print out just those rows where the name is "IRENE". You'll need to read the file in again.

  ```python
  file = open('baby_names_nyc.csv')
  csv_data = csv.reader(file)
  for row in csv_data:
      if row[3] == 'IRENE':
          print row
  ```

#### Local Setup

  Exit Python using Control-D and in the same directory, do the following commands from the command-line:

  * `sudo pip install virtualenvwrapper`
  * `mkvirtualenv exercises`
  * `pip install agate`
  * `pip install jupyter`

#### Working with an online CSV file

  Now let's setup what we need to grab a file from the Web, including the library that handles [making web requests](http://docs.python-requests.org/en/master/). Copy the following command:

  `pip install urllib3[secure] pyopenssl ndg-httpsclient pyasn1 requests`

  Then type `python` to start a new session:

  ```python
  import csv
  import requests
  url = "https://raw.githubusercontent.com/dwillis/smpa3193-exercises/master/baby_names_nyc.csv"
  r = requests.get(url)
  csv_data = csv.reader(r.iter_lines())
  for row in csv_data:
    print row
  ```

  Now let's do it again, trying to isolate on "ELIJAH" using a conditional.
