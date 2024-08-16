<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
</head>
<body>

<h1>Customer Segmentation for Airlines using K-Means Clustering Models</h1>

<p>This project aims to create a segmentation for customers in an airline company based on their spending and the frequency of their flights. The goal is to develop a more personalized approach, create effective marketing campaigns, and improve airline services.</p>

<h2>Data</h2>
<p>The dataset consists of 62,988 entries and 22 columns:</p>
<ul>
    <li><strong>FFP_DATE</strong></li>
    <li><strong>FIRST_FLIGHT_DATE</strong></li>
    <li><strong>GENDER</strong></li>
    <li><strong>FFP_TIER</strong></li>
    <li><strong>WORK_CITY</strong></li>
    <li><strong>WORK_PROVINCE</strong></li>
    <li><strong>WORK_COUNTRY</strong></li>
    <li><strong>AGE</strong></li>
    <li><strong>LOAD_TIME</strong></li>
    <li><strong>FLIGHT_COUNT</strong></li>
    <li><strong>BP_SUM</strong></li>
    <li><strong>SUM_YR_1</strong></li>
    <li><strong>SUM_YR_2</strong></li>
    <li><strong>SEG_KM_SUM</strong></li>
    <li><strong>LAST_FLIGHT_DATE</strong></li>
    <li><strong>LAST_TO_END</strong></li>
    <li><strong>AVG_INTERVAL</strong></li>
    <li><strong>MAX_INTERVAL</strong></li>
    <li><strong>EXCHANGE_COUNT</strong></li>
    <li><strong>avg_discount</strong></li>
    <li><strong>Points_Sum</strong></li>
    <li><strong>Point_NotFlight</strong></li>
</ul>

<h3>Key Data Insights</h3>
<ul>
    <li><strong>AGE:</strong> The average customer age is 44.7 years, with most customers between 38 and 50 years old.</li>
    <li><strong>FLIGHT_COUNT:</strong> Customers have flown an average of 39.9 flights, with a wide range (3 to 213 flights).</li>
    <li><strong>BP_SUM (Travel Plan):</strong> Customers have an average travel plan of 44,771.65, with significant variability (13,956 to 505,308).</li>
    <li><strong>SUM_YR_1 (Yearly Spending 1):</strong> Average spending in the first year is 20,162.50, ranging from 0 to 239,560.</li>
    <li><strong>SUM_YR_2 (Yearly Spending 2):</strong> Average spending in the second year is 22,459.85, with a range similar to the first year (0 to 234,188).</li>
    <li><strong>SEG_KM_SUM (Total Kilometers Flown):</strong> Customers have flown an average of 62,257.70 kilometers, with a broad range (19,422 to 580,717 km).</li>
    <li><strong>LAST_TO_END (Days Since Last Flight):</strong> The average number of days since the last flight is 41.20, with high variability (1 to 667 days).</li>
    <li><strong>AVG_INTERVAL (Average Interval Between Flights):</strong> The average interval between flights is 22.42 days, ranging from 2 to 296.5 days.</li>
    <li><strong>MAX_INTERVAL (Maximum Interval Between Flights):</strong> The longest interval between flights averages 107.24 days, with a wide range (6 to 572 days).</li>
    <li><strong>EXCHANGE_COUNT:</strong> The average number of exchanges is 1.62, ranging from 0 to 46.</li>
    <li><strong>avg_discount:</strong> The average discount received is 0.82, with most discounts between 0.70 and 0.86.</li>
    <li><strong>Points_Sum:</strong> The total points earned average 51,180.18, with a wide range (13,956 to 795,398 points).</li>
    <li><strong>Point_NotFlight:</strong> Non-flight points average 6.95, with a range of 0 to 140 points.</li>
</ul>

<h2>Notebook Contents</h2>
<ol>
    <li>Data Processing</li>
    <li>Exploratory Data Analysis (EDA)
        <ul>
            <li>Summary Statistics for Numerical Variables</li>
            <li>Summary Statistics for Categorical and Date Variables</li>
            <li>Univariate Analysis: Numeric Data</li>
            <li>Univariate Analysis: Categorical Data</li>
            <li>Bivariate Analysis</li>
            <li>Multivariate Analysis</li>
        </ul>
    </li>
    <li>Data Preprocessing</li>
    <li>Feature Engineering
        <ul>
            <li><strong>RFM Features</strong>
                <ul>
                    <li><strong>Recency (R):</strong> Indicates how recently a customer has made a purchase. A lower recency value means the customer has purchased more recently, indicating higher engagement with the brand.</li>
                    <li><strong>Frequency (F):</strong> Signifies how often a customer makes a purchase within a certain period. A higher frequency value indicates a customer who interacts with the business more often, suggesting higher loyalty or satisfaction.</li>
                    <li><strong>Monetary (M):</strong> Represents the total amount of money a customer has spent over a certain period. Customers with higher monetary values have contributed more to the business, indicating their potential high lifetime value.</li>
                </ul>
            </li>
        </ul>
        <p>Mapping the provided features to the RFM model:</p>
        <ul>
            <li><strong>Recency:</strong> <em>LAST_TO_END:</em> Represents the number of days since the customer's last flight. A lower number indicates more recent activity, which is crucial for recency analysis.</li>
            <li><strong>Frequency:</strong> <em>FLIGHT_COUNT:</em> Indicates how many flights the customer has taken. Higher values represent more frequent engagement with the airline.</li>
            <li><strong>Monetary:</strong> <em>SUM_YR_1 and SUM_YR_2:</em> These represent the customer's spending in two different years. Combining these gives a good estimate of the total monetary value of each customer.</li>
        </ul>
    </li>
    <li>Handling Outliers</li>
    <li>Modeling: K-Means Clustering
        <ul>
            <li>Cluster Tuning</li>
            <li>Cluster Visualization</li>
            <li>Insight - Analysis Clustering</li>
            <ul>
                <li><strong>High-value Customers (Cluster 0):</strong> More engaged, fly more frequently, have flown more recently, and spend more, making them highly valuable to the airline.</li>
                <li><strong>Low-value Customers (Cluster 1):</strong> Less engaged, fly less frequently, have not flown as recently, and spend less, making them less valuable compared to Cluster 0.</li>
            </ul>
            <li><strong>Cluster Characteristics</strong>
                <ul>
                    <li><strong>Cluster 0:</strong>
                        <ul>
                            <li>Recency: Lower recency score (1.43), indicating they have flown more recently compared to Cluster 1.</li>
                            <li>Frequency: Higher flight frequency (mean of 1.28), indicating more frequent engagement.</li>
                            <li>Monetary: Higher average spending (4.20), making them more valuable customers.</li>
                        </ul>
                    </li>
                    <li><strong>Cluster 1:</strong>
                        <ul>
                            <li>Recency: Higher recency score (2.25), indicating they have not flown as recently as customers in Cluster 0.</li>
                            <li>Frequency: Lower flight frequency (mean of 0.70), indicating less frequent engagement.</li>
                            <li>Monetary: Lower average spending (3.49), making them less valuable compared to Cluster 0.</li>
                        </ul>
                    </li>
                </ul>
            </li>
        </ul>
    </li>
</ol>

</body>
</html>
