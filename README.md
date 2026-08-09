# ria-operations-control-dashboard
Power BI portfolio dashboard simulating RIA operations control reporting, including service request backlog, client follow-ups, AUM reconciliation, operational exceptions, and compliance evidence tracking using synthetic wealth management operations data.


RIA Operations Control Dashboard
Client Onboarding, Account Maintenance & Compliance Exceptions


Project Overview
This project is a Power BI portfolio dashboard designed to simulate an operations control report for a Registered Investment Adviser (RIA). The report tracks service request workload, client follow-up activity, AUM/revenue reconciliation, operational exceptions, and compliance task exceptions across a synthetic RIA operations dataset.
The purpose of the project is to demonstrate how Power BI can be used to monitor operational risk, service-level performance, data quality issues, compliance evidence gaps, and reconciliation controls in a wealth management operations environment.
The report is structured as a multi-page operational control dashboard with executive-style KPI summaries, drilldown visuals, slicers, and exception-level detail tables.
________________________________________
Business Problem
RIA operations teams often need visibility into multiple control areas at once:
•	Service request backlog and SLA risk
•	Client follow-up tasks waiting on advisors, clients, or custodians
•	AUM and advisory fee reconciliation results
•	Operational exceptions from source systems and workflow processes
•	Compliance task evidence, overdue items, and missing documentation
Without centralized reporting, these issues can be difficult to prioritize. This dashboard consolidates operational signals into a structured Power BI report that allows users to quickly identify workload bottlenecks, aging items, missing evidence, and exception trends.
________________________________________
Report Objectives
The dashboard was designed to answer the following business questions:
1.	Operations Overview
o	How many requests are open?
o	How many items are overdue?
o	Which request types are driving operational workload?
o	Which advisors have the highest SLA risk?
2.	Client Review & Follow-Up Tracker
o	Which client follow-ups are waiting on action?
o	Who or what is blocking follow-up completion?
o	Which client follow-ups are aging the longest?
3.	AUM / Revenue Reconciliation
o	What is the ending AUM trend over time?
o	What is advisory fee revenue by advisor?
o	Are there reconciliation variances or exceptions?
4.	Operational Exceptions
o	What operational exceptions are open?
o	Which exception types and source systems are driving issue volume?
o	Which exceptions have been aging the longest?
5.	Compliance Exceptions
o	Which compliance tasks are overdue?
o	Which tasks are missing required evidence?
o	Which completed tasks are missing documentation?
o	Which compliance categories have the largest overdue task volume?
________________________________________
Dashboard Pages
1. RIA Operations Overview
The Operations Overview page provides a high-level summary of service request health and backlog risk.
Key components:
•	Open Requests
•	Overdue Requests
•	SLA Breach %
•	Completion Rate
•	Average Days to Complete
•	Open Operational Exceptions
•	Open Requests by Request Type
•	Advisor Workload & SLA Risk summary table
Purpose:
This page gives users a fast executive-level view of operational health. It highlights workload volume, SLA exposure, and the request types or advisors contributing most to backlog risk.
________________________________________
2. Client Review & Follow-Up Tracker
The Client Review & Follow-Up Tracker focuses on follow-up activity and stalled client service requests.
Key components:
•	Follow-Ups Required
•	Waiting on Advisor
•	Waiting on Custodian
•	Waiting on Client
•	Overdue Follow-Ups
•	Average Follow-Up Age
•	Follow-Ups by Request Type
•	Advisor Follow-Up Workload
•	Client Follow-Up Action List
Purpose:
This page is designed to identify client follow-ups requiring action. It helps operations users understand where requests are stuck, who is responsible, and which items should be prioritized based on age or overdue status.
________________________________________
3. AUM / Revenue Reconciliation
The AUM / Revenue Reconciliation page provides a simplified view of assets under management, advisory fee revenue, and reconciliation control metrics.
Key components:
•	Ending AUM
•	Net Flows
•	Advisory Fee Revenue
•	AUM Variance
•	Total Exceptions
•	Ending AUM Trend
•	Advisor Reconciliation Summary
Purpose:
This page summarizes financial reconciliation activity and highlights advisor-level AUM and fee revenue. It is intentionally kept simple to avoid overloading the report with financial detail while still demonstrating reconciliation monitoring.
________________________________________
4. Operational Exceptions
The Operational Exceptions page tracks open operational data and workflow exceptions.
Key components:
•	Open Operational Exceptions
•	High Severity Exceptions
•	Average Exception Age Days
•	Accepted Risk Exceptions
•	Operational Exceptions by Severity
•	Operational Exceptions by Exception Type
•	Exceptions by Source System
•	Exception Detail Table
Purpose:
This page supports exception review and operational risk monitoring. It identifies issue volume by severity, type, and source system, while the detail table provides record-level traceability.
________________________________________
5. Compliance Exceptions
The Compliance Exceptions page tracks overdue compliance tasks and missing compliance evidence.
Key components:
•	Open Compliance Tasks
•	Missing Evidence Tasks
•	Overdue Compliance Tasks
•	Completed Tasks Missing Evidence
•	Compliance Tasks by Evidence Status
•	Overdue Compliance Tasks by Category
•	Compliance Task Review Detail
Purpose:
This page helps users identify compliance documentation gaps, overdue tasks, and completed tasks where required evidence is missing. It supports compliance task review and control validation.
________________________________________
Dataset
This project uses a synthetic dataset modeled around common RIA operations workflows. The data was created for portfolio and demonstration purposes only.
The dataset includes operational concepts such as:
•	Service requests
•	Advisor assignments
•	Client names and IDs
•	Request types
•	Request statuses
•	Due dates and completed dates
•	SLA and overdue indicators
•	AUM values
•	Advisory fee revenue
•	Compliance task categories
•	Evidence attachment indicators
•	Data quality and operational exceptions
•	Source systems
•	Severity levels
•	Resolution statuses
No real client, advisor, financial, or firm data is used.
________________________________________
Data Model Summary
The report is based on fact-style tables representing different operational domains:
Service Request Data
Used for:
•	Operations Overview
•	Client Review & Follow-Up Tracker
Example fields:
•	Request Type
•	Request Status
•	Created Date
•	Due Date
•	Completed Date
•	Advisor Name
•	Client Name
•	Owner Team
•	Priority
•	Follow-Up Required
•	SLA / Overdue indicators
AUM / Revenue Data
Used for:
•	AUM / Revenue Reconciliation
Example fields:
•	Beginning AUM
•	Ending AUM
•	Inflows
•	Outflows
•	Market Change
•	Advisory Fee Revenue
•	AUM Reconciliation Variance
•	Advisor Name
•	Custodian
•	Month Start
Operational Exception Data
Used for:
•	Operational Exceptions
Example fields:
•	Exception ID
•	Client ID
•	Exception Type
•	Severity
•	Detected Date
•	Source System
•	Owner Team
•	Resolution Status
•	Days From Detection
Compliance Task Data
Used for:
•	Compliance Exceptions
Example fields:
•	Task ID
•	Task Name
•	Compliance Category
•	Evidence Attached
•	Compliance Evidence Status
•	Task Status
•	Due Date
•	Days Overdue
•	Advisor Name
•	Client Name


