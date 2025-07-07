# RESULTS: Cryptopunk NFT Analysis Project


## TABLE OF CONTENTS
<b>SKILLS:</b> `Data Analysis`, `Data Exploration`, `SQL`, `Aggregation`, `Summary Function`:

- [Total number of sales within the dataset (January 2018 to December 2021)](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#total-number-of-sales-within-the-specified-period)
- [Identification of the top 5 most expensive transactions by USD price.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#identification-of-the-top-5-most-expensive-transactions-by-usd-price)
- [Calculation of a moving average of USD prices to observe price trends.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#calculation-of-a-moving-average-of-usd-prices-to-observe-price-trends)
- [Determination of average sale prices for each NFT name.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#determination-of-average-sale-prices-for-each-nft-name)
- [Analysis of sales volume and average ETH price by day of the week.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#analysis-of-sales-volume-and-average-eth-price-by-day-of-the-week)
- [Construction of a descriptive summary for each transaction.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#construction-of-a-descriptive-summary-for-each-transaction)
- [Creation of a dedicated view for purchases made by a specific wallet address.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#creation-of-a-dedicated-view-for-purchases-made-by-a-specific-wallet-address)
- [Visualization preparation for ETH price ranges (histogram).](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#visualization-preparation-for-eth-price-ranges-histogram)
- [Comparative analysis of highest and lowest sale prices for each NFT.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#comparative-analysis-of-highest-and-lowest-sale-prices-for-each-nft)
- [Identification of the most sold NFT each month/year and its associated price.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#identification-of-the-most-sold-nft-each-monthyear-and-its-associated-price)
- [Calculation of total monthly sales volume.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#calculation-of-total-monthly-sales-volume)
- [Counting transactions for a specific wallet.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#counting-transactions-for-a-specific-wallet)
- [Development of an "estimated average value calculator" to account for outlier sales and provide a more representative daily average price.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#development-of-an-estimated-average-value-calculator-to-account-for-outlier-sales-and-provide-a-more-representative-daily-average-price)


<h2>QUESTIONS</h2>
  
<h3>Total number of sales within dataset (January 2018 to December 2021)</h3>

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

<img src="https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Total%20Sales.png" widht="450" height="4" alt="Total Sales">

<br>

<b>INSIGHT</b> 
 
This is a fundamental first step in data exploration, providing a quick overview of the dataset's volume. A high count suggests a bustling market, while a low count might indicate niche activity. It helps in understanding the scale of the data.

<h1></h1>
  
<h3>Identification of the top 5 most expensive transactions by USD price</h3>

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

<img src="https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Top%205%20Most%20Expensive%20Cryptopunk%20NFT%20Transaction.png" widht="450" height="4" alt="Top 5 Most Expensive Cryptopunk NFT Transaction ">

<br>

<b>INSIGHT</b> 

Identifying top transactions immediately highlights outliers or significant events in the market. It can reveal specific NFTs that command extremely high values, potentiallu indicating rarity, historical significance, or intense speculation, which are crucial for understanding marlet dynamics and value drivers.

<h1></h1>
  
<h3>Calculation of a moving average of USD prices to observe price trends</h3>

<h1></h1>

This query calculates a 50-transaction simple moving average of the USD price for each NFT transaction, ordered chronologically by date and timestamp. Both the individual usd_price and the calculated moving_average_usd_price are rounded to the nearest whole dollar for cleaner presentation and easier interpretation.
 
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

<img src="https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Calculating%20Moving%20Average%20USD%20Prices%20of%20Last%2050%20Transactions.png" widht="450" height="4" alt="Calculating Moving Average USD Prices of Last 50 Transactions">

<br>

<b>INSIGHT</b> 

Moving averages are crucial for smoothing out short-term market noise and revealing underlying price trends. By averaging the last 50 transactions, this query helps visualize whether NFT prices, on average, were increasing, decreasing, or remaining stable over time, providing a clearer picture of market sentiment and momentum. Rounding the prices to whole dollars simplifies the visual representation of these trends, making it easier to grasp the general direction of the market without being distracted by minor decimal fluctuations. While rounding can introduce small inaccuracies at an individual transaction level, for aggregated trend analysis like a moving average over many transactions, its impact is generally minimal and beneficial for clarity.

<h1></h1>
  
<h3>Determination of average sale prices for each NFT name</h3>

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
  
<h3>Analysis of sales volume and average ETH price by day of the week</h3>

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
  
<h3>Construction of a descriptive summary for each transaction</h3>

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
  
<h3>Creation of a dedicated view for purchases made by a specific wallet address</h3>

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
  
<h3>Visualization preparation for ETH price ranges (histogram)</h3>

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
  
<h3>Comparative analysis of highest and lowest sale prices for each NFT</h3>

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
  
<h3>Identification of the most sold NFT each month/year and its associated price</h3>

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
  
<h3>Calculation of total monthly sales volume</h3>

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
  
<h3>Counting transactions for a specific wallet</h3>

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
  
<h3>Development of an "estimated average value calculator" to account for outlier sales and provide a more representative daily average price</h3>

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

