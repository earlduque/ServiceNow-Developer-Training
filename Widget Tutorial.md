# Create a Widget Using AngularJS and GlideRecords
Objective: Learn what Angular is used for in HTML, how to query databases in server script using GlideRecords

## Table of Contents

## What is a Widget?

## AngularJS Basics

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

## Tutorial
### Create your Widget
### Add Server Script to Widget
### Add HTML to Widget
### Use Angular to Add Data to Widget

## Other Related Articles
 
