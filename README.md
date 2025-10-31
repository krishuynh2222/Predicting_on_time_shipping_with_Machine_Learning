# Predicting on-time shipping with Machine Learning

## Introduction 
The rapid acceleration of the e-commerce sector has made on-time package delivery the single most important determinant of customer loyalty and logistical success. Consequently, logistics networks are under immense pressure to achieve high service reliability. Predicting the timeliness of a shipment is a highly dimensional challenge influenced by dynamic variables such as traffic, weather, area, route distance, and the performance history of the delivery agent.

To address this problem, this project utilizes a hybrid machine learning approach to provide actionable foresight into these operations. I deploy two supervised classification models, Logistic Regression and Support Vector Machine (SVM), trained on Amazon's historical delivery data to accurately predict delivery performance. Crucially, this predictive capability is paired with an unsupervised technique, K-Means clustering coupled with Principal Component Analysis (PCA), to identify and segment operational patterns. This combined methodology transforms raw data into a powerful tool for strategic resource allocation and continuous efficiency improvement.

## Methodology 
The initial dataset contained 43,739 records and 16 attributes related to delivery operations, including agent demographics, location coordinates, weather, traffic, and delivery times. During the data cleaning phase, missing values in numerical attributes were imputed using the median, while categorical attributes were filled using the mode to preserve data consistency. All duplicate rows were identified and removed to prevent redundancy in the analysis. 

The Haversine formula was applied to compute the distance between store and drop locations, creating a new feature (Distance_km). Categorical variables (e.g, Weather, Traffic, Area, Vehicle, Category) were encoded using One-Hot Encoding. Numerical variables (Agent Age, Agent Rating, Distance) were standardized using StandardScaler. 

#### Statistical Summary
A statistical overview revealed that the median delivery time was 125 minutes, consistent with the threshold for defining on-time performance. 

<img width="530" height="361" alt="Screenshot 2025-10-31 at 12 29 54 PM" src="https://github.com/user-attachments/assets/8a7b0a53-3325-417e-b5f0-65ea63be080b" />

#### Model Selection 
The two supervised models proved effective in predicting on-time delivery. The SVM model's marginally superior performance, combined with the detailed insights from the clustering analysis, provides a comprehensive view of delivery dynamics.

| Model               | Accuracy | Precision | Recall | F1-Score | AUC   |
|--------------------|---------|-----------|--------|----------|-------|
| Logistic Regression | 0.79    | 0.79      | 0.79   | 0.79     | 0.883 |
| SVM                 | 0.80    | 0.80      | 0.80   | 0.80     | 0.883 |

Both supervised models achieved strong overall accuracy, demonstrating strong predictive capability. The clustering analysis provided descriptive insights into delivery dynamics, supporting performance segmentation and strategic resource allocation.

#### Cluster Analysis (K-Means Clustering)

| Cluster | Delivery_Time (min) | Distance (km) | Agent_Rating | Agent_Age |
|--------|------------------|---------------|-------------|-----------|
| 0      | 191.51           | 15.18         | 4.70        | 31.98     |
| 1      | 72.89            | 6.02          | 4.72        | 26.88     |
| 2      | 174.85           | 10.73         | 4.65        | 31.80     |
| 3      | 124.01           | 10.34         | 4.76        | 29.96     |

The clustering results reveal four distinct delivery segments:
- **Cluster 1 (Fastest/Youngest):** Characterized by the shortest delivery time (~ 73 min) and shortest average distance; contains the youngest agents. This represents optimal performance.
- **Cluster 0 (Slowest/Longest Distance):** Defined by the longest average delivery time (~ 92 min) and longest average distance; tends to have older agents. This represents high-risk, delayed deliveries.
- **Cluster 3 (On-Time/High Rated):** Delivery time is near the median (~ 125 min) and contains the highest rated agents. Performance is reliable and on schedule.
- **Cluster 2 (Intermediate Delay):** Slower than cluster 3 but significantly faster than cluster 0; moderate distance. This represents a potential operational bottleneck where delays are moderate.

# Conclusion and future works
This study successfully applied Logistic Regression, SVM, and K-Means Clustering with PCA to analyze and predict shipment delivery performance. The SVM model achieved the best predictive accuracy ($80.0\%$) and equal AUC ($0.883$), confirming its robustness for classification tasks. K-Means Clustering provided complementary insights by revealing four distinct delivery patterns, helping to identify groups of agents or deliveries requiring strategic focus.

For future work, three main areas are recommended to enhance the model's practical utility:
- **Real-Time Data Integration:** Incorporate real-time data such as live traffic and weather APIs for dynamic predictions that adapt to constantly changing conditions.
- **Advanced Algorithms:** Apply more advanced ensemble algorithms such as Random Forest or XGBoost, or deep learning models like Neural Networks, to potentially enhance accuracy and capture more complex non-linear relationships.
- **Deployment:** Develop an interactive dashboard to monitor on-time delivery rates and cluster patterns in real time, allowing logistics managers to make immediate operational decisions.