Key DAX Measures

Below are examples of measures used in the report.

Open Compliance Tasks
Open Compliance Tasks =
COALESCE (
CALCULATE (
COUNTROWS ( FactComplianceTasks ),
FactComplianceTasks[Task Status] <> "Completed"),0)

Missing Evidence Tasks
Missing Evidence Tasks =
CALCULATE (
COUNTROWS ( FactComplianceTasks ),
KEEPFILTERS ( FactComplianceTasks[Task Status] <> "Completed" ),
KEEPFILTERS ( FactComplianceTasks[Evidence Attached] = FALSE() ))

Overdue Compliance Tasks
Overdue Compliance Tasks =
CALCULATE (
COUNTROWS ( FactComplianceTasks ),
KEEPFILTERS ( FactComplianceTasks[Task Status] <> "Completed" ),
KEEPFILTERS ( FactComplianceTasks[Due Date] < TODAY() ))

Completed Tasks Missing Evidence
Completed Tasks Missing Evidence =
CALCULATE (
COUNTROWS ( FactComplianceTasks ),
FactComplianceTasks[Task Status] = "Completed",
FactComplianceTasks[Evidence Attached] = FALSE())

Follow Up Required
Follow Up Required =
CALCULATE (
COUNTROWS ( FactServiceRequests ),
KEEPFILTERS (
FactServiceRequests[Request Status] IN {
"Waiting on Client",
"Waiting on Advisor",
"Waiting on Custodian" }))

Average Follow-Up Age
Avg Follow-Up Age =
AVERAGEX (
FILTER (
FactServiceRequests,
FactServiceRequests[Request Status] IN {
"Waiting on Client",
"Waiting on Advisor",
"Waiting on Custodian"
}
&& ISBLANK ( FactServiceRequests[Completed Date] )
),
DATEDIFF (
FactServiceRequests[Created Date], TODAY(), DAY))

Days From Detection
Days From Detection =
DATEDIFF (
FactDataQualityExceptions[Detected Date], TODAY(), DAY)

