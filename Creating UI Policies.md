
# UI Policies in ServiceNow

**[What is a UI Policy?](#what-is-a-ui-policy)**<br>
**[What does a UI Policy Do?](#what-does-a-ui-policy-do)**<br>
**[Create a new UI Policy](#create-a-new-ui-policy)**<br>
**[UI Policies and Catalog Items](#creating-a-ui-policy-on-a-catalog-item)**<br>
**[Things to Try](#things-to-try)**<br>
**[Videos and Related Content](#videos-and-related-content)**


## What is a UI Policy?
A UI policy stands for "user interface policy". A UI policy is a rule that controls the appearance and other characteristics on a field in a form.

## What does a UI Policy do?
The purpose of UI Policies in ServiceNow are to change the behavior of forms and control and customize process flows.

UI Policies can do many things such as, for example: 
* Make specific fields on forms mandatory
* Dynamically hide or show fields depending on the selection of other fields 
* Make certain fields read only,
* And more

Basic UI Policies don't require the use of scripting, but for more advanced or customized options, use the **Run Scripts** option.

While client scripts can be used to perform all these actions, for faster loading times UI Policies should be used whenever possible.

*Note: ```ui_policy_admin``` role is required to make these changes*

## Create a new UI Policy

Refer to ServiceNow [documentation](https://docs.servicenow.com/bundle/london-platform-administration/page/administer/form-administration/task/t_CreateAUIPolicy.html) for more information.

**1.** Navigate to **System UI > Policies**.<br>
**2.** Click **New**.<br>
**3.** To change the view, in **Related Links** click **Default View**.<br>
**4.** Select the table to be affected by the UI Policy.<br>
**5.** Click submit.<br>    

*Just a reminder* that in order for the UI policy to work as intended: 
* It must be set to an 'Active' state
* The items in the Conditions field must evaluate to true
* The field specified in the UI policy action is present on the specified form

## Creating a UI Policy on a Catalog Item

**1.** To make a UI Policy for a Catalog Item, scroll down to the bottom of the Catalog Item and click **Catalog UI Policies.*<br>
<img width="1169" alt="screen shot 2019-01-23 at 2 22 19 pm" src="https://user-images.githubusercontent.com/6828733/51641253-873c5680-1f1a-11e9-8351-d8ea5c0cfc59.png"><br>
**2.** Click **New**.<br>
<img width="276" alt="screen shot 2019-01-23 at 2 26 55 pm" src="https://user-images.githubusercontent.com/6828733/51643937-29f8d300-1f23-11e9-9ae7-a40b5413112d.png"><br>
**3.** Make sure that it applies to Catalog Item, not a Variable Set.<br>
**4.** Provide a short description of what your UI Policy is meant to do.<br>
**5.** Choose a set a conditions that evaluates to true (form field, filter condition, 'OR' field).<br>
<img width="832" alt="screen shot 2019-01-23 at 3 29 44 pm" src="https://user-images.githubusercontent.com/6828733/51644184-32054280-1f24-11e9-8afa-c856643d5d73.png"><br>
**6.** Make sure to set the appropriate order for the UI Policy (it automatically sets it at 100).<br>
**7.** Make sure to check/uncheck options that control when the UI Policy is applied: (Applies on Catalog Item View, Applies on Catalog Tasks, Requested Items, On Load, and Reverse if False).<br>
<img width="1136" alt="screen shot 2019-01-23 at 3 29 49 pm" src="https://user-images.githubusercontent.com/6828733/51644350-ba83e300-1f24-11e9-8663-5fc3cf7fbeb6.png"><br>
**8.** If further customization is required, click on the **Scripts** tab next to **When to Apply** tab, and check the **Run Scripts** box.<br>
<img width="1161" alt="screen shot 2019-01-23 at 3 39 54 pm" src="https://user-images.githubusercontent.com/6828733/51644487-2a926900-1f25-11e9-858e-1baf876294e4.png">
**9.** Make sure to check that the appropriate selection is chosen under the *Run Scripts in UI* list (generally we select the All option).<br>
**10.** Enter scripts to execute of UI Policy conditions evaluate to *True* or *False* (i.e. setting up an error message when the user attempts to enter an invalid response to a field).<br>
**11.** Before you submit, be sure that the UI Policy is set to **Active**.<br>
**12.** Submit.


## Things to try
* Requiring certain fields to be mandatory
* Dynamically hiding/Showing certain fields depending on the selections the user makes
* Making a field mandatory after a user selects an option



## Videos and Related Content
[ServiceNow Training Part - 10 (Client Script & UI Policy)](https://www.youtube.com/watch?v=1GIdGNuNZRI) <br>
[New UI Policy functionality in ServiceNow London Release](https://www.youtube.com/watch?v=Qem95_fJzN0) <br>
[Creating UI Policies In ServiceNow](https://www.youtube.com/watch?v=JVtooXnOwFc) <br>
[15. ServiceNow UI Policy - Use Cases with Solution](https://www.youtube.com/watch?v=C4St-ZIFZy4) <br>
[ServiceNow UI Policy Action Tutorial | ServiceNow Tutorial For Beginners | What is AIX ? - ExcelR](https://www.youtube.com/watch?v=WFZfWB1LOGs)

