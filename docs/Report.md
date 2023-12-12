
- **Sophia Sarica, Fall 2023**


# SL-RAT Score Degradation Rate Prediction Project

Prepared for the UMBC Data Science Master's Degree Capstone


## Resources and Links
- **Author's GitHub Repository:** [DATA-606-2023-FALL-THURSDAY/Sarica_Sophia](https://github.com/DATA-606-2023-FALL-THURSDAY/Sarica_Sophia/tree/main)
- **Author's LinkedIn Profile:** [Sophia Sarica on LinkedIn](https://www.linkedin.com/in/sophiasarica/)
- **PowerPoint Presentation:** [Google Drive Link](https://docs.google.com/presentation/d/1dSqiAfP1anTtzu7SzB0HDjxOEkOUnNh4/edit?usp=drive_link&ouid=114108728469769953895&rtpof=true&sd=true)
- **PowerPoint Presentation/Recording:** [Google Drive Link](https://docs.google.com/presentation/d/1DeDVeLofCdsgJRr18nxUeLW_5GKbDpdX/edit?usp=drive_link)



## Background

The Sewer Line Rapid Assessment Tool (SL-RAT) represents a pivotal advancement in wastewater management, harnessing cutting-edge acoustic technology to offer real-time assessments of sewer line blockages. This innovation empowers collection system operators to make informed decisions regarding the allocation of cleaning efforts, a critical element in ensuring the seamless operation of sewer systems. The integration of SL-RAT technology holds immense significance, allowing operators to focus their resources precisely where and when needed most, thereby conserving time, water, and financial resources. The tool's ability to generate scores ranging from 0 to 10 following its application to a pipe is a game-changer. A score within the 0-3 range is a vital indicator of immediate blockage, demanding urgent attention. This project explores the potential of determining degradation rates and SL-RAT scores to revolutionize the efficiency of sewer preventive maintenance operations, ultimately benefitting system owners by optimizing their financial, staff, and equipment resources for a more sustainable and cost-effective approach to sewer system management.


## Description of Data Sources 

This dataset combines critical data from two distinct sources: The Sewer System Workorder database and the Geographic Information System (GIS) database. The dataset dimensions are as follows: The GIS table comprises approximately 4.8+ MB of data with dimensions of 62728x8, while the Sewer System Workorder table contains about 7.5+ MB of data with dimensions of 33807x22.

### Sewer System Workorder Database Table Columns:
- **FACILITYID (object):** A unique identifier representing individual segments between two manholes in the sewer system.
- **WORKORDERID (int64):** Unique Workorder Number for each assesments for the asset.
- **DESCRIPTION (OBJECT):** The description is structured in a way to indicate the nature of the work such as inspection, maintenance, repair etc. 
- **COMPLETED_DATE (datetime64[ns]):** Indicates the date of completion for the activity.
- **SLRAT_SCORE (float64):** The pivotal SL-RAT score, a numeric value ranging from 0 to 10, signifying the condition of the sewer line.

### GIS Table Database Table Columns:
- **FACILITYID (object):** A unique identifier representing individual segments between two manholes in the sewer system.
- **TYPE (object):** Describes the type of pipe associated with the facility.
- **LINING_TYP (object):** Represents the type of pipe connections used.
- **PIPE_SIZE (float64):** Specifies the size of the pipe.
- **PIPE_MATER (object):** Identifies the material composition of the pipe.
- **SLOPE (float64):** Records the pipe slope associated with each FacilityID.
- **LENGTH (float64):** Denotes the length of the pipe segment.
- **INSTALL_DATE:** Reflects the time elapsed since the installation date.



## Exploratory Data Analysis (EDA) - Key Observations and Interpretations

### Distribution of Numerical Features


![Distribution of PIPE_SIZE](Screen%20Shot%202023-11-29%20at%2010.41.04%20PM.png)

![Distribution of UPSTREAM_I](Screen%20Shot%202023-11-29%20at%2010.41.22%20PM.png)


- **Pipe Sizes**: Most of the pipe sizes center around 8 units.
- **Slopes**: Most slopes are less than 5, with a few exceptions.
- **Length Distribution**: The distribution appears fairly uniform, with a slight skew towards shorter lengths.
- **Feature 1**: The distribution is slightly left-skewed, with most values around 300 to 400.
- **Feature 2 (UPSTREAM_I)**: Similar to UPSTREAM_I, most values are around 300 to 400.
- **Installation Periods**: The distribution shows multiple peaks, indicating that installations occurred in different periods.

### Correlation Matrix


![Correlation Matrix](Screen%20Shot%202023-12-12%20at%202.30.30%20PM.png)

- **General Observation**: None of the numerical features have a strong correlation with each other.
- **Specific Correlation**: The highest correlation is between `UPSTREAM_I` and `DOWNSTREAM` with a value of 0.96, which is expected as they are related parameters.

### Distribution of the Target Variable


![Distribution of Target Variable](Screen%20Shot%202023-11-29%20at%2010.27.17%20PM.png)


- **Imbalance in Target Variable**: The target variable shows some imbalance with more instances of class 1 compared to class 0.
- **Model Training Consideration**: This imbalance will need to be accounted for in the model training phase.


## Model Evaluation Summary

### Random Forest Classifier Performance Without Oversampling

The application of the RandomForestClassifier on the dataset without handling the imbalanced target data yielded the following baseline performance metrics:

| Metric     | Score (%) |
|------------|-----------|
| Accuracy   | 73.68     |
| Precision  | 71.58     |
| Recall     | 73.68     |
| F1 Score   | 69.63     |

These results indicate a moderate level of effectiveness for the Random Forest Classifier under these conditions, highlighting potential areas for improvement in balancing the model's precision and recall.

### Enhanced Random Forest Classifier Performance After Data Preprocessing

Data preprocessing steps such as encoding categorical variables, scaling features, and addressing imbalanced target data have led to the following improved performance metrics:

#### Class-wise Performance:

| Class   | Precision | Recall  | F1-Score | Support  |
|---------|-----------|---------|----------|----------|
| Class 0 | 84.83%    | 88.17%  | 86.47%   | 279      |
| Class 1 | 86.90%    | 83.27%  | 85.05%   | 263      |

#### Overall Performance:

| Metric       | Score   | 
|--------------|---------|
| Accuracy     | 85.79%  | 
| Macro Avg    | 85.87%  | 
| Weighted Avg | 85.84%  | 

These results demonstrate significant improvements in the model's performance across all metrics, indicating the effectiveness of the preprocessing steps in enhancing model accuracy and balance between precision and recall.

### Random Forest Model Performance: Grid Search Optimization vs. Default Parameters

After conducting a GridSearch to optimize the Random Forest model, observing slightly improvements in performance metrics compared to the model with default parameters. Below is the comparison:

#### Model Configuration Comparison:

| Metric                 | Configuration 1 (Optimized with Grid Search) | Configuration 2 (Default Parameters) |
|------------------------|----------------------------------------------|--------------------------------------|
| Accuracy               | 86.90%                                       | 85.79%                               |
| Precision - Class 0    | 85.86%                                       | 84.83%                               |
| Precision - Class 1    | 88.10%                                       | 86.90%                               |
| Recall - Class 0       | 89.25%                                       | 88.17%                               |
| Recall - Class 1       | 84.41%                                       | 83.27%                               |
| F1-Score - Class 0     | 87.52%                                       | 86.47%                               |
| F1-Score - Class 1     | 86.21%                                       | 85.05%                               |
| Macro Avg Precision    | 86.98%                                       | 85.87%                               |
| Macro Avg Recall       | 86.83%                                       | 85.72%                               |
| Macro Avg F1-Score     | 86.87%                                       | 85.76%                               |
| Weighted Avg Precision | 86.95%                                       | 85.84%                               |
| Weighted Avg Recall    | 86.90%                                       | 85.79%                               |
| Weighted Avg F1-Score  | 86.87%                                       | 85.79%                               |

Configuration 1 represents the model with hyperparameters optimized using GridSearch, whereas Configuration 2 runs with the algorithm's default parameters. 

#### Analysis:

- **Accuracy:** Configuration 1 achieves a higher accuracy of 86.90%, compared to Configuration 2's 85.79%.
- **Precision:** Both classes show improved precision in Configuration 1, with Class 0 at 85.86% and Class 1 at 88.10%.
- **Recall:** Configuration 1 exhibits a higher recall for Class 0 (89.25%), but a slightly lower recall for Class 1 (84.41%) compared to Configuration 2.
- **F1-Score:** Configuration 1 leads in F1-Scores for both classes, indicating a better balance between precision and recall.



## ROC Curve Evaluation Comparison

The ROC curves for the Naive Bayes and Random Forest models are depicted below, illustrating the performance of each model in terms of the trade-off between the True Positive Rate and False Positive Rate.

### Naive Bayes Model
![ROC Curve - Naive Bayes](Screen%20Shot%202023-11-29%20at%2010.59.06%20PM.png)
*The AUC (Area Under the Curve) for the Naive Bayes model is 0.66, indicating a fair level of predictive ability.*

### Random Forest Model
![ROC Curve - Random Forest](Screen%20Shot%202023-11-29%20at%2010.58.54%20PM.png)
*The AUC for the Random Forest model is 0.94, signifying a high level of predictive ability.*

Comparatively, the Random Forest model demonstrates a significantly better performance with a higher AUC value, indicating a more accurate model for classification.


## Conclusion

The RandomForest model has shown impressive results in infrastructure management, especially for sewer systems. With careful fine-tuning and calibration to handle class imbalances, the model delivers high predictive accuracy. This accuracy is key for improving maintenance and extending the lifespan of sewer infrastructure. By spotting potential system failures ahead of time, the RandomForest model can be a powerful tool for maintaining consistent and dependable service. Using it can boost operational efficiency and contribute significantly to the sustainability and smooth operation of vital community infrastructure.