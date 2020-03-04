# Sacramento Homeless Services Dashboard

##### A project to provide a user friendly and interactive dashboard with data from Sacramento County's Homeless Management Information System

![top_of_dash](https://github.com/code4sac/sacramento-county-homeless-hmis-data/blob/master/images/HMIS_dash_top.JPG)

###### A homeless management information system (HMIS) is a database used to aggregate data on homeless populations served across the United States. This repository contains the source Sacramento County HMIS data (\*plus a locally-created exit_destinations csv file), a Jupyter Notebook that loads the data into a PostgreSQL database, a flask API that then serves the data from the database, and finally a web based dashboard using HTML, CSS, and JavaScript. The dashboard includes interactive charts that allows users to explore homeless services program volumes, outcomes, and participant demographics. An explanation of assumptions made for chart plotting is also included at the bottom of this readme.

![mid_dash](https://github.com/code4sac/sacramento-county-homeless-hmis-data/blob/master/images/HMIS_dash_middle.JPG)

## Execution Instructions

1. Create a local PostgreSQL database named "sac_hmis_db".
2. Open DB_Load Jupyter Notebook and add in your PostgreSQL `username` and `password` in the second cell.
3. Run all cells in DB_Load Jupyter notebook.
4. From the terminal, navigate to the "Flask-App" folder and run app.py by typing: `python app.py`.
5. Open a new terminal, navigate to the "Homeless-Dashboard" folder, and have python set up a local server by typing `python -m http.server`.
6. Open your browser then go to the url `http://localhost:8000/`.

![bottom_dash](https://github.com/code4sac/sacramento-county-homeless-hmis-data/blob/master/images/HMIS_dash_bottom.JPG)

## Contents

#### Data (folder):

- DB_Load:
  - Jupyter Notebook that executes raw SQL to create PostgreSQL database tables.
  - Formats then loads csv files into database.
  - Creates multiple views and new aggregate tables in database. This leverages the benefits of a relational database to extract valuable information from the raw data.
  - Uses Pandas to manipulate some tables and do some calculations on the data before writing back into database.
- CSV files containing all raw data that is used in this project.
  - Data source can be found [here](https://github.com/code4sac/sacramento-county-homeless-hmis-data/tree/master/data). An additional spreadsheet with exit destinations was created to facilitate analysis.

#### Flask-App (folder):

- app.py:
  - Python file using Flask to create a local API that returns the aggregate tables as a JSON object.

#### Homeless-Dashboard (folder):

- index.html -> html file containing structure of dashboard.
- static:
  - JS -> app.js -> a JavaScript file that hits Flask API and dynamically builds the dashboard utilizing the Highcharts library.
  - CSS -> style.css -> a Cascading Style Sheet that adds style and formatting to the dashboard.

## Assumptions Used for Producing Charts

#### Data included from January 1, 2015 through August 31, 2019

- There is a large data dump that happened in 2014 which impacts the data.
- While there are some dates in the dataset after August 2019, it appears to be incomplete.

#### Volume/Program Participation

- In and out are straightforward counts of activity within the time period.
- Active includes those enrolled in a program who do not have an exit date prior to the end of the time period, plus those with an exit date during the time period.
- Each enrollment counted – clients included more than once if actively enrolled in more than one program
- For yearly chart, included rudimentary projection for full year for sake of comparison. In and out for final 4 months are added in as means of previous months for 2019. Active is trickier to estimate and shows an assumed 5% growth from 2018.

#### Outcomes/Program enrollees with permanent housing upon program exit

- For those who exited a program in the period, shows the number who exited to permanent housing divided by the total number of exits. Permanent housing is defined as Category 1 as defined in “Variables included in County Data” spreadsheet’s “Exit Destination” worksheet.
- Clients are only counted once. If client happens to have an exit to permanent housing and an exit in the same period to something other than permanent housing, they are counted as an exit to permanent housing.

#### Outcomes/Average time to permanent housing

- Time calculated for those who started in transitional housing or day/emergency shelter and exited to permanent housing Category 1.

#### Demographics

- Grouped unknown categories together. For example, in Race chart, unknown includes categories ‘Client Refused', 'Data Not Collected', 'Client doesn't Know', and ‘NULL’.

## Project Leads

[Graham Penrose](https://www.linkedin.com/in/graham-penrose-ab6a7b188/) & [Scott Clark](https://www.linkedin.com/in/scott-d-clark/)
