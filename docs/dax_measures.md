## Open Compliance Tasks
Open Compliance Tasks =
COALESCE (
CALCULATE (
COUNTROWS ( FactComplianceTasks ),
FactComplianceTasks[Task Status] <> "Completed"),0)

## Missing Evidence Tasks
Missing Evidence Tasks =
CALCULATE (
COUNTROWS ( FactComplianceTasks ),
KEEPFILTERS ( FactComplianceTasks[Task Status] <> "Completed" ),
KEEPFILTERS ( FactComplianceTasks[Evidence Attached] = FALSE() ))

## Overdue Compliance Tasks
Overdue Compliance Tasks =
CALCULATE (
COUNTROWS ( FactComplianceTasks ),
KEEPFILTERS ( FactComplianceTasks[Task Status] <> "Completed" ),
KEEPFILTERS ( FactComplianceTasks[Due Date] < TODAY() ))

## Completed Tasks Missing Evidence
Completed Tasks Missing Evidence =
CALCULATE (
COUNTROWS ( FactComplianceTasks ),
FactComplianceTasks[Task Status] = "Completed",
FactComplianceTasks[Evidence Attached] = FALSE())

## Follow Up Required
Follow Up Required =
CALCULATE (
COUNTROWS ( FactServiceRequests ),
KEEPFILTERS (
FactServiceRequests[Request Status] IN {
"Waiting on Client",
"Waiting on Advisor",
"Waiting on Custodian" }))

## Average Follow-Up Age
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

## Days From Detection
Days From Detection =
DATEDIFF (
FactDataQualityExceptions[Detected Date], TODAY(), DAY)

## Ending AUM in Millions
Ending AUM ($M) =
DIVIDE (
[Total Ending AUM],
1000000)


## Net Flows
Net Flows =
SUM ( FactAUMRevenue[Inflows] ) - SUM ( FactAUMRevenue[Outflows] )
****