Ending AUM in Millions
Ending AUM ($M) =
DIVIDE (
[Total Ending AUM],
1000000)

Net Flows
Net Flows =
SUM ( FactAUMRevenue[Inflows] ) - SUM ( FactAUMRevenue[Outflows] )

Report Design Decisions
KPI-First Layout
Each page uses KPI cards at the top to summarize key operational health indicators before moving into charts and detail tables. This structure mirrors common business reporting patterns where users first need a quick summary, then supporting detail.

Simple Visual Structure
The report intentionally avoids excessive visuals. Most pages use:
•	KPI cards
•	One to three core visuals
•	A details table for actionability
This keeps the report easy to scan and prevents dashboard clutter.

Detail Tables for Traceability
Operational and compliance dashboards include detail tables because summary visuals alone are not enough for control review. The tables allow users to review specific exception records, overdue tasks, and follow-up items.

Slicers for User Filtering
Slicers are included for reporting periods and key operational dimensions such as:
•	Request Type
•	Advisor
•	Task Name
•	Compliance Category
•	Custodian
•	Severity
•	Resolution Status
These slicers allow users to narrow the dashboard to a specific operational area, advisor, or time period.




Simplified Financial Formatting
AUM values were converted into millions using a dedicated measure to make the reconciliation table easier to read. The table uses a field label such as Ending AUM ($M) to represent values in millions without requiring long raw currency values in every row.
Skills Demonstrated
This project demonstrates the following Power BI and analytics skills:
•	Power BI report development
•	KPI dashboard design
•	DAX measure creation
•	Calculated columns
•	Date-based aging calculations
•	SLA and overdue logic
•	Exception monitoring
•	Compliance evidence tracking
•	Reconciliation reporting
•	Table and chart formatting
•	Slicer configuration
•	Operational workflow analysis
•	Data quality/control reporting
•	Dashboard storytelling
•	Synthetic business dataset modeling
Business Value
The dashboard demonstrates how an RIA operations team could use Power BI to improve visibility into daily operational controls.
Potential business value includes:
•	Faster identification of overdue service requests
•	Better visibility into advisor workload and follow-up bottlenecks
•	Improved monitoring of missing compliance evidence
•	More transparent operational exception tracking
•	Easier review of aging exceptions and stale tasks
•	Centralized reconciliation view for AUM and advisory fee reporting
•	More actionable reporting for operations, compliance, and client service teams

Project Limitations
This project uses synthetic data and is intended for portfolio demonstration purposes only. It does not represent a production RIA system or real client records.
Potential enhancements for a production version could include:
•	Integration with CRM, portfolio management, custodian, or document management systems
•	Automated refresh from operational databases
•	Row-level security by advisor or team
•	More detailed audit trail reporting
•	Historical trend analysis for exception volume and SLA performance
•	Drill-through pages for specific clients, advisors, or exception records
•	Automated alerts for high-risk or aging exceptions

Repository Structure
ria-operations-control-dashboard/
│
├── README.md
├── data/
│ └── synthetic_ria_operations_dataset.xlsx
│
├── powerbi/
│ └── RIA_Operations_Control_Dashboard.pbix
│
├── screenshots/
│ ├── 01_operations_overview.png
│ ├── 02_client_follow_up_tracker.png
│ ├── 03_aum_revenue_reconciliation.png
│ ├── 04_operational_exceptions.png
│ └── 05_compliance_exceptions.png
│
└── documentation/
└── dax_measures.md


Screenshots
Operations Overview
screenshots/01_operations_overview.png
 
Client Review & Follow-Up Tracker
screenshots/02_client_follow_up_tracker.png
 
AUM / Revenue Reconciliation
screenshots/03_aum_revenue_reconciliation.png
 
Operational Exceptions
screenshots/04_operational_exceptions.png
 

Compliance Exceptions
screenshots/05_compliance_exceptions.png
 

How to Use This Report
1.	Open the .pbix file in Power BI Desktop.
2.	Use slicers at the top of each page to filter by date, advisor, request type, task name, custodian, or category.
3.	Review KPI cards for summary-level operational health.
4.	Use charts to identify workload, overdue, exception, or reconciliation drivers.
5.	Use detail tables to review specific records requiring follow-up.

Summary
The RIA Operations Control Dashboard is a Power BI portfolio project that demonstrates how operational, compliance, and reconciliation data can be organized into an actionable control report for a wealth management operations environment.
The report combines KPI summaries, workload analysis, aging calculations, exception tracking, compliance evidence monitoring, and reconciliation views into a single multi-page dashboard. It is designed to show practical Power BI reporting skills in a realistic RIA operations context.
