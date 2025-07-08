# Cryptopunks-NFT-Analysis-Project

<h2>Table of Contents</h2>

- [<b>Project Overview</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/README.md#project-overview)
- [<b>Skills Demonstrated</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/README.md#skills-demonstrated)
- [<b>Key Analyses Performed</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/README.md#key-analyses-performed)
- [<b>Dataset</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/README.md#dataset)
- [<b>How to Use This Repository</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/README.md#how-to-use-this-repository)
- [<b>Results: CryptoPunks NFT Analysis Report</b>](https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project/blob/main/Results/CryptoPunks%20NFT%20Analysis%20Report.md)

<h1></h1>

<h2>Project Overview</h2>

A NFT (Non-Fungible Token) is a type of digital asset that represents ownership of a unique item or a piece of content on a blockchain. NFTs, as unique digital assets on the blockchain, have rapidly emerged as a prominent technology, with billions of dollars transacted annually. While the long-term future and regulatory landscape of NFTs remain uncertain, the inherent transparency of blockchain technology means all transactions are publicly recorded, providing a rich dataset for analysis.

This project delves into the sales history of CryptoPunks, where each record represents a distinct NFT sale, capturing details such as buyer and seller addresses, transaction prices in ETH and USD, sale dates and times, NFT IDs, transaction hashes, and NFT names.

<h1></h1>

<h2>Skills Demonstrated</h2>

- <b>Data Analysis using SQL:</b> Proficiently querying and manipulating large datasets to extract meaningful insights.
- <b>Aggregation and Summary Functions:</b> Utilizing SQL's powerful aggregation capabilities (e.g., `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`) and window functions to summarize and analyze data effectively.
- <b>Date and Time Functions:</b> Extracting and analyzing trends based on various time granularities (e.g., daily, monthly, day of the week).
- <b>Data Transformation:</b> Creating new derived columns and manipulating existing data for enhanced analysis.
- <b>View Creation:</b> Defining logical views for simplified access to frequently used or derived datasets.
- <b>Subqueries and Joins:</b> Combining data from different perspectives to answer complex analytical questions.

<h1></h1>

<h2>Key Analyses Performed</h2>

This project addresses a series of analytical questions, including:
- Total number of sales within the specified period.
- Identification of the top 5 most expensive transactions by USD price.
- Calculation of a moving average of USD prices to observe price trends.
- Determination of average sale prices for each NFT name.
- Analysis of sales volume and average ETH price by day of the week.
- Construction of a descriptive summary for each transaction.
- Creation of a dedicated view for purchases made by a specific wallet address.
- Comparative analysis of highest and lowest sale prices for each NFT.
- Identification of the most sold NFT each month/year and its associated price.
- Calculation of total monthly sales volume.

<h1></h1>

<h2>Dataset</h2>

- <i>Rows:</i> `19,920`
- <i>Columns:</i> `9`
- <i>File size:</i> `3.9MB`

The dataset used for this analysis comprises real-world CryptoPunks sales data from January 1st, 2018, to December 31st, 2021. The table includes the following columns:

| Column Name      | Description                                     |
| :--------------- | :---------------------------------------------- |
| `buyer_address`  | The blockchain address of the NFT buyer.        |
| `eth_price`      | The price of the NFT sale in Ethereum (ETH).    |
| `usd_price`      | The price of the NFT sale in US Dollars (USD).  |
| `seller_address` | The blockchain address of the NFT seller.       |
| `day`           | The date of the NFT sale.                       |
| `utc_timestamp`           | The time of the NFT sale.                       |
| `token_ID`         | The unique identifier for the CryptoPunk NFT.   |
| `transaction_hash` | The unique hash of the blockchain transaction.  |
| `name`       | The name or specific identifier of the NFT (e.g., "CryptoPunk #1234"). |

<h1></h1>
  
<h2>How to Use This Repository</h2>

This repository contains SQL scripts that can be executed against a database containing the CryptoPunks sales data. Each script corresponds to a specific analytical question or task outlined above.
- <b>1. Clone the repository:</b>
  ```bash
  git clone https://github.com/LashawnFofung/Cryptopunks-NFT-Analysis-Project.git
  ```
- <b>2. Set up your database:</b> Ensure you have a SQL database (e.g., PostgreSQL, MySQL, SQL Server) configured and the CryptoPunks sales data loaded into a table with the specified schema.
- <b>3. Execute SQL scripts:</b> Run the SQL files provided in the repository against your database to replicate the analyses.

Feel free to explore the SQL queries and adapt them for further analysis or different datasets.
