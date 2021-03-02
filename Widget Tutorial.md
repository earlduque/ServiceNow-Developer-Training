# Create a Widget Using AngularJS and GlideRecords
Objective: Learn what Angular is used for in HTML, how to query databases in server script using GlideRecords

## Table of Contents

## What is a Widget?
A widget is a reuseable components which make up the functionality of a portal page and allow users to interact with the service portal and displays information. There are six parts to a widget: HTML, CSS, Client Script, Server Script, Link Function, Options. We will only be focusing on HTML, Client and Server Scripts, and CSS for this tutorial. 

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
### Create your Widget
### Add Server Script to Widget
### Add HTML to Widget
### Use Angular to Add Data to Widget

## Other Related Articles
 
