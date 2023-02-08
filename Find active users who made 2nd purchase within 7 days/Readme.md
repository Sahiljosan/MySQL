## Problem Statement
Write a query that'll identify returning active users.  <br>
A returning active user is a user that has made a second purchase within 7 days of any other of their purchases. <br>
Output a list of user_ids of these returning active users. <br>

## Table name `amazon_transactions`


```
select distinct(user_id) from
(select *,
lead(created_at) over (partition by user_id order by created_at) next_purchase
from amazon_transactions
) sbqry

where datediff(next_purchase,created_at) <= 7;
```


## Expected Output
![](https://i.imgur.com/ViqVbiS.png)
