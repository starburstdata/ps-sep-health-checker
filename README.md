# Health Status Checker

# THIS TOOL IS NOT OFFICIALLY SUPPORTED BY STARBURST DATA.  IT WAS CREATED BY OUR PROFESSIONAL SERVICES TEAM TO AID WITH SPECIFIC USE CASES.

# Prerequisites
   - Installed Python3 or above
        * *Note*: *Tested in 3.10.9*
   - Installed Jupyter Notebooks
        * Use `pip` and `pip3` to install on MacOS. Example: `pip3 install jupyter`
   - A catalog in Starburst Enterprise Platform (SEP) is connected to [Backend Service DB](https://docs.starburst.io/latest/admin/backend-service.html)
   - Installed Python modules specified in [requirements.txt](https://github.com/starburstdata/ps-health-status-checker/blob/main/requirements.txt).
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

# Execution
Before you can Notebook code you need to provide input parameters. Those allow you to connect the tool to [Backend Service DB](https://docs.starburst.io/latest/admin/backend-service.html) of the SEP cluster you want to analyze and specify timeframe for analysis. For detailed explanation of the parameters refer to [Input parameters](https://github.com/starburstdata/ps-health-status-checker/tree/main?tab=readme-ov-file#input-parameters) paragraph.

# Detailed Description

Description of the different sections used in the notebook

## Input parameters
To run this cell requires the following parameters to be provided:
- `input_file`: File `input_health_check_configs.json` that contain predefined KPIs and corresponding queries.
- `hostname`: Starburst Enteprise Platform (SEP) hostname
- `port`: SEP port
- `role`: If SEP is using [BIAC](https://docs.starburst.io/latest/security/biac-overview.html) as AuthZ tool - specify here a role name to assume when connected (The role must have select access on the given catalog/schema tables
- `username`: SEP username to use (masked)
- `password`: SEP password to use (masked)
- `catalog`: SEP catalog that exposes [Backend Service DB](https://docs.starburst.io/latest/admin/backend-service.html)
- `schema`: The schema name where Backend Service DB is deployed
     * Should contain key tables like `completed_queries` and `cluster_metrics`. Most often located in the `public` schema
 - `analysis_start_date` and `analysis_end_date`: timeframe for analysis in `YYYY-MM-DD` format
    
## Main code
This cell has the code that iterates over the KPIs in the input json and executes the queries in sStarburst. Some important aspects of this cell are:
- The code uses the [trino-python-client](https://github.com/trinodb/trino-python-client) and makes the connection via `dbapi`
- The code uses the following python modules: `trino, csv, json, argparse, getpass, logging, datetime, pandas, matplotlib, numpy, dash, plotly`.
    
## Cluster health
This section captures the following KPIs:
- Daily CPU Usage (avg/median)
- Hourly CPU Usage (avg/median)
- Daily Memory Usage (avg/median)
- Hourly Memory Usage (avg/median)
- Hourly Node Count (avg/median)
- Minutely CPU Usage (avg/median)
- Minutely Memory Usage (avg/median)
- Minutely Node Count (avg/median)

## Query health
This section captures the following KPIs:
- Query Trends By Query Type
- Query Failure Rate By Query Type
- Failed Queries Count By Query Type
- Failed Queries Count By Error Type
- Failed Queries Count by Error Name
- Concurrency - Queries Per Minute
- Data Processed Over Time
- Query Performance And Time Metrics
    
## Top X Queries Analysis (X is set to 10 currently)
This section allows to drill down on queries which could possibly be a bottleneck
- Top X Queries based on Execution Time is secs
- Top X Queries based on Planning Time is secs
- Top X Queries based on Scheduled Time is secs
- Top X Queries based on CPU Time is secs
- Top X Queries based on Analysis Time is secs
- Top X Queries based on Data Scanned in GBs
- Top X Queries based on Splits Processed
