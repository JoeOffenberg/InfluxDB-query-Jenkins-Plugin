# InfluxDB Query Jenkins Plugin

The plugin provides a mechanism for querying InfluxDB as a post build step for use as a deployment gateway.   Using a time series database to for aggregating testing and development tool data makes sense if you can query it after all the testing is complete to determine if a build is stable.  

## Installation
  Prequisites

  * Jenkins running on Java 1.7 or later
  


## Global Configuration

  Select Manage Jenkins -> Configure Plugin 
  scroll down to **InfluxDB Query Plugin**
  
  **InfluxDB URL:**  The complete url including port of the Influxdb e.g. http://localhost:8086 or http://host.domain.com:8086 
  
  **InfluxDB Database**  Database name where relevant events are stored e.g. _overops_
  
  **InfluxDB User**  InfluxDB username with access to the relevant events.
  
  **InfluxDB Password**  Password for InfluxDB user.
  
Test connection would show you a count of available metrics.  If the count shows 0 measurements, credentials are correct but    database may be wrong.  If credentials are incorrect you will receive an authentication error.
  

## Job Post Build Configuration
  **Influx Query**  InfluxDB select query to retun errors pertaining to the current build.  May use Jenkins tokens such as build number in the query.  e.g. 
      select * from DevOps where application = 'ArchRival2.1' deployment = '2-1-$BUILD_NUMBER'

  **Max Record Count**  Number of acceptable errors.  If query record count exceeds this limit and if Mark Build Unstable is selected, the build will be marked unstable.

  **Retry Count**  Number of times to execute the query as a single post-build step.

  **Retry Interval**  Time to wait in between each query in seconds.

  **Mark Build Unstable**  Check if we should mark the build unstable if the Max Record Count is exceeded.  

  **Show Query Results**  Check if we should should display the query results in the Jenkins console.
