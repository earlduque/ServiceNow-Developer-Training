## Client Scripts in ServiceNow
### Overview
Client scripts are used to customize features using JS <br>
You can use scripts to run on server as well as client browsers <br>
Since servers have direct access to the database server scripts are used to modify records in the DB and generate events

Since the client has access to forms client scripts are used to tailor forms to the current user and conditions

Client Scripts can be used to configure forms, form fields and form values in real time while user is using form

Client scripts can fields hidden or visible, read-only/writable, optional/mandatory and can set the value in one field depending on other field 

Modify options in choice list depending on users role display messages based on the value in a field
powerful way to tailor a form in real time

*Note: to view all Client Scripts in your ServiceNow instance, head to **System Definition > Client Scripts** or type **"Client Scripts"** in the navigator*

a. To see client scripts for a specific form, go to incidents, click on a specific form, click on the hamburger menu on the upper left corner of the page, click **configure** and then select **client scripts**

There are a few different kinds of scripts:

* an ```onLoad()```script which controls how the form *first* appears to the user; in other words, how the page *loads*.
* an ```onChange()``` scripts which changes the form when the user changes a field, which is useful for automatically setting the value of a field, or displaying a message depending on the value(s) a user enters 
* an ```onSubmit()``` script which runs when the user submits the form, which is useful for validating values that the user entered.
* an ```onCellEdit()``` is similar to an onChange() function, except the script runs when a user changes a field on a list rather than a form.

Client Scripts interact with the system through a set of APIs (*Application Programming Interface*) 

b. Head back to list of scripts and head to client sc
c. client scripts configure forms and their fields.values thru api through api GlideForm 
call GlideForm API thru g_form to do things like: highlight area, get info or set value for field
change choices in a list

glide user api provides information about the current user through the **g_user** object

glide record API makes calls to the database on the server without having to use mySQL

example:<br>
```javascript
var gr = new GlideRecord(g_form.getTableName)
```

