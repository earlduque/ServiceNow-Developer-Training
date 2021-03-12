# Create a Widget Using AngularJS and GlideRecords
Objective: Learn what Angular is used for in HTML, how to query databases in server script using GlideRecords

## What is a Widget?
A widget is a reuseable component which make up the functionality of a portal page and allow users to interact with the service portal and displays information. There are six parts to a widget: HTML, CSS, Client Script, Server Script, Link Function, Options. We will only be focusing on HTML, Client and Server Scripts, and CSS for this tutorial. 

### HTML
The HTML accepts and displays data, as well as provides the basic structure to the widget. This will be what the user sees in the end product and browser.
### CSS
CSS or Cascading Style Sheets allows styling of the HTML and customization to the contents on a page. This includes borders, fonts, colors, visibility, size, positioning, and many others.
### Client Script
The widget's Client Script defines the AngularJS controller. It defines the behavior of the widget and delivers the data model to the HTML.
### Server Script
The Server Script handles any interaction within the ServiceNow instance. You can reference script includes, get data from tables, do updates, etc. In this tutorial, we will be retrieving data from a table within ServiceNow. 

## Using GlideRecords to Query Tables
`GlideRecord` can be useful for retrieving and querying records. For example, a record/table can be queried to find all active cases with a keyword and return the first 10 in descending order by created date.

1. To query a table, first create an object for the desired table: 
```
var targetGR = new GlideRecord('sn_customerservice_case');
```
**Note:** *Avoid* naming your variable gr, as it may potentially interfere with global variables. Good practices include naming your GlideRecord objects descriptive names, for example: `incGR` or `inc_gr`.

2. After initializing the GlideRecord object, add filters to the query. Filters specify which results from the table to return and can include: state, priority, date, assignment groups, etc. After adding all the desired filters, run the query by calling `targetGR.query();`

```
// Filter all active cases
targetGR.addQuery('active', true);

// Filter all cases whose short_description contains the word 'Urgent'
targetGR.addQuery('short_description,'CONTAINS','Urgent');

// Return the query in order of descending date created (newest created first)
targetGR.orderByDesc('sys_created_on');

// Return only first 10 filtered cases
targetGR.setLimit(10);

// Run query
targetGR.query();
```
Other available JavaScript operators that can be used to query can be found [here]( https://docs.servicenow.com/bundle/madrid-application-development/page/script/server-scripting/concept/c_UsingGlideRecordToQueryTables.html])

3. After querying the table, push each result from the query onto an array to be called in HTML.
```
// Initialize an empty array using data.variable
data.records = [];

//While there is another record to access in the GlideRecord, push record to array
while(targetGR.next()) {
 var temp = {};
 //choose what information to display
 data.records.push(temp);
}
```

## AngularJS Basics
After querying a table, angular directives are used to display the results of the query to the HTML. Service Portal uses angular directive to construct decision logic using controller and html views. We should have a basic understanding for the various directive available.

`Ng-click` is a directive in angular to define functionality on a button or link etc

`Ng-if` is used to apply any conditional logic to the html page based on true/false. The condition within the “” of ng-if should evaluate to true/false.

`Ng-repeat` is used to iterate through a loop when there is a list of items.

`Ng-model` binds both ways so from html we can update back the variable. This can be used when we submit a form (with latest changes). 

`Ng-bind` is used to attach a variable from the client script to the html page.

## Tutorial
For this widget, suppose you are interested in seeing which incidents your team should work on resolving first in order to work most efficiently.
### Create your Widget
1. Log on to your PDI (personal developer instance) in ServiceNow. If you do not have one, sign up [here](https://developer.servicenow.com/dev.do).
![Colorful Modern Stickers Remote Learning Events and Special Interest Presentation](https://user-images.githubusercontent.com/63329562/110164545-5b9d2300-7da6-11eb-9f2e-6eb14d40c268.jpg)
2. Navigate to **Service Portal** -> **Service Portal Configuration** -> **Widget Editor** -> **Create New Widget**
3. A pop-up will appear. Name your Widget Name and Widget ID. 

![e31db13272e7462856d9bfaa0bfc1d0c](https://user-images.githubusercontent.com/63329562/110165083-38bf3e80-7da7-11eb-8f36-dfb458afaae4.png)

**Note:** You can test out your widget and see what it looks like at any time by going to a new tab using this URL: {yourInstanceUrl}/sp?id=practice_widget

4. You should now be able to see the HTML Template, Client Script, and Server Script. This will be where you will be customizing your widget.

![b615e9c237b8a71d391c8a385a8f1942](https://user-images.githubusercontent.com/63329562/110165569-f5b19b00-7da7-11eb-8513-c2011936b555.png)


### Add Server Script to Widget
1. For our Server Script, we want to query the Incident Table to find the 10 most recent active incidents that have a Priority=1. You can preview this table in your portal by navigating to **incident.list**
3. Using the template from the **Using GlideRecords to Query Tables** section, you can now create your query.
```
var incRec = new GlideRecord('incident');
incRec.addQuery('active', true);
incRec.addQuery('priority', 1);
incRec.orderByDesc('sys_created_on');
incRec.setLimit(10);
incRec.query();
data.incidentList = [];

while(incRec.next()) {
 var temp = {};
 temp.number = incRec.number.toString();
 temp.short_description = incRec.short_description.toString();
 data.incidentList.push(temp);
    }

```
### Add HTML to Widget
**Note**: Panels are bordered boxes with some padding around its elements. These are part of the Bootstrap CSS Framework that can help customize the look of your widget. 
```
<div class="panel panel-default">
  <div class="panel-heading">${Most Current Priority 1 Tickets}
   </div>
  <div class="panel-body">
   </div>
</div>
```
### Use Angular to Add Data to Widget
Based on the HTML template above, where does it make sense to put the data within the panel?
```
<table ng-repeat="incident in data.incidentList">
  <td title="incident.number">{{incident.number}} - </td>
  <td title="incident.short_description">{{incident.short_description}}</td>
</table>
```
Save your widget by pressing the Save button, or by using the hotkey ⌘+s. Congratulations! You can now preview your completed widget. 
![b2983bd93e5c1c2d58cdf1742ac32461](https://user-images.githubusercontent.com/63329562/111001166-28273f00-8338-11eb-9a93-ffc9deef4aa6.png)

*BONUS* Try these other ideas to further customize your widget:
* Add CSS to your widget to change the font, size, etc. Explore Bootstrap for more formatting options.
* Implement a searchbar to your widget.
* Implement buttons to your widget that change the value of a field when clicked.

## Other Related Articles
[Bootstrap Panels](https://www.w3schools.com/bootstrap/bootstrap_panels.asp)

[Angular Basics and Data Flow](https://www.learnnowlab.com/Service-Portal-Widgets/)

[Javascript Operators](https://docs.servicenow.com/bundle/madrid-application-development/page/script/server-scripting/concept/c_UsingGlideRecordToQueryTables.html)

[Why You Shouldn't Name Your Variable GR](https://www.youtube.com/watch?v=H_eoB6LXPrs&ab_channel=EarlDuque)
