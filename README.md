# NextGenLearners-Week1-Data-Cleaning
Week 1 - Foundations: Cleaning and Exploring the Applicant Dataset
EXECUTIVE SUMMARY
Real-world data is inherently messy and unpredictable. It frequently contains missing values, typos, duplicate entries, inconsistent formatting, and improper data types. This repository contains the complete end-to-end data cleaning, wrangling, and initial exploratory data analysis (EDA) pipeline for raw applicant records, processed programmatically using Python and Pandas.   
The primary objective of this project is to simulate the exact workflow of a Data Analyst at NextGenLearners—transforming raw, untrusted applicant records into an accurate, reliable, and reproducible dataset ready for analytical reporting and downstream decision-making.  

REPOSITORY DELIVERABLES
Fully documented Google Colab / Jupyter Notebook containing executable Python cleaning code accompanied by detailed explanations for every major decision.   applicants_cleaned.csv

The final exported clean dataset featuring zero critical missing values, no duplicates, standardized categories, and verified data types.   README.mdComprehensive project documentation detailing the methodology, cleaning decisions, and data quality summary report.
DATA CLEANING PIPELINE AND METHODOLOGY

Step 1: Environment Setup and Data Exploration

The workspace was initialized using Pandas within a notebook environment to allow seamless integration of executable logic and structured documentation.
Data Shape Assessment: Analyzed total row and column dimensions via df.shape. 
Structure and Data Types: Evaluated schema definitions and non-null counts using df.info().   
Quality Audit: Identified exact null counts per feature via df.isnull().sum() and quantified exact duplicate rows via df.duplicated().sum(). 

Step 2: Justified Missing Value Handling

Instead of applying blanket drop rules, missing data was evaluated column-by-column based on domain necessity:   
Applicant Name: Missing entries represent unidentifiable applications. These rows were removed using df.dropna(subset=['Applicant Name']).  
Email: Serves as a primary communication handle. Missing entries were imputed with "not_provided@example.com" to keep the rest of the application data intact for broader domain trend analysis. 
University: A missing university name does not invalidate candidate eligibility. Imputed using df['University'].fillna('Not Specified').
Status: Unassigned status fields indicate unprocessed submissions. Imputed with default status "Under Review".  

Step 3: Deduplication Strategy

Deduplication was executed in two systematic phases:   
Exact Matching: Removed identical row duplicates across all features using df.drop_duplicates().   
Near-Duplicate Filtering: Identified resubmissions and formatting variants by matching unique Email addresses, retaining only the first entry via df.drop_duplicates(subset=['Email'], keep='first').

Step 4: Categorical Standardization and Text Cleaning

Unstructured text entries cause severe miscounts during aggregation.   
Whitespace Elimination: Applied .str.strip() across text features to trim leading and trailing whitespace.   
Domain Mapping: Constructed an explicit dictionary mapping all inconsistent spellings (e.g., "web dev", "WEB DEV", "webdev") into 5 standardized track labels.   Status Uniformity: Applied Title Case formatting ("Under Review", "Selected", "Rejected") via .str.title().   

Step 5: Type Conversions (Dates and Phone Numbers)

Application Date: Converted plain text string dates to native datetime64 objects using pd.to_datetime(..., errors='coerce'). The errors='coerce' parameter handles corrupted dates gracefully by replacing them with NaT without breaking execution.   
Phone: Cleaned dashes and spaces while preserving string data types to retain crucial leading zeros. 

DATA QUALITY SUMMARY REPORT

Starting Dataset (Initial):Total Rows: ~85 Rows   Total Columns: 7 Columns   Missing Values: Present across Name, Email, University, and Status   Duplicates: Present (Exact and Near-duplicates)   Domain Variations: 9+ inconsistent spelling variations   Application Date Format: Plain Text (object type)   
Cleaned Dataset (Final):Total Rows: ~78 Rows (Incomplete/unidentifiable records removed)   Total Columns: 7 Columns   Missing Values: 0 Nulls in critical fields   Duplicates: 0 Duplicates (Fully deduplicated by exact match and Email)   Domain Applied: Exactly 5 Clean Categories (Validated with .unique())   Application Date Format: Converted to datetime64 type   

HOW TO REPRODUCEClONE

Repository:git clone https://github.com/YourUsername/YourRepoName.gitcd YourRepoName
Execute Pipeline:Open Week1_Data_Cleaning_YourName.ipynb in Google Colab or Jupyter Notebook and run all cells sequentially (Runtime -> Run All)[cite: 1, 6].

PRE-SUBMISSION CHECKLIST VERIFICATION

Reproducible Execution: Notebook runs top-to-bottom without red error cells[cite: 6, 8].Documented Rationale: Every code block is paired with clear justifications[cite: 6, 8].
No Manual Editing: All fixes were applied programmatically via Pandas (no Excel modifications)[cite: 7, 8].Clean Exports: applicants_cleaned.csv and .ipynb notebook are pushed to the repository.   
