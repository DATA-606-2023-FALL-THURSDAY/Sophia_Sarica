# SL-RAT Score Degradation Rate Predicton  Project
*September 03, 2023*


## Title and Author

- SL-RAT Score Degradation Rate Prediction Project

- Prepared for UMBC Data Science Master Degree Capstone by: Dr. Chaojie (Jay) Wang
- Sophia Sarica
- [Author's  GitHub Repository](https://github.com/DATA-606-2023-FALL-THURSDAY/Sarica_Sophia/tree/main)
- [Author's LinkedIn Profile](https://www.linkedin.com/in/sophiasarica/)
- Link to your PowerPoint presentation file
- Link to your YouTube video







## Background

The Sewer Line Rapid Assessment Tool (SL-RAT) represents a pivotal advancement in wastewater management, harnessing cutting-edge acoustic technology to offer real-time assessments of sewer line blockages. This innovation empowers collection system operators to make informed decisions regarding the allocation of cleaning efforts, a critical element in ensuring the seamless operation of sewer systems. The integration of SL-RAT technology holds immense significance, allowing operators to focus their resources precisely where and when needed most, thereby conserving time, water, and financial resources. The tool's ability to generate scores ranging from 0 to 10 following its application to a pipe is a game-changer. A score within the 0-3 range is a vital indicator of immediate blockage, demanding urgent attention. This project explores the potential of determining degradation rates and SL-RAT scores to revolutionize the efficiency of sewer preventive maintenance operations, ultimately benefitting system owners by optimizing their financial, staff, and equipment resources for a more sustainable and cost-effective approach to sewer system management.

## Data: Sewer System SL-RAT Scores and GIS Attributes

This dataset amalgamates critical data from two distinct sources: the Sewer System Workorder database and the Geographic Information System (GIS) database. The aim is to create a comprehensive dataset for analyzing SL-RAT scores within the sewer system, utilizing GIS attributes for enriched context. The dataset dimensions are as follows: the GIS table comprises approximately 4.8+ MB of data with dimensions of 62728x8, while the Workorder table contains about 7.5+ MB of data with dimensions of 33807x22.

### Workorder Table Columns:
- **FACILITYID (object):** A unique identifier representing individual segments between two manholes in the sewer system.
- **COMPLETED_DATE (datetime64[ns]):** Indicates the date of completion for the activity.
- **SLRAT_SCORE (float64):** The pivotal SL-RAT score, a numeric value ranging from 0 to 10, signifying the condition of the sewer line.


### GIS Table:
The FACILITYID (object) column serves as the primary key to join the GIS table with the Workorder table, facilitating the integration of geographical attributes.

- **FACILITYID (object):** A unique identifier representing individual segments between two manholes in the sewer system.
- **TYPE (object):** Describes the type of pipe associated with the facility.
- **LINING_TYP (object):** Represents the type of pipe connections used.
- **PIPE_SIZE (float64):** Specifies the size of the pipe.
- **PIPE_MATER (object):** Identifies the material composition of the pipe.
- **SLOPE (float64):** Records the pipe slope associated with each FacilityID.
- **LENGTH (float64):** Denotes the length of the pipe segment.
- **INSTALL_DATE:** Reflects the time elapsed since the installation date.


### Machine Learning (ML) Model Considerations:
For ML model development, the following columns are crucial:
- **Rate (float64):** Calculated column using COMPLETED_DATE and SLRAT_SCORE. This column converted  to the target variable with the given criteria and represent 0 and 1 for the ML model.
- **TYPE (object):** Categorical feature denoting the type of pipe.
- **LINING_TYP (object):** Categorical feature describing the type of pipe connections.
- **PIPE_SIZE (float64):** Numerical feature indicating the pipe size.
- **PIPE_MATER (object):** Categorical feature specifying the pipe material.
- **SLOPE (float64):** Numerical feature indicating the slope.
- **LENGTH (float64):** Numerical feature representing the length of the pipe segment.
- **time_since_install_date (float64):** Feature capturing the time elapsed since installation.

