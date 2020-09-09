# Homework 2 - JavaScript Basics

**Due: 9/18 (Fri) 18:00 (This is a hard deadline)**

This is an **individual** assignment.
This assignment is for you to become familiar with JavaScript. JavaScript will be used to build a frontend system in hw3, using the React framework. By implementing features in this assignment, you will learn the followings:

1. JavaScript built-in methods (e.g. `map`, `filter`, etc)
2. JavaScript regular expression `RegExp`
3. Handling HTML form element

### Popular Baby Name Website

Using the information parsed in hw1, you will implement a website that shows the statistics (e.g. annual ranking,year-on-year change of name popularity) of popular baby names in the USA. To complete this assignment, you have to implement 4 functions (`parseAndSave`, `provideYearData`, `provideChartData`, and `handleSignUpFormSubmit`) in `app.js`. The skeleton of each function is provided. 

### File Description

```bash
[hw2 root]
  ├── app.js  <= you need to modify this file.
  ├── base.css
  ├── base.js
  ├── chart
  │   └── chart.min.js
  ├── data
  │   └── babyname.report.csv
  ├── index.html
  └── materialize
      ├── LICENSE
      ├── README.md
      ├── css
      │   └── materialize.min.css
      └── js
          └── materialize.min.js
```

Each of the file or directory in this repository serves the following role:

**NOTE: Students are only required to modify `app.js` file in this section.**

- `app.js` : includes data parsing/processing and form checking functions.
- `base.js` : includes event handling and rendering codes. Functions in `app.js` are called in `base.js`.
- `index.html` : defines the layout of the webpage.
- `data/babyname.report.csv` : includes the top 1000 baby names for each year (it is the output of hw1). 
- `base.css` : style formats utilized by `index.html`.
- `chart/chart.min.js` : includes a function which visualizes a baby name's rank trend.
- `materialize/` : `Materialize` CSS framework code.

The following 4 functions in `app.js` are to be filled in by students:

- `parseAndSave(text)`: parses `text` (the content of CSV file) and saves the parsed data into the global variable, `records`.
- `provideYearData(year)`: filters baby names of the `year` from `records` and joins the male and female records with the same rank. The output is an array of joined data that are organized in ascending order based on the rank.
- `provideChartData(name, gender)`: returns the ranks from 2001 to 2018 of a baby name to show the chart of name popularity by year.
- `handleSignUpFormSubmit(form)`: checks if the sign up form at the bottom of the web page satisfies the requirements.

You can refer to `base.js` to figure out the usages of each function and how the elements of the html changes using DOM APIs.
(This is optional; It's totally okay to skip it over.)

### How To Start


To open the website, you should run an HTTP server. There are two options to do this:

**[Option 1] Open with Python `http.server`.**

```bash
$ cd swpp-hw2-USERNAME    # You should run the server in hw2 root directory.
$ python -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...

# You will a message like above. Copy and paste the address to your web browser.
```

When you open the url (`http://0.0.0.0:8000/` in the example above), you can see the initial skeleton website.


**[Option 2] Open with VSCode extension "Live Server".**

<p align="center"><img src="images/live_server_extension.png" width="400" alt="live server extension"></img></p>

- Open VSCode extension tab (Code > Preferences > Extensions) and search **"Live Server"**.
- When you click **"Install"**, then you can find a **"Go Live"** button on the right-bottom side of the status bar.

<p align="center"><img src="images/enable_live_server.png" width="400" alt="start live server"></img></p>

- Open your hw2 root folder (e.g. swpp-hw2-USERNAME) on VSCode. (File > Open)
- Click **"Go Live"** button, then your default web browser will be automatically opened, and you will see the initial website like below.

<p align="center"><img src="images/before_preview.png" width="500" alt="site overview"></img></p>

- When you click a name, an empty chart will be dropped down.

<p align="center"><img src="images/before_chart.png" width="500" alt="chart overview"></img></p>

- When you want to close the live server, click the button highlighted with the red box.

<p align="center"><img src="images/disable_live_server.png" width="400" alt="disable live server"></img></p>

### Expected Output

Correctly implemented functions in `app.js` will show the results as follows:

**1) `parseAndSave` and `provideYearData`**

By implementing both `parseAndSave` and `provideYearData`, name and rank data of the year will show up in the table.

<p align="center"><img src="images/after_list.png" width="500" alt="correct list"></img></p>

**2) `provideChartData`**

A baby name's rank chart will be drawn with the data provided by `provideChartData`, when the user clicks a name in the table.

