# Workflow Standards

A ServiceNow workflow is used to automate processes. A workflow is a sequence of activities, such as generating records, notifying users of pending approvals, or running scripts. Workflows contain activities that are a set of instructions, including but not limited to approvals, scripting, timers, and email notifications.  
  
### General 
- Include the Workflow: Standard Open Message at the beginning of the item workflow. 
- Include the Workflow: Standard Close Message at the end of the item workflow. 
- When possible, notifications should be created via the Create Event activity which then triggers a notification. Notification activities are also acceptable but Create Event is preferred. Do not send notifications via a Run Script activity. 
- All activities should lead to the End activity. 
- Any workflow section that is repeatable should be made into its own workflow so that it can be used as a sub-workflow in other workflows. 
 
### Good Practices for Workflow Design 
- Use the workflow validation tool provided by ServiceNow. 
- Use the workflow scratchpad. Pass data between workflow activities. 
- Use else/catch-all logic to handle exceptions 
- It is preferred that approval requirements are handled at the start of a workflow.  
- Tasks that the user cancels or skips should avoid canceling the entire Request or downstream tasks in separate and independent request items.  
- Split large or complex workflows into smaller sub-flows.  
- Using sub-flows enables unit testing and reuse. 
- Data can be passed between sub-flows using workflow inputs and return values 
 
### Workflow States 
- All RITM (Request Item) workflows should have a beginning state and an end state even if completely automated. 
- Set the RITM state to “Work in Progress” at the beginning of the workflow. 
- Set the RITM assignment group to the relevant group at the beginning of the workflow. 
- At the end of a workflow, set the RITM state to “Closed Complete.” 
- At the end of the workflow's failure path (if there is one), set the RITM state to “Closed Incomplete.” 
- “Closed Skipped” is rarely used in RITM workflows, as it means there is no work to be done. The standard is to set the RITM state to “Closed Incomplete” instead. 
- Failure paths should never cause a RITM state of “Closed Complete.”  
 
### Workflow Stages 
- If there is an Approval request, set the stage title to “Waiting for Approval.” at a minimum, it is preferred that you customize this stage to say “Waiting for approval from [group]” 
- If there is a Catalog Task, set stage names to “Fulfillment.”  Use “Fulfillment” instead of “Delivery” unless both are being used. As with Approval, it is preferred that you make the stage name more descriptive. 
- Do not use the "Request Approved" stage (this pertains to the Request Item (RITM), not the approval request. 
- Completion Paths 
- Set the last activity before End activity to “Completed” stage 
 
### Failure Paths 
- When a Catalog Task completion path exists, set the failure path to the “Request Cancelled” stage. 
- Only use the “Request Cancelled” stage for a path with no Catalog Tasks or Approvals (e.g., checking to see if the submitter of the item is authorized to submit the item). 
- Do not set additional stages for more than one failure path. 
 
### Render stages from a workflow-driven method.  
- The Stage order should be Computed. 
- Stage values and their corresponding display values must be the same. 
- Ensure that the “End” activity can never be reached earlier than any other intended activity on the workflow, as this will cause the workflow to end regardless of anything else still in progress on the workflow. 
- Ensure workflows that are completed have been published 
- In approval activities that have group approvals, utilize the “Approval - User” activity instead of the “Approval - Group” activity unless you understand the differences and need the exact functionality of the latter. 
- Wait for condition activities should wait for changes to the exact record being watched 
- It is preferred that workflows eventually reach the end activity. 

### Workflow Notifications  
- Minimize the number of notifications sent to users.
- Do not send redundant or duplicate notifications.
    - Example: Approvals generate notifications automatically from notifications configured on the approval table. Your workflow does not need to send a notification letting a user know if it has been approved or rejected. 
- Avoid hardcoding notifications. Use independent notifications. 