# Healthcare Performance Dashboard

## Project Overview 

This project is an interactive Healthcare Performance Analysis developed in Microsoft Power BI to evaluate the performance of a healthcare organization from operational, financial, and patient-experience perspectives.

The dashboard was designed around the following objectives:

• How is our healthcare organization performing

• What are our patients experiencing, and where are the major areas that require attention?

Rather than focusing only on visualizing data, the project uses data analysis and business intelligence techniques to identify meaningful patterns across:

* Patient volume
* Patient demographics
* Diagnoses
* Patient outcomes
* Department performance
* Waiting times
* Patient satisfaction
* Branch performance
* Revenue
* Costs
* Profitability
* Revenue targets
* Financial performance by state
* Returning patients

The dashboard was developed as a multi-page Power BI report with interactive slicers, navigation, drill-through functionality, dynamic titles/insights, tooltips, and analytical visuals.

## Business Problem

Healthcare organizations generate large amounts of operational, financial, and patient-related data. However, raw data does not automatically provide management with meaningful answers.
Management needs to understand not only what happened, but also:
* Where patient activity is concentrated
* Which departments receive the most visits
* How patient volumes change over time
* Which states and branches generate the most revenue
* Whether revenue is meeting established targets
* How much the organization spends on healthcare delivery
* How profitable different areas of the organization are
* How long patients wait
* How satisfied patients are
* What types of diagnoses are most common
* How patient outcomes are distributed
* The difference between new and returning patients
* Which operational areas require further investigation
  
The business problem was therefore translated into three major analytical questions:

1. How is the organization performing?
This focuses on:
* Patients
* Visits
* Revenue
* Cost
* Profit
* Revenue per patient
* Revenue versus target
* Monthly performance
* State and branch performance
2. What are patients experiencing?
This focuses on:
* Patient demographics
* Diagnoses
* New versus returning patients
* Waiting time
* Satisfaction
* Patient outcomes
* Department experiences
3. Where are the major areas requiring attention?
This focuses on identifying patterns such as:
* Departments with high waiting times
* Areas with lower satisfaction
* States or branches with weaker performance relative to targets
* Departments with unusual patient volumes
* Outcome patterns requiring further investigation
* Financial areas where costs and revenue need closer monitoring

## Dataset Description 

The project uses an Excel-based healthcare dataset containing patient, operational, financial, and target information.

The dataset covers:
* 1,200 patient records
* 4 states
* 12 branches
* 6 departments/services
* 6 diagnoses
* 4 patient outcomes
* January–December 2025

The project also includes supporting tables for targets and dates.

## Main Data Components

### Patient Visits
The Patient Visits data contains the core transactional/operational healthcare records.

The data supports analysis across areas such as:
* Patient ID 
* Visits date and count
* Patient demographics
* Departments
* Service
* Diagnoses
* States
* Branches
* Revenue
* Costs
* Waiting time
* Satisfaction
* Patient outcomes
* Payment method
* Insurance type

### State Targets
The State Targets table provides target values that can be compared against actual revenue performance.
This enables the dashboard to answer:
Is actual revenue meeting the expected target?

### Date Table
A dedicated Date Table was incorporated into the model to support proper time-based analysis.
It enables analysis such as:
* Monthly patient visits
* Monthly revenue
* Monthly financial performance
* Month-over-month analysis
* Date filtering
* Year/month reporting
  
The reporting period covered by the dataset is January to December 2025.

## Tools & Technologies 

### Microsoft Excel

Used for:

* Initial dataset inspection
* Data quality checks
* Understanding column structures
* Identifying inconsistencies
* Preliminary analysis

### Microsoft Power BI

Used for:

* Data modeling
* Data transformation
* DAX calculations
* Interactive visualizations
* Dashboard development
* KPI reporting
* Business analysis
* Drill-through
* Tooltips
* Slicers
* Page navigation
* Dynamic insights
* Conditional formatting

### Power Query

Power Query was used for data preparation and transformation, including:

* Reviewing data types
* Cleaning inconsistent values
* Handling blanks
* Checking duplicates
* Preparing date fields
* Creating/adjusting supporting tables
* Preparing the data for modeling.
  
### DAX

Used to create calculated measures for:

* Patient volume
* Visit volume
* Revenue
* Cost
* Profit
* Profit margin
* Average waiting time
* Average satisfaction 
* Average daily visits
* Average revenue per patient
* Average visits per patient
* Average patient age
* Profit per patient
* Cost per visit
* Revenue target
* Achievement %
* MoM revenue growth %
* Previous month revenue 
* Revenue variance
* Returning patients
* New Patients
* Positive outcome rate
* Dynamic insights
* Calculated column - Age group

A separate sort column was also created so the age groups appear in chronological order.

## Data Cleaning Process 

Before building the Power BI dashboard, the healthcare dataset was examined to identify structural, categorical, numerical, and analytical issues that could affect the reliability of the final report.
The cleaning process was not limited to removing blanks or duplicates. It also included validating whether the dataset behaved correctly when used for patient, operational, financial, and time-based analysis.

### 1. Reviewed the Overall Dataset Structure

The first step was to understand the data.
This was particularly important because the dataset contains both patient-level and visit-level information.
A patient can have more than one visit, meaning:
1 patient does not necessarily equal 1 row/visit.
This distinction became important later when calculating total patients, new patients, returning patients, and visit volumes.
 
### 2. Patient Count vs Visit Count
One of the most important validation checks was distinguishing between:
Unique Patients
and
Total Visits
The dataset contained:
* 1,200 unique patients
* 2,920 total visits
This confirmed that patients could appear across multiple healthcare visits.
Therefore, using a simple row count to represent patients would produce an incorrect patient count.
The dashboard used distinct patient logic for patient-level KPIs and Sum for visit-level counting for operational activity.

### 3. Pediatrics Age Inconsistencies

The Pediatrics department contains a large number of patients aged 19 and above.

There were:

* 221 Pediatrics records
* 179 patients aged 19+

This means approximately 81% of Pediatrics records were associated with patients aged 19 or older.

There were also several patients aged 90 in Pediatrics.

These records were treated as data-quality flags rather than automatically removed.

After validation, Pediatrics was retained as an analytical category in the final report.
The validated Pediatrics results were:
* 221 patients
* 515 visits
* ₦9.39M revenue
* 45.27 minutes average waiting time.

### 4. Maternity Gender and Age Inconsistencies

The Maternity department contains both male and female records.

There were:

* 189 Maternity records
* 94 male
* 95 female

There were also patients aged 17 and below associated with Maternity, including some very young records.

These observations may indicate data-entry, department-classification, or dataset-design issues and should be validated before making clinical conclusions.

### 5. Month Sorting Issue
A month-ordering issue was identified during dashboard development.
When month names are treated as text, Power BI can sort them alphabetically rather than chronologically.

A numeric month-order field was therefore used to sort the month name correctly.
This ensured that monthly patient and revenue trends followed the actual calendar sequence.

### 6. Revenue vs Target Validation
The State Targets table was used to compare actual revenue against expected revenue.
An aggregation issue was identified during dashboard development where the target could be interpreted incorrectly depending on the visual’s filter context.
The target should be evaluated at the appropriate state/time level rather than blindly treating every target value as an independent transaction.
This was important because the dashboard question was:
How does actual revenue compare with the expected target?
rather than:
What is the sum of every target row regardless of context?
The final report therefore treated target analysis as a benchmark comparison.

## Data Model

Data Model

The project uses a simple star-schema-style model.

Patient_Visits serves as the central fact table, while Date_Table and State_Targets provide supporting dimensions.

## Dashboard Structure 

The Power BI dashboard was structured into five analytical pages.

### Page 1 — Executive Overview

Provides a high-level view of organizational performance.

### KPIs

* Total Patients
* Total Visits
* Total Revenue
* Total Profit
* Profit Margin %
* Achievement %

### Visuals

* Monthly Patient Visits
* Revenue by State
* Patients by Department
* Revenue vs Target
* Patient Outcome Distribution

### Slicers

* Date
* State
* Branch
* Department
* Gender

### Page 2 — Patient Analysis

This page focuses on patient demographics and behavior.

### KPIs

* Total Patients
* Average Daily Visits
* Average Visits per Patient
* Average Patient Age

### Visuals

* Patients by Age Group
* Male vs Female Patients
* Patients by Diagnosis
* Patients by State
* New vs Returning Patients
* Patient Records

The page was designed to answer:

* Which age group represents the largest patient population?
* Which diagnoses are most common?
* Which states have the highest patient volume?
* How many patients are returning?
* Who exactly are the patients and how often do they visits?  

### Page 3 — Hospital Operations

This page evaluates operational performance across departments and branches.

### KPIs 

* Total Visits
* Average Waiting Time
* Average Satisfaction
* Average Visits per Patient
* Average Daily Visits
* Busiest Department

### Visuals

* Visits by Outcome 
* Department by Average Waiting Time
* Patient Satisfaction by Department
* Branch Performance 
* Monthly Patient Volume
* Visits by Department 

The analysis focuses on:

* Department workload
* Waiting time
* Patient satisfaction
* Branch volume
* Operational pressure points

### Page 4 — Financial Performance

This page evaluates the organization’s financial performance.

### KPIs

* Total Revenue
* Total Cost
* Total Profit
* Profit Margin %
* Revenue Target
* Revenue Variance

### Visuals

* Revenue by State
* Revenue by Department
* Revenue by Service
* Profit by Department
* Monthly Revenue Trend

### Page 5 — Patient Experience

This page focuses specifically on patient satisfaction and experience.

### KPIs 

* Average Satisfaction
* Average Waiting Time
* Positive Outcome Rate

### Visuals

* Satisfaction by Department
* Satisfaction by Branch
* Satisfaction vs Waiting Time
* Satisfaction by Outcome
* Satisfaction Gender

The page helps identify differences in patient experience across departments and branches.

### Drill-Through
A drill-through page was incorporated to allow users to move from summarized dashboard information into more detailed patient-level records.
For example, a user can select an analytical category and drill through to the underlying patient information.
The drill-through page was kept separate from the main navigation experience so that it functions as a contextual detail page rather than appearing as a normal dashboard page.
This improves navigation and keeps the main report structure clean.

### Tooltips

Custom tooltips were incorporated to provide additional information without overcrowding the primary dashboard visuals.

Instead of displaying every possible metric directly on the page, a user can hover over a visual and access additional context.

### Dashboard Navigation

Page navigation was incorporated to allow users to move between the major analytical areas.

The navigation structure separates:

* Executive Overview
* Patient Analysis
* Hospital Operations
* Financial Analysis
* Patient Experience

The drill-through page is treated differently because it serves as a detailed analytical destination rather than a standard report section.

### Dynamic Insights

Dynamic insights were used to turn numerical analysis into readable business statements.
For example, rather than forcing management to interpret every percentage or chart independently, a DAX-driven insight can communicate whether performance is:
* Positive
* Stable
* Declining
* Requiring attention
The same approach can be used to dynamically identify:
* Top-performing states
* Top departments
* Highest waiting-time department
* Revenue performance
* Patient patterns
This supports the overall storytelling objective of the project.

## Key Insights 

### 1. Executive Overview

* The organization recorded 1,200 patients and 2,920 visits, generating ₦47.84M in revenue and ₦18.35M in profit.
* Overall profit margin was 38.35%, indicating positive profitability within the recorded data.
* Rivers recorded the highest patient volume and revenue among the four states.
* Overall revenue achievement was 23.92% of the ₦200M annual target, highlighting a significant target gap.

### 2. Patient Analysis

* The 35–44 age group had the highest patient volume, with 244 patients.
* Malaria was the most frequently recorded diagnosis, followed by Typhoid and Hypertension.
* Rivers had the highest patient volume with 322 patients.
* 889 patients (74.1%) were classified as returning patients, compared with 311 new patients.
* Recovered was the most common recorded patient outcome, accounting for 54.1% of patients.

### 3. Hospital Operations

* Pediatrics recorded the highest patient volume, with 221 patients and 515 visits.
* Laboratory had the highest average waiting time at approximately 47 minutes.
* Obio-Akpor handled the highest number of visits with 303 visits, while also recording a relatively high average waiting time of 49 minutes.
* Satisfaction scores were relatively similar across departments, ranging from 3.69 to 3.74.

