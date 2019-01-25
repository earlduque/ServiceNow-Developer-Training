## Client Scripts in ServiceNow

Overview<br>
GlideForm API<br>
Types of Scripts<br>
Tutorial


### Overview
____
Client scripts are used to customize features using JavaScript <br>

You can use scripts to run on server as well as client browsers <br>

Since servers have direct access to the database server scripts are used to modify records in the DB and generate events

Since the client has access to forms client scripts are used to tailor forms to the current user and conditions

Client Scripts can be used to configure forms, form fields and form values in real time while user is using form

Some of the things that client scripts can do include:
* Place the cursor in a form field on form load
* Generate alerts, confirmations, and messages
* Populate a form field in response to another field's value
* Highlight a form field
* Validate form data
* Modify choice list options
* Hide/Show fields or sections

Modify options in choice list depending on users role display messages based on the value in a field
powerful way to tailor a form in real time

*Note: to view all Client Scripts in your ServiceNow instance, head to **System Definition > Client Scripts** or type **"Client Scripts"** in the navigator*

~~a. To see client scripts for a specific form, go to incidents, click on a specific form, click on the hamburger menu on the upper left corner of the page, click **configure** and then select **client scripts**~~
###Types of Scripts
There are a few different kinds of scripts:
<img width="339" alt="screen shot 2019-01-25 at 1 26 29 pm" src="https://user-images.githubusercontent.com/6828733/51774718-22166b80-20a8-11e9-8e1f-37461dc9ee79.png">

* an ```onLoad()```script which controls how the form *first* appears to the user; in other words, how the page *loads*.
* an ```onChange()``` scripts which changes the form when the user changes a field, which is useful for automatically setting the value of a field, or displaying a message depending on the value(s) a user enters 
<img width="518" alt="screen shot 2019-01-25 at 1 24 22 pm" src="https://user-images.githubusercontent.com/6828733/51774738-35c1d200-20a8-11e9-864d-5ccc8fa24676.png">

* an ```onSubmit()``` script which runs when the user submits the form, which is useful for validating values that the user entered.
<img width="764" alt="screen shot 2019-01-25 at 1 24 28 pm" src="https://user-images.githubusercontent.com/6828733/51774760-496d3880-20a8-11e9-839c-3c1a28ae6292.png">
* an ```onCellEdit()``` is similar to an onChange() function, except the script runs when a user changes a field on a list rather than a form. (But we don't really need to worry about this one)

Client Scripts interact with the system through a set of APIs (*Application Programming Interface*) 

~~b. Head back to list of scripts and head to client scipts~~ <br>


####GlideForm API
Client scripts configure forms and their fields.values through an api named GlideForm 
You can call GlideForm API through g_form to do things like: highlight area, get info or set value for field
change choices in a list

example:
```javascript
function onLoad() {
    g_form.removeOption('priority', '1');
}
```
Here's a list of **g_form** methods you can use which allow you to do the following:
* Draw attention: ```flash()```, ```showFieldMsg()```
* Get information: ```getValue()```, ```getReference()```
* Change a field value: ```setValue()```, ```clearValue()```
* Change a choice list: ```addOptions()```, ```clearOptions()```
* Get field information: ```getSections()```, ```isNewRecord()```
* Form actions: ```addInfoMessage()```, ```clearMessages()```

```g_user``` Glide User methods provide information about the current user through the global **g_user** object

| ```g_user``` Methods  |            Properties           |
|-----------------------|---------------------------------|
|```getClientData()```  |```firstName```                  |
|```getFullName()```    |```lastName```                   |
|```hasRole()```        |```userID```                     |
|```hasRoleExactly()``` |```userName```                   |
|```hasRoleFromList()```|                                 |
|```hasRoles()```       |                                 |

example:
```javascript
function onLoad() {
    if (g_user.hasRole('itil_admin')) {
        return;
    }
}
```

```g_record``` Glide Record methods make calls to the database on the server without having to use mySQL and uses the ```gr``` object.

example:
```javascript
function onSubmit() {
    var gr = new GlideRecord(g_form.getTableName)
    if(!gr.get(g_form.getUniqueValue())){
        return;
    }
}
```
The GlideAjax API sends work to the server using a script include with the ```ajax``` object.

example:
```javascript
function onChange(){
    if (newValue ==='') {
      return;
    }
    var ajax = new GlideAjax('AssessmentUtilsAjax');
    ajax.addParam('sysparm_metricJ_type', String(newValue));
    ajax.addParam('sysparm_name', 'GetMetricTypeTable'); 
    ajax.getXML(function(response){
        if(response){
            var table = response.responseXML.documentElement.getAttribute("answer");
            g_form.setValue('table', 'table');
        }
    })
}
```

###
