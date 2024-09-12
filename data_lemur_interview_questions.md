## SQL_DataLemur_Twitter

### Question:
Assume you're given a table Twitter tweet data, write a query to obtain a histogram of tweets posted per user in 2022. Output the tweet count per user as the bucket and the number of Twitter users who fall into that bucket.

In other words, group the users by the number of tweets they posted in 2022 and count the number of uthesers in each group.

**tweets Table:**

![tweets](./image-1.png)

**Example Output:**

![](./image.png)

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
ORDER BY
  users_num DESC
;
```
