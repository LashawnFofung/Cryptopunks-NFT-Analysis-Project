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

<h1></h1>
  
<h3>Total number of sales within dataset (January 2018 to December 2021).</h3>

 This query counts all rows in the `cryptopunkdata` table, providing the total number of NFT sales recordered from January 1, 2018 to December 31, 2021 in the dataset.

<br>

<b>SQL</b>
``` /*Total number of sales within the specified period.*/
SELECT COUNT(*) AS total_sales
FROM cryptopunkdata;
```
<br>

<img src="https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Total%20Sales.png" widht="450" height="4" alt="Total Sales">

<br>

<b>INSIGHT</b> 
 
This is a fundamental first step in data exploration, providing a quick overview of the dataset's volume. A high count suggests a bustling market, while a low count might indicate niche activity. It helps in understanding the scale of the data.

<h1></h1>
  
<h3>Identification of the top 5 most expensive transactions by USD price.</h3>

<br>
 This query retrieves the `name`, `eth_price`, `usd_price`,and `day` for the five highest-priced NFT transactions based on their USD value.
 
<br>

<b>SQL</b> 

```
SELECT
	name, 
	eth_price,
	usd_price,
	day
FROM 
	cryptopunkdata 
ORDER BY 
	usd_price 
LIMIT 5;
```

<br>

<img src="https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Top%205%20Most%20Expensive%20Cryptopunk%20NFT%20Transaction.png" widht="450" height="4" alt="">

<br>

<b>INSIGHT</b> 

Identifying top transactions immediately highlights outliers or significant events in the market. It can reveal specific NFTs that command extremely high values, potentiallu indicating rarity, historical significance, or intense speculation, which are crucial for understanding marlet dynamics and value drivers.

<h1></h1>
  
<h3>Calculation of a moving average of USD prices to observe price trends.</h3>

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
  
<h3>Determination of average sale prices for each NFT name.</h3>

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
  
<h3>Analysis of sales volume and average ETH price by day of the week.</h3>

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
  
<h3>Construction of a descriptive summary for each transaction.</h3>

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
  
<h3>Creation of a dedicated view for purchases made by a specific wallet address.</h3>

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
  
<h3>Visualization preparation for ETH price ranges (histogram).</h3>

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
  
<h3>Comparative analysis of highest and lowest sale prices for each NFT.</h3>

<br>

<b>QUERY</b> 

```

```

<br>

<img src="" widht="450" height="4" alt="">

<br>

<b>INSIGHT</b> 

<h1></h1>
  
<h3>Identification of the most sold NFT each month/year and its associated price.</h3>

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
  
<h3>Calculation of total monthly sales volume.</h3>

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
  
<h3>Counting transactions for a specific wallet.</h3>

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
  
<h3>Development of an "estimated average value calculator" to account for outlier sales and provide a more representative daily average price.</h3>

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

