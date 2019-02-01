# Business Rules in ServiceNow

### Table of Contents
**[What is a Business Rule?](#what-is-a-business-rule)**<br>
**[Business Rule Actions]()**<br>
**[When should I use a Business Rule](#when-should-i-use-a-business-rule)**<br>
**[Business Rule Processing Flow](#business-rule-operating-flow)**<br>
**[Creating a Business Rule](#creating-a-business-rule)**<br>


### What is a Business Rule?
____

Business Rules are server-side scripts that run by database operations (i.e. when database records are queried, updated, inserted, or deleted).

Business rules respond to database operations regardless of of access method, so it doesn't matter whether users interact with records through forms and list, web services, or data imports.

Business rules don't necessarily monitor forms, nor form fields, but *will* run if and when forms forms interact with the database when records are saved, updated or submitted.

ServiceNow offers over 2,400 out-of-the-box business rules and they're commonly used throughout the system.

Business rules give us access to:
* Current object (current)
* Previous object (previous)
* Scratchpad (g_scratchpad)

:arrow_up: *What does this mean?*
Let's say we have a Business Rule that runs when a new incident is inserted into the incident table. Think of that incident being the current object. To access the number assigned to the newly created incident, we can use ``current.number`` in a script. That's how we have access to a current object.

### Business Rule Actions
___

Business Rules can peform a variety of actions such as:
* Changing values on a form that is being updated by the user. Field values can be set to specific values available for that field, values copied from other fields, and relative values determined by the role of the user.
* Displaying information messages to the user.
* Modifying values on child tasks when changes are made to parent tasks.
* Preventing users from accessing or modifying certain form fields.
* Setting a list of condition that, if met, will abort the current database transaction, thus preventing the user from saving the record to the database.

*Administrators have the ability set field values, create information messages, and abort transactions without the need to write a script*

### When should I use a Business Rule?
___

Business rules are used for tasks like automatically changing values in form fields when specific conditions are met, or to create actions for email notifications and script actions. 

The following options provided determine the time the business rule should run:

|         Option        |       When the rule runs        |
|-----------------------|---------------------------------|
|         Before        |After the user submits the form, but before any action is taken on the record in the database|
|         After         |After the user submits the form, and after any action is taken on the record in the database|
|         Async         |When the scheduler runs the scheduled job created from the business rule, the system will create a scheduled job from the business rule after the user submits the form and after any action is taken in the database|
|        Display        |Before the form is presented to the user, just after the data is read from the database|

The database operations that the system takes on the record:

|         Option        |       When the rule runs        |
|-----------------------|---------------------------------|
|        Insert         |When a user creates a new record and the system adds it to the database|
|        Update         |When the user modifies an existing record|
|         Query         |Before a query for a record or a list of records is sent to the database. Typically you should use query for a **before business rule**|
|        Delete         |   When a user deletes a record  |



### Business Rule Operating Flow
___

Below is an example of a Business Rule operating flow:
**1.** The user sends a request to the server for a specific incident (query).<br>
**2.** Application server requests record from the database server.<br>
**3.** The database server responds to the application server with the record.<br>
**4.** The application server checks for display-business-rules, then sends the resonse back to the user. The display event will fire any existing display-business-rules.<br>
**5.** User modifies incident record and sends update request.<br>
**6.** Application server receives update, checks for before-business-rules, then sends to database server to be updated.<br>
**7.** The database server updates the record.<br>
**8.** Lastly, the application server checks for after-business-rules.<br><br>
<img width="1299" alt="screen shot 2019-01-31 at 3 16 30 pm" src="https://user-images.githubusercontent.com/6828733/52095970-fd276a00-2579-11e9-9a20-aa78e4e94c6e.png">
<br><br>
![businessruleprocessingflow](https://user-images.githubusercontent.com/6828733/52096034-33fd8000-257a-11e9-8d09-2f6512826a8d.png) <br>

### Creating a Business Rule
____

**1.** Navigate to **System Definition > Business Rules**.<br>
**2.** Click **New**.<br>
**3.** A Business Rule runs a specific table. After naming your Business Rule, choose a table you wish to modify from the **Table** list.<br>
<img width="937" alt="screen shot 2019-01-31 at 4 08 37 pm" src="https://user-images.githubusercontent.com/6828733/52094077-8044c200-2572-11e9-8fc6-6cd312b336d0.png">
<br><br>

In this example, we are looking at a Business Rule that creates an asset on an insert. The table that this Business Rule will be modifying is the Configuration Items [cmdb_ci] table. <br>
**4.** Afterwards, we have to specify *when* we want the Business Rule to run (i.e. *before* a record is inserted, *after* a record is inserted, etc.) The order will specify the order in which the Business Rule will run in.<br>
**5.** Next, you have to select the conditions under which the Business Rule will run. There are two conditions: database operations, and custom conditions. Custom conditions will either allow you to choose from the *Filter Conditions* field shown at the bottom, or using a *Condition* script field under the **Advanced** tab.<br>
<img width="915" alt="screen shot 2019-01-31 at 3 52 09 pm" src="https://user-images.githubusercontent.com/6828733/52093606-acf7da00-2570-11e9-9656-442987197269.png"><br><br>
*Note: In order to access the *Condition* script field, the **Advanced** checkbox on the upper right hand side of the form, under the **Active** checkbox*.<br>
Using the filter conditions allows you to automatically filter condition scenarios from lists they have provided (like UI policies).<br>
 If you are writing a custom script, you must specify the condition in which the Business Rule should run in the *Condition* field.<br>
 <img width="899" alt="screen shot 2019-01-31 at 4 33 36 pm" src="https://user-images.githubusercontent.com/6828733/52094942-f991e400-2575-11e9-9376-ca3db225f422.png"><br><br>
 ```(current.asset.nil()  || (current.asset.ci != current.sys_id))```
 
 In this example, the condition will only run *if* the current asset is nil, or in other words, the current CI record does not have an asset associated with it **OR** if the current asset CI does not equal with the ``current_sys_id``
 
 When the condition evaluated to true, the script underneath the condition will run.
<br>
**6.** After everything on the form has been filled out, hit **Submit**.<br>.
