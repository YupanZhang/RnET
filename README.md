# RnET
Extremely randomized trees model for Ra prediction 
<img width="866" height="670" alt="image" src="https://github.com/user-attachments/assets/87433f9c-c665-4261-a1bf-d786ffd7f92e" />
<img width="1592" height="610" alt="image" src="https://github.com/user-attachments/assets/093b24e1-124b-440a-81fe-41b5165a5a96" />



# Ra Prediction Model
The RaET Model is a Python-based machine learning tool designed specifically for predicting Ra values in China. By processing various environmental feature data (such as CEC, Clay, DTB, etc.), the model achieves accurate prediction of Ra values using the ExtraTreesRegressor algorithm and includes complete functional modules such as data preprocessing, model optimization, and result visualization.

**Compatibility Notes​**
It is recommended to use Python versions 3.8 - 3.11 to ensure all functions work properly.

# Algorithm Overview​

The workflow of the model is mainly divided into three key stages:​

**Data Processing and Visualization (Data Distribution, Percentiles, Outlier Removal):** 
Reads raster image data, processes NoData values, performs data cleaning (removes outliers), and displays data distribution characteristics.

**Model Construction and Optimization (Modeling: Data Augmentation, Adaptive Weights, Prediction Correction):**
Based on the preprocessed data, uses data augmentation technology to expand samples in sparse intervals, introduces an adaptive weight strategy to enhance the model's attention to key intervals, optimizes model parameters through grid search, and corrects prediction results for intervals to improve prediction accuracy.​

**Prediction and Result Saving:**
Uses the trained model to predict Ra values for new data, saves the prediction results as raster files, and displays the prediction results through visualization.​
The functions of each stage are implemented through modular code, allowing users to run specific steps individually or execute the complete process according to their needs. The code contains detailed comments to facilitate users' understanding of the implementation logic of each link.​

**Environment Configuration**
Before running this model, please ensure that the following necessary dependencies are installed.

**Recommended Versions​**
The model has been tested in the following environment and library versions. If you encounter compatibility issues, it is recommended to use these versions:​
Python Version: 3.8 - 3.11​
Operating System: Windows 64-bit​
​
Library​ Recommended Version​
numpy​ 1.24.3​

pandas​ 2.0.3​

rasterio​ 1.3.9​

matplotlib​ 3.7.1​

seaborn​ 0.12.2​

scikit-learn​ 1.3.0​

scipy​ 1.15.1​

tqdm​ 4.65.0​
​
# Data Preparation

ra.tif: Ra value data, used as the target variable of the model​

cec.tif: Cation exchange capacity data, used as a feature variable​

clay.tif: Clay content data, used as a feature variable​

dtb.tif: Soil layer thickness data, used as a feature variable​

oc.tif: Organic carbon content data, used as a feature variable​

ph.tif: pH value data, used as a feature variable

glim.tif: 16 lithological classes, used as a feature variable

sand.tif: gravimetric percentage of sand in the soil, used as a feature variable

silt.tif: gravimetric percentage of silt in the soil, used as a feature variable

sbd.tif: soil bulk density, used as a feature variable

**Data Preprocessing Instructions​**
The input data must be in raster image format (TIF). The model will automatically read and process the NoData values in it.​
The model uses the IQR method to remove outliers to improve data quality. Users can adjust relevant parameters according to the actual characteristics of the data.​

# Usage Steps​
**Set Data Path:** Modify the data_path variable in the code to specify the folder path where the input data is located.​

**Data Processing:** Run the code in the "Data Distribution, Percentiles, Outlier Removal" section to complete data reading, preprocessing, and visualization, and generate the processed dataset.​

**Model Training and Optimization:** Execute the code in the "Modeling: Data Augmentation, Adaptive Weights, Prediction Correction" section to perform data augmentation, model training, parameter optimization, and prediction correction, and obtain the optimized model and prediction results.​

**Prediction and Result Saving:** Run the code in the "Prediction" section to use the trained model for Ra value prediction, and save the prediction results as a raster file (predicted_ra_ET.tif) and a visualization image (predicted_ra_ET.png). The output path can be modified through the output_dir parameter.​

# Function Description​

**1.Data Processing Module​**
**Reading Raster Data:** Reads TIF format raster data through the read_raster function and obtains NoData values.​

**Processing NoData Values:** Uses the process_raster function to convert NoData values to NaN for subsequent data processing.​

**Removing Outliers:** Identifies and removes outliers using the IQR method to improve data reliability.​

**Data Visualization:** Draws boxplots to show feature distributions, and analyzes relationships between features through kernel density estimation plots and correlation heatmaps.​

**2.Model Construction Module​**
**Data Augmentation:** Performs data augmentation for sparse intervals of Ra values (by default, intervals below 25 and above 65) by adding Gaussian noise and slightly perturbing target values to expand the sample size.​

**Adaptive Weights:** Dynamically adjusts weights according to the number of samples in different intervals, making the model pay more attention to sparse intervals with fewer samples.​

**Parameter Optimization:** Uses grid search (GridSearchCV) to optimize the parameters of the ExtraTreesRegressor model to improve model performance.​

**Prediction Correction:** Corrects the prediction results for specific intervals (low-value and high-value intervals) to reduce systematic errors.​


**3.Prediction Module​**
**Batch Prediction:** Supports batch prediction for large-scale data to avoid memory overflow issues.​

**Result Saving:** Saves the prediction results in raster image format, retaining the coordinate reference system and transformation information of the original data for subsequent spatial analysis.​

**Result Visualization:** Draws a spatial distribution map of the prediction results to intuitively display the prediction of Ra values.​

# Output Results​
Processed datasets and related visualization images (boxplots, kernel density estimation plots, correlation heatmaps, etc.).​
Model performance evaluation indicators, including RMSE, MAE, R², and MAPE, showing the performance of original predictions and corrected predictions respectively.​
Predicted result raster file (predicted_ra_ET.tif) and visualization image (predicted_ra_ET.png).​

# Notes​
Before running the model, ensure the integrity and correctness of the input data to avoid program failure due to missing data or format errors.​
Parameters such as data augmentation and adaptive weights can be adjusted according to the actual data characteristics to obtain better prediction results.​
For large-scale data, the prediction process may take a long time, and the program will display the current progress through a progress bar.
