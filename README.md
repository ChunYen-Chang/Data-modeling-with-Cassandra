# Data modeling with Cassandra (By using Sparkify data)
#### PROJECT BACKGROUND AND SUMMARY
- ###### BACKGROUND
    Sparkify is a startup company which provides the music streaming app. Recently, the analytics team in this company is interested in understanding their user activity on its music streaming app in order to provide better user experience for their user. To achieve the goal, the analytical team sets up a relational database (postgres) to store the users' data. However, instead of using relational database to store the data, the analytical team now decides to use a no-sql database (Cassandra) to store the data. This project aims for creating a Cassandra database which hosts all user activity data, song data, and users' personal data. 

- ###### PROJECT DETAILS
    In this project, it will create an ETL data pipeline to extract data from log dataset and song dataset, transform these data into a format which analytics team prefers, and put data into a Cassandra database. The detailed ETL process can be described below:

    **Step 1:** Use python to extract data from all csv files and save into an "overall csv file" for further use.

    **Step 2:** Design Cassandra tables based on analytics team's need and put data in these tables. As the design philosophy in Cassandra is different than tranditional SQL database (**Create table based on queries**), we must develop the table based on queries the analytics team prefers

- ###### DATA MODELING
    Since the Data Modeling philosophy in Apache Cassandra is creating table based on queries, this project will do the data modeling task based on queries we receive from the analytical team. In the follow paragraph, it shows the queries from analytical team and how we do data modeling based on these queries.

    **Query 1:** Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4
    ```
    query = "CREATE TABLE IF NOT EXISTS song_information_on_specific_session"

    query = query + "(sessionId int, itemInSession int, artist text, song text, length float, PRIMARY KEY (sessionId, itemInSession))"`
    ```

    **Query 2:** Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182
    ```
    query = "CREATE TABLE IF NOT EXISTS song_for_specific_session_and_user"

    query = query + "(sessionId int, userId int, itemInSession int, artist text, song text, firstName text, lastName text, PRIMARY KEY ((sessionId, userid), itemInSession))"
    ```

    **Query 3:** Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'<br/>
    ```
    query = "CREATE TABLE IF NOT EXISTS song_listerned_by_who"

    query = query + "(song text, userId int, firstName text, lastName text, PRIMARY KEY (song, userId))"
    ```
------------
#### FILES IN THE REPOSITORY
1. **etl.ipynb**: a jupyter notebook file which detail how access to Casandra database, extract data from the song and log file, transform song and log data into the format the analytics team wants, and dump data into Casandra database.

2. **event_data folder**: a folder which stores the raw event data of this project

3. **event_datafile_new.csv**: a csv file which stores the data which is received the data transformation process.
------------
#### HOW TO RUN THE PROJECT
To start the project, you need **etl.ipynb**. Use jupyter notebook to open **etl.ipynb** and run the command in this .ipynb file.

