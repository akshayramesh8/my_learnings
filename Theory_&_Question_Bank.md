## Question Bank

### Question:
Assume you're given a table Twitter tweet data, write a query to obtain a histogram of tweets posted per user in 2022. Output the tweet count per user as the bucket and the number of Twitter users who fall into that bucket.

In other words, group the users by the number of tweets they posted in 2022 and count the number of uthesers in each group.

**tweets Table:**
![tweets](./DL_T1.png)


**Example Output:**
![](./DL_T2.png)

## Solution Code:
```sql
SELECT
  tweet_count AS tweet_bucket,
  count(user_id) AS users_num
FROM
(
    SELECT 
      user_id, 
      count(tweet_id) AS tweet_count
    FROM 
      tweets
    WHERE 
      tweet_date >= '01/01/2022 00:00:00' AND 
      tweet_date <= '12/31/2022 23:59:59'
    GROUP BY
      user_id
) AS tweet_counts
GROUP BY
  tweet_bucket

# Question Bank
## HackerRank:

1. Question:
![[Pasted image 20241010185539.png]]
Solution:
```sql
select top 1 city , len(city) from station where len(city) = (select max(len(city)) from station) order by city asc

select top 1 city , len(city) from station where len(city) = (select min(len(city)) from station) order by city asc
```

2. Question:
![[Pasted image 20241010190156.png]]
Solution:
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE
CITY = (
SELECT CITY
WHERE CITY LIKE 'A%' OR CITY LIKE 'E%' OR CITY LIKE 'I%' OR CITY LIKE 'O%' OR CITY LIKE 'U%')
ORDER BY CITY;
```

3. Question:
![[Pasted image 20241010191150.png]]
```sql
select distinct city from station where city like '[a,e,i,o,u]%' and city like '%[a,e,i,o,u]';

OR

SELECT DISTINCT (CITY) FROM STATION WHERE LEFT(CITY, 1) IN ('A', 'E', 'I', 'O', 'U') AND RIGHT(CITY, 1) IN ('A', 'E', 'I', 'O', 'U');
```

4. Question:
![[Pasted image 20241010192319.png]]
```sql
SELECT DISTINCT CITY FROM STATION WHERE CITY NOT LIKE '[A,E,I,O,U]%' ORDER BY CITY;
```

5. Question
![[Pasted image 20241011105554.png]]
```sql
SELECT DISTINCT CITY FROM STATION WHERE CITY NOT LIKE '[A,E,I,O,U]%' OR CITY NOT LIKE '%[a,e,i,o,u]' ORDER BY CITY;
```

6. Question:
![[Pasted image 20241011111102.png]]
Sample:
![[Pasted image 20241011111132.png]]
Solution:
```sql
SELECT NAME FROM STUDENTS WHERE MARKS>75 ORDER BY RIGHT(NAME,3),ID ASC
```

7. Question:
![[Pasted image 20241011112103.png]]
Sample:
![[Pasted image 20241011112128.png]]
Solution:
```sql
SELECT NAME FROM EMPLOYEE WHERE SALARY > 2000 AND MONTHS < 10 ORDER BY EMPLOYEE_ID ASC;
```

## END OF BASIC CHALLENGES
__________________________________

8. Question:
![[Pasted image 20241011112625.png]]
Solution:
```sql
SELECT COUNT(NAME) FROM CITY WHERE POPULATION > 100000; 
```

9. Question:
![[Pasted image 20241011112944.png]]
Solution:
```sql
SELECT SUM(POPULATION) FROM CITY WHERE DISTRICT = 'California';
```

10. Question:
![[Pasted image 20241011113518.png]]
Solution:
```sql
SELECT ROUND(AVG(POPULATION), 0) FROM CITY;
```

11. Question:
![[Pasted image 20241011113832.png]]
Solution:
```sql
SELECT SUM(POPULATION)
FROM CITY
WHERE COUNTRYCODE = 'JPN';
```

12. Question:
![[Pasted image 20241011114110.png]]
Solution:
```sql
SELECT MAX(POPULATION) - MIN(POPULATION)
FROM CITY;
```


13. Question:
![[Pasted image 20241011131341.png]]
Sample:
![[Pasted image 20241011131406.png]]
Explanation:
![[Pasted image 20241011131436.png]]
Solution:
```sql
SELECT CAST(ABS(ROUND(AVG(SALARY) - AVG(CONVERT(DECIMAL(10,2),REPLACE(SALARY,'0',''))),0)) + 1 AS INT)
FROM EMPLOYEES;
```

14. Question:

![[Pasted image 20241014123358.png]]
![[Pasted image 20241014123418.png]]
Explanation:
![[Pasted image 20241014123511.png]]


ask:
earnings = salary x total months
find all max total earnings 
total number of employees who have max earnings
print as 2 space-separated integers

Solution:
```sql
SELECT MAX(SALARY*MONTHS), COUNT(*) FROM EMPLOYEE WHERE (SALARY*MONTHS) >= (SELECT MAX(SALARY*MONTHS) FROM EMPLOYEE);
```

15. Question:
![[Pasted image 20241014150633.png]]
Solution:
```sql
select cast(sum(lat_n) AS decimal(10,2)), cast(sum(long_w) AS decimal (10,2))
from station;
```

16. Question:
![[Pasted image 20241014150801.png]]
Solution:

ask: 
- sum(LAT_N)
- HAVING 38.7880 < LAT_N < 137.2345
- ROUND TO 4 DECIMAL PLACES
  
