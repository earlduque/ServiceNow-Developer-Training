# Business Rules in ServiceNow

### Table of Contents
What is a Business Rule?






### What is a Business Rule?
____

JavaScript that runs on the server.

Business Rules are server-side scripts that run by database operations (i.e. when database records are queried, updated, inserted, or deleted).

Business rules respond to database operations regardless of of access method, so it doesn't matter whether users interact with records through forms and list, web services, or data imports.

Business rules don't necessarily monitor forms, nor form fields, but *will* run if and when forms forms interact with the database when records are saved, updated or submitted.

ServiceNow offers over 2,400 out-of-the-box business rules and they're commonly used throughout the system.

Business rules give us access to:
* Current object (current)
* Previous object (previous)
* Scratchpad (g_scratchpad)

:arrow_up: *What does this mean?*
Let's say we have a Business Rule that runs when a new incident is inserted into the incident table. Think of that incident being the current object. To access the number assigned to the newly created incident, we can use current.number in a script. That's how we have access to a current object.

### When should I use a Business Rule?

Business rules are used for tasks like automatically changing values in form fields when specific conditions are met, or to create actions for email notifications and script actions. 

