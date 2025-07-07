# RESULTS: CryptoPunk NFT Analysis Project


## QUESTIONS TABLE OF CONTENTS
<b>SKILLS:</b> `Data Analysis`, `Data Exploration`, `SQL`, `Aggregation`, `Summary Function`:

- [1. Total number of sales within the dataset (January 2018 to December 2021)](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#total-number-of-sales-within-the-specified-period)
  
- [2. Identification of the top 5 most expensive transactions by USD price.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#identification-of-the-top-5-most-expensive-transactions-by-usd-price)

- [3. Calculation of a moving average of USD prices to observe price trends.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#calculation-of-a-moving-average-of-usd-prices-to-observe-price-trends)

- [4. Determination of average sale prices for each NFT name.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#determination-of-average-sale-prices-for-each-nft-name)

- [5. Analysis of sales volume and average ETH price by day of the week.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#analysis-of-sales-volume-and-average-eth-price-by-day-of-the-week)

- [6. Construction of a descriptive summary for each transaction.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#construction-of-a-descriptive-summary-for-each-transaction)

- [7. Creation of a dedicated view for purchases made by a specific wallet address.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#creation-of-a-dedicated-view-for-purchases-made-by-a-specific-wallet-address)

- [8. Visualization preparation for ETH price ranges (histogram).](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#visualization-preparation-for-eth-price-ranges-histogram)

- [9. Comparative analysis of highest and lowest sale prices for each NFT.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#comparative-analysis-of-highest-and-lowest-sale-prices-for-each-nft)

- [10. Identification of the most sold NFT each month/year and its associated price.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#identification-of-the-most-sold-nft-each-monthyear-and-its-associated-price)

- [11. Calculation of total monthly sales volume.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#calculation-of-total-monthly-sales-volume)

- [12. Counting transactions for a specific wallet.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#counting-transactions-for-a-specific-wallet)

- [13. Development of an "estimated average value calculator" to account for outlier sales and provide a more representative daily average price.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#development-of-an-estimated-average-value-calculator-to-account-for-outlier-sales-and-provide-a-more-representative-daily-average-price)

<h1></h1>

<h2>QUESTIONS</h2>
  
<h3>1. Total number of sales within dataset (January 2018 to December 2021)</h3>

<h1></h1>

 This query counts all rows in the `cryptopunkdata` table, providing the total number of NFT sales recordered from January 1, 2018 to December 31, 2021 in the dataset.

<br>

<b>SQL</b>

```
/*Total number of sales within the specified period.*/
SELECT COUNT(*) AS total_sales
FROM cryptopunkdata;
```
<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Total%20Sales.png)

<br>

<b>INSIGHT</b> 
 
This is a fundamental first step in data exploration, providing a quick overview of the dataset's volume. A high count suggests a bustling market, while a low count might indicate niche activity. It helps in understanding the scale of the data.

<h1></h1>
  



<h3>2. Identification of the top 5 most expensive transactions by USD price</h3>

<h1></h1>

This query retrieves the `name`, `eth_price`, `usd_price`,and `day` for the five highest-priced NFT transactions based on their USD value.
 
<br>

<b>SQL</b> 

```
/*Identification of the top 5 most expensive transactions by USP price*/
SELECT
	name, 
	eth_price,
	ROUND(usd_price,0) AS usd_price_no_decimals, -- Rounds to 0 decimal places
	day
FROM 
	cryptopunkdata 
ORDER BY 
	usd_price DESC
LIMIT 5;
```

<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Top%205%20Most%20Expensive%20Cryptopunk%20NFT%20Transaction.png)

<br>

<b>INSIGHT</b> 

Identifying top transactions immediately highlights outliers or significant events in the market. It can reveal specific NFTs that command extremely high values, potentiallu indicating rarity, historical significance, or intense speculation, which are crucial for understanding marlet dynamics and value drivers.

<h1></h1>
  

<h3>3. Calculation of a moving average of USD prices to observe price trends</h3>

<h1></h1>

This query calculates a 50-transaction simple moving average of the USD price for each NFT transaction, ordered chronologically by date and timestamp. Both the individual `usd_price` and the `calculated moving_average_usd_price` are rounded to the nearest whole dollar for cleaner presentation and easier interpretation.
 
<br>

<b>QUERY</b> 

```
/*Calculation of a moving average of USD prices that averages the last 50 transactions.*/
SELECT
    name,
    eth_price,
 	ROUND(usd_price,0) AS usd_price_no_decimals, -- Revoved decimals from usd_price 
 	ROUND(AVG(usd_price) OVER
 		(ORDER BY day ASC, `utc_timestamp` ASC ROWS BETWEEN 49 PRECEDING
 		AND CURRENT ROW),0) AS moving_average_usd_price -- Removed decimals from moving average usd-price
 FROM 
 	cryptopunkdata
 ORDER BY 
 	day ASC, `utc_timestamp` ASC;
```

<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Calculating%20Moving%20Average%20USD%20Prices%20of%20Last%2050%20Transactions.png)

<br>

<b>INSIGHT</b> 

Moving averages are crucial for smoothing out short-term market noise and revealing underlying price trends. By averaging the last 50 transactions, this query helps visualize whether NFT prices, on average, were increasing, decreasing, or remaining stable over time, providing a clearer picture of market sentiment and momentum. Rounding the prices to whole dollars simplifies the visual representation of these trends, making it easier to grasp the general direction of the market without being distracted by minor decimal fluctuations. While rounding can introduce small inaccuracies at an individual transaction level, for aggregated trend analysis like a moving average over many transactions, its impact is generally minimal and beneficial for clarity.

<h1></h1>
  

<h3>4. Determination of average sale prices for each NFT name</h3>

<h1></h1>

This query computes the average USD sales price for each unique CryptoPunk NFT, listing them from the most expensive average to the least.
 
<br>

<b>QUERY</b> 

```
/*Determination of average sale prices for each NFT name. Sort descending. Name the average column as average_price.*/
SELECT 
	name,
	ROUND(AVG(usd_price),0) AS average_price
FROM 
	cryptopunkdata 
GROUP BY 
	name 
ORDER BY 
	average_price DESC;
```

<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/AVG%20Sales%20Prices%20by%20name.png)

<br>

<b>INSIGHT</b> 

This analysis helps in understanding the inherent value or market perception of different individual NFTs within the CryptoPunks collection. It can highlight which specific Punks (e.g., those with rare traits) consistently sell for more, pointing to key value attributes within the collection.

<h1></h1>
  
<h3>5. Analysis of sales volume and average ETH price by day of the week</h3>

<h1></h1>

This query aggregates the number of sales and the average ETH price per transaction for each day of the week, ordering the results by the count of sales from lowest to highest.
 
<br>

<b>QUERY</b> 

```
/*Analysis of sales volume, average ETH price, and USD Price by day of the week.
 * Order by the count of transactions in ascending order.
 */

SELECT 
	CASE 
		WHEN DAYOFWEEK(day) = 1 THEN 'Sunday'
		WHEN DAYOFWEEK(day) = 2 THEN 'Monday'
		WHEN DAYOFWEEK(day) = 3 THEN 'Tuesday'
		WHEN DAYOFWEEK(day) = 4 THEN 'Wednesday'
		WHEN DAYOFWEEK(day) = 5 THEN 'Thursday'
		WHEN DAYOFWEEK(day) = 6 THEN 'Friday'
		WHEN DAYOFWEEK(day) = 7 THEN 'Saturday'
		ELSE 'Unknown'
	END AS day_of_week,
	COUNT(*) AS number_of_sales,
	ROUND(AVG(eth_price),10) AS average_eth_price, -- Removed decimals if more than 10 places.
	CONCAT('$', FORMAT(AVG(usd_price),2)) AS average_usd_price -- Added '$' in front of value. Removed decimals if more than 2 places.
FROM 
	cryptopunkdata
GROUP BY 
	day_of_week 
ORDER BY 
	number_of_sales ASC;
```

<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Sales%20Volume%20%26%20Average%20ETH%20Price%20%26%20USD%20Price.png)

<br>

<b>INSIGHT</b> 

This helps identify temporal patterns in NFT trading activity. Are certain days of the week more active for sales, or do prices fluctuate based on the day? This could uncover insights into typical buyer behavior or market liquidity patterns throughout the week.

<h1></h1>
  
<h3>6. Construction of a descriptive summary for each transaction</h3>

<h1></h1>

This query
 
<br>

<b>QUERY</b> 

```

```

<br>

<img src="" widht="450" height="4" alt="">

<br>

<b>INSIGHT</b> 

<h1></h1>
  
<h3>7. Creation of a dedicated view for purchases made by a specific wallet address</h3>

<h1></h1>

This query
 
<br>

<b>QUERY</b> 

```

```

<br>

<img src="" widht="450" height="4" alt="">

<br>

<b>INSIGHT</b> 

<h1></h1>
  
<h3>8. Visualization preparation for ETH price ranges (histogram)</h3>

<h1></h1>

This query
 
<br>

<b>QUERY</b> 

```

```

<br>

<img src="" widht="450" height="4" alt="">

<br>

<b>INSIGHT</b> 

<h1></h1>
  
<h3>9. Comparative analysis of highest and lowest sale prices for each NFT</h3>

<h1></h1>

This query

<b>

<b>QUERY</b> 

```

```

<br>

<img src="" widht="450" height="4" alt="">

<br>

<b>INSIGHT</b> 

<h1></h1>
  
<h3>10. Identification of the most sold NFT each month/year and its associated price</h3>

<h1></h1>

This query
 
<br>

<b>QUERY</b> 

```

```

<br>

<img src="" widht="450" height="4" alt="">

<br>

<b>INSIGHT</b> 

<h1></h1>
  
<h3>11. Calculation of total monthly sales volume</h3>

<h1></h1>

This query
 
<br>

<b>QUERY</b> 

```

```

<br>

<img src="" widht="450" height="4" alt="">

<br>

<b>INSIGHT</b> 

<h1></h1>
  
<h3>12. Counting transactions for a specific wallet</h3>

<h1></h1>

This query
 
<br>

<b>QUERY</b> 

```

```

<br>

<img src="" widht="450" height="4" alt="">

<br>

<b>INSIGHT</b> 

<h1></h1>
  
<h3>13. Development of an "estimated average value calculator" to account for outlier sales and provide a more representative daily average price</h3>

<h1></h1>

This query
 
<br>

<b>QUERY</b> 

```

```

<br>

<img src="" widht="450" height="4" alt="">

<br>

<b>INSIGHT</b> 



<h1></h1>
  
<h3></h3>

<br>

<img src="" widht="450" height="4" alt="">

