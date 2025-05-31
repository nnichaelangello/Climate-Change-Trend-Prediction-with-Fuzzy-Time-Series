# Climate Change Trend Prediction with Fuzzy Time Series

## Project Description
This project leverages the **Fuzzy Time Series (FTS)** method to predict trends in time-series data, initially focusing on the `SP.URB.TOTL` (urban population) indicator from the **Climate Change Indicators** dataset provided by the World Bank. The dataset spans from 1960 to 2023 and includes various indicators. The project explores data analysis, preprocessing, modeling, and future predictions to support insights into climate-related trends.

## Methodology

### 1. Exploratory Data Analysis (EDA)
- **Objective**: To understand the dataset's structure, identify patterns, and assess suitability for Fuzzy Time Series modeling.
- **Approach**:
  - Loaded and inspected the dataset, focusing on columns such as Country Name, Indicator Code, and yearly data from 1960 to 2024.
  - Selected `SP.URB.TOTL` as the initial indicator for analysis.
  - Evaluated missing values, revealing an average of 2.82% per year, with 100% missing data in 2024.
  - Analyzed trends for Aruba, observing a rise from 27,887 in 1960 to 47,554 in 2023.
  - Conducted an ADF Test for stationarity, yielding a p-value of 0.963, indicating non-stationary data.
  - Examined distribution across countries, noting high variability with a standard deviation of 325 million.
  - Assessed correlations between indicators, identifying a strong correlation (0.988) between `SP.URB.TOTL` and `SP.POP.TOTL`.
- **Findings**:
  - The data exhibits a clear upward trend and non-stationarity, making it an appropriate candidate for Fuzzy Time Series.
  - No duplicates were found, and missing values were minimal except for the year 2024.

### 2. Preprocessing
- **Objective**: To prepare the data for Fuzzy Time Series modeling by ensuring cleanliness and compatibility.
- **Approach**:
  - Restricted the analysis to the 1960–2023 period, excluding 2024 due to complete missing data.
  - Applied linear interpolation to handle missing values, though no missing values were present in the Aruba dataset.
  - Used the Interquartile Range (IQR) method with Winsorization to manage outliers, finding no significant outliers.
  - Performed Min-Max normalization to scale data to the [0, 1] range, facilitating fuzzification.
- **Findings**:
  - The dataset for Aruba was complete and clean, with no need for interpolation.
  - Normalization successfully transformed the data into a suitable format for fuzzy modeling, preserving the trend.

### 3. Fuzzy Time Series Modeling
- **Objective**: To develop a predictive model using Fuzzy Time Series to forecast urban population trends.
- **Approach**:
  - **Fuzzy Interval Definition**: Divided the normalized data ([0, 1]) into 7 intervals: A1 [0.000, 0.143], A2 [0.143, 0.286], A3 [0.286, 0.429], A4 [0.429, 0.571], A5 [0.571, 0.714], A6 [0.714, 0.857], and A7 [0.857, 1.000].
  - **Fuzzification**: Assigned fuzzy labels (A1–A7) to each data point and calculated membership degrees using a triangular membership function.
  - **Fuzzy Relationships**: Constructed Fuzzy Logical Relationships (FLR) and Fuzzy Logical Relationship Groups (FLRG), such as A1 → [A1, A2].
  - **Prediction and Defuzzification**: Predicted values for t+1 based on FLRG, then converted back to the original scale using the data range.
  - **Evaluation**: Measured model accuracy with Root Mean Square Error (RMSE) of 931.20 on the original scale.
- **Findings**:
  - The model effectively captured the long-term upward trend in urban population.
  - Distribution of fuzzy labels showed dominance of A1 (26 occurrences) in early years and A6/A7 (15 and 11 occurrences) in later years, reflecting population growth.
  - FLRG revealed stable transitions (e.g., A1 → A1, 24 times), with limited inter-interval shifts.
  - RMSE of 931.20 indicated good performance relative to the data range (~19,667), though short-term fluctuations were less accurately modeled.

### 4. Future Prediction
- **Objective**: To forecast the urban population in Aruba for 2024–2030 based on historical trends.
- **Approach**:
  - Utilized the last fuzzy label (A7 in 2023) as the starting point.
  - Applied FLRG to predict future values iteratively, updating the label after each prediction.
  - Defuzzified predictions to the original scale using the minimum and maximum values of the dataset.
- **Findings**:
  - Predictions indicated a stable upward trend, consistent with the historical growth pattern.
  - The forecast suggested continued population increase through 2030, aligning with the observed trend.

## Results
- **Model Performance**: The Chen's FTS order-1 model achieved an RMSE of 931.20, demonstrating strong capability in capturing long-term trends while showing limitations in short-term variability.
- **Trend Insights**: The urban population in Aruba has shown a consistent increase over 63 years, with predictions suggesting this trend will persist.
- **Future Projections**: The model forecasts a steady rise in urban population from 2024 to 2030, providing a baseline for further climate-related analysis.

## Potential Improvements
- Enhance accuracy by implementing Weighted Fuzzy Time Series.
- Explore higher-order models (e.g., order-2) to better capture complex patterns.
- Extend the analysis to climate-specific indicators such as CO2 emissions or average temperature if available in the dataset.

## Contributions
This project is open to contributions. Please open an *issue* or *pull request* on GitHub for suggestions or improvements. Contact: [insert your contact information].

## License
This project is licensed under the [MIT License](LICENSE).

## Notes
Developed in May 2025 with assistance from Grok 3 by xAI. The dataset is sourced from the World Bank and used solely for academic and research purposes.
