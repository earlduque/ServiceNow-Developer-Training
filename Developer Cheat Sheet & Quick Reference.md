# Cheat Sheet & Quick Reference

## Keyboard Shortcuts in Studio
(For Windows: Use Ctrl key instead of Cmd) <br>

| Action               | Shortcut          |
| :------------------- |:------------------|
| Help                 | `Cmd + H`         |
| Toggle Full Screen   | `Ctrl + M`        |
| Start Searching      | `Cmd + F`         |
| Find Next            | `Cmd + G`         |
| Find Previous        | `Cmd + Shift + G` |
| Replace              | `Cmd + E`         |
| Replace All          | `Cmd + ;`         |
| Toggle Comment       | `Cmd + /`         |
| Scripting Assistance | `Ctrl + Space`    |
| Show Description     | `Cmd + J`         |

## Debugger Shortcuts

| Action                            | Shortcut      |
| :-------------------------------- | :------------ |
| Start Debugger                    | `F2`          |
| Pause Debugging                   | `SHIFT + F2`  |
| Resume Script Execution           | `F9`          |
| Step over next function call      | `F8`          |
| Step into next function call      | `F7`          |
| Step out of current function call | `SHIFT + F8`  |

## Common APIs/Code Snippets
#### Create a new record in a table
```javascript
var grIncident = new GlideRecord('incident');
grIncident.newRecord();
grIncident.short_description = 'Hello from the cheat sheet!';
grIncident.insert();
```
#### Get a record by ID
```javascript
var grIncident = new GlideRecord('incident');
if (grIncident.get('incidentSysID')) {
  // Do something!
  gs.log(grIncident.number + ': ' + grIncident.short_description);
}
```
#### Count active records using GlideAggregate
```javascript
var gaIncCount = new GlideAggregate('incident');
gaIncCount.addQuery('active', 'true');
gaIncCount.addAggregate('COUNT');
gaIncCount.query();

var count = 0; // This will hold the final count
if (gaIncCount.next()) {
  count = gaIncCount.getAggregate('COUNT');
}
```
#### Convert JS Object to JSON
```javascript
var jsonString = JSON.stringify(obj);
```
#### Convert a JSON string to JS Object
```javascript
var obj = JSON.parse(jsonString);
```
#### Look up task records in new state
```javascript
var grTask = new GlideRecord('task');
grTask.addQuery('state', '1');
grTask.query();

while (grTask.next()) {
  // Do something with each task
}
```
#### Add OR conditions to a GlideRecord query
```javascript
var grIncident = new GlideRecord('incident');
var qc = grIncident.addQuery('state', '1'); // A or B or C
qc.addOrCondition('state', '2');
qc.addOrCondition('state', '3');
grIncident.query();

while (grIncident.next()) {
  // Do something...
}

var grIncident = new GlideRecord('incident');
grIncident.addQuery('priority', '1'); // A and (B or C)
var qc = grIncident.addQuery('state', '1');
gc.addOrCondition('state', '2');
grIncident.query();

while (grIncident.next()) {
  // Do something...  
}
```
#### Commmon GlideSystem methods
```javascript
var user     = gs.getUser(); // Get current user Object
var userID   = gs.getUserID(); // Get current user's ID
var userName = gs.getUserName(); // Get current user's user_name
var groups   = gs.getUser().getMyGroups(); // Get current user's groups
var isMember = gs.getUser().isMemberOf(current.getValue('assignment_group')); // Check by GroupID
var isMember = gs.getUser().isMemberOf('Service Desk'); // Check by Group Name
var hasRole  = gs.hasRole('itil'); // Determine if current user has 'itil' role
```

## Common AngularJS Directives for using in the HTML Template
| Directive         | Purpose        |
| :---------------- | :------------- |
| `ng-model`        | This directive binds an input, select, textarea (or custom form control) to the Angular Scope       |
| `ng-repeat`       | Iterate through a data array to e.g. build a list of records or a table |
| `ng-show/ng-hide` | Evaluate an expression to determine if an element is shown |
| `ng-if`           | Evaluate an expression to determine if an element is shown (removes the element from the DOM, therefore more costly - **BUT** it will trigger a re-evaluation of the widget code, which can come in handy.) |
| `ng-class`        | Equivalent to the CSS element 'class' - count e.g. be used to assign a CSS class conditionally  |
| `ng-change`       | Triggered when the according element changes (e.g. `ng.change = "c.myChangeFunction()"`) |
| `ng-include`     | Fetches, compiles and includes an external HTML fragment (e.g. Angular template) |
| `watch`          | AngularJS record watcher - e.g. used to do something on the client when value changes on the server  |

## Service Portal Client Side Utilities
| API                              | Purpose        |
| :------------------------------- | :------------- |
| `spUtil`                         | Client side only utility. Can be used for example to add Info Messages to the page - also required for recrodWatch functionality. See [documentation](https://docs.servicenow.com/bundle/madrid-application-development/page/app-store/dev_portal/API_reference/spUtil/concept/spUtilAPI.html) for more functions available |
| `addErrorMessage/addInfoMessage` | Displays a notification message of different types (requires `spUtil` to work - e.g. `spUtil.addInfoMessage("Your order has been placed")`)  |
| `recordWatch`                    | Requires `spUtil`. Will watch a specific query on a defined table for updates, if an update happens you can respond to it in real-time. <br>Usage: `spUtil.recordWatch($scope, "incident", "active=true");`  |
| `rootScope`                      | The root scope element will e.g. let you broadcast and event to the rootScope of the page (allows communication between widgets). <br> Usage: `$rootScope.broadcastEvent("myEvent.name", parm1);` |
| console (Browser)                | Powerful utility available in both client and server. Can be used to "log" debug messages of, for exmaple, the data object |

## Service Portal Server Side Utilities
| API               | Purpose        |
| :---------------- | :------------- |
| `$sp`             | Server side only utility. Can be used, for example, to get parameters from the URL and get the GlideRecord for the current Portal. See [documentation](https://docs.servicenow.com/bundle/madrid-application-development/page/app-store/dev_portal/API_reference/GlideSPScriptableScoped/concept/c_GlideSPScriptableScopedAPI.html) for a list of all available functions. |
| console (Browser) | Powerful utility available in both client and server. Can be used to "log" debug messages. |


## References
Copied over from ServiceNow _Developer Cheat Sheet + Quick Reference_ brochure. Slight edits have been made.
