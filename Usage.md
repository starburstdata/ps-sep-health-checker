# Health Checker Tool

After the notebook "HealthCheckerTool_v1_20Oct23.ipynb" is imported into jupyter, execute the cells in order.

Prerequisites:
   - Use Python3 or above
   - The insights DB should be added as a catalog in starburst
   - Various python modules used are specified below

Here's a description of the different sections in the notebook

- Input parameters - This cell accepts the following inputs to run the tool:
    - input_file: File "input_health_check_configs.json" that contain predefined KPIs and corresponding queries.
    - hostname: Starburst host url
    - port: port
    - role: role to assume (The role must have select access on the given catalog/schema tables
    - username: input connection user (masked)
    - password: input connection user pasword (masked)
    - catalog: The catalog that exposes the insights db
    - schema: The schema that holds the tables like completed_queries and cluster_metrics (most likely should be 'public')
    - analysis_start_date and analysis_end_date: timeframe for analysis in YYYY-MM-DD format
    
- Main Code - This cell has the code that iterates over the KPIs in the input json and executes the queries in starburst. Some important aspects of this cell are:
    - The code uses the trino python client and makes the connection using dbapi
    - Key python modules needed are trino,csv,json,argparse,getpass,logging,datetime,pandas,matplotlib,numpy,dash,       plotly 
    
- Cluster Health - Section that captures the following KPIs:
    - minutely cpu/memory usage over time (avg/median)
    - minutely query counts over time (avg/median)
    - minutely node availability over time
    
- Query Health - Section that captures the following KPIs:
    - Query trends over time / by query type
    - failure rates over time / by query type
    - failure counts over time / by query type
    - failure counts over time / by query type / by error type
    - failure counts over time / by query type / by error type / by error code-name
    
- Drill Down On Errors
    - Drill down into failed queries using various filters
    
- Concurrency
    - Queries per minute over time, represented by size of bubbles in the chart
    
- Data Processed Over Time
    - Avg input / output rows/bytes
    - Splits processed
    
- Query Performance Over Time
    - Various time metrics like CPU time, execution time, wait time, wall time, queued time, analysis time, planning, time, scheduled time input / output rows/bytes
    
- Top X Queries (X is set to 10 currently) - Drill down on queries which could possibly be bottlenecks
    - Top X Queries based on Execution Time is secs
    - Top X Queries based on Planning Time is secs
    - Top X Queries based on Scheduled Time is secs
    - Top X Queries based on CPU Time is secs
    - Top X Queries based on Analysis Time is secs
    - Top X Queries based on Data Scanned in GBs
    - Top X Queries based on #Splits Processed