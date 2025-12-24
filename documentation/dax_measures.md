# DAX Measures & Calculated Columns

This document outlines the key DAX calculations used in the dashboard.

## Calculated Columns

### Resolution Time (Hours)
```DAX
Resolution_Time_Hours =
DATEDIFF(
    'Operations'[Created_Date],
    'Operations'[Resolved_Date],
    HOUR
)

SLA_Status =
IF(
    'Operations'[Resolution_Time_Hours] <= 'Operations'[SLA_Hours],
    "Met",
    "Missed"
)

Month =
FORMAT('Operations'[Created_Date], "MMM")

SLA Compliance % =
DIVIDE(
    CALCULATE(COUNTROWS('Operations'), 'Operations'[SLA_Status] = "Met"),
    COUNTROWS('Operations')
)

SLA Compliance % =
DIVIDE(
    CALCULATE(COUNTROWS('Operations'), 'Operations'[SLA_Status] = "Met"),
    COUNTROWS('Operations')
)

SLA Missed =
CALCULATE(
    COUNTROWS('Operations'),
    'Operations'[SLA_Status] = "Missed"
)

