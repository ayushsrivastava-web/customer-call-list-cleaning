# Customer Call List Data Cleaning Project (Python & Pandas)

## 📌 Project Overview
This repository contains a comprehensive data cleaning project using **Python** and the **Pandas** library. The raw dataset (`Customer Call List.xlsx`) contained messy text formatting, duplicate rows, irregular phone numbers, unformatted addresses, and unnecessary columns. This project systematically cleans and standardizes the dataset into a ready-to-use format for business communication.

---

## 🛠️ Repository File Structure

```text
customer-call-list-cleaning/
├── data/
│   ├── Customer Call List.xlsx       <-- Raw dataset file
│   └── cleaned_customer_list.csv     <-- Final cleaned output dataset
├── python_scripts/
│   └── data_cleaning.ipynb           <-- Jupyter Notebook containing all cleaning steps
├── screenshots/                      
│   ├── raw_data_preview.png
│   └── cleaned_data_preview.png
└── README.md
```

---

## 🧹 Data Cleaning Steps & Transformation Logic
The raw dataset was processed and sanitized through the following sequential steps using Python:
1. **Loading the Dataset:**  Imported pandas and loaded the Excel file into a dataframe.
```python
import pandas as pd
df = pd.read_excel("Customer Call List.xlsx")
```
### Output Snapshots
[Loading_The_Dataset]()

2. **Removing Duplicate Rows:** Identified and dropped duplicate customer records to maintain data integrity.
```Python
df = df.drop_duplicates()
```
### Output Snapshots
[Loading_The_Dataset]()

3. **Dropping Unnecessary Columns:** Removed columns that did not add analytical value to the customer contact process (e.g., Not_Useful_Column).
```Python
df = df.drop(columns="Not_Useful_Column")
```
### Output Snapshots
[Loading_The_Dataset]()

4. **Cleaning String Columns:** Cleaned messy characters, symbols (..., /, _), and extra whitespaces from columns like Last_Name using .str.strip().
-Standardized categorical values in Paying Customer and Do_Not_Contact columns (converting "Yes/No" variations uniformly to "Y/N").

5. **Standardizing Phone Numbers:** Removed unwanted alphanumeric characters and symbols using regular expressions (regex).
-Cleaned up empty and missing phone strings (nan, Na).
```python
df["Phone_Number"] = df["Phone_Number"].str.replace('[^a-zA-Z0-9]','',regex=True)
```
### Output Snapshots
[Loading_The_Dataset]()

6. **Splitting Address Information:**  Split the combined Address column into distinct fields (Street_Address, State, and Zip_Code) using .str.split().
```Python
df[["Street_Address","State","Zip_Code"]] = df["Address"].str.split(',', n=2, expand=True)
```
### Output Snapshots
[Loading_The_Dataset]()

7. **Handling Missing Values & Filtering Contact Rules:** Replaced null values with empty strings or handled missing data appropriately.
-Filtered out customers who opted out of contact (Do_Not_Contact == "Y") or had missing phone numbers.
```Python
for x in df.index:
    if df.loc[x,"Do_Not_Contact"] == "Y":
        df.drop(x, inplace=True)
```
### Output Snapshots
[Loading_The_Dataset]()

8. **Resetting DataFrame Index:** Cleaned up the final index sequence to ensure sequential ordering.
```Python
df = df.reset_index(drop=True)
```
### Output Snapshots
[Loading_The_Dataset]()

---

## 🚀 How to Run This Project
```text
-Clone or download this repository.
-Ensure you have Python and Pandas installed.
-Place your Customer Call List.xlsx file inside the data/ folder.
-Run the Jupyter Notebook or Python script to execute the data cleaning pipeline.
```

---
