# ServiceNow GlideAjax
This tutorial will teach the fundamentals of GlideAjax and how to use it inside of ServiceNow. The purpose of GlideAjax is to allow for the scripts on the client-side to send and receive information to and from the server. An example of its uses is when we need to make a GlideRecord call in a client script.

## Setup
Navigate to *Script Include* and create a new one. Write a Name and check *Client callable* the script section should now autofill to something like:
```
var TestAjax = Class.create();
TestAjax.prototype = Object.extendsObject(AbstractAjaxProcessor, {

    type: 'TestAjax'
});
```
This will be the script that houses functions that can be called in our client scripts.

Next create a new catalog item. Add a new single line text variable and a new on change catalog client script selecting the previous variable. From this foundation we will practice GlideAjax.

## GlideAjax
Next we will practice calling a basic script include.
```
var TestAjax = Class.create();
TestAjax.prototype = Object.extendsObject(AbstractAjaxProcessor, {
    practiceFunc:function(){
      return "Hello " + this.getParameter("sysparm_testname") + "!";
    },
    type: 'TestAjax'
});
```

This will be the script include that is called in our client script.
```
function onChange(control, oldValue, newValue, isLoading) {
      if (isLoading || newValue == '') {

              return;

      }
      var ga = new GlideAjax('TestAjax');
      ga.addParam('sysparm_name', 'practiceFunc');
      ga.addParam('sysparm_testname', g_form.getValue("test"));
      ga.getXML(updateFunc);
}
```

This is the basics of our ajax call. We begin by creating a new GlideAjax object providing it with the name of our script include. Next we add the param for *sysparm_name* which will be the name of the function we want to call in our script include. Lastly, *sysparm_testname* is the name of the parameter passed into the function. *ga.getXML* is the call that will execute the script include and *updateFunc* is callback function.

Next in our client script we will have
```
  function updateFunc(response) {
    var answer = response.responseXML.documentElement.getAttribute("answer");
    alert(answer)
  }
```

Now hit try it and fill in the single line variable name. When you click off you should be met with an alert message. This means our basic GlideAjax worked! This is the basic format of script includes. Now we can do more complicated things like calling GlideRecord in our script include function and returning its contents. 


## Conclusion
This tutorial has covered the fundamentals of GlideAjax and how to go about using it. The example provided is rather basic, but covers the basis of its functionality. GlideAjax is a powerful tool and is often times one of the few ways to accomplish a task.