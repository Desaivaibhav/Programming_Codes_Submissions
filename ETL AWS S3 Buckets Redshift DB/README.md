

Python script to build an ETL pipeline, which ingests data files in S3 source bucket to AWS
Redshift table, and run queries against them to extract/format desired data, then pack and ship them to
destination bucket.

Source data fields:
PID, Ad_id, id_type, UA, IP, epoch_timestamp, lat, long, accuracy, optout, country, proc_date

Final data format:
-Final data fields are ‘Ad_id’, ‘id_type’, ‘lat’ and ‘long’
- Only want 3 decimal spaces on ‘lat’ and ‘long’ field
- De-duplicate on field ‘Ad_id’, ‘id_type’, ‘lat’ and ‘long’, meaning if there’re rows that has the
same values in these 4 fields, take one record only.
- Convert epoch_timestamp into YYYY-MM-DD HH:MM:SS format.
- Format each row into JSON with filed names as keys.
- Final data file name should be ‘scanbuy-<yyyymmdd>.json.gz’
- Print the total row count and unique Ad_id at the end of the script.
- Create the table and include your initials in the table name (“yourtablename_yourinitials”)

S3 detail:
Access key: ============================
Secret key: ============================
Source bucket: tmp1.sl.com
Destination bucket: tmp2.sl.com
Bucket location: US-EAST-1

Redshift connection detail:
URL: jdbc:redshift://============.us-east-1.redshift.amazonaws.com:5439/tempdb
Database: tempdb
Schema: tempschema (full priv.)
User: tempuser
Pswd: ============




Steps I followed:

- Connect Redshift and create final table as per the data
- Get List of files at source bucket
- Create Staging table
- Copy the file to Redshift Stage Table
- Query the staged data to get year of file
- Load(unload) required data(format) from stage table and export to destination S3 bucket
- get the unloaded count
- Load the data from staging table to destination Table with conversion of epoch time to Timestamp
- Drop the staging table