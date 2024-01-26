# D365Usgae
### Collect Dynamics 365 Daily Usage 

Power Platform Solution to collect data from Application Insights on Dynamics 365 usage. Tested with Customer Engagement Applications (Sales, Customer Service, Field Service)

### Process
A Power Automate flow runs every day. It executes a Kusto query against Application Insights to collect Dynamics 365 usage records from the prior 24 hours. A unique user is identified by at least one usage record in Application Insights per user per day. Usage records are written to the AppUsage table. Each AppUsage record includes the Azure AD Object ID for each user, the app used, and the date of use. The AppMap table contains long and short pretty names useful for reporting purposes. A Model Driven App is included to help administer the AppMap table. 

### Solution Components
  - D365Usage Admin : Model Driven App to maintain the AppMap table
  - AppMap Table : maps application names from Application Insights records to report friendly names
  - AppUsage Table : contains daily application usage records. This table could grow quickly depending on number of active daily users. It would be wise to consider an aggregation strategy that condenses daily user records into weekly or monthly records in a separate table and then removes daily records from the AppUsage table.
  - GetApplicationInsights : Cloud flow that runs once per day. It gathers Application Insight records from the previous 24 hours and writes them to the AppUsage table in Dataverse.
  - D365Usage : Power BI sample Report and Dataset 







