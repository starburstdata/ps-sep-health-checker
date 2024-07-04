# Health Status Checker

# THIS TOOL IS NOT OFFICIALLY SUPPORTED BY STARBURST DATA.  IT WAS CREATED BY OUR PROFESSIONAL SERVICES TEAM TO AID WITH SPECIFIC USE CASES.

# Prerequisites
   - Installed Python3 or above
        * *Note*: *Tested in 3.10.9*
   - Installed Jupyter Notebooks
        * Use `pip` and `pip3` to install on MacOS. Example: `pip3 install jupyter`
   - A catalog in Starburst Enterprise Platform (SEP) is connected to [Backend Service DB](https://docs.starburst.io/latest/admin/backend-service.html)
   - Installed Python modules specified in requirements.txt.
        * Use `pip` and `pip3` to install on MacOS. Example: `pip install -U -r ./requirements.txt`

# Installation
   - Clone the repo:
   `git clone https://github.com/starburstdata/ps-health-status-checker`

   - Go inside the project folder:
   `cd ./ps-health-status-checker`

   - Install Python modules application uses:
   `pip install -U -r ./requirements.txt`

   - Install Jupyter Notebooks module:
   `pip3 install jupyter`

   - Start a Jupyter session on your browser at with command:
   `jupyter notebook`

   - This should launch a jupyter session on `http://localhost:8888/`

   - Open (Import) the notebook `health_status_checker.ipynb` into jupyter, and execute the cells in order.

# Detailed Description

Here's a description of the different sections used in the notebook

- Input parameters - This cell accepts the following inputs to run the tool:
    - input_file: File `input_health_check_configs.json` that contain predefined KPIs and corresponding queries.
    - hostname: Starburst host url
    - port: port
    - role: role to assume when using biac (The role must have select access on the given catalog/schema tables
    - username: input connection user (masked)
    - password: input connection user pasword (masked)
    - catalog: The catalog that exposes the insights db
    - schema: The schema that holds the tables like `completed_queries` and `cluster_metrics` (most often located in the `public` schema)
    - analysis_start_date and analysis_end_date: timeframe for analysis in YYYY-MM-DD format
    
- Main Code - This cell has the code that iterates over the KPIs in the input json and executes the queries in starburst. Some important aspects of this cell are:
    - The code uses the trino python client and makes the connection using dbapi
    - Key python modules needed are: `trino, csv, json, argparse, getpass, logging, datetime, pandas, matplotlib, numpy, dash, plotly`
        * Optional: you can use the requirements.txt to install the required modules using pip
            * `pip install -U -r ./requirements.txt`
    
- Cluster Health - Section that captures the following KPIs:
    - Daily CPU Usage (avg/median)
    - Hourly CPU Usage (avg/median)
    - Daily Memory Usage (avg/median)
    - Hourly Memory Usage (avg/median)
    - Hourly Node Count (avg/median)
    - Minutely CPU Usage (avg/median)
    - Minutely Memory Usage (avg/median)
    - Minutely Node Count (avg/median)

- Query Health - Section that captures the following KPIs:
    - Query Trends By Query Type
    - Query Failure Rate By Query Type
    - Failed Queries Count By Query Type
    - Failed Queries Count By Error Type
    - Failed Queries Count by Error Name
    - Concurrency - Queries Per Minute
    - Data Processed Over Time
    - Query Performance And Time Metrics
    
- Top X Queries Analysis(X is set to 10 currently) - Drill down on queries which could possibly be bottlenecks
    - Top X Queries based on Execution Time is secs
    - Top X Queries based on Planning Time is secs
    - Top X Queries based on Scheduled Time is secs
    - Top X Queries based on CPU Time is secs
    - Top X Queries based on Analysis Time is secs
    - Top X Queries based on Data Scanned in GBs
    - Top X Queries based on Splits Processed