### 4. Financial Performance

* Rivers generated the highest revenue at approximately ₦12.73M.
* Pediatrics generated the highest departmental profit at approximately ₦3.71M.
* None of the four states reached its annual revenue target.
* Anambra had the largest absolute revenue shortfall, while Lagos recorded the lowest target achievement percentage.

### 5. Patient Experience

* Overall patient satisfaction was 3.71/5.
* Pharmacy had the highest departmental satisfaction score at 3.74, while Maternity had the lowest at 3.69.
* Nnewi recorded the highest branch satisfaction at 3.88, while Lekki recorded the lowest at 3.60.
* Waiting time and satisfaction showed little relationship in the dataset, with a correlation of approximately 0.002.
* This suggests that factors beyond waiting time may be influencing patient satisfaction.

## Recommendations

Based on the analysis, several areas can be prioritized for further investigation.

### 1. Investigate Revenue Target Gaps

All states recorded revenue below their annual targets.

Management should investigate:

* Revenue generation opportunities
* Patient volume versus revenue
* Service utilization
* State-level performance
* Pricing and revenue structure
* Whether the annual targets are appropriate for the period and dataset scope

The target gap should also be interpreted carefully if the dataset represents a sample rather than complete annual activity.

### 2. Investigate High-Volume Branches

Obio-Akpor recorded the highest visit volume while also recording a relatively high average waiting time.

Management could investigate:

* Staffing levels
* Patient flow
* Appointment scheduling
* Department capacity
* Peak periods
* Registration and service bottlenecks

### 3. Review Laboratory Waiting Times

Laboratory recorded the highest departmental average waiting time.

Management could examine:

* Laboratory staffing
* Test processing times
* Patient queues
* Sample collection processes
* Equipment availability
* Peak demand periods

### 4. Monitor Patient Satisfaction

Although departmental satisfaction differences are relatively small, Maternity recorded the lowest departmental satisfaction score.

Branch-level analysis also showed differences in satisfaction, with Lekki recording the lowest branch score.

These areas can be investigated further through:

* Patient feedback
* Service-level analysis
* Complaint data
* Staff-patient interactions
* Waiting and service processes

### 5. Investigate Patient Retention

Approximately 74.1% of patients were classified as returning based on Visit_Count.

This is a significant pattern worth monitoring.

Further analysis could examine:

* Which departments generate the most repeat visits
* Which diagnoses are associated with repeat visits
* Repeat visits by branch
* Revenue generated by returning patients
* Whether repeat visits represent planned follow-up care or other utilization patterns

### 6. Improve Data Quality Controls

The demographic and departmental inconsistencies identified in Pediatrics and Maternity should be reviewed.

Future data collection processes should include validation rules for:

* Age
* Department
* Gender
* Diagnosis
* Service
* Outcome

This would improve the reliability of demographic and clinical analysis.

## Conclusion

This project demonstrates how Power BI can transform healthcare operational, financial, and patient data into an interactive business solution.

The dashboard provides management with visibility into:

* Patient volume
* Patient demographics
* Diagnoses
* Patient outcomes
* Department performance
* Branch performance
* Waiting times
* Patient satisfaction
* Revenue
* Costs
* Profitability
* Revenue targets

The analysis shows a healthcare organization with positive recorded profitability, substantial repeat-patient activity, and measurable patient volumes across states and departments.

At the same time, the dashboard highlights several areas requiring further investigation, particularly revenue target achievement, operational waiting times, branch performance, patient experience, and data-quality inconsistencies.

An important lesson from the project was that effective business analysis is not simply about creating attractive visualizations. The goal is to connect data, metrics, and business questions so that decision-makers can understand what is happening, where it is happening, and what areas deserve further investigation.

## Project Skills Demonstrated

This project demonstrates practical experience in:

* Data cleaning
* Data quality assessment
* Data modeling
* Star-schema design
* Power BI
* DAX
* KPI development
* Financial analysis
* Patient analytics
* Operational analysis
* Data visualization
* Business storytelling
* Dashboard design
* Insight generation
* Decision-support reporting
