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
var incident_gr = new GlideRecord('incident'); 
incident_gr.addQuery('active', true);
incident_gr.addQuery('state', '1'); 
incident_gr.query();

// Print out number of new incidents
gs.info("Number of new incidents:");
gs.info(incident_gr.getRowCount());

// Loop through record and print INC number and link
gs.info("Printing incident numbers:");
while(incident_gr.next()) { 
   gs.info(incident_gr.getValue('number'));
   gs.info(incident_gr.getLink(false));
}
```
In the above code:

- ```var incident_gr = new GlideRecord('incident');``` creates a new ```GlideRecord``` object called ```incident_gr``` which accesses the incident table. **Important:** refrain from using ```gr``` as a name for your ```GlideRecord``` Objects as many scripts use this name for their ```GlideRecord``` objects. Having different ```GlideRecord``` objects with the same name could produce odd errors which are difficult to debug.

- ```addQuery()``` is used to add filters to our query. These filters help specify properties which we would like our queried results to have.

- ```query()``` tells our GlideRecord object to query the records which satisfy the filters we added using ```addQuery()```. All results are added to a list in our ```GlideRecord``` object.

- ```gs.info()``` serves as a print function, allowing us to display information to the user.

- ```next()``` returns the next record in the list of records contained in our GlideRecord object. It should be noted that when used in the while loop:

```
while(incident_gr.next()){
   //some code
}
```
The loop evaluates to ```true``` if the object returned by ```incident_gr.next()``` is not null, or in otherwords, if there are still object(s) in the list.

- ```getValue()``` returns a property value of the current record.

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
var inc_gr = new GlideRecord('incident');
inc_gr.initialize();
inc_gr.setValue('short_description', 'Issue with signing into email');
inc_gr.setValue('category', 'email');
inc_gr.caller_id.setDisplayValue('Earl Duque');
inc_gr.insert();
```

## Resources
For additional information, refer to:
[Using GlideRecord to Query Tables](https://docs.servicenow.com/bundle/madrid-application-development/page/script/server-scripting/concept/c_UsingGlideRecordToQueryTables.html)

[GlideRecord Documentation](https://docs.servicenow.com/bundle/madrid-application-development/page/app-store/dev_portal/API_reference/glideRecordScoped/concept/c_GlideRecordScopedAPI.html)
