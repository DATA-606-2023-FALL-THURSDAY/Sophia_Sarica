
- **Sophia Sarica, Fall 2023**


# SL-RAT Score Degradation Rate Prediction Project

Prepared for the UMBC Data Science Master's Degree Capstone


## Resources and Links
- **Author's GitHub Repository:** [DATA-606-2023-FALL-THURSDAY/Sarica_Sophia](https://github.com/DATA-606-2023-FALL-THURSDAY/Sarica_Sophia/tree/main)
- **Author's LinkedIn Profile:** [Sophia Sarica on LinkedIn](https://www.linkedin.com/in/sophiasarica/)
- **PowerPoint Presentation:** [Google Drive Link](https://docs.google.com/presentation/d/1dSqiAfP1anTtzu7SzB0HDjxOEkOUnNh4/edit?usp=drive_link&ouid=114108728469769953895&rtpof=true&sd=true)
- **YouTube Video:** _(Placeholder for YouTube video link)_


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

## Distribution of Numerical Features


![Distribution of PIPE_SIZE](Screen%20Shot%202023-11-29%20at%2010.41.04%20PM.png)

![Distribution of UPSTREAM_I](Screen%20Shot%202023-11-29%20at%2010.41.22%20PM.png)


- **Pipe Sizes**: Most of the pipe sizes center around 8 units.
- **Slopes**: Most slopes are less than 5, with a few exceptions.
- **Length Distribution**: The distribution appears fairly uniform, with a slight skew towards shorter lengths.
- **Feature 1**: The distribution is slightly left-skewed, with most values around 300 to 400.
- **Feature 2 (UPSTREAM_I)**: Similar to UPSTREAM_I, most values are around 300 to 400.
- **Installation Periods**: The distribution shows multiple peaks, indicating that installations occurred in different periods.

### Correlation Matrix


![Correlation Matrix](Screen%20Shot%202023-11-29%20at%2010.27.05%20PM.png)

- **General Observation**: None of the numerical features have a strong correlation with each other.
- **Specific Correlation**: The highest correlation is between `UPSTREAM_I` and `DOWNSTREAM` with a value of 0.96, which is expected as they are related parameters.

### Distribution of the Target Variable


![Distribution of Target Variable](Screen%20Shot%202023-11-29%20at%2010.27.17%20PM.png)


- **Imbalance in Target Variable**: The target variable shows some imbalance with more instances of class 1 compared to class 0.
- **Model Training Consideration**: This imbalance will need to be accounted for in the model training phase.
