# Kusto-Parse-Signinlogs
Parses the native signin logs within Azure to a more readable format with key columns

If you wish to turn the query into a function which you could simply call within log analytics etc. simply change the following line:

1.
let ParamUPN = "UserToLookup@Company.com";
let Data =
SigninLogs
| where TimeGenerated between ((ago(1d) - 1d) .. (now() + 1d))

to:
let Data =
SigninLogs
| where TimeGenerated between ((ParamDateTime - ParamScope) .. (ParamDateTime + ParamScope))

2. click save > save as

3. Give it a name "SigninParsed" for example.

4. Set the parameters:
    Type:      |   Name:
    datetime   |   ParamDateTime
    string     |   ParamUPN
    timespan   |   ParamScope
    
press save and the query should now be able to call with the following command:

Example:

SigninParsed("7/7/2022", "Jane.Doe@company.com", 2d)
