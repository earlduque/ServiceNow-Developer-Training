# Business Rules in ServiceNow

### Table of Contents
**[What is a Business Rule?](#what-is-a-business-rule)**<br>
**[Business Rule Actions]()**<br>
**[When should I use a Business Rule](#when-should-i-use-a-business-rule)**<br>
**[Business Rule Processing Flow](#business-rule-operating-flow)**<br>
**[Creating a Business Rule](#creating-a-business-rule)**<br>
**[]()**<br>


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



### Creating a Business Rule
____

**1.** Navigate to **System Definition > Business Rules**<br>
**2.** Click **New**<br>
**3.** A Business Rule runs a specific table. After naming your Business Rule, choose a table you wish to modify from the **Table** list.<br>
**4.** Next, you have to select the conditions under which the Business Rule will run. The first condition you must set <br>
**5.**<br>
**6.**<br>
**7.**<br>
**8.**<br>