# Client Scripts in ServiceNow
## Table of Contents 
**[Overview](#overview)**<br>
**[Types of Scripts](#types-of-scripts)**<br>
**[GlideForm API](#glideform-api)**<br>
<<<<<<< HEAD
**[Tutorial](#tutorial)**<br>
**[Other Things to Try](#other-things-to-try)**
=======
**[Tutorial](#tutorial)**
>>>>>>> d8ddaede16a2bdc261dfeab14900fba4e7a00777


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


### Types of Scripts
There are a few different kinds of scripts:
<img width="339" alt="screen shot 2019-01-25 at 1 26 29 pm" src="https://user-images.githubusercontent.com/6828733/51774718-22166b80-20a8-11e9-8e1f-37461dc9ee79.png">

* an ```onLoad()```script which controls how the form *first* appears to the user; in other words, how the page *loads*.
* an ```onChange()``` scripts which changes the form when the user changes a field, which is useful for automatically setting the value of a field, or displaying a message depending on the value(s) a user enters 
<img width="518" alt="screen shot 2019-01-25 at 1 24 22 pm" src="https://user-images.githubusercontent.com/6828733/51774738-35c1d200-20a8-11e9-864d-5ccc8fa24676.png">

* an ```onSubmit()``` script which runs when the user submits the form, which is useful for validating values that the user entered.
<img width="764" alt="screen shot 2019-01-25 at 1 24 28 pm" src="https://user-images.githubusercontent.com/6828733/51774760-496d3880-20a8-11e9-839c-3c1a28ae6292.png">
* an ```onCellEdit()``` is similar to an onChange() function, except the script runs when a user changes a field on a list rather than a form. (But we don't really need to worry about this one)

Client Scripts interact with the system through a set of APIs (*Application Programming Interface*) 

<br>


<<<<<<< HEAD
###GlideForm API
=======
### GlideForm API
>>>>>>> d8ddaede16a2bdc261dfeab14900fba4e7a00777
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

### Tutorial

*Here is a tutorial on making your first client script using JavaScript and the GlideForm API. We are just going to do some simple date validation.*

**1.** Make sure you use either your **Sand** or **Learn** environment before continuing onto the next step.<br>
**2.** In your navigation bar, search for "Maintain Items" and head to that page.
**3.** Create a new Catalog Item called "About Me" (you can name it something else if you'd like)
<br>**4.** Fill out the short description and hit 'Submit'
<br>**5.** Create two new variables to start: Full Name (type: Single Line Text) and Birthdate (type: Date)
<br>**6.** After creating your new variables, scroll down to the bottom of the page and select **Catalog Client Scripts**
<br>**7.** Select **New**
<img width="872" alt="screen shot 2019-01-30 at 12 22 16 pm" src="https://user-images.githubusercontent.com/6828733/52010179-b65a4700-2489-11e9-8358-8f1f00aac65f.png">
**8.** Make sure to select "Mobile/Service Portal" 
<img width="375" alt="screen shot 2019-01-30 at 12 06 44 pm" src="https://user-images.githubusercontent.com/6828733/52009759-92e2cc80-2488-11e9-988d-54a12a999167.png">
<br>**9.** We're going to create an ```onChange()``` client script to verify that the user filling out the form selects a date in the past. So on the upper right side of the form, select ```onChange()``` under the **Type** field.
<br>**10.** Select the birthdate **variable** you created earlier <br>
<img width="425" alt="screen shot 2019-01-30 at 12 06 14 pm" src="https://user-images.githubusercontent.com/6828733/52009792-a2faac00-2488-11e9-9069-7a13baf425fd.png">
<br>**11.** Make sure 
<br>**12.** After ```onChange()``` has been selected, the **Script** field should automatically be filled with a generic ```onChange()``` function. If not, copy and paste the following code:

```javascript
function onChange(control, oldValue, newValue, isLoading) {
   if (isLoading || newValue == '') {
      return;
   }

   //Type appropriate comment here, and begin script below
   
}

```
<br>**13.** Since we need to access a form value, we are going to use the **g_form** API we mentioned earlier. Underneath the closing bracket of the **if** statement, create a new variable (here we are calling it *dat*) and assign it to a ```g_form.getValue()``` method which selects the ```birthdate``` variable in order to access the value selected by the user, like this:
```javascript
var dat = g_form.getValue('birthdate');
```
<br>**14.** Since we need to compare ```Date()``` objects, we next need to declare a new variable called ```bday```  and assign it to a new ```Date()``` object which takes ```dat``` as an argument.
<br>**15.** Next, we need to make sure that the date selected is not a future date, since you obviously were not born in the future. So now we create a new variable called ```today ``` and assign it to a a new ```Date()``` object as well. If given no arguments, the JavaScript ```Date()``` object defaults to the current date: ```	var today = new Date();```
<br>**16.** Next, we need an **if** statement which takes a condition that compares the two ```Date()``` objects. This is done to check if the ```bday``` value is less than ```today``` in order to see if the birthdate is a future date, which is not an acceptable value.
<br>**17.** Inside the **if** statement, we want to a window pop up to alert the user that the date they've selected an invalid date if the **if** statement condition evaluates to **true**. The ```alert()``` window should read something like this: "The date selected is in the future, please select a date in the past"
<br>**18.** Next, we want to reset the **Birthdate** field since we need the user to reselect a new date. Again, we are going to use the **g_form** API to **set** the ```birthdate``` value to **empty** by using g_form's ```setValue()``` method. ```setValue``` takes two arguments, the first being the *variable* of which you wish to set, the second argument being the *value* you wish to set the variable *to*. By now your code should resemble this:
```javascript
function onChange(control, oldValue, newValue, isLoading) {
	if (isLoading || newValue == '') {
		return;
	}
	var dat = g_form.getValue('birthdate');
	var bday = new Date(dat);
	var today = new Date();
	if(bday > today) {
		alert('The date selected is in the future, please select a date in the past');
		g_form.setValue('birthdate', '');
	} 
}
```
<br>**19.** Now, click **Update & Exit**. This should redirect you to your Catalog Item.
<br>**20.** On the upper right corner of the page, click **Try It**
<br>**21.** Fill out the **About Me** form and try to choose a future date as your birthday.
<br>**22.** You should see an alert window tell you that your choice is invalid. When you close the alert message, you should see that the **Birthdate** field has been set to empty.
<br> 
##### Congratulations! You've just created your first client script.

#### Other things to try:
* Adding a few more fields and creating an ``onLoad()`` that autofills the user and email fields.
* Instead of having a date validation ``onChange()`` script, make it so that the date is validated until the form is submitted using an ``onSubmit`` script.
* Use ``onSubmit()`` to produce a pop up window asking if the user is sure that they want to submit the form. Only submit if the user selects "Yes".
* Depending on a previously selected value, modify the options on a list of a following field.
* Produce an error message using ``onChange()`` (instead of a pop up) alerting the user that their selection/input is invalid.



