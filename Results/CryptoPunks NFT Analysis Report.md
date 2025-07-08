# Results & Queries: CryptoPunk NFT Analysis Project


## TABLE OF CONTENTS (QUESTIONS): 

- [1. Total number of sales within the dataset (January 2018 to December 2021)](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/CryptoPunks%20NFT%20Analysis%20Report.md#1-total-number-of-sales-within-dataset-january-2018-to-december-2021)
  
- [2. Identification of the top 5 most expensive transactions by USD price.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/CryptoPunks%20NFT%20Analysis%20Report.md#2-identification-of-the-top-5-most-expensive-transactions-by-usd-price)

- [3. Calculation of a moving average of USD prices to observe price trends.](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/CryptoPunks%20NFT%20Analysis%20Report.md#3-calculation-of-a-moving-average-of-usd-prices-to-observe-price-trends)

- [4. Determination of average sale prices for each NFT name.]()

- [5. Analysis of sales volume, average ETH price, and USD price by day of the week.]()

- [6. Construction of a descriptive summary for each transaction.]()

- [7. Creation of a dedicated view for purchases made by a specific wallet address.]()

- [8. Comparative analysis of highest and lowest sale prices for each NFT.]()

- [9. Identification of the most sold NFT each month/year and its associated price.]()

- [10. Calculation of total monthly sales volume.]()


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

This foundational metric reveals <b>$19,920 total NFT sales</b>, highlighting the active and extensive scale of the CryptoPunks market within the dataset and providing a crucial baseline for further analysis.

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

The analysis of the top transactions immediately reveals the immense value potential within the CryptoPunks market, showcasing extraordinary outliers. Led by <b>CryptoPunk #5822</b> at a staggering <b>$23.7 million USD</b>, these top sales underscore the highly speculative and collectable nature of these NFTs. Even beyond the absolute peak, transactions like <b>CryptoPunk #5577</b> at <b>$7.82 million USD</b> and <b>CryptoPunk #3100</b> at <b>$7.58 million USD</b> demonstrate a multi-million dollar tier of highly sought-after assets. These extreme valuations indicate deep market demand, perceived rarity, and the significant role of historical context or unique traits in driving prices for specific CryptoPunks. Identifying these transactions is crucial for understanding the market's upper echelons, key value drivers, and the potential for rapid price appreciation.

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

This analysis, utilizing a 50-transaction simple moving average, effectively smooths out the inherent volatility of individual NFT sales to highlight underlying price trends in the CryptoPunks market. As observed in the provided results, the `moving_average_usd_price` for the depicted period (January 2022) generally hovers around the $200,000 USD mark. This consistency in the moving average suggests a period of relative stability in the average valuation of CryptoPunks based on recent transaction activity, offering a clearer signal of immediate market sentiment and potential price trajectory than isolated high or low sales.

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

This analysis provides a crucial long-term valuation perspective by calculating the average USD sale price for each individual CryptoPunk (`name`). As revealed by the results, certain CryptoPunks consistently command exceptionally high average prices, with `CryptoPunk #7078` leading at over $2.8 million USD, and several others frequently exceeding the $2 million mark. This substantial difference in average valuation highlights that perceived rarity, unique traits, or historical significance translate into sustained higher market demand and pricing for specific NFTs within the collection, offering vital insights into what attributes drive consistent value over time.

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

This analysis segmenting sales activity by the day of the week offers valuable insights into the CryptoPunks market's cyclical behavior. The results indicate a discernible pattern in trading volume: 

	<b>Sundays consistently exhibit the lowest number of sales (2,490 transactions), with activity progressively increasing throughout the week to peak on Thursdays (3,156 transactions).</b> 
 
Despite this notable variation in daily transaction volume, <b>the average ETH and USD prices for CryptoPunks remain remarkably stable across all days</b>, fluctuating within a tight range (e.g., average USD price holds consistently around $173,000 to $183,000). This suggests that while market participants may prefer to engage more actively mid-week, these daily volume shifts do not significantly impact the underlying average valuation of CryptoPunks, pointing to a relatively stable pricing baseline regardless of daily transaction intensity.

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

This query calculates the total sales volume in USD for each month and year, rounding the sum to the nearest hundred dollars.
 
<br>

<b>QUERY</b> 

```
/*Calculation of total montly sales volume*/
SELECT
	DATE_FORMAT(day,'%Y-%M') AS month_year,
	ROUND(SUM(usd_price), -2) AS total_monthly_volume_rounded_hundreds
FROM 
	cryptopunkdata
GROUP BY 
	month_year 
ORDER BY 
	month_year ASC;
```

<br>

<b>RESULTS</b>

View query results: [<b>HERE</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Images/Calculation%20of%20Total%20Volume.png)

<br>

<b>INSIGHT</b> 

This provides a macroscopic view of market activity, showing how much money was transacted in the CryptoPunks market on a monthly basis. Trends in total volume can indicate periods of market boom or bust, overall investor interest, and liquidity within the collection over time.

<h1></h1>
  
