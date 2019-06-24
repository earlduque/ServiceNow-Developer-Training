# GlideRecords
Objective: Learn how to use ```GlideRecord``` within ServiceNow

## Overview
The ```GlideRecord``` class is used for executing database operations without having to write SQL queries. ```GlideRecord``` can be useful for retrieving records which would be difficult to find using the GUI filtering options.

## Tutorial
To practice using `GlideRecord`: 
1. Open your [personal developer instance](https://developer.servicenow.com/app.do#!/instance?wu=true)
2. In the navigation menu, search `System Definition` and then select the sub-category `Scripts - Background`
3. 
```javascript
// Here is an example that gets the count of number of new incidents and provides the INC number and link
var gr = new GlideRecord('incident'); // create new GlideRecord from incident table
gr.addQuery('active', true); // filter out for active incidents only
gr.addQuery('state', '1'); // filter out for incidents in state 1 (new)
gr.query();

gs.info("Number of new incidents: ");
gs.info(gr.getRowCount());

gs.info("Printing incident numbers:");
while(gr.next()) { // loop through records
   gs.info(gr.getValue('number')); // print out INC number
   gs.info(gr.getLink(false)); // print out INC link
}
```
4. Click the `Run script` button
5. The script will run and the result will show something like this: ` ***Script: Number of incidents: 8`
You can use this process to test out different GlideRecord examples

## Resources
[Using GlideRecord to Query Tables](https://docs.servicenow.com/bundle/madrid-application-development/page/script/server-scripting/concept/c_UsingGlideRecordToQueryTables.html)

[GlideRecord Documentation](https://docs.servicenow.com/bundle/madrid-application-development/page/app-store/dev_portal/API_reference/glideRecordScoped/concept/c_GlideRecordScopedAPI.html)
