# Data with Danny #
##  Main points
**Count(*):** doesnot consider null or not
**Count(1):** checks if it's null, hence is slower. Same is the case with **count(col_name)**
**Group by:** divides the table into subgroups based on groupby and aggregate function returns one row from each subgroup.
>**window function:**  AS below over()
>
```sql
select rating, 
       count(*) as frequency,
       count(*) :: numeric / sum(count(*)) over() as percentage
from dvd_rentals.film_list 
group by rating;
```
>**::**- does type casting as numeric divided by numeric maybe float and SQL may not display float. OR we can use as **CAST(_column_name_   AS     _new-data-type_)**
The above query can be made in percentage by multiplying by 100 and rounding to two decimal positions
```sql
SELECT
  rating,
  COUNT(*) AS frequency,
  ROUND(
    100 * COUNT(*)::NUMERIC / SUM(COUNT(*)) OVER (),2
  ) AS percentage
FROM dvd_rentals.film_list
GROUP BY rating
ORDER BY frequency DESC;
```


- Frequency of combination of rating and category in descending order

```sql
select rating,
             category,
              count(*) as frequency
from dvd_rentals.film_list
group by rating , category
order by frequency desc
limit 10;`
```





> Written with [StackEdit](https://stackedit.io/).
