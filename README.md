# GTC ML Project 1 - Data Cleaning & Preprocessing Challenge  

## 📌 Objective  
The goal of this project is to build a **robust data preprocessing pipeline** for a hotel booking cancellation prediction model. The focus is not on training the final machine learning model but on ensuring that the dataset is **clean, consistent, and ML-ready**.  

The **business problem**: The revenue team has identified that **last-minute booking cancellations** significantly impact profitability. To minimize losses, accurate predictions are needed — but that requires well-prepared data.  

---

## 📂 Dataset  
- **Source:** `hotel_bookings.csv` (direct from Property Management System - PMS)  
- **Shape:** 119,390 rows × 32 columns  
- **Data Types:** Mix of categorical, numerical, and date columns  

---

## 🔍 Phase 1: Exploratory Data Analysis (EDA) & Data Quality Report  
- Generated **summary statistics** (`.describe()`, `.info()`)  
- Identified **missing values** using `isna().sum()` and visualized with heatmaps  
- Detected **outliers** in key numerical columns (`adr`, `lead_time`) using **boxplots** and the **IQR method**  
- Documented **main issues**:  
  - Missing values in `children`, `country`, `agent`, `company`  
  - Incorrect data types (`children`, `agent`, `company`, `reservation_status_date`)  
  - Extreme outliers in `adr` and `lead_time`  
  - Presence of duplicate rows  

---

## 🧹 Phase 2: Data Cleaning  
- **Missing Values Handling**:  
  - `agent`, `company` → filled with `"None"` / `0`  
  - `country` → imputed with **mode** or `"Unknown"`  
  - `children` → imputed with **median**  
- **Removed duplicates** to ensure data consistency  
- **Outlier handling**: capped `adr` values above **1000** and applied percentile-based capping for `lead_time`  
- **Fixed data types**:  
  - `children` → `int`  
  - `agent`, `company` → categorical IDs (`Int64`)  
  - `reservation_status_date` → `datetime64`  

---

## ⚙️ Phase 3: Feature Engineering & Preprocessing  
- **New Features**:  
  - `total_guests = adults + children + babies`  
  - `total_nights = stays_in_weekend_nights + stays_in_week_nights`  
  - `is_family = 1 if (children > 0 or babies > 0) else 0`  
- **Encoding**:  
  - One-Hot Encoding for **low-cardinality** categorical variables (`meal`, `market_segment`)  
  - Frequency encoding for **high-cardinality** variable (`country`)  
- **Removed Data Leakage**: Dropped `reservation_status` and `reservation_status_date`  
- **Final Split**:  
  - Training: 80%  
  - Testing: 20%  
  - `random_state=42` for reproducibility  

---

## ✅ Main Data Quality Issues  
1. **Missing values** in key columns (`children`, `country`, `agent`, `company`)  
2. **Incorrect data types** that required conversion  
3. **Outliers** in `adr` and `lead_time`  
4. **Duplicate records** present in raw dataset  
5. **Potential data leakage** from reservation status columns  

---

## 📊 Key Insights from EDA  
- **Cancellation Rate:** ~37% of bookings were canceled  
- **Repeat Guests:** Only ~0.3% repeated visits → very low loyalty rate  
- **Yearly Trend:** Significant increase in bookings from **2015 → 2016**, followed by a slight decline in 2017  

---

## 🚀 Final Dataset Readiness  
The dataset is now **clean, encoded, and split into train/test sets**, making it fully prepared for machine learning model development.  
