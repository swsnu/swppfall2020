# Homework 1 - Python Basics

**Due: 9/11 (Fri) 18:00 (This is a hard deadline)**

This assignment is for you to become familiar with Python, which will be used to build a backend system in hw4.
This is an **individual** assignment.

From the beginning to the end of the development, you must use **GitHub** for version control.
This will be used for your submission as well, so please keep it in mind.

## Fix History
Click the links to see the commits that made changes.

- 9/6
  - [**Correction**: fix the example for `BabynameParser` in README.md](https://github.com/swsnu/swppfall2020/commit/8cf6a26a601eab25a89b033be2e3695873ce9039#diff-d4ebad57de104fd377fa5c0bd6f6dc92)

- 9/5
  - [**Comment fix for clarification**: Clarified comments for BabynameParser.](https://github.com/swsnu/swppfall2020/commit/9db5bab5158d99f71b2350707c60147f9d841f05)
  - [**Comment fix for clarification**: Clarified comments for run.py.](https://github.com/swsnu/swppfall2020/commit/e431fd115dc8eb1fd1408d3747c275be36ada7ee)
  - [**Comment fix for clarification**: Clarified comments for check_filename_existence](https://github.com/swsnu/swppfall2020/commit/969175222c1d9c99eb904e94782d8289f6e43d47)

- 9/4
  - [**Correction**: The output csv file name should be `babyname.report.csv`, not `output.csv`.](https://github.com/swsnu/swppfall2020/commit/0a01ada276c2052066777b0323c60db49b286adc)
  - [**Comment fix for clarification**: In `babyname_parser.py`, `parse` method returns a list of lambda function's output.](https://github.com/swsnu/swppfall2020/commit/559d1c68899789cb916cc8c0e5900152de16c9e3)
  - [**Correction**: `BabyFetchException` is raised when fetch is failed.](https://github.com/swsnu/swppfall2020/commit/f680a4ebbc9107971febbe5ec4fef1c4e8735d47)

## Python

### Objective

In this assignment, you will practice fetching HTML files from the Internet website, parsing the HTML files, and creating a csv file for the parsed data.
Based on the provided skeleton code, you will implement the functions needed to do the tasks above.

You don't have to understand the implemented methods provided in the skeleton code, but studying them can be useful for your future term project.
This project is a modification of google's [Baby Names Python Exercise](https://developers.google.com/edu/python/exercises/baby-names).

The goal of this assignment is to practice using various functions of the Python language.
In this assignment, you will get familiar with:

- Built-in functions
  - Python provides many useful built-in functions. You can write code more efficiently and effectively if you are fluent with such functions. 
- Class
  - You will need to modularize and encapsulate your code to neatly manage your project. Class is a core concept to achieve such objectives. It is an important component in design patterns that you will learn in future classes.
  Since you will define your own models with classes in homework 3, you should be familiar with it.
- Decorator
  - [Decorator](https://www.python.org/dev/peps/pep-0318/) is a special syntax in python for transforming functions using closure. It is also an important feature for applying design patterns in python, such as defining static methods or class methods.
  Many functions from Django are provided as decorators as well, especially with user authentication, which you will be using in homework 3.
- Lambda function
  - Lambda function helps you write your python code in a functional programming style. In certain situations, functional style makes your code more concise and easy to modularize.
  For more information, read [Functional Programming HowTo](https://docs.python.org/3/howto/functional.html).

### 1. Implement script to fetch the html files of popular babynames
You need to implement the `fetch.py` file that sends a request to fetch the HTML files from the [Social Security Administration website](https://www.ssa.gov/cgi-bin/popularnames.cgi), which provides neat data by year of what names are the most popular for babies born that year in the USA. We will extract HTML files ranging from 2001 to 2018. After fetching the files, you have to save them under `babydata` directory. The expected HTML files are given for reference under `babydata` directory. They should be matched with the output files that your script generates. To complete the fetching script, you should implement the following functions:

**1) `fetch_top_1000`**
This method receives two arguments: the year of interest and the target url. It returns the contents of the html file fetched from the given webpage. Use `urllib` to fetch the html file. Refer to [python documentation](https://docs.python.org/3/library/urllib.request.html#urllib.request.urlopen) for more information on `urllib`.

**2) `safe_internet_fetch`**
You need to implement a decorator that checks whether the request was successful. This decorator will decorate the `fetch_top_1000` function to handle the situations where fetching fails due to an invalid url or internet connection error by throwing `BabyFetchException`.
You can catch the above error using [urllib.error.URLError] (https://docs.python.org/3/library/urllib.error.html)
This method should be implemented as a decorator in order to be easily applied to other methods. Please check out [this document](https://www.programiz.com/python-programming/decorator) to understand how to implement python decorator.

For debuggability, defining your own exception and intentionally raising the exception is useful because you can identify the root cause of the exception and distinguish the exception from others. We provide `BabyFetchException` for this purpose. If the decorated function fails to fetch the data, this decorator has to raise the custom `BabyFetchException` with custom error message: `Request Failed`. We will not grade your decorator with it's stack trace but just test the class of the raised exception and it's message.

### 2. Implement `BabynameParser`

You need to implement the babyname parser class that parses the popular names and their ranks from the html files you saved.
In the skeleton code, `BabyParser` class is defined in `babyname_parser.py`. To complete the parser, you should implement the following functions:

**1) `__init__`**

This method is the constructor of the parser.
In this method, you need to extract a list of the tuples of (rank, male-name, female-name) from the given html file. 

**2) `check_filename_existence`**

You need to implement a decorator that checks whether the file exists or not.
This decorator will decorate the `__init__` of the parser to prevent constructing a parser with non-existing file name.

Just like the `safe_internet_fetch` above, we provide `BabynameFileNotFoundException` for this purpose. 
If there is no such file with the generated filename following the convention of the function to decorate, this decorator has to raise the custom `BabynameFileNotFoundException` with custom error message: `No such file: {filename}`.
You can assume that `filename` is the name generated using the first and second argument (i.e. directory path and year) for the function to decorate.

**3) `parse`**

This method applies a given lambda function to all of the extracted tuples and returns the results.

**Usage**

When you are done, you can parse any information about the popluar name ranks in a year by using the implemented parser. 
In the python console, you can test your code with the provided `2001.html` file like below.

```
>>> from babyname_parser import BabynameParser
>>> parser = BabynameParser("/{YOUR_HW_PATH}/babydata", 2001)
>>> parser.year
'2001'
>>> parser.rank_to_names_tuples
[('1', 'Jacob', 'Emily'), ('2', 'Michael', 'Madison'), ('3', 'Matthew', 'Hannah'), ...]
>>> parser.parse(lambda rank_to_names_tuple: rank_to_names_tuple[0])
['1', '2', '3', '4', '5', '6', '7', '8', '9', '10', ...]
>>> BabynameParser("./babydata", 1900)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "babyname_parser.py", line 61, in decorated
    raise BabynameFileNotFoundException("No such file: {}".format(filename))
babyname_parser.BabynameFileNotFoundException: No such file: ./babydata/1900.html
```

You should **NOT** edit parts other than those marked as `TODO`s in your skeleton code when you submit your assignment, because we will grade your `BabynameParser` implementation by not only running `run.py` file but also importing the class and test the methods like above (with different files and lambdas, of course).
Also, the error message that comes out when the entered file does not exist must be 
`No such file: {filename}` and the result of `parse` method must be a list of all processed tuples.
Same applies to the `fetch.py`.

### 3. Fill the run script

In `run.py` file, a skeleton code using the parser is provided.
Your task is to complete the code to parse all the html files that contain the popular baby names `BabynameParser`, and save all the data in a single csv file.

When you run `python run.py 2001 2018`,the script must generate a csv file named `babyname.report.csv`.
The content of the csv file should be as follows:

```
$ tail -10 /{YOUR_HW_PATH}/babydata/babyname.report.csv
2018,991,Emmarie,F,
2018,992,Esperanza,F,30
2018,993,Kailyn,F,90
2018,994,Aiyana,F,147
2018,995,Keilani,F,
2018,996,Austyn,F,
2018,997,Whitley,F,
2018,998,Elina,F,
2018,999,Kimora,F,34
2018,1000,Maliah,F,72

$ head -10 /{YOUR_HW_PATH}/babydata/babyname.report.csv
year,rank,name,gender,rank_change
2001,1,Jacob,M,
2001,2,Michael,M,
2001,3,Matthew,M,
2001,4,Joshua,M,
2001,5,Christopher,M,
2001,6,Nicholas,M,
2001,7,Andrew,M,
2001,8,Joseph,M,
2001,9,Daniel,M,
```

## Grading

### Python (15 points)

We will test your code under Python 3.7.

- `fetch.py` (total 3 points)
  - `safe_internet_fetch` : 1 point
  - `fetch_top_1000` : 2 points 
- `babyname_parser.py` (total 6 points)
  - `check_filename_existence` : 1 point
  - `BabynameParser > parse` : 5 points (includes the `__init__` constructor)
- `run.py` (total 6 points)
  - `BabyRecord > to_csv_record` : 1 point
  - `main` : 5 points
- Partial points for minor errors


## Submission

Due: 9/11 (Fri) 18:00 (This is a hard deadline)

You must create your own *private* repository under your account.
You don't need to submit your homework by email.
**Make sure to name your repository properly and to add TA as your collaborator in the repository settings!** (Detailed instructions below).
We will check the snapshot of the *master* branch of your Github repository at the deadline and grade it.
Since there are many students in this class, we need to automatize the grading process, so your homework may not be graded properly if your directory hierarchy doesn't look like this:
```
repository_root
├── LICENSE.txt
├── NOTICE.txt
├── babydata
│   ├── 2001.html-2018.html
│   └── babyname.report.csv
├── babyname_parser.py
├── fetch.py
└── run.py
```
Also, make sure to push your work on Github on time.

### Instructions on creating a private repository

#### I. Get GitHub Student Developer Pack

1. Go to `https://education.github.com`.
2. Follow instructions to `Request a discount`.

#### II. Make your private repository

1. Go to your github profile: `https://github.com/YOUR_USERNAME`.
2. Under `Repositories`, click on `New`.
3. Fill in `swpp-hw1-USERNAME` as your repository name, and mark is as `Private`. (e.g., `swpp-hw1-kdh0102`)
4. Hit `Create repository`.
5. In terminal, go to the directory that you will be working in (e.g., `~/workspace/swpp-hw1-USERNAME` or `~/swpp-hw1-USERNAME`)
6. Type in and run the following commands, which is also shown on the page that you will be looking at after step 4:

```
echo "# asdf" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/USERNAME/swpp-hw1-USERNAME
git push -u origin master
```

Alternatively you can start by copying skeleton codes :)
```
cp -r ${swppfall2020-home}/hw1 ~/workspace/swpp-hw1-USERNAME
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/USERNAME/swpp-hw1-USERNAME
git push -u origin master
```

7. Under `Settings` then `Collaborators` tab, Add Homework TA as your collaborator: **`kdh0102`**.
8. You're all set! After finishing your homework, push your contents to your repository on time!
