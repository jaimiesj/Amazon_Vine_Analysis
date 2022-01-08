# Amazon Vine Analysis
## Overiew
The purpose of this analysis was determine if there was any bias in reviews of participants in the Vine program versus those not in the Vine program

## Results
- There were 61 paid reviews and 16459 unpaid reviews

<img width="179" alt="Paid vs Non Paid" src="https://user-images.githubusercontent.com/88955412/148657840-c394fc8c-be09-48ef-8244-1672fbb5a484.png">

- There were 34 5 star Vine reviews while there were 8375 5 star non-Vine reviews
<img width="50" alt="Paid 5 star" src="https://user-images.githubusercontent.com/88955412/148657955-a68a032a-fb41-4073-afb0-472a9493a07b.png">
<img width="45" alt="Non paid 5 star" src="https://user-images.githubusercontent.com/88955412/148657967-01eb53b2-84d0-4fe6-8905-28fc15f80c51.png">

- 55% of Vine reviews were 5 stars while 50% of non-Vine reviews were 5 stars
<img width="147" alt="Paid percent" src="https://user-images.githubusercontent.com/88955412/148658053-e78436fa-d021-44bc-8c70-efbc056e5105.png">
<img width="146" alt="Unpaid percent" src="https://user-images.githubusercontent.com/88955412/148658058-ac788e5f-0583-4772-b1b3-3c34629324e5.png">

## Sumary
It would appear there is no positivity bias for reviews in the Vine program as the percent of 5 star ratings were almost equal between Vine and non-Vine members. Another analysis that could be performed could look at repeat reviewers and track their ratings, to determine if there is any bias in specific reviews always giving postive reviews in the Vine program versus repeat reviewers not in the Vine program


## SQL Code

Find below the SQL line of code used to preform the above analysis

- CREATE TABLE vine_2 AS SELECT * FROM vine_table WHERE total_votes >= 20

- SELECT * FROM vine_2 WHERE CAST(helpful_votes AS FLOAT)/CAST(total_votes AS FLOAT) >= 0.5

- CREATE TABLE vine_paid AS SELECT * FROM vine_2 WHERE vine = 'Y'

- SELECT * FROM vine_paid

- CREATE TABLE vine_unpaid AS SELECT * FROM vine_2 WHERE vine = 'N'

- SELECT (
	SELECT COUNT(*) 
	FROM vine_paid
	) AS number_of_paid_reviews,
	(SELECT COUNT(*)
	FROM vine_unpaid
	) AS number_of_unpaid_reviews
	
- SELECT COUNT(*) FROM vine_paid AS five_star_paid_reviews WHERE star_rating = 5

- SELECT COUNT(*) FROM vine_unpaid AS five_star_unpaid_reviews WHERE star_rating = 5

- SELECT star_rating, count(star_rating) as star_count, count(star_rating) * 100 / (select count(*) from vine_paid) as paid_percent FROM vine_paid GROUP BY star_rating

- SELECT star_rating, count(star_rating) as star_count, count(star_rating) * 100 / (select count(*) from vine_unpaid) as unpaid_percent FROM vine_unpaid GROUP BY star_rating
	
