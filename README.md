# Data-Modeling-with-Apache-Cassandra

## Required libraries

- cassandra
- numpy
- pandas

## Project

Created tables must be denormalized for Cassandra. Tables must be created from user activity logs.

Assumed select queries
1. Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4
2. Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182
3. Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'

## Files

- Data-MOdeling-with-Apache-Cassandra.ipynb: this notebook to develop the ETL process and create tables. Executing select query is also discribed.

## Data

### Event data

event_data that have CSV files is partitioned by date. Here are examples of filepaths to two files in the dataset:

```
event_data/2018-11-08-events.csv
event_data/2018-11-09-events.csv
```

## ETL Processes

- Implement the logic in section Part I of the notebook to iterate through each event file in event_data to process and create a new CSV file in Python
- Make necessary edits to Part II of the notebook to include Apache Cassandra CREATE and INSERT statements to load processed records into relevant tables in your data model
- Test by running SELECT statements after running the queries on your database

## Result tables

### music_app_history (for the first query)

To select spesific user by using song, Primary key (partition key) is set to song. Clustering column is user_id because data must become uniqe by user.

- TABLE
  - song text
  - user_id int
  - first_name text
  - last_name text
- PRIMARY KEY
  - song
- CLUSTERING COLUMN
  - user_id

### user_activity (for the second query)

To select spesific user activity by using user_id and session_id, Primary key (partition key) is set to (user_id, session_id). Clustering columns must be set to item_in_session because data is sorted by item_in_session.

- TABLE
  - user_id int
  - session_id int
  - item_in_session int
  - artist text
  - song text
  - first_name text
  - last_name text
- PRIMARY KEY
  - user_id
  - session_id
- CLUSTERING COLUMN
  - item_in_session

### user_listening_song (for the third query)

To select spesific user by using song, Primary key (partition key) is set to song. Clustering column is user_id because data must become uniqe by user.

- TABLE
  - song text
  - user_id int
  - first_name text
  - last_name text
- PRIMARY KEY
  - song
- CLUSTERING COLUMN
  - user_id
  
## Acknowledgements

 wish to thank Udacity for advice and review.