Solution:
```sql
SELECT CAST(SUM(LAT_N) AS DECIMAL(10,4))
FROM STATION
WHERE LAT_N BETWEEN 38.7880 AND 137.2345;
```

17. Question:
![[Pasted image 20241014151804.png]]
**Note: HAVING can be used only with an aggregate function or in a group by clause.**

Solution:
```sql
SELECT CAST(LONG_W AS DECIMAL(10,4))
FROM STATION
WHERE LAT_N = (SELECT MAX(LAT_N) FROM STATION WHERE LAT_N < 137.2345);
```

18. Question:
![[Pasted image 20241014152744.png]]
#### MANHATTAN DISTANCE
**Definition:** The distance between two points measured along axes at right angles. In a plane with p1 at (x1, y1) and p2 at (x2, y2), it is |x1 - x2| + |y1 - y2|.

_Note: This is easily generalized to higher dimensions. Manhattan distance is often used in integrated circuits where wires only run parallel to the X or Y axis. See links at [_Lm distance_](https://xlinux.nist.gov/dads/HTML/lmdistance.html) for more detail._

_

Also known as [_rectilinear_](https://xlinux.nist.gov/dads/HTML/rectilinear.html) distance, Minkowski's L1 distance, taxi cab metric, or city block distance.

_

_[_Hamming distance_](https://xlinux.nist.gov/dads/HTML/HammingDistance.html) can be seen as Manhattan distance between bit vectors.

This could fall in the domain of [[Geometry]]

*What is a bit vector?*

*A bit vector is **a vector in which each element is a bit** (so its value is either 0 or 1). In most vectors, each element has a different address in memory and can be manipulated separately from the other elements, but we also hope to be able to perform “vector operations” that treat all elements uniformly.*
![[Pasted image 20241014153721.png]]

Solution:
```sql
SELECT CAST((MAX(LAT_N) - MIN(LAT_N)) + (MAX(lONG_W) - MIN(LONG_W)) AS DECIMAL(10,4))
FROM STATION
```

19. Question:
![[Pasted image 20241014154013.png]]
Note:
**Euclidean Distance (or) Pythagorean Distance**
![[Pasted image 20241014153927.png]]

Solution:
```sql
SELECT CAST(SQRT(POWER(MAX(LAT_N)-MIN(LAT_N),2) + POWER(MAX(LONG_W)-MIN(LONG_W),2)) AS DECIMAL(10,4)) FROM STATION;
```

20. Question:
![[Pasted image 20241014171638.png]]
Solution:
```sql
SELECT DISTINCT CAST(PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY LAT_N) OVER () AS DECIMAL(10,4)) AS median
FROM STATION;
```
#### ^ SQL Function for Finding Median #Median
<sup><sub>Reference:</sup></sub>
![[Pasted image 20241014171832.png]]
PERCENTILE_CONT **interpolates the appropriate value, which might or might not exist in the data set**, while PERCENTILE_DISC always returns an actual value from the set. [[Functions]]

```SQL
-- to partition median by city:
SELECT DISTINCT CITY, CAST(PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY LAT_N) OVER (PARTITION BY CITY) AS DECIMAL(10,4)) AS median
FROM STATION;
```
![[Pasted image 20241014173453.png]]

21. Question
![[Pasted image 20241014174508.png]]
![[Pasted image 20241014174532.png]]
![[Pasted image 20241014174608.png]]
![[Pasted image 20241014174646.png]]
![[Pasted image 20241014174719.png]]
![[Pasted image 20241014174829.png]]

Solution:
```sql

SELECT TEMP.HACKER_ID, TEMP.NAME, SUM(TEMP.SCORE) AS TOTAL_SCORE
FROM
(
	SELECT HACKERS.HACKER_ID, HACKERS.NAME, SUBMISSIONS.CHALLENGE_ID, MAX(SCORE) AS SCORE
	FROM HACKERS INNER JOIN SUBMISSIONS ON HACKERS.HACKER_ID = SUBMISSIONS.HACKER_ID
	GROUP BY HACKERS.HACKER_ID, HACKERS.NAME, SUBMISSIONS.CHALLENGE_ID) AS TEMP

WHERE TEMP.HACKER_ID NOT IN (
	SELECT HACKERS.HACKER_ID
	FROM HACKERS INNER JOIN SUBMISSIONS ON HACKERS.HACKER_ID = SUBMISSIONS.HACKER_ID
	GROUP BY HACKERS.HACKER_ID
	HAVING SUM(SUBMISSIONS.SCORE) = 0 )
	
GROUP BY TEMP.HACKER_ID, TEMP.NAME
ORDER BY TOTAL_SCORE DESC, TEMP.HACKER_ID ASC; 

```

22. Question:
![[Pasted image 20241016173349.png]]
![[Pasted image 20241016173403.png]]
![[Pasted image 20241016173418.png]]
![[Pasted image 20241016173436.png]]
![[Pasted image 20241016173519.png]]
![[Pasted image 20241016173535.png]]
![[Pasted image 20241016173555.png]]
![[Pasted image 20241016173608.png]]

Solution:
```sql
SELECT W.ID, WP.AGE, W.COINS_NEEDED, W.POWER
FROM WANDS AS W
JOIN WANDS_PROPERTY AS WP ON W.CODE = WP.CODE
JOIN
    (
    SELECT AGE AS A, MIN(COINS_NEEDED) AS MCN, POWER AS P
    FROM WANDS AS W
    JOIN WANDS_PROPERTY AS WP ON W.CODE = WP.CODE
    WHERE IS_EVIL = 0
    GROUP BY POWER, AGE
    ) AS TEMP
ON WP.AGE = A AND W.COINS_NEEDED = MCN AND W.POWER = P
ORDER BY W.POWER DESC, WP.AGE DESC;
```

### Explanation of Code and Logic:
This SQL query involves joining two tables (`WANDS` and `WANDS_PROPERTY`) and selecting specific rows based on conditions that minimize the `coins_needed` value for each combination of `power` and `age`. It also filters out "evil" wands and orders the result by `power` and `age` in descending order.

### Tables Involved:
- **`WANDS` (alias `W`)**: This table likely contains information about different wands, including attributes like `id`, `coins_needed` (the cost of the wand), and `power` (the power level of the wand).
- **`WANDS_PROPERTY` (alias `WP`)**: This table contains properties of the wands, such as the `age` (the age of the wand or the user) and possibly whether a wand is "evil" (`IS_EVIL` flag).
- **`TEMP`**: A derived table (subquery) used to find the minimum cost (`coins_needed`) for each unique combination of `power` and `age`.

### SQL Query Breakdown:

#### 1. **Main Query**:
```sql
SELECT W.id, WP.age, W.coins_needed, W.power
FROM WANDS AS W
JOIN WANDS_PROPERTY AS WP ON W.CODE = WP.CODE
```
- **`SELECT W.id, WP.age, W.coins_needed, W.power`**:
  - The main query selects four fields: `id` (from the `WANDS` table), `age` (from the `WANDS_PROPERTY` table), `coins_needed` (from the `WANDS` table), and `power` (from the `WANDS` table).

- **`JOIN WANDS_PROPERTY AS WP ON W.CODE = WP.CODE`**:
  - This performs an inner join between the `WANDS` and `WANDS_PROPERTY` tables on the `CODE` column, meaning the data from both tables is combined for wands that have the same `CODE`.

#### 2. **Subquery (`TEMP`)**:
```sql
(SELECT age AS A, MIN(coins_needed) AS MCN, power AS P
 FROM WANDS AS W1
 JOIN WANDS_PROPERTY AS WP1 ON W1.CODE = WP1.CODE
 WHERE IS_EVIL = 0
 GROUP BY power, age) AS TEMP
```
- **`JOIN`**: Similar to the main query, this subquery joins the `WANDS` table (`W1`) with the `WANDS_PROPERTY` table (`WP1`) using the `CODE` column.

- **`WHERE IS_EVIL = 0`**:
  - This condition filters out any "evil" wands, i.e., only rows where the `IS_EVIL` column is `0` (non-evil) are included.

- **`GROUP BY power, age`**:
  - The subquery groups the results by `power` and `age`, which means that for each unique combination of `power` and `age`, the query will return a row.

- **`MIN(coins_needed) AS MCN`**:
  - For each combination of `power` and `age`, the query calculates the **minimum** value of `coins_needed` and aliases it as `MCN` (Minimum Coins Needed).

- **Result of Subquery (`TEMP`)**:
  - The subquery returns a table (`TEMP`) with the columns `A` (age), `MCN` (minimum coins needed), and `P` (power), for each combination of `power` and `age`.

#### 3. **Join with `TEMP`**:
```sql
ON WP.age = A AND W.coins_needed = MCN AND W.power = P
```
- The main query joins the subquery result (`TEMP`) on three conditions:
  - The `age` from the `WANDS_PROPERTY` table (`WP.age`) must match the `age` (`A`) from the subquery.
  - The `coins_needed` from the `WANDS` table (`W.coins_needed`) must match the minimum `coins_needed` (`MCN`) from the subquery.
  - The `power` from the `WANDS` table (`W.power`) must match the `power` (`P`) from the subquery.
  
This ensures that only the rows where the wand's `coins_needed` is the **minimum for that specific combination** of `power` and `age` are selected.

#### 4. **Order By Clause**:
```sql
ORDER BY W.power DESC, WP.age DESC;
```
- The final result is ordered by:
  - **`W.power DESC`**: Wands with higher power appear first (descending order).
  - **`WP.age DESC`**: If multiple wands have the same power, the ones with a higher age appear first (descending order).

### Logic Behind the Query:

1. **Joining the Tables**: The query first joins the `WANDS` and `WANDS_PROPERTY` tables to get combined information about each wand and its properties.
   
2. **Subquery**:
   - The subquery (`TEMP`) is designed to find the **minimum cost** (`coins_needed`) for each unique combination of `power` and `age`, but only for non-evil wands (`IS_EVIL = 0`).
   
3. **Filtering the Main Query**: The main query then filters the rows using the subquery by ensuring that the `coins_needed` for a given wand is the minimum for its combination of `power` and `age`.

4. **Final Output**: The output consists of only those wands that have the **minimum cost** for each combination of `power` and `age`, and the results are sorted by power (high to low) and age (high to low).

### Example:

Assume the following data:

#### WANDS Table:
| id  | code | coins_needed | power |
|-----|------|--------------|-------|
| 1   | A    | 50           | 100   |
| 2   | A    | 40           | 100   |
| 3   | B    | 30           | 80    |
| 4   | B    | 25           | 80    |

#### WANDS_PROPERTY Table:
| code | age | is_evil |
|------|-----|---------|
| A    | 10  | 0       |
| B    | 20  | 0       |

The subquery will return the following (filtered and grouped by `power` and `age` with minimum `coins_needed`):
| A   | MCN | P   |
|-----|-----|-----|
| 10  | 40  | 100 |
| 20  | 25  | 80  |

Now, the main query will join this subquery with the original tables and return the rows where `coins_needed` matches `MCN` for that `age` and `power`. The final output might look like this:
| id  | age | coins_needed | power |
|-----|-----|--------------|-------|
| 2   | 10  | 40           | 100   |
| 4   | 20  | 25           | 80    |

The result will be ordered by power (descending) and then by age (descending).

### Conclusion:
This query retrieves wands that have the **minimum coins needed** for each specific combination of `power` and `age`, excluding evil wands. The results are sorted by the highest power and age, giving you the most powerful and cost-efficient non-evil wands.

```sql

SELECT W.ID, WP.AGE, W.COINS_NEEDED, W.POWER
FROM WANDS AS W
JOIN WANDS_PROPERTY AS WP ON W.CODE = WP.CODE
JOIN
    (
    SELECT AGE AS A, MIN(COINS_NEEDED) AS MCN, POWER AS P
    FROM WANDS AS W
    JOIN WANDS_PROPERTY AS WP ON W.CODE = WP.CODE
    WHERE IS_EVIL = 0
    GROUP BY POWER, AGE
    ) AS TEMP
ON WP.AGE = A AND W.COINS_NEEDED = MCN AND W.POWER = P
ORDER BY W.POWER DESC, WP.AGE DESC;

```

23. Question:
![[Pasted image 20241016191227.png]]
![[Pasted image 20241016191243.png]]
![[Pasted image 20241016191301.png]]
![[Pasted image 20241016191333.png]]
![[Pasted image 20241016191353.png]]
![[Pasted image 20241016191412.png]]
![[Pasted image 20241016191432.png]]
![[Pasted image 20241016191453.png]]
![[Pasted image 20241016191510.png]]

Solution:
First Attempt Code (Wrong):
```SQL
SELECT HACKERS.HACKER_ID, HACKERS.NAME, COUNT(CHALLENGES.CHALLENGE_ID) AS CHALLENGES_CREATED
FROM HACKERS 
JOIN CHALLENGES ON HACKERS.HACKER_ID = CHALLENGES.HACKER_ID
JOIN 
	(
	SELECT H.HACKER_ID AS ID, H.NAME COUNT(C.CHALLENGE_ID) AS TOTAL_CHALLENGES
	FROM HACKERS AS H
	JOIN CHALLENGES AS S ON H.HACKER_ID = C.HACKER_ID
	WHERE 
	GROUP BY H.HACKER_ID
	HAVING C.CHALLENGE_ID = 
		(
		CASE 
			WHEN COUNT(C.CHALLENGE_ID) > MAX(COUNT(C.CHALLENGE_ID)) THEN 1 
			ELSE 0
			END
		) AS MAX_CHALLENGES
	)
ON HACKERS.HACKER_ID = ID AND CHALLENGES_CREATED > TOTAL_CHALLENGES
GROUP BY HACKERS.HACKER_ID
ORDER BY CHALLENGES.CHALLENGE_ID DESC, HACKERS.HACKER_ID ASC;
```
<u>NOTE:</u> - An aggregate may not appear in the WHERE clause unless it is in a subquery contained in a HAVING clause or a select list, and the column being aggregated is an outer reference.
###### Correct Code:
```SQL
SELECT H.HACKER_ID, H.NAME, COUNT(CHALLENGE_ID) AS CHALLENGES_CREATED
FROM HACKERS AS H
JOIN CHALLENGES AS C ON H.HACKER_ID = C.HACKER_ID
GROUP BY H.HACKER_ID, H,NAME
HAVING COUNT(CHALLENGE_ID) NOT IN 
	(
	SELECT X.CHALLENGECOUNT
	FROM 
		(
		SELECT H.HACKER_ID, H.NAME, COUNT(CHALLENGE_ID) AS CHALLENGECOUNT
		FROM HACKERS AS H
		JOIN CHALLENGES AS C ON H.HACKER_ID = C.HACKER_ID
		WHERE COUNT(CHALLENGE_ID) <>
			(
			SELECT COUNT(CHALLENGE_ID)
			FROM CHALLENGES 
			GROUP BY HACKER_ID
			ORDER BY 1 DESC
			)
	GROUP BY X.CHALLENGECOUNT
	HAVING COUNT(X.CHALLENGECOUNT) > 1
	)
ORDER BY 3 DESC, 1 ASC;
```

24. Question:
![[Pasted image 20241017153816.png]]
![[Pasted image 20241017153835.png]]
![[Pasted image 20241017153852.png]]
![[Pasted image 20241017153918.png]]
![[Pasted image 20241017153936.png]]
![[Pasted image 20241017154002.png]]
![[Pasted image 20241017154029.png]]
![[Pasted image 20241017154057.png]]
![[Pasted image 20241017154114.png]]

Solution:

Let's look at the ask:
- **Main Query**: Write a query to print the respective _hacker_id_ and _name_ of hackers who achieved full scores for _more than one_ challenge. 
- Order your output in descending order by the total number of challenges in which the hacker earned a full score. 
- If more than one hacker received full scores in same number of challenges, then sort them by ascending _hacker_id_.

First Attempt Code (Wrong):
```sql
SELECT H.HACKER_ID, H.NAME, S.SCORE, COUNT(CHALLENGE_ID) 
FROM HACKERS AS H
JOIN SUBMISSIONS AS S ON H.HACKER_ID = S.HACKER_ID
HAVING COUNT(CHALLENGE_ID) IN 
    (SELECT X.SCORE
     FROM 
        (
        SELECT H.HACKER_ID, H.NAME, COUNT(CHALLENGE_ID) AS CHALLENGECOUNT, S.SCORE AS SCORE
     FROM HACKERS AS H
     JOIN SUBMISSIONS AS S ON H.HACKER_ID = S.HACKER_ID
     GROUP BY H.HACKER_ID, H.NAME
     HAVING S.SCORE >= 100
         ) X
     GROUP BY 1
     ORDER BY X.CHALLENGECOUNT DESC
        )
ORDER BY 4 DESC, 1 ASC;
```
NOTE: The ORDER BY clause is invalid in views, inline functions, derived tables, subqueries, and common table expressions, unless TOP, OFFSET or FOR XML is also specified.

##### Correct Code:
```SQL
SELECT H.HACKER_ID, H.NAME
FROM HACKERS AS H
JOIN SUBMISSIONS AS S ON H.HACKER_ID = S.HACKER_ID
JOIN CHALLENGES AS C ON S.CHALLENGE_ID = C.CHALLENGE_ID
JOIN DIFFICULTY AS D ON C.DIFFICULTY_LEVEL = D.DIFFICULTY_LEVEL
WHERE S.SCORE = D.SCORE
GROUP BY H.HACKER_ID, H.NAME
HAVING COUNT(CHALLENGE_ID > 1)
ORDER BY COUNT(CHALLENGE_ID) DESC, H.HACKER_ID ASC;
```

25. Question:
![[Pasted image 20241017171157.png]]
![[Pasted image 20241017171216.png]]
![[Pasted image 20241017171243.png]]
![[Pasted image 20241017171308.png]]
![[Pasted image 20241017171329.png]]
![[Pasted image 20241017171347.png]]
![[Pasted image 20241017171401.png]]

Solution:

ASK:
- Write a query to output the names of those students whose best friends got offered a higher salary than them. 
- Names must be ordered by the salary amount offered to the best friends. It is guaranteed that no two students got same salary offer.

```sql
SELECT NAME
FROM STUDENTS AS S
JOIN FRIENDS AS F ON S.ID = F.ID
JOIN PACKAGES AS P1 ON F.ID = P.ID
JOIN PACKAGES AS P2 ON S.ID = P.ID
WHERE P2.SALARY > P1.SALARY
ORDER BY P1.SALARY;
```







## DataLemur: 
#### SQL Interview Questions

1. Amazon | Easy
![[Pasted image 20241021160048.png]]

Solution:

ask:
- average stars for each product every month
- month in numerical value
- product_id and average star rating rounded to two decimal places
- sort O/P on month, product_id

code:
```sql
SELECT 
	CONVERT(REVIEW_ID AS DECIMAL(10,2) 
	CAST(ROUND(USER_ID) AS DECIMAL(10,2))
	EXTRACT MONTH FROM SUBMIT_DATE AS MONTH
	AVERAGE(STARS) AS AVG_RATING
FROM REVIEWS
GROUP BY PRODUCT_ID
ORDER BY MONTH, PRODUCT_ID

```


2. LinkedIN | Easy
![[Pasted image 20241021161732.png]]
![[Pasted image 20241021161753.png]]
![[Pasted image 20241021161811.png]]

Solution:

ask:
- candidates proficient in Python, Tableau and PostgreSQL
- query list of candidates who possess these 3 skills
- sort O/P by candidate_id ASC

code:
```sql
SELECT 
  EXTRACT(MONTH FROM submit_date) AS mth,
  product_id,
  ROUND(AVG(stars), 2) AS avg_stars
FROM reviews
GROUP BY 
  EXTRACT(MONTH FROM submit_date), 
  product_id
ORDER BY mth, product_id;
```

#### SUPER IMPORTANT: SQL - <u>ORDER OF EXECUTION</u>
![[Pasted image 20241021162753.png]]
![[Pasted image 20241021163338.png]]
![[Pasted image 20241027115905.png]]

When to use `WHERE` and `HAVING`
![[Pasted image 20241028110504.png]]

3. Facebook | Easy
![[Pasted image 20241021163555.png]]
![[Pasted image 20241021163854.png]]
![[Pasted image 20241021163909.png]]

ask:
- return user_id that have zero likes
- O/P sorted in page_id ASC

code I wrote:
```SQL
WITH (SELECT PAGE_ID, LIKED_DATE
FROM PAGES AS P
LEFT JOIN PAGE_LIKES AS PL ON P.PAGE_ID = PL.PAGE_ID
WHERE LIKED_DATE IS NULL) AS LIKED_PAGES

SELECT PAGE_ID
FROM LIKED_PAGES
ORDER BY PAGE_ID ASC;
```

efficient code:
```sql
SELECT page_id FROM pages EXCEPT SELECT page_id FROM page_likes;
```

other solutions:
```sql
SELECT page_id FROM pages WHERE page_id NOT IN ( SELECT page_id FROM page_likes WHERE page_id IS NOT NULL );

SELECT page_id FROM pages WHERE NOT EXISTS ( SELECT page_id FROM page_likes AS likes WHERE likes.page_id = pages.page_id ;)
```

4. Tesla | Unfinished Parts | Easy
![[Pasted image 20241021170204.png]]
![[Pasted image 20241021170224.png]]
![[Pasted image 20241021170243.png]]

ask:
- parts that have begun the assembly process but not finished yet
- no finished_date = unfinishe part

code:
```SQL
SELECT PART, ASSEMBLY_STEP
FROM PARTS_ASSEMBLY
WHERE FINISH_DATE IS NULL;
```

5. New York Times | Laptop vs. Mobile Viewership | Easy
![[Pasted image 20241021170920.png]]
![[Pasted image 20241021170935.png]]
![[Pasted image 20241021170950.png]]

ask:
- total viewership for mobile and laptops
- 1 as mobile_views
- 2 = laptop_views

code:
```sql
SELECT DISTINCT
	SUM(CASE WHEN DEVICE_TYPE = 'laptop' THEN 1 ELSE 0 END) AS LAPTOP_VIEWS,
	SUM(CASE WHEN DEVICE_TYPE IN ('phone', 'tablet') THEN 1 ELSE 0 END) AS MOBILE_VIEWS
FROM VIEWERSHIP;


SELECT COUNT(*) FILTER (WHERE device_type = 'laptop') AS laptop_views, COUNT(*) FILTER (WHERE device_type IN ('tablet', 'phone')) AS mobile_views FROM viewership;
```

6. Facebook | Average Post Hiatus (Part 1) | Easy
![[Pasted image 20241021180501.png]]
![[Pasted image 20241021180533.png]]

ask:
- query to find the number of days between each user’s first post of the year and last post of the year in the year 2021 
- Output the user and number of the days between each user's first and last post

code:
```SQL
SELECT
	USER_ID,
	MAX(POST_DATE::DATE) - MIN(POST_DATE::DATE) AS DIFFERENCE
FROM 
	POSTS
WHERE
	DATE_PART('YEAR', POST_DATE::DATE) = 2021
GROUP BY 
	USER_ID
HAVING 
	COUNT(POST_ID) > 1;
```
![[Pasted image 20241021184246.png]]


7. Microsoft | Teams Power Users | Easy
![[Pasted image 20241022103916.png]]
![[Pasted image 20241022103939.png]]
![[Pasted image 20241022104010.png]]

ask:
- Identify top 2 Power Users who sent the highest number of messages on Microsoft Teams in August 2022 
- Display the IDs of these 2 users along with the total number of messages they sent 
- Output the results in descending order based on the count of the messages

code:
```SQL
SELECT sender_id, COUNT(message_id) AS MESSAGE_COUNT
FROM messages
WHERE EXTRACT(MONTH FROM sent_date::DATE) = 08 AND EXTRACT(YEAR FROM sent_date::DATE) = 2022 
GROUP BY sender_id
ORDER BY 2 DESC
LIMIT 2;
```

8. LinkedIN | Duplicate Job Listings | Easy 
![[Pasted image 20241022123109.png]]
![[Pasted image 20241022123134.png]]
![[Pasted image 20241022123155.png]]

ask:
retrieve the count of companies that have posted duplicate job listings.

code:
```SQL
with job_count_cte as (
select company_id, title, description, count(job_id) AS job_count
from job_listings
group by company_id, title, description)

select distinct count(company_id) AS duplicate_companies
from job_count_cte 
where job_count > 1;
```

9. Robinhood | Cities With Completed Trades | Easy
![[Pasted image 20241022130004.png]]
![[Pasted image 20241022130023.png]]
![[Pasted image 20241022130040.png]]
![[Pasted image 20241022130056.png]]

ask:
- retrieve the top three cities that have the highest number of completed trade orders listed in descending order
- output the city name and the corresponding number of completed trade orders

code:
```sql
-- My code:
WITH TRADES_INFO AS (
SELECT *
FROM TRADES T
INNER JOIN USERS U ON T.USER_ID = U.USER_ID
WHERE T.STATUS NOT LIKE 'Cancelled')

SELECT CITY, COUNT (ORDER_ID) AS TOTAL_ORDERS
FROM TRADES_INFO
GROUP BY CITY
ORDER BY COUNT(ORDER_ID) DESC
LIMIT 3;

-- DL Code:
SELECT users.city, COUNT(trades.order_id) AS total_orders FROM trades INNER JOIN users ON trades.user_id = users.user_id WHERE trades.status = 'Completed' GROUP BY users.city ORDER BY total_orders DESC LIMIT 3;
```

10. Amazon | Average Review Ratings | Easy
![[Pasted image 20241024124903.png]]
![[Pasted image 20241024124931.png]]
![[Pasted image 20241024124948.png]]
```sql
```
code:
```sql
SELECT 
  EXTRACT(MONTH FROM SUBMIT_DATE) AS mth,
  PRODUCT_ID AS product,
  CAST(AVG(STARS) AS DECIMAL(10,2)) AS avg_stars
FROM
  REVIEWS
GROUP BY
  EXTRACT(MONTH FROM SUBMIT_DATE), PRODUCT_ID
ORDER BY 
  1, 2
```

11. FAANG | Well Paid Employees | Easy
![[Pasted image 20241025082231.png]]
![[Pasted image 20241025082258.png]]

ask: 
- identify all employees who earn more than their direct managers
- the result should include the employee's ID and name

code:
```sql
SELECT E.EMPLOYEE_ID, E.NAME AS EMPLOYEE_NAME
FROM EMPLOYEE AS M
JOIN EMPLOYEE E ON M.EMPLOYEE_ID = E.MANAGER_ID
WHERE E.SALARY > M.SALARYY > M.SALARY
```

12. Facebook | App Click-through Rate (CTR) | Easy
![[Pasted image 20241025093315.png]]
![[Pasted image 20241025093340.png]]
![[Pasted image 20241025093536.png]]
Definition and note:

- Percentage of click-through rate (CTR) = 100.0 * Number of clicks / Number of impressions
- To avoid integer division, multiply the CTR by 100.0, not 100.


ask:
- calculate the click-through rate (CTR) for the app in 2022
- round the results to 2 decimal places

code:
```sql
SELECT 
  APP_ID,
  CAST(100.0 *
  SUM(CASE WHEN EVENT_TYPE LIKE 'click' THEN 1 ELSE 0 END) / 
  SUM(CASE WHEN EVENT_TYPE LIKE 'impression' THEN 1 ELSE 0 END) AS DECIMAL(10,2)) AS ctr
FROM
  EVENTS
WHERE
  EXTRACT(YEAR FROM TIMESTAMP) = 2022
GROUP BY
  APP_ID;

-- Alternate solutions:

-- using count(case)
SELECT 
	app_id, 
	ROUND(100.0 * 
	COUNT(CASE WHEN event_type = 'click' THEN 1 ELSE NULL END) / 
	COUNT(CASE WHEN event_type = 'impression' THEN 1 ELSE NULL END), 2) AS ctr_rate 
FROM events 
WHERE timestamp >= '2022-01-01' AND timestamp < '2023-01-01' 
GROUP BY app_id;

-- using sum(1)(filter)
SELECT 
	app_id, 
	ROUND(100.0 * 
	SUM(1) FILTER (WHERE event_type = 'click') / 
	SUM(1) FILTER (WHERE event_type = 'impression'), 2) AS ctr_app 
FROM events 
WHERE timestamp >= '2022-01-01' AND timestamp < '2023-01-01' 
GROUP BY app_id;
```
##### **SUM(1) FILTER (WHERE event_type = 'click')**

- **`SUM(1)`**: This is effectively counting rows. Each time a row is encountered that satisfies the `FILTER` condition, it adds `1` to the sum. So, this is counting the number of `click` events.
- **`FILTER (WHERE event_type = 'click')`**: The `FILTER()` clause specifies that only rows where `event_type = 'click'` are considered for this sum.

Thus, **`SUM(1) FILTER (WHERE event_type = 'click')`** counts how many times a `click` event occurred for each `app_id`.

13. TikTok | Second Day Confirmation | Easy
![[Pasted image 20241025110351.png]]
![[Pasted image 20241025110418.png]]
![[Pasted image 20241025110438.png]]
Definition:
- `action_date` refers to the date when users activated their accounts and confirmed their sign-up through text messages.
ask: 
- display the user IDs of those who did not confirm their sign-up on the first day, but confirmed on the second day

Code:
```sql
SELECT DISTINCT E.USER_ID
FROM EMAILS E
JOIN TEXTS T ON E.EMAIL_ID = T.EMAIL_ID
WHERE 
  T.SIGNUP_ACTION = 'Confirmed' AND
  T.ACTION_DATE = E.SIGNUP_DATE + INTERVAL '1 DAY';
```

[Date Time Functions Refresher](https://datalemur.com/sql-tutorial/sql-date-time-function) #Important

14. IBM | IBM db2 Product Analytics | Easy
![[Pasted image 20241025112849.png]]
![[Pasted image 20241025113005.png]]
![[Pasted image 20241025113028.png]]

ask:
-  generate data to populate a histogram that shows the number of unique queries run by employees during the third quarter of 2023 (July to September)
- it should count the number of employees who did not run any queries during this period
- display the number of unique queries as histogram categories, along with the count of employees who executed that number of unique queries

code:
```sql
WITH EMPLOYEE_QUERIES AS (
  SELECT 
    E.EMPLOYEE_ID, 
    COALESCE(COUNT(DISTINCT Q.QUERY_ID), 0) AS UNIQUE_QUERIES
  FROM 
    EMPLOYEES E
  LEFT JOIN 
    QUERIES Q ON E.EMPLOYEE_ID = Q.EMPLOYEE_ID
  AND 
    QUERY_STARTTIME::DATE BETWEEN '07/01/2023' AND '09/30/2023'
  GROUP BY 
    E.EMPLOYEE_ID
)
  
SELECT
  UNIQUE_QUERIES,
  COUNT(EMPLOYEE_ID) AS EMPLOYEE_COUNT
FROM 
  EMPLOYEE_QUERIES
GROUP BY 
  UNIQUE_QUERIES
ORDER BY 
  UNIQUE_QUERIES;
```
NOTE:
`COALESCE()`
![[Pasted image 20241025123232.png]]
![[Pasted image 20241025123318.png]]
![[Pasted image 20241025123336.png]]

15. JPMorgan Chase | Cards Issued Difference | Easy
![[Pasted image 20241025123936.png]]
![[Pasted image 20241025123956.png]]
![[Pasted image 20241025124011.png]]

ask:
- output the name of each credit card and the difference in the number of issued cards between the month with the highest issuance cards and the lowest issuance 
- arrange the results based on the largest disparity

code: 
```sql
SELECT 
	CARD_NAME, 
	MAX(ISSUED_AMOUNT) - MIN(ISSUED_AMOUNT) AS DIFFERENCE
FROM 
	MONTHLY_CARDS_ISSUED
GROUP BY 
	CARD_NAME
ORDER BY 2 DESC;
```

16. Alibaba | Compressed Mean | Easy
![[Pasted image 20241027120239.png]]
![[Pasted image 20241027120334.png]]

ask:
- find the mean number of items per order on Alibaba, rounded to 1 decimal place using tables which includes information on the count of items in each order (`item_count` table) and the corresponding number of orders for each item count (`order_occurrences` table)

code:
```sql
SELECT 
  CAST(SUM(ITEM_COUNT * ORDER_OCCURRENCES) * 1.0 / 
  SUM(ORDER_OCCURRENCES) AS DECIMAL(10,1)) AS MEAN
FROM 
	ITEMS_PER_ORDER
```

17. Uber | User's Third Transaction | Medium
![[Pasted image 20241027123555.png]]
![[Pasted image 20241027123626.png]]

ask:
- obtain the third transaction of every user
- output the user id, spend and transaction date

code:
```sql
SELECT 
	USER_ID, 
	SPEND, 
	TRANSACTION_DATE
FROM (
	SELECT
		USER_ID,
		SPEND,
		ROW_NUMBER() OVER(PARTITION BY USER_ID ORDER BY TRANSACTION_DATE) AS ROW,
		TRANSACTION_DATE
	FROM 
		TRANSACTIONS) AS TRANSACTION_ORDER
WHERE ROW = 3;
```

18. FAANG | Second Highest Salary | Medium
![[Pasted image 20241027125148.png]]
![[Pasted image 20241027125206.png]]

code:
```sql
SELECT MAX(SALARY) AS SECOND_HIGHEST_SALARY
FROM EMPLOYEE
WHERE SALARY < (SELECT MAX(SALARY) FROM EMPLOYEE); 

-- Alternate code with CTE
WITH highest_salary_cte AS (
  SELECT MAX(salary) AS highest_salary
  FROM employee
)

SELECT MAX(salary) AS second_highest_salary
FROM employee
WHERE salary < (
    SELECT MAX(SALARY)
    FROM employee
);
```

19. CVS Health | Pharmacy Analytics (Part 1) | Easy
![[Pasted image 20241028101544.png]]
![[Pasted image 20241028101609.png]]
![[Pasted image 20241028101629.png]]

ask:
- top 3 most profitable drugs sold
- how much profit they made 
- (Assume that there are no ties in the profits.) 
- display the result from the highest to the lowest total profit

code: 
```sql
SELECT DRUG, SUM(TOTAL_SALES - COGS) AS TOTAL_PROFIT
FROM PHARMACY_SALES
GROUP BY DRUG
ORDER BY 2 DESC
LIMIT 3;

-- Above code can be written shortly as:
SELECT DRUG, TOTAL_SALES - COGS AS TOTAL_PROFIT
FROM PHARMACY_SALES
ORDER BY 2 DESC
LIMIT 3;
```

20. CVS Health | Pharmacy Analytics (Part 2) | Easy
![[Pasted image 20241028103108.png]]
![[Pasted image 20241028103133.png]]
![[Pasted image 20241028103151.png]]
![[Pasted image 20241028103206.png]]

ask:
-  identify the manufacturers associated with the drugs that resulted in losses for CVS Health
- calculate the total amount of losses incurred 
- output the manufacturer's name, the number of drugs associated with losses, and the total losses in absolute value
- display the results sorted in descending order with the highest losses displayed at the top

code:
```sql
SELECT MANUFACTURER, COUNT(DRUG) AS DRUG_COUNT, ABS(SUM(TOTAL_SALES - COGS)) AS TOTAL_LOSS
FROM PHARMACY_SALES
WHERE TOTAL_SALES - COGS < 0
GROUP BY MANUFACTURER
ORDER BY TOTAL_LOSS DESC;
```

Note:
![[Pasted image 20241028105302.png]]

21. CVS Health | Pharmacy Analytics (Part 3) | Easy
![[Pasted image 20241028114254.png]]
![[Pasted image 20241028114317.png]]
![[Pasted image 20241028114334.png]]
![[Pasted image 20241028114354.png]]

ask:
- calculate the total drug sales for each manufacturer
- round the answer to the nearest million and report your results in descending order of total sales
- in case of any duplicates, sort them alphabetically by the manufacturer name
- format your results as follows: "$36 million"

code:
```sql
SELECT 
  MANUFACTURER, 
  CONCAT('$', ROUND(SUM(TOTAL_SALES) / 1000000), ' million') AS SALE
FROM PHARMACY_SALES
GROUP BY MANUFACTURER
ORDER BY SUM(TOTAL_SALES) DESC, 1;

-- Code with CTE:
WITH drug_sales AS ( SELECT manufacturer, SUM(total_sales) as sales FROM pharmacy_sales GROUP BY manufacturer ) SELECT manufacturer, ('$' || ROUND(sales / 1000000) || ' million') AS sales_mil FROM drug_sales ORDER BY sales DESC, manufacturer;
```
Note:
![[Pasted image 20241028120227.png]]

22. Snapchat | Sending vs. Opening Snaps | Medium
![[Pasted image 20241028120548.png]]
![[Pasted image 20241028120611.png]]
![[Pasted image 20241028120630.png]]
![[Pasted image 20241028120647.png]]

ask:
- Write a query to obtain a breakdown of the time spent sending vs. opening snaps as a percentage of total time spent on these activities grouped by age group
- Round the percentage to 2 decimal places in the output
- Calculate the following percentages:
    - time spent sending / (Time spent sending + Time spent opening)
    - Time spent opening / (Time spent sending + Time spent opening)
- To avoid integer division in percentages, multiply by 100.0 and not 100.

code:
```sql

```
    
    
    
    
    
    
    
    
    
    

#### [[Statistics]]
1. Question
![[Pasted image 20241021175826.png]]

Calculations & Solution:
![[Pasted image 20241021180047.png]]
https://datalemur.com/questions/coin-fairness-test






ORDER BY
  users_num DESC
;
```
