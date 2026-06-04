# What Drives the Price of a Used Car?

An empirical analysis of used car resale values using the CRISP-DM (Cross-Industry Standard Process for Data Mining) framework. This project builds regularized linear regression models (Ridge & Lasso) to predict used car prices and identify the key factors that drive depreciation or command a premium in the market.

## Project Structure
* **[prompt_II.ipynb](prompt_II.ipynb)**: The main Jupyter notebook containing detailed data profiling, exploratory visualizations, data cleaning, model training, hyperparameter tuning, and diagnostic residual plots.
* **data/vehicles.csv**: The source dataset containing listing information for 426,880 used cars.

---

## Executive Report for Used Car Dealerships

**Subject:** Used Car Resale Price Drivers & Inventory Optimization Strategies
**Target Audience:** Dealership Management and Inventory Acquisition Teams

### **Executive Summary**
Using a dataset of over 345,000 historical vehicle listings across the United States, we trained regularized machine learning models to identify the exact attributes that drive used car prices. Our final model successfully explains **78.05%** of used car pricing variance with a mean absolute prediction error (MAE) of **$4,303.99**.

Below, we detail the key value drivers (premiums), value depreciators, and actionable inventory buying rules of thumb to maximize your dealership's profitability and turnover.

---

### **1. The Two Pillars of Depreciation: Age and Mileage**
Our model shows that **Age** and **Mileage** have a nearly identical impact on vehicle depreciation. Standardized coefficients indicate:
* **Vehicle Age:** Every 6.5 years of vehicle age reduces its value by **$3,776.52** (holding all else constant).
* **Mileage:** Every 50,000 miles on the odometer reduces its value by **$3,578.03**.
* *Actionable Insight:* Prioritize vehicles that have high age but exceptionally low mileage, or vice versa, but avoid vehicles where both are high, as depreciation compounds rapidly.

---

### **2. High-Yield Inventory (Command a Premium)**
Dealerships should target these specific models and features to command a resale premium:
* **Specific Vehicle Model (High-Yield Models):** The vehicle model is the single largest predictor of baseline pricing (commanding a premium of **+$6,987.03**). Specifically, target high-volume, high-yield models in these three lucrative segments:
  - *Heavy-Duty Trucks & Commercials:* **RAM 3500/5500** (Avg: $40.2k - $47.0k), **GMC Sierra 3500HD** (Avg: $42.5k), **Ford F-350/F-550 Super Duty** (Avg: $42.2k), and **Chevrolet Silverado 2500HD/3500HD** (Avg: $40.0k - $41.3k).
  - *Luxury SUVs:* **Audi Q8 Premium** (Avg: $62.3k), **GMC Yukon SLT** (Avg: $47.0k), **Acura MDX SH-AWD** (Avg: $40.7k), and **Jaguar E-Pace P250** (Avg: $39.2k).
  - *Sports & Lifestyle Vehicles:* **Jeep Gladiator** (Avg: $48.7k), **Chevrolet Corvette Stingray** (Avg: $48.5k), **Audi S5 Premium Plus** (Avg: $40.0k), and **Nissan 370Z Nismo** (Avg: $40.0k).
* **Body Type:** Convertibles command a **+$2,843.77** premium and off-road vehicles (jeeps, trucks) command a **+$2,259.62** premium over standard sedans.
* **Premium Engines:** Large 10 and 12-cylinder engines command an average premium of **+$2,521.68**.
* **Vehicle Condition:** Clean, "new" condition used cars command a **+$2,444.04** premium.

---

### **3. High-Risk Inventory (Accelerated Depreciation)**
Dealerships should avoid or deeply discount acquisitions with these attributes:
* **Fuel Type:** Gas-powered cars are priced **$6,903.16 cheaper** than diesel counterparts on average. Hybrid and electric vehicles are also **~$6,000 cheaper** than diesel, indicating that diesel configurations (trucks and commercial vans) retain their value far better than gas or alternative fuels.
* **Engine Size:** Budget 3 and 4-cylinder engines are priced **$6,802.97** and **$5,732.04 cheaper** than the average baseline.
* **Title Status:** Vehicles with rebuilt or salvage titles drop in value by **-$3,729.21** and **-$3,857.83** respectively. Parts-only titles drop value by **-$4,753.07**.

---

### **4. Actionable Inventory Rules of Thumb**
* **Target the High-Yield Segments:** Instead of stocking generic sedans, structure your purchasing pipeline around the identified high-yield models: heavy-duty diesel work trucks (Ford Super Duty, RAM 3500), luxury SUVs (Audi Q8, GMC Yukon), and sports/lifestyle cars (Jeep Gladiator, Corvette). These segments command the largest average resale margins.
* **The "Diesel and Truck" Focus:** Target diesel trucks and utility vans. They resist standard depreciation far better than gas passenger vehicles.
* **The "Condition/Title" Shield:** Do not acquire salvage or rebuilt title vehicles unless bought at a discount of at least $4,000 below clean-title market value.
* **Engine Selection:** Favor larger cylinder counts (V6, V8, or 12-cylinders) over small commuter engines (3/4-cylinders) in markets where consumer purchasing power is higher, as they command higher resale margins.

---

## Model Evaluation Summary

We compared three modeling approaches to predict resale value:
1. **Ordinary Least Squares (OLS) Linear Regression** (Baseline)
2. **Ridge Regression (`RidgeCV` with L2 regularization)**
3. **Lasso Regression (`GridSearchCV` with L1 regularization)**

Due to robust preprocessing (including out-of-fold target encoding for high-cardinality nominals), the models behaved highly similarly and stably:

| Model | Train MAE | Test MAE | Train RMSE | Test RMSE | Train $R^2$ | Test $R^2$ |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Linear Regression (OLS)** | $4,110.22 | $4,303.98 | $6,212.90 | $6,589.96 | 0.8062 | 0.7805 |
| **Ridge Regression (RidgeCV)** | $4,110.21 | $4,303.99 | $6,212.90 | $6,589.99 | 0.8062 | 0.7805 |
| **Lasso Regression (GridSearchCV)** | $4,110.07 | $4,303.97 | $6,212.92 | $6,590.10 | 0.8062 | 0.7805 |

* **Generalizability:** The extremely small gap between train and test performance ($R^2$ diff of ~2.5%) proves that the models do not suffer from overfitting and will generalize well to future used car listings.
* **Diagnostics:** Residual plots show normally distributed errors centered on 0, validating our regression coefficients. Minor heteroscedasticity is observed only for vehicles valued above $40,000, indicating that luxury pricing is naturally more volatile.
