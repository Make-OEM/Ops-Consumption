# Ops-Consumption

The Make OEM Whitelabel administrator as well as the Organization administrator might need to monitor the monthly operation consumption of the organizations, teams or scenarios within their instance. 

This scenario is set up to get organizations, teams and scenarios consumptions. It could be adapted in order to get the consumption of only Organizations, teams or scenarios by only keeping the corresponding route.
It is scheduled to run every 29 days in order to get the consumption of the previous month. Please refer to the Make API documentation to understand what these endpoints return. The first (today - 31 days) and last (today) returned values don’t represent the entire day's consumption, therefore they should be ignored. 
This scenario is designed to ignore the first returned value and overwrite the last value of the previous run. 

The unique key for each record is composed as follow:
* For Organization’s consumption: “OrganizationId_date”
* For Team’s consumption: “OrganizationId_TeamId_date”
* For scenario’s consumption: “OrganizationId_TeamId_ScenarioId_date”

This allows us to retrieve and overwrite the needed record.

Please upload this scenario using the blueprint. Create the 3 Data Stores using the provided structure and connect the right data to each scenario following the overall architecture document. 
The data could be then transferred to a third party tool to display a dashboard or send notifications for example. 

