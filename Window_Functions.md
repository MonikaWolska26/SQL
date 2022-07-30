# SQL

#### OVER()

example:

	SELECT 
   	column1,
   	column2,
   	SUM(column2) OVER (
      	ORDER BY column1
   	) AS 'alias_name'
	FROM
   	table
	WHERE
   	column3 = 'string';
		
- OVER: This is the clause that designates SUM as a window function.
- ORDER BY month: Here we declare what we would like our window function to do

#### PARTITION BY 
PARTITION BY is a subclause of the OVER clause and divides a query’s result set into parts. It’s very similar to GROUP BY except it does not reduce the number of rows returned.

While using GROUP BY only allows one row to be returned for each group, PARTITION BY allows you to see all of the resultant rows.

#### FIRST_VALUE() LAST_VALUE()

- FIRST_VALUE() returns the first value in an ordered set of values.
- LAST_VALUE() returns the last value in an ordered set of values.

example first value:

	SELECT
		username,
		posts,
		FIRST_VALUE (posts) OVER (
			PARTITION BY username 
			ORDER BY posts
		) fewest_posts
	FROM
		social_media;
		
example last value:

	SELECT
		username,
		posts,
		LAST_VALUE (posts) OVER (
			PARTITION BY username 
			ORDER BY posts
			RANGE BETWEEN UNBOUNDED PRECEDING AND 
			UNBOUNDED FOLLOWING
		) most_posts
	FROM
		social_media;

#### LAG / LEAD

Window functions can use LAG or LEAD in order to access information from a row at a specified offset which comes before (LAG) or after (LEAD) the current row.

This means that by using LAG or LEAD you can access any row before or after the current row, which can be very useful in calculating the difference between the current and adjacent row.

LAG takes up to three arguments:
- column (required)
- offset (optional, default 1 row offset)
- default (optional, what to replace default null values with)

LEAD looks to future rows, instead of LAG, which looks to previous rows.

#### ROW_NUMBER()

The most straight-forward way to order our results is by using the ROW_NUMBER function which adds a sequential integer number to each row.

example:

	SELECT 
		ROW_NUMBER() OVER (
			ORDER BY streams_millions
		) AS 'row_num', 
		artist, 
		week,
		streams_millions
	FROM
		streams;
		
#### RANK()

example:

	SELECT 
		RANK() OVER (
			ORDER BY streams_millions
		) AS 'rank', 
		artist, 
		week,
		streams_millions
	FROM
	

   streams;

#### NTILE

example:

	SELECT 
		NTILE(5) OVER (
			ORDER BY streams_millions DESC
		) AS 'weekly_streams_group', 
		artist, 
		week,
		streams_millions
	FROM
		streams;

The last window function we are going to learn is called NTILE and this can be used to find quartiles, quintiles or whatever ntile your data-driven heart desires.

NTILE allows you to break your data into roughly equal groups, based on what ntile you’d like: so if you were using quartile, it would divide the data into four groups (quarters).

When using NTILE you are required to provide a bucket, which represents the number of groups you’d like your data broken down into: NTILE(4) would be four “buckets” which would represent quartiles.

