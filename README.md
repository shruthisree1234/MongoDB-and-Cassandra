# MongoDB-and-Cassandra

You are a data engineer at a data analytics consulting company. Your company prides itself in being able to efficiently handle data in any format on any database on any platform. Analysts in your office need to work with data on different databases, and data in different formats. While these analysts are good at analyzing data, they count on you to be able to move data from external sources into various databases, to be able to move data from one type of database to another, and be able to run basic queries on various databases.

Objectives

Import data into a MongoDB database.
Query data in a MongoDB database.
Export data from MongoDB.
Import data into a Cassandra database.
Query data in a Cassandra database.

curl -O https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-DB0151EN-edX/labs/FinalProject/movies.json

Task 1: Import movies.json into mongodb server into a database named entertainment and a collection named movies.
Task 2: Write a mongodb query to find the year in which most number of movies were released
Task 3: Write a mongodb query to find the count of movies released after the year 1999
Task 4: Write a query to find out the average votes for movies released in 2007
Task 5: Export the fields _id, title, year, rating and director from the movies collection into a file named partial_data.csv
Task 6 - Create a keyspace named entertainment
Task 7 - Import partial_data.csv into cassandra server into a keyspace named entertainment and a table named movies
Task 8 - Write a cql query to count the number of rows in the movies table
Task 9 - Create an index for the rating column in the movies table using cql
Task 10 - Write a cql query to count the number of movies that are rated 'G'.

QUERIES
Task 2: Write a mongodb query to find the year in which most number of movies were released (in MongoDB)
db.movies.aggregate([
{
	"$group": {
		"_id": "$year",
		"moviecount": {"$sum":1}
	},
},
{
	"$sort": {"moviecount": -1}
},
{
	"$limit": 1
}
])

Task 4: Write a query to find out the average votes for movies released in 2007 (in MongoDB)
db.movies.aggregate([
{
	"$match": { "year": 2007}
},
{
	"$group": {
		"_id": "$year",
		"averagevote": {"$avg": "$Votes"}
	}
}
])

Task 7 - Import partial_data.csv into cassandra server into a keyspace named entertainment and a table named movies
CREATE TABLE movies(
id text PRIMARY KEY,
title text,
year text,
rating text,
director text
);

COPY entertainment.movies(id,title,year,rating,director) FROM 'partial_data.csv' WITH DELIMITER=',' AND HEADER=TRUE;


Task 9 - Create an index for the rating column in the movies table using cql
CREATE INDEX IF NOT EXISTS rating_index ON entertainment.movies (rating);
