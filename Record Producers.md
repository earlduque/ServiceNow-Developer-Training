# Creating a Complete Record Producer
Objective: learn about record producers, and server-side scripts.

Login to your Personal Developer Instance

### Create the Record Producer
1. Go to the Catalog Items table (Look for Request Catalog Configuration > Catalog Defnitions > Maintain Items)
2. Create new
3. Fill out these values:
    1. Name: [your name]'s IT Services Record Producer
    2. Table name: Case [sn_customerservice_case]
    3. Short description: A record producer designed for practicing servicenow admin fundamental skills
4. Click Submit at the bottom left
5. You've now created a record producer. Find your record producer on the Record Producers table, and select it.

### Editing the Server-Side Script
1. In your record producer, find the "What it will contain" tab (should be just below the Record Producer's fields) and make sure it's selected
2. In that tab, scroll down to the "Script" section. This is where the server-side script is (i.e. run by the backend, not the frontend)<sup>1</sup>
3. In the script, type in the following code **above** the "DO NOT MODIFY" section<sup>2,3</sup>:
```javascript
current.assignment_group = "";
current.u_organization = "";
current.service_offering = "";
current.short_description = "";
current.contact_type = "web";
current.u_case_type = "Request";
current.u_variables.display = true;
```
4. Gather the following variables and select any record's sys_id to your liking (right-click > Copy sys_id)<sup>4</sup>
    * assignment_group - (sys_user_group.list in filter navigator)
    * u_organization - (u_ucsd_organization_table.list)
    * service_offering - (service_offering.list)
    * short_description - Any string
5. Click "Try It" in the top right, fill out the form, and submit it.
6. Go to your created cases (Work > Created By Me > Cases) and find your newly created case
7. Double check that the "Assignment group", "Organization", "Service offering", and "Short description fields are filled-out. You've just created a server-side script!

Server-side scripts can get much more in-depth. You can use [ServiceNow's Glide class](https://docs.servicenow.com/bundle/paris-application-development/page/script/general-scripting/reference/r_GlideClassOverview.html) to edit databases at scale, execute server-side code directly from the client, create custom forms, etc. It is very powerful! But with great power comes with great responsibility! **Even so much as one messed up capitalization in a server-side script could ruin the whole UCSD database! Be careful, and always contact your supervisor if you're not sure a script will run as intended!**

### Mapping Variables to Case Fields
This section will introduce the creation of variables, using the GlideSystem (or ```gs```) to get logged-in user information, and mapping a variable to a field in a generated case.
1. Go to your record producer and create a new Variable
2. Setting Variables on Main Page
    * At the top of the new variable, select the "Map to field" checkbox. 
    * In the Field dropdown, find "Contact (Customer)". This will allow you to map whatever value your variable has to the "Contact (Customer)" field of the Generated Task Record (we're generating cases).
    * For Type, select Reference.
    * For Question, put "Contact of Form"
3. Navigate to the "Type Specifications" tab
    * For the "Reference" field, put "User [sys_user]". All available values for our variable should reference records from _this_ table.
4. Navigate to the "Default Value" tab
    * Put this code in the "Default value" field: ```javascript: gs.getUserID()```<sup>5</sup>
5. Click Submit in the bottom left.

Now what have you done so far? You've created a variable that will map to a field in the generated record, made it reference the user table so that, in the frontend, when the user selects your variable field, it will show a dropdown of all of the users from UCSD's user database, and you gave it a default value using some javascript code. Complicated stuff!

In the future, you'll be messing with even cooler scripts that will be able to automate many more things (you can even make a form that will send text messages to people, or make a robot send messages to your slack channel)!

### Server-Side Print-Debugging
1. For server-side print-debugging, you will have to use ```gs.info()``` and then look in System Logs > Application Logs for the information that is logged
2. A rule of thumb for ```gs.info()``` calls is to format it as ```gs.info([your name] - , ...)```. This is because, in the SNOW-Development environment, there are tons of forms printing info at the same time, so it will be impossible to find your own if you do not prepend your name to your console output. Example:
    ```javascript 
    gs.info('rickesh - ' + gs.getUser());
    ```

### Record Producer Accessibility
This section is mainly meant as a heads-up (you are not changing values on your record producer). Right now, your record producer is considered 'Unlisted'. That means that no one can access your form unless you give them the direct link to access it. Well that's kind of annoying, so let's change that:
1. Go to your Record Producer and find the "Accessibility" tab.
2. Here, you will find two fields: "Catalogs" and "Category". 
    * The catalog is the main overarching department that the record producer will belong to (e.g. Customer Services, Payroll, Customer Service, etc.).
    * Category is a sub-category that belongs to the department.
3. Although, we won't be changing these, keep in mind that this is how forms are listed and unlisted for UCSD.

### Footnotes
1. This is different from client-side scripts. Client-side scripts run in the frontend and any ```alert()``` calls for client-side print-debugging will actually be visible on the form itself. Client-side scripts will run _as an action is performed or when the form loads_. This is not true for server-side scripting. For record producers, scripts will run _after_ you submit the form. For debugging details, see Server-Side Print-Debugging
2. Variable Explanations
    * Each of these variable names can be found by going to any generated case (Case > Cases > All Cases - All Groups) and right-clicking on one of the field names. At the bottom of the context menu, you will see "Show - [variable name]"
    * Assignment Group, Organization, Service Offering, and Short Description are the most common. Don't worry about the last three for now.
3. The reason why we use ```current``` is because ```current``` refers to the newly Generated Task Record (see the field right above Script). Because we're working on the Case table (remember, you set Table name previously), when you submit your form, it will generate a case. ```current``` refers to all of the fields in the generated case, and you can edit them directly by referring to their variable name.
4. The reason why we use sys_id's instead of hard-coded names is because we don't want our code to break if an assignment group or service offering's name changes. The sys_id will reference that record regardless of name changes.
5. What is this doing? This is saying, "Use some javascript code and the GlideSystem (```gs```) to get the current logged-in user's ID. Now, although we're giving the backend the user id directly, it will first search through the user's table for that id, and then return the name of that user. 