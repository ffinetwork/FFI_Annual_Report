# Prep

## Setting up Project Directory 

1. Go to the FFI_Annual_Report Github page <            >. 

2. wget https://github.com/[user]/[repo]/archive/[branch].zip
with [user], [repo], and [branch] replaced with the appropriate fields.

Alternatively, if you are having trouble downloading it from Github, you can copy the "FFI_Annual_Report" zip file from the FFI annual reports folder to your local computer.

3. Open RStudio and navigate to the FFI_Annual_Report folder. Stay in this file location.

## FAO Data

For the more detailed version, refer to the "Annual Report Data Compilation SOP" which will walk through each step with pictures and detailed information/instructions. This is just a rough reminder of the steps.

1. Download the newest FAO data from <https://www.fao.org/faostat/en/#data> following the instructions in the “Instructions for downloading FAO data” document in the SOP folder.

After following the instructions, you should have two CSV files:
- `fao_sua_YEAR.csv` that contains data from FAO Supply and Utilization Accounts 
- `fao_foodbalance_YEAR.csv` that contains data from FAO Food Balance Sheets data
[Replace YEAR with the year of the current annual report]

2. Place the two CSV files in the folder called "Raw_Data". There is already a CSV file in there called `country_names.csv` (DO NOT EDIT THIS!). In total, you should now have three CSV files in the Raw_Data folder.

## Non-FAO Data

1. Follow the instructions in the "Instructions for downloading Non-FAO Data" document and "Annual Reports Data Compilation SOP" in the SOP folder, and run the NonFAO_Annual_Report R code to get CSV files with non-FAO data (from FAO Crops and Livestocks and Comtrade) for all three grains (wheat, maize, and rice). These files are in the `Final_Output` folder and are:
- `nonfao_wheat_YEAR.csv`
- `nonfao_maize_YEAR.csv`
- `nonfao_rice_YEAR.csv`

2. Copy and paste them in the appropriate Excel columns in the NonFAO Excel sheet and filled in any other missing data you could find from smaller sources. Also make sure that the supply and intake columns are calculated using Excel formulas. 

3. Transfer your Excel columns back into the original Non-FAO CSV files (`nonfao_wheat_YEAR.csv`, `nonfao_Maize_YEAR.csv`, and `nonfao_rice_YEAR.csv`. Make sure that all values do not have commas!

4. Place the completed three non-FAO CSV files (`nonfao_wheat_YEAR.csv`, `nonfao_maize_YEAR.csv`, and `nonfao_rice_YEAR.csv`) into the Raw_Data folder as well.

5. You should now have SIX total datasets in the Raw_Data folder.
- `fao_sua_YEAR.csv`: Contains FAO country data from the FAO Supply and Utilization Accounts Sheet
- `fao_foodbalance_YEAR.csv`: Contains FAO country data from the FAO Food Balance Sheet
- `nonfao_wheat_YEAR.csv`: Contains non-FAO country data for wheat 
- `nonfao_maize_YEAR.csv`: Contains non-FAO country data for maize
- `nonfao_rice_YEAR.csv`: Contains non-FAO country data for rice
- `country_names.csv`: Contains the names of all countries (both FAO and non-FAO)

6.  Open the config.yml document and replace the year with the
    year of the current annual report.

7.  Synchronize the project environment's R packages by:

-   In the R console tab,
    -   install the `renv` package if you do not already have it
        installed. Verify it's installed by running
        `"renv" %in% row.names(installed.packages())` and getting the
        value `TRUE`
-   In the Terminal tab, navigate to the project directory. Type `pwd`
    to get the current directory path
-   In the R console tab,
    -   type `setwd("_")` and replace the blank with the directory path
    -   type `getwd()` and hit the enter button to verify you are in the
        correct directory
    -   type `renv::restore()`

8.  Go back to the terminal tab. Make the three non-FAO grain sheets by:
- First typing `export YEAR="_"` and replace the blank with the current annual report year. This will retrieve the current annual report year as a system environment variable to help the Makefile commands run smoothly
- Then typing `make` to run all the R scripts to create the final three non-FAO grain sheets

# Project Directory Description

-   `Raw_Data/` folder should contain the six raw CSV files

    -   "fao_sua_YEAR.csv"
    -   "fao_foodbalance_YEAR.csv"
    -   "nonfao_wheat_YEAR.csv"
    -   "nonfao_maize_YEAR.csv"
    -   "nonfao_rice_YEAR.csv"
    -   "country_names.csv"

-   `Cleaned_Data/` folder contains the four cleaned RDS files

    -   "fao_sua_YEAR.rds"
    -   "fao_foodbalance_YEAR.rds"
    -   "nonfao_wheat_YEAR.rds"
    -   "nonfao_maize_YEAR.rds"

-   `Final_Output/` folder contains three final CSV files that merge FAO
    and non-FAO data for each grain

    -   "wheat_YEAR.csv"
    -   "maize_YEAR.csv"
    -   "rice_YEAR.csv"

-   `Code/` folder contains R scripts described below

-   `Makefile` is a document that specifies how to build the three final
    grain sheets automatically. Essentially, it contains rules to
    create each output so one can use a shortcut and doesn't have to run
    all of the individual R code scripts separately.

-   `config.yml` is a document that specifies a parameter or variable
    that we don't want hard-coded into any of the code since it can
    change. It contains one parameter (the year of the current annual
    report) so file names can be customized to the current annual
    report's year

# Code Description

-   `Code/clean_fao_data.R`:
    -   clean FAO SUA and Food Balances data from `Raw_Data/` folder
-   `Code/clean_nonfao_data.R`:
    -   clean non-FAO data from `Raw_Data/` folder
-   `Code/wheat.R`:
    -   read in and compile FAO and non-FAO data for wheat
    -   save wheat trade sheet in `Final_Output/` folder
-   `Code/maize.R`:
    -   read in and compile FAO and non-FAO data for wheat
    -   save maize trade sheet in `Final_Output/` folder
-   `Code/rice.R`:
    -   read in and compile FAO and non-FAO data for rice
    -   save rice trade sheet in `Final_Output/` folder
