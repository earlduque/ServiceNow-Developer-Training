# GlideRecords
Objective: Learn how to use `GlideRecord` within ServiceNow

## Overview
The `GlideRecord` class is used for executing database operations without having to write SQL queries. `GlideRecord` can be useful for retrieving records which would be difficult to find using the GUI filtering options.

## Tutorial
To practice using `GlideRecord`: 
1. Open your [personal developer instance](https://developer.servicenow.com/app.do#!/instance?wu=true)
2. In the navigation menu, search `System Definition` and then select the sub-category `Scripts - Background`
3. Copy this script into the text area:
```javascript
// Here is an example that gets the count of new incidents and provides the INC number & link

// create new GlideRecord from incident table
// Filter for active incidents in state 1 (new)
var gr = new GlideRecord('incident'); 
gr.addQuery('active', true);
gr.addQuery('state', '1'); 
gr.query();

// Print out number of new incidents
gs.info("Number of new incidents:");
gs.info(gr.getRowCount());

// Loop through record and print INC number and link
gs.info("Printing incident numbers:");
while(gr.next()) { 
   gs.info(gr.getValue('number'));
   gs.info(gr.getLink(false));
}
```
4. Click the `Run script` button
5. The script will run and the result will show something like this: 
``` 
*** Script: Number of new incidents: 
*** Script: 1
*** Script: Printing out incident numbers:
*** Script: INC000046
*** Script: incident.do?sys_id=a9e30c7dc61122760116894de7bcc7bd&sysparm_stack=incident_list.do?sysparm_query=active=true
```

You can use this process to test out different GlideRecord examples

## Additional Examples
We can use GlideRecord methods to make changes such as inserts, updates, and deletions.
Here's an example to create a new incident using the `initialize` and `insert` methods.

``` javascript
//Create a new Incident record and populate the fields with the values below
var gr = new GlideRecord('incident');
gr.initialize();
gr.short_description = 'Issue with signing into email';
gr.category = 'email';
gr.caller_id.setDisplayValue('Earl Duque');
gr.insert();
```

## Resources
[Using GlideRecord to Query Tables](https://docs.servicenow.com/bundle/madrid-application-development/page/script/server-scripting/concept/c_UsingGlideRecordToQueryTables.html)

[GlideRecord Documentation](https://docs.servicenow.com/bundle/madrid-application-development/page/app-store/dev_portal/API_reference/glideRecordScoped/concept/c_GlideRecordScopedAPI.html)
