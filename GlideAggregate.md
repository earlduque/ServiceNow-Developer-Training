# GlideAggregate

Objective: Learn how to use `GlideAggregate` within ServiceNow.

## Overview

The `GlideAggregate` class is an extension of `GlideRecord`. `GlideAggregate` allows database aggregation queries like `COUNT`, `SUM`, `MIN`, `MAX`, and `AVG` to be done.

This can be helpful in creating customized reports or in calculations for calculated fields.

Note: `GlideAggregate` only works on number fields.

## Demo

To practice using `GlideAggregate` within ServiceNow:

1. Log into your personal developer instance
2. Navigate to `System Definition - Scripts - Background`
3. Copy this script into the text area:

```js
// Here is an example that gets a count of the number of records in the Incident table:

var count = new GlideAggregate("incident");
count.addAggregate("COUNT");
count.query();

var incidents = 0;
if (count.next()) {
    incidents = count.getAggregate("COUNT");
}
gs.log("Number of incidents: " + incidents);
```

5. Click the `Run script` button
6. The script will run and the result will show something like: `*** Script: Number of incidents: 680569`

You can use this process to test out different `GlideAggregate` examples.

## Additional Examples

The previous example did not include any query, since it counted all records from the Incident table.

To get a count of only active Incidents, you can add a query to a `GlideAggregate` just like how you would to a `GlideRecord`. Here's an example to get a count of the number of active incidents:

```js
var count = new GlideAggregate("incident");
count.addQuery("active", "true");
count.addAggregate("COUNT");
count.query();

var incidents = 0;
if (count.next()) {
    incidents = count.getAggregate("COUNT");
}
```

## Resources

For additional information, refer to the [GlideAggregate API](https://docs.servicenow.com/bundle/jakarta-application-development/page/app-store/dev_portal/API_reference/glideAggregateScoped/concept/c_GlideAggregateScopedAPI.html).
