<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
</head>
<body>

<h1>Customer Segmentation for Airlines using K-Means Clustering Models</h1>

<p>This project aims to create a segmentation for customers in an airline company based on their spending and the frequency of their flights. The goal is to develop a more personalized approach, create effective marketing campaigns, and improve airline services.</p>
<a href="https://github.com/jvontama96/AirlinesCustomerClustering_RFM_KMeans/blob/main/Customer_Airlines_Clustering_KMeans_RFM.ipynb">Full Project Documentation</a></p>
<h2>Data Understanding</h2>
<p>The dataset consists of 62,988 entries and 22 columns, which include:</p>

<h3><strong>Categorical Features:</strong></h3>
<ul>
    <li><strong>FFP_DATE</strong></li>
    <li><strong>FIRST_FLIGHT_DATE</strong></li>
    <li><strong>GENDER</strong></li>
    <li><strong>FFP_TIER</strong></li>
    <li><strong>WORK_CITY</strong></li>
    <li><strong>WORK_PROVINCE</strong></li>
    <li><strong>WORK_COUNTRY</strong></li>
    <li><strong>LOAD_TIME</strong></li>
    <li><strong>LAST_FLIGHT_DATE</strong></li>
</ul>

<h3><strong>Numerical Features and Statistical Insights:</strong></h3>
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

<h2>Project Pipeline</h2>
<ol>
    <li> <a href="https://github.com/jvontama96/AirlinesCustomerClustering_RFM_KMeans/tree/main/Exploratory%20Data%20Analysis">Exploratory Data Analysis (EDA) (Click to access the directory)</a>
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
    <li>Handling Outliers of RFM Feature</li>
    <li><a href="https://github.com/jvontama96/AirlinesCustomerClustering_RFM_KMeans/tree/main/Flight_Tuning_and_ClusterResult">Modeling K-Means Clustering:</a></li>
        <ul>
            <li>Cluster Tuning: Elbow and Silhouette Method</li>
            <img src="https://github.com/jvontama96/AirlinesCustomerClustering_RFM_KMeans/blob/main/Flight_Tuning_and_ClusterResult/flight_tuning_elbow.png?raw=true" alt="elbow" style="width:50%; max-width:400px;">
           <p> we observe that the suggested optimal k value is 6. However, we don't have a very distinct elbow point in this case, to choose the best k within this range, we can employ the silhouette analysis, another cluster quality evaluation method.</p>
            <img src="https://github.com/jvontama96/AirlinesCustomerClustering_RFM_KMeans/blob/main/Flight_Tuning_and_ClusterResult/flight_tuning_silhouette.png?raw=true" alt="silhouette" style="width:50%; max-width:400px;">
           <p>Based on above guidelines and after carefully considering the silhouette plots, it's clear that choosing ( k = 2) is the better option. This choice gives us clusters that are more evenly matched and well-defined, making our clustering solution stronger and more reliable.</p>
            <li>Cluster Visualization and Distribution</li>
            <img src="https://github.com/jvontama96/AirlinesCustomerClustering_RFM_KMeans/blob/main/Flight_Tuning_and_ClusterResult/flight_cluster_result.png?raw=true" alt="cluster" style="width:50%; max-width:400px;">
             <img src="https://github.com/jvontama96/AirlinesCustomerClustering_RFM_KMeans/blob/main/Flight_Tuning_and_ClusterResult/flight_cluster_distribution.png?raw=true" alt="cluster" style="width:50%; max-width:400px;">
            <table border="1">
    <thead>
        <tr>
            <th>Cluster</th>
            <th>R_mean</th>
            <th>R_median</th>
            <th>F_mean</th>
            <th>F_median</th>
            <th>M_mean</th>
            <th>M_median</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>0</td>
            <td>1.432229</td>
            <td>1.447158</td>
            <td>1.283357</td>
            <td>1.255273</td>
            <td>4.202056</td>
            <td>4.175323</td>
        </tr>
        <tr>
            <td>1</td>
            <td>2.246072</td>
            <td>2.322219</td>
            <td>0.703111</td>
            <td>0.698970</td>
            <td>3.487693</td>
            <td>3.506776</td>
        </tr>
    </tbody>
</table>
            <li>Cluster Analysis </li>
            <ul>
                <li><strong>High-value Customers (Cluster 0):</strong> More engaged, fly more frequently, have flown more recently, and spend more, making them highly valuable to the airline.</li>
                <li><strong>Low-value Customers (Cluster 1):</strong> Less engaged, fly less frequently, have not flown as recently, and spend less, making them less valuable compared to Cluster 0.</li>
            </ul>
            <li><strong>Cluster Characteristics</strong></li>
                <img src="https://github.com/jvontama96/AirlinesCustomerClustering_RFM_KMeans/blob/main/Flight_Tuning_and_ClusterResult/cluster_characteristic.png?raw=true" alt="cluster" style="width:50%; max-width:400px;">
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
<h2>Business Recommendations and Actions</h2>

<h3>Cluster 0: High-Value Customers</h3>
<ol>
    <li>
        <strong>Enhance Loyalty and Retention:</strong> 
        Offer premium loyalty programs, such as tier upgrades, early boarding, or bonus miles, to reward their frequent engagement and encourage continued spending.
    </li>
    <li>
        <strong>Personalized Offers:</strong> 
        Provide personalized travel packages or exclusive promotions based on their preferences to further enhance their customer experience.
    </li>
    <li>
        <strong>Upsell and Cross-Sell:</strong> 
        Introduce value-added services, such as travel insurance, lounge access, or hotel partnerships, to maximize revenue from these high-value customers.
    </li>
</ol>

<h3>Cluster 1: Low-Value Customers</h3>
<ol>
    <li>
        <strong>Targeted Reactivation Campaigns:</strong> 
        Send tailored promotions, such as discounted fares or loyalty program enrollment incentives, to encourage these customers to fly more frequently.
    </li>
    <li>
        <strong>Engage Through Personalized Communication:</strong> 
        Use data-driven insights to provide relevant travel suggestions, destination guides, or offers to re-engage them with the airline.
    </li>
    <li>
        <strong>Improve Accessibility:</strong> 
        Address potential barriers, such as cost or scheduling, by offering flexible booking options or affordable travel packages to boost their participation.
    </li>
</ol>
</body>
</html>
