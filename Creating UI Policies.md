
# UI Policies in ServiceNow

## What is a UI Policy?
A UI policy stands for "user interface policy". A UI policy is a rule that controls the appearance and other characteristics on a field in a form.

## What does a UI Policy do?
The purpose of UI Policies in ServiceNow are to change the behavior of forms and control and customize process flows.

UI Policies can do many things such as, for example: make specific fields on forms mandatory, dynamically hide or show fields depending on the selection of other fields, make certain fields read only, and more.

Basic UI Policies don't require the use of scripting, but for more advanced or customized options, use the **Run Scripts** option.

While client scripts can be used to perform all these actions, for faster loading times UI Policies should be used whenever possible.

*Note: ui_policy_admin role is required to make these changes*

## To create a new UI Policy

Refer to ServiceNow [documentation](https://docs.servicenow.com/bundle/london-platform-administration/page/administer/form-administration/task/t_CreateAUIPolicy.html) for more information.

1. Navigate to System UI > Policies
2. Click 'New'
3. To change the view, in **Related Links** clikc **Default View**
4. Select the table to be affected by the UI Policy.
5. Click submit.

### Just a reminder that
In order for the UI policy to work as intended, it must be set to an 'Active' state, the items in the Conditions field must evaluate to true, and the field specified in the UI policy action is present on the specified form.
