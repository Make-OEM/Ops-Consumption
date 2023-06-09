# Ops-Consumption
The Make OEM Whitelabel administrator might need to monitor the monthly operation consumption of the organizations within their instance. 

Please refer to the Consumption Monitoring Architecture file in order to get an overview of this solution.

This set of scenarios allows the monitoring of each organization's monthly consumption, by getting the consumption automatically before each monthly reset as well as a continuous monitoring with a frequency that could be adapted in order to be aware of the consumption levels of each organization and maybe set some notifications or alarms. 

The set is composed of 5 scenarios, 2 of which are cloned for each organization, as well as 3 data stores.
- **Get Consumption Before Reset Scenario:** this scenario is scheduled to run a couple of minutes (adjustable) before the organization reset to get the monthly consumption of the current period and store it in the Monthly_Consumption data store. The scheduling of this scenario is done automatically when the scenario {Schedule Get Consumption Before Reset} runs. This scenario is cloned at the creation of each organization where the organization ID is also added to the scenario parameters. 
- **Update Next_Reset After Reset:** This scenario updates the value of Next_Reset in the data store [Org_List] used to schedule the scenario that gets the consumption. For example the next reset date of the organization A is the 09/04 at 16h10, the scenario {Get consumption before reset} will be scheduled at 16h08 and the scenario {Update Next_reset After Reset} at 16h12, the latter will update the value of Next-Reset in the Data Store [Org_List] to 09/05 at 16h10. This scenario is also cloned at the creation of an organization and is supplied with its ID.
- **Schedule Get Consumption Before Reset:** This scenario goes through the list (Data Store [Org_List]) of all the organizations once a month and schedules their linked {Get Consumption Before Reset} and {Update Next Reset After Reset} scenarios depending on the next reset time.
- **Create a new Org:** This scenario creates a new organization and simultaneously clones the {Get Consumption Before Reset} and {Update Next Reset After Reset} scenarios and supplies them with the organization ID as well as adds the organization details to the Data Store [Org_List]. Please use the provided organization license example to create the structure for the first module Create JSON. Whenever a new organization is created a new folder, whose title includes the organization ID, will be created and it shall contain the two cloned scenarios {Get Consumption Before Reset} and {Update Next Reset After Reset} for this specific organization.
- **Organization Consumption Monitoring:** this scenario gets all the organizations and the consumption data of each organization and stores it in the data store [Consumption Monitoring]. It can be scheduled everyday and complemented by a notification or alarm system. 

This set of scenarios is only valid for organizations with a monthly renewal. If the renewal is on a yearly basis, the scenarios need to be adapted to the fact that the returned consumption data is from the last 60 days, following a rolling window model. 

Please upload all these scenarios in a separate folder using their blueprints. Create the 3 Data Store using the provided structure and connect the right data to each scenario following the overall architecture document. 

Please use the Data Store example in order to create their structure.