<p align="center"><img src="images/after_chart.png" width="500" alt="correct chart"></img></p>

**3) `handleSignUpFormSubmit`**

By clicking the sign-up button, `handleSignUpFormSubmit` will conduct form checking and an alert message will show up. There are four input fields to fill in and each field should meet the following requirements to be validated.

- Email: Start with characters other than @ or whitespace, followed by an @ sign, followed by more characters (except `@`, `.`, or whitespace), then a `.`, and finally followed by 2 to 3 alphabets from a to z.
  - `characters(except for whitespace and '@')` **@** `characters(except for whitespace, '@' and '.')` **.** `2-3 alphabets` 
  - *characters* mean one or more characters including alphabets, numbers or special characters.
  - *alphabets* include both lowercase and uppercase.
  - e.g.) valid@javascript.com (O), invalid@snu.ac.kr (X)
- First name (English) : Start with a capital letter, followed by one or more lowercase letters. Should only contain alphabets (A-Z, a-z)
- Last name (English) : Start with a capital letter, followed by one or more lowercase letters. Should only contain alphabets (A-Z, a-z)
- Date of birth: The format should be YYYY-MM-DD.
  - YYYY (Year) : Must be a number between 1900 and 2020 (inclusive).
  - MM (Month) : Must be a number with two digits between 01 and 12.
  - DD (Date) : Must be a number with two digits between 01 and 31.

If users submit invalid data, the alert message should pop up and validation error messages show up right below the corresponding input fields. The validation error messages of each field should be:

- First Name : "Invalid first name"
- Last Name : "Invalid last name"
- Email : "Invalid email"
- Data of birth : "Invalid date of birth"

Below is an example when you enter the wrong data into every field.

<p align="center"><img src="images/invalid_example.png" width="500" alt="invalid form"></img></p>

Following is an example when you enter the valid data into every field. In this case, each input field should not show any message.

<p align="center"><img src="images/valid_example.png" width="500" alt="valid form"></img></p>

If the form does not satisfy the requirements (for example, if Email, First Name, Last Name and Data of Birth fail), the alert message should look like:

```
You must correct: 

First Name
Last Name
Email
Date of Birth
```
The first error message "You must correct" is followed by the empty line. Names of incorrect inputs are listed up from the third line. The listing order of those names does not matter. Leading and trailing whitespaces of each line are not taken into account in grading.

If the form satisfies the requirements, the alert message **must** be `Successfully Submitted!`. No leading and trailing whitespaces are allowed.

You should set the value of `alertMessage` following the specification above.
Please make sure that you do not trigger the alert function in this function. It is handled in `base.js`.

The function argument `form` is of `HTMLFormElement`.
This is a DOM element corresponding to the following form tag in `index.html`:
```html
<form id="signup-form" class="...">
  ...
  <input name="first-name" type="text" class="...">
</form>
```
You can access the input element of the form using the `name` attribute of the form (e.g. `let field = form['first-name']`).
Then, you can access its value with `field.value`.
All the other input fields can be accessed likewise.

For more information on HTML Form APIs,
see the documents: [HTMLFormElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement) and [HTMLInputElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement).



**Important Note**:
You **must not** manipulate or directly read from HTML elements
except the `form` object given as function argument in `app.js`.
For example, you are not allowed to get the reference to the form
by using `document.getElementById`, `document.querySelector` and other similar APIs.


## Grading

This assignment is composed of a total of 15 points.

The functions in `app.js` will be graded. We will see the outputs to validate your answers.

- `parseAndSave` : 3 points
- `provideYearData` : 5 points
- `provideChartData` : 2 points
- `handleSignUpFormSubmit` : 5 points
- Partial points for minor errors


## Submission

**Due: 9/18 (Fri) 18:00 (This is a hard deadline)**

We will check the snapshot of the *master* branch of your Github repository at the deadline and grade it. As you already did in hw1, create a **private** repository with name `swpp-hw2-{USERNAME}` and add TA **`kdh0102`** as your collaborator in the repository settings! Your repository should look like below:

```bash
repository_root/
  ├── app.js
  ├── base.css
  ├── base.js
  ├── chart
  │   └── chart.min.js
  ├── data
  │   └── babyname.report.csv
  ├── index.html
  └── materialize
      ├── LICENSE
      ├── README.md
      ├── css
      │   └── materialize.min.css
      └── js
          └── materialize.min.js
```

Also, make sure to push your work on Github on time.
