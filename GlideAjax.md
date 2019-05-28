# ServiceNow GlideAjax

This tutorial will teach the fundamentals of GlideAjax and how to use it inside of ServiceNow. The purpose of GlideAjax is to allow for the scripts on the client-side to send and receive information to and from the server. An example of its uses is when we need to make a GlideRecord call in a client script.

**\*Note:** GlideAjax requires prior knowledge of JavaScript\*

---

**[Overview & Brief Explanation](#overview-and-brief-explanation)**<br>
**[Stages of GlideAjax](#stages-of-glideajax)**<br>
**[Scripting Locations](#scripting-locations)**<br>
**[GlideAjax Process](#glideajax-process)**<br>
**[GlideAjax Example](#glideajax-example)**<br>
**[Tutorial](#tutorial)**<br>
**[Conclusion](#conclusion)**

## Overview and Brief Explanation

-   It has both client side and server side components.The GlideAjax class enables a client script to call server side code in a script includes.

-   The GlideAjax API itself is a client side API, but is used to call server side in a script-includes

-   It has both client side and server side components and is similar to jQuery's AJAX method.

-   AJAX stands for "Asynchronous Javascript And XML"

-   Used to make client side requests to the server-side without requiring a "page reload", ServiceNow utilizes a browser API called XMLHttpRequest to make AJAX calls (GlideAjax calls this API to make requests, but uses a layer of abstraction)

## Stages of GlideAjax

1. Client side code calls the GlideAjax API, which is making an XMLHttpRequest behind the scenes to the server
2. Server side processes the request and returns a response
3. The client side processes the response (we have to tell the browser what to do with the information in the response from the server)

## Scripting Locations

There are two scripting locations to GlideAjax: Server side and client side.

While GlideAjax API is a client side API, we are still accessing server side code. Client script which contains GlideAjax API and methods. often times stored in client scripts or UI pages.

Server side code is stored in a script include

## GlideAjax Process

Here is an example of the GlideAjax process:

When we're on a task record like an incident, after the form loads, we want to make an AJAX request to the server side, which will update the location of the current user, leveraging the browser's geolocation API.
Once the page loads, the browser pulls in the current user's location, makes a request in the background via GlideAjax, to the server side to save that to the record

1. Client makes a request for a page that contains a client script with GlideAjax.
2. Server processes the request from the client, it sends client task form along with client script.
3. After the onLoad event occurs, the client side script is executed which calls the GlideAjax API.
4. GlideAjax accesses browser's XMLHttpRequest API and generates a request.
5. Browser's XMLHttpRequest API sends data back to ServiceNow in the background.
6. A request from the client invokes a Script include, where request data is used to call certain methods with arguments. The data is packaged up in the form of a response.
7. Browser receives response from the server side
8. Client Script callback processes returned data and updates location field on task

## GlideAjax Example

In order to help remember the differences between the Client and Server elements of a GlideAjax call, here is a simple example:

**\*Tip:** Client callable must be checked in the 'script include' in order for this to work\*

_Note: Github Markup does not support colored/highlighted test, so we will use blocks of color to differentiate between the different pieces._

-   ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) **Red:** The name of the **class** you create, which is generally the same name of the **Script Include**.

*   ![#ffa53f](https://placehold.it/15/ffa53f/000000?text=+) **Orange:** The name of the **function** used in a **script include**. A single script is able to include _multiple functions_ that accept and return different parameters. For example, one could create a _single_ **script include** for retrieving data related to users and continue adding functions to it (as needed).

-   ![#fbff44](https://placehold.it/15/fbff44/000000?text=+) **Yellow:** The parameter that is passed through the URL of the AJAX call, to which you may add more than one parameter. Generally this is information used to create a **GlideRecord call** in the **script include**.

*   ![#25ba31](https://placehold.it/15/25ba31/000000?text=+) **Green:** The function that asynchronously awaits a response. Any code that needs to _wait_ for a response _needs_ to go in the function that is called inside the **getXML()** function. Code that **does not** need to wait should go _directly after_ the **getXML()** call within the main **client script** function and **will not await a response before executing**.

-   ![#1589F0](https://placehold.it/15/1589F0/000000?text=+) **Blue:** This is the data you will need from the server. The pieces of data are added to an object in the **script include** and then passed back to the **client script**. Once these are returned, you can choose what to do with them. In this particular example they are being used to set a value on a form.

**Code Reference Chart:**

| Type                                                     | Properties            |
| -------------------------------------------------------- | --------------------- |
| ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) | `ucd_GetLocationData` |
| ![#ffa53f](https://placehold.it/15/ffa53f/000000?text=+) | `getCampus`           |
| ![#fbff44](https://placehold.it/15/fbff44/000000?text=+) | `sysparm_buildingid`  |
| ![#25ba31](https://placehold.it/15/25ba31/000000?text=+) | `updateCampus`        |
| ![#1589F0](https://placehold.it/15/1589F0/000000?text=+) | `updateCampus`        |

#### Client Script:

```javascript
function onChange(control, oldValue, newValue, isLoading) {
    if (isLoading || newValue == "") {
        return;
    }

    var ga = new GlideAjax("ucd_GetLocationData");
    ga.addParam("sysparm_name", "getCampus");
    ga.addParam("sysparm_buildingid", g_form.getValue("u_building"));
    ga.getXML(updateCampus);
}

function updateCampus(response) {
    var answer = response.responseXML.documentElement.getAttribute("answer");
    var clearvalue; // Stays Undefined

    if (answer) {
        var returneddata = JSON.stringify(answer);
        g_form.setValue("campus", returneddata.sys_id, returneddata.name);
    } else {
        g_form.setValue("campus", clearvalue);
    }
}
```

#### Server Script (Script Include):

```javascript
var ucd_GetLocationData = Class.create();

ucd_GetLocationData.prototype = Object.extendsObject(AbstractAjaxProcessor, {
    getCampus: function() {
        var buildingid = this.getParameter("sysparm_buildingid");
        var loc = new GlideRecord("cmn_location");
        if (loc.get(buildingid)) {
            var campus = new GlideRecord("cmn_location");
            if (campus.get(loc.parent)) {
                var json = new JSON();
                var results = {
                    sys_id: campus.getValue("sys_id"),
                    name: campus.getValue("name")
                };

                return json.parse(results);
            }
        } else {
            return null;
        }
    }
});
```

## Tutorial

We want to: update the short description of an incident to Hello World! when the incident form loads.

Log into your personal developer instance.

1. Go to the navigator and head to **System Definition > Script Includes**. <br>
   <img width="282" alt="screen shot 2019-02-21 at 3 33 41 pm" src="https://user-images.githubusercontent.com/6828733/53210959-769ffe80-35f4-11e9-9aaa-9fe117f80ef5.png"> <br>
2. Click **New**.<br>
3. Name the new Script Include "ServiceNowGlideAjaxTutorial". We will need to remember the exact name later.<br>

<img width="1090" alt="screen shot 2019-02-21 at 3 52 58 pm" src="https://user-images.githubusercontent.com/6828733/53211044-bd8df400-35f4-11e9-92ca-088523115c95.png"> <br>

4. Select "Client Callable" <br>
5. The **Script** field auto populates after naming the Script Include. We are then going to create a method called "sayHello" and return a "Hello World!" string. Update the code so that it looks like this:<br>
   <img width="1147" alt="screen shot 2019-02-21 at 3 54 02 pm" src="https://user-images.githubusercontent.com/6828733/53211072-d4cce180-35f4-11e9-8546-09a79b366fd5.png"> <br>
6. Click Submit.<br>
7. Be sure to copy the name of your Script Include (i.g. ServiceNowGlideAjaxTutorial) <br>
8. In the navigator head to **Client Scripts**. <br>
   <img width="279" alt="screen shot 2019-02-21 at 4 00 18 pm" src="https://user-images.githubusercontent.com/6828733/53211100-f4640a00-35f4-11e9-8e0a-926080e1a9da.png"> <br>
9. Create a new Client Script called "OnLoadHello"
10. We are going to create a new **GlideAjax object** within our **onLoad()** function with the same name as our **Script Include**. <br>
11. We'll add the name of the method we want to call and pass in the keyword `sysparm_name` and then the name of the method we created in our Script Include, `sayHello`.
12. Then we want to use **getXML()** and pass in the name of our callback function.
13. then we create the callback function and pass in `response` as an argument
14. We then need to create a variable called `answer` and assign it to the attribute we want from `response`.
15. Then we need to update our incident description field with the "Hello world!" text by using `g_form.setValue()`. Your code should now look like this: <br>
    <img width="1149" alt="screen shot 2019-02-21 at 4 06 49 pm" src="https://user-images.githubusercontent.com/6828733/53211218-47d65800-35f5-11e9-973c-8e81479ae6bf.png"><br>
16. Hit **Submit**. <br>
17. Navigate to **Incidents** and click on any incident. You should see that the short description to the incident has been changed to "Hello World!". <br>
    <img width="690" alt="screen shot 2019-02-21 at 4 52 31 pm" src="https://user-images.githubusercontent.com/6828733/53212250-20818a00-35f9-11e9-9a2c-0245db157450.png"><br>
    <img width="680" alt="screen shot 2019-02-21 at 4 52 41 pm" src="https://user-images.githubusercontent.com/6828733/53212277-3ee78580-35f9-11e9-878a-1503a9639c4d.png">

## Conclusion

This tutorial has covered the fundamentals of GlideAjax and how to go about using it. The example provided is rather basic, but covers the basis of its functionality. GlideAjax is a powerful tool and is often times one of the few ways to accomplish a task.

**Congrats! You've just completed your first GlideAjax tutorial.**
