# RESULTS: CryptoPunk NFT Analysis Project


## QUESTIONS TABLE OF CONTENTS
<b>SKILLS:</b> `Data Analysis`, `Data Exploration`, `SQL`, `Aggregation`, `Summary Function`:

- [1. Total number of sales within the dataset (January 2018 to December 2021)](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#total-number-of-sales-within-the-specified-period)
  
- [2. Identification of the top 5 most expensive transactions by USD price.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#identification-of-the-top-5-most-expensive-transactions-by-usd-price)

- [3. Calculation of a moving average of USD prices to observe price trends.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#calculation-of-a-moving-average-of-usd-prices-to-observe-price-trends)

- [4. Determination of average sale prices for each NFT name.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#determination-of-average-sale-prices-for-each-nft-name)

- [5. Analysis of sales volume, average ETH price, and USD price by day of the week.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/CryptoPunks%20NFT%20Analysis%20Report.md#5-analysis-of-sales-volume-average-eth-price-and-usd-price-by-day-of-the-week)

- [6. Construction of a descriptive summary for each transaction.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#construction-of-a-descriptive-summary-for-each-transaction)

- [7. Creation of a dedicated view for purchases made by a specific wallet address.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/Report.md#creation-of-a-dedicated-view-for-purchases-made-by-a-specific-wallet-address)

- [8. Comparative analysis of highest and lowest sale prices for each NFT.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/CryptoPunks%20NFT%20Analysis%20Report.md#8-comparative-analysis-of-highest-and-lowest-sale-prices-for-each-nft)

- [9. Identification of the most sold NFT each month/year and its associated price.]()

- [10. Calculation of total monthly sales volume.]()

- [11. Counting transactions for a specific wallet.]()

- [12. Development of an "estimated average value calculator" to account for outlier sales and provide a more representative daily average price.]()

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
  
<h3>5. Analysis of sales volume, average ETH price, and USD price by day of the week</h3>

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

This query constructs a human-readable summary sentence for each NFT sale, detailing the NFT name, sale price in USD, buyer, seller, and date.
 
<br>

<b>QUERY</b> 

```

/*Construction of a descriptive summary for each transaction.*/
SELECT
	CONCAT(
		name, ' was sold for $', FORMAT(ROUND(usd_price), 2),
		' to ', buyer_address,
		' from ', seller_address,
		' on ', day
	)	AS summary
FROM 
	cryptopunkdata;
```

<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Descriptive%20Summary%20for%20Each%20Transaction.png)


<br>

<b>INSIGHT</b> 

While not directly quantitative, this query aids in qualitative data exploration by making individual transactions more immediately understandable. It helps in quickly reviewing specific sales events in a narrative format, which can be useful for spot-checking data integrity or gaining a quick sense of transaction flow.

<h1></h1>
  
<h3>7. Creation of a dedicated view for purchases made by a specific wallet address</h3>

<h1></h1>

This statement creates a SQL view named `1919_purchases` that encapsulates all transaction data where the specified wallet address (`0x1919db36ca2fa2e15f9000fd9cdc2edcf863e685`) acted as the buyer.
 
<br>

<b>QUERY</b> 

```
/*Creation of a view called "1919_purchases" and contains any sales where
 * "0x1919db36ca2fa2e15f9000fd9cdc2edcf863e685" was the buyer. */
CREATE VIEW 1919_purchases AS
SELECT * FROM cryptopunkdata
WHERE 
	buyer_address = '0x1919db36ca2fa2e15f9000fd9cdc2edcf863e685';
```

<br>

<b>To see new View called "1919_purchases:</b>

<br>

```
/*To show 1919_purchases view in the current database.*/
SELECT * FROM 1919_purchases;
```
<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Creation%20of%20View.png)


<br>

<b>INSIGHT</b> 

Views are crucial for focusing exploration on specific subsets of data without modifying the original table. This view allows for easy and repeatable analysis of a particular high-activity buyer's purchasing patterns, which can reveal their investment strategy, preferred NFTs, or overall market impact.

<h1></h1>
  
<h3>8. Comparative analysis of highest and lowest sale prices for each NFT</h3>

<h1></h1>

This query combines two result sets: one showing the highest USD price for each unique NFT (labeled 'highest'), and another showing the lowest USD price for each unique NFT (labeled 'lowest'), then orders them by NFT name and status.

<br>

<b>QUERY</b>

```
/*Comparative analysis of highest and lowest sale prices for each NFT.
 * Formatted with commas and always 2 decimal places. */
SELECT 
	cryptopunkdata.name AS name,
	FORMAT(MAX(cryptopunkdata.usd_price),2) AS price,
	'highest' AS status
FROM 
	cryptopunkdata 
GROUP BY 
	cryptopunkdata.name
UNION ALL
SELECT 	
	name AS name,
	FORMAT(MIN(cryptopunkdata.usd_price),2) AS price,
	'lowest' AS status
FROM 
	cryptopunkdata 
GROUP BY 
	cryptopunkdata.name 
ORDER BY 
	name ASC, status ASC;
```

<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Comparative%20analysis%20of%20highest%20%26%20lowest%20sale%20price.png)


<br>

<b>INSIGHT</b> 

This comparison highlights the price volatility and range for individual NFTs. A large difference between highest and lowest prices for the same NFT indicates significant market fluctuations or changes in perceived value over time. This is critical for understanding risk and potential return on investment for specific digital assets.

<h1></h1>
  
<h3>9. Identification of the most sold NFT each month/year and its associated price</h3>

<h1></h1>

This multi-step query first cleans the `day` column to ensure consistent date formatting, handling potential variations or errors in the original data. It then proceeds to aggregate the sales data, calculating the total sales count and average USD price for each NFT (`name`) within each month-year (`YYYY-MM`). Subsequently, it uses a ranking function (`ROW_NUMBER()`) to identify the single most frequently sold NFT for every given month and year, selecting the NFT with the highest sales count (tie-breaking alphabetically by NFT name). The final output includes the month-year, the NFT's name, its total sales count for that month, and its average sale price in USD (formatted with thousands separators and two decimal places).
 
<br>

<b>QUERY</b> 

```
/*Without comments
*Identification of the most sold NFT each month / year combination?*/

/*Clean the 'day' column to ensure consistent data format*/
WITH Cleaned_Data AS (
	SELECT
	    day,
	    name,
	    usd_price,
	    CASE  
	        WHEN STR_TO_DATE(day, '%m/%d/%y') IS NOT NULL THEN STR_TO_DATE(day, '%m/%d/%y') 
	        WHEN STR_TO_DATE(day, '%Y-%m-%d') IS NOT NULL THEN STR_TO_DATE(day, '%Y-%m-%d') 
	        WHEN STR_TO_DATE(day, '%m-%d-%y') IS NOT NULL THEN STR_TO_DATE(day, '%m-%d-%y') 
	        WHEN STR_TO_DATE(SUBSTRING_INDEX(day, ' ', 1), '%m/%d/%y') IS NOT NULL
	             THEN STR_TO_DATE(SUBSTRING_INDEX(day, ' ', 1), '%m/%d/%y')
	        ELSE NULL  
	    END AS cleaned_day
	FROM
	   cryptopunkdata
),
    
-- First step in multiple CTE is MonthlySales CTE - aggregrates the sales data.
Monthly_Sales AS (  
	SELECT
		DATE_FORMAT(cleaned_day, '%m/%y') AS sale_month_year, 
		name, 
		COUNT(*) AS nft_monthly_sales_count,  
		AVG(usd_price) AS average_monthly_usd_price  
	FROM
		Cleaned_Data  
	WHERE 
		cleaned_day IS NOT NULL  
	GROUP BY
		sale_month_year, name

),

-- Second step in multiple CTE is RankedMonthlySales CTE - ranks te NFTs within each sale_month_year based on their nft_monthly_sales_count.
Ranked_Monthly_Sales AS (
	SELECT 
		sale_month_year,
		name, 
		nft_monthly_sales_count,
		average_monthly_usd_price,
		ROW_NUMBER() OVER 
			(PARTITION BY sale_month_year ORDER BY nft_monthly_sales_count DESC, 
				name ASC)  
				AS rn  
	FROM
		Monthly_Sales
)

-- Third step/Final SELECT statement in multiple CTE - retrieves only the rows where ranked number (rn) is 1, 
-- effectively selecting the single most sold NFT for each month-year.
SELECT
	sale_month_year,
	name AS NFT_name,
	nft_monthly_sales_count AS sales_count_in_month,
	CONCAT('$', FORMAT(average_monthly_usd_price, 2)) AS price_in_usd 												
FROM 
	Ranked_Monthly_Sales
WHERE
	rn = 1 
ORDER BY 
	sale_month_year ASC; 
```

<br>

<b>More Detailed QUERY with Comments</b>

```
/*Identification of the most sold NFT each month / year combination?
 * What was the name and the price in USD?
 * Order in chronological format
 * Multi-step query use of Commmon Table Expression (CTEs) to identify the most sold NFT for each month and year, 
 * 	along with its average price. 
 * First step is MonthlySales CTE - aggregrates the sales data.
 * Second step is RankedMonthlySales CTE - ranks te NFTs within each sale_month_year based on their nft_monthly_sales_count.
 * Third step/Final SELECT statement - retrieves only the rows where ranked number (rn) is 1, effectively selecting the single most sold NFT for each month-year.
 * %y is year
 * %m is (month)
 * %d is (date)*/

/*Clean the 'day' column to ensure consistent data format*/
WITH Cleaned_Data AS (
	SELECT
	    day,
	    name,
	    usd_price,
	    -- Attempt to convert 'day' using multiple formats, prioritizing your known format
	    CASE  -- Try MM/DD/YY first (your observed format)
	        WHEN STR_TO_DATE(day, '%m/%d/%y') IS NOT NULL THEN STR_TO_DATE(day, '%m/%d/%y') -- Add more WHEN clauses here if you identified other incorrect date formats in your data
	        																				-- For example, if some dates are 'YYYY-MM-DD':
	        WHEN STR_TO_DATE(day, '%Y-%m-%d') IS NOT NULL THEN STR_TO_DATE(day, '%Y-%m-%d') -- If some dates are 'MM-DD-YY':
	        WHEN STR_TO_DATE(day, '%m-%d-%y') IS NOT NULL THEN STR_TO_DATE(day, '%m-%d-%y') -- Handle cases where 'day' might be a full datetime string like 'MM/DD/YY HH:MM:SS'
	        WHEN STR_TO_DATE(SUBSTRING_INDEX(day, ' ', 1), '%m/%d/%y') IS NOT NULL
	             THEN STR_TO_DATE(SUBSTRING_INDEX(day, ' ', 1), '%m/%d/%y')
	        ELSE NULL  -- For any value that still doesn't match, return NULL
	    END AS cleaned_day
	FROM
	   cryptopunkdata
),
    
-- First step in multiple CTE is MonthlySales CTE - aggregrates the sales data.
Monthly_Sales AS (  
	SELECT
		DATE_FORMAT(cleaned_day, '%m/%y') AS sale_month_year, -- Formats the cleaned date into 'YY-MM' for grouping
		name, -- Uses 'name' column for NFT name
		COUNT(*) AS nft_monthly_sales_count,  -- Counts sales for each NFT per month/year
		AVG(usd_price) AS average_monthly_usd_price  -- Calculates average USD price for each NFT per month/year
	FROM
		Cleaned_Data  -- Selecting from the Cleaned_Data CTE
	WHERE 
		cleaned_day IS NOT NULL  -- Exclude rows where data cleaning failed 
	GROUP BY
		sale_month_year, name

),

-- Second step in multiple CTE is RankedMonthlySales CTE - ranks te NFTs within each sale_month_year based on their nft_monthly_sales_count.
Ranked_Monthly_Sales AS (
	SELECT 
		sale_month_year,
		name, 
		nft_monthly_sales_count,
		average_monthly_usd_price,
		ROW_NUMBER() OVER 
			(PARTITION BY sale_month_year ORDER BY nft_monthly_sales_count DESC, -- divides the data into separate groups for each month-year
																				-- ORDER BY ranks NFTs from highest sales count to lowest within each month-year group
				name ASC)  -- arranges NFTs by name alphabetically if two NFTs have the same nft_monthly_sales_count with same month-year
				AS rn  -- columns assigns a unique rank number to each NFT within montly group. The NFT with the highest sales count gets rn = 1
	FROM
		Monthly_Sales
)

-- Third step/Final SELECT statement in multiple CTE - retrieves only the rows where ranked number (rn) is 1, 
-- effectively selecting the single most sold NFT for each month-year.
SELECT
	sale_month_year,
	name AS NFT_name, -- renamed for clarity in output
	nft_monthly_sales_count AS sales_count_in_month,
	CONCAT('$', FORMAT(average_monthly_usd_price, 2)) AS price_in_usd -- Added '$' in front of value for usd_price. 
																	 -- Formated for easier readability. Removing decimals if more than 2 places.												
FROM 
	Ranked_Monthly_Sales
WHERE
	rn = 1 -- Filters to keep only the top-ranked NFT for each month-year
ORDER BY 
	sale_month_year ASC;  -- Ensures the final results are in chronological order by month-year	
```


<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Multiple%20CTE%20Most%20Sold%20NFT%20Each%20Month.png)

<br>

<b>INSIGHT</b> 

This analysis provides powerful insights into NFT market dynamics by first ensuring data quality in timestamps and then systematically identifying trending assets. By highlighting the single most sold NFT each month, it effectively cuts through market noise to reveal which specific CryptoPunks gained significant popularity or experienced heightened trading activity during particular periods. This can help correlate market trends with broader events, community interest, or media attention, offering a clear view of shifting demand for individual assets within the collection over time.

<h1></h1>
  
<h3>10. Calculation of total monthly sales volume</h3>

<h1></h1>

This query
 
<br>

<b>QUERY</b> 

```

```

<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>]()


<br>


<b>INSIGHT</b> 

<h1></h1>
  
<h3>11. Counting transactions for a specific wallet</h3>

<h1></h1>

This query
 
<br>

<b>QUERY</b> 

```

```

<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>]()

<br>

<b>INSIGHT</b> 

<h1></h1>
  
<h3>12. Development of an "estimated average value calculator" to account for outlier sales and provide a more representative daily average price</h3>

<h1></h1>

This query
 
<br>

<b>QUERY</b> 

```

```

<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>]()

<br>

<b>INSIGHT</b> 



<h1></h1>
  
<h3></h3>

<br>

<img src="" widht="450" height="4" alt="">

