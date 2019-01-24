# Bootstrap
Bootstrap can be thought of as an open source framework containing CSS styles, JavaScript libraries, and HTML files. Bootstrap consists of hundreds of classes that aim to make more advanced CSS and HTML functionality more accessible. This tutorial will be and introductory course in how Bootstrap can be utilized in HTML and CSS. The most important applications of Bootstrap in ServiceNow will be using it to create reactive widgets/html pages. I will not be covering basic concpets in HTML and CSS during this tutorial.

## Setup
We will begin by setting up a widget in ServiceNow so that we can play with a few Bootstrap classes. You can also use an in browser development environment, but I highly reccomend working in ServiceNow. ServiceNow is our development platform afterall.

To begin:
1. Log into the sandbox instance of ServiceNow
2. In the navigator search "Service Portal Configuartion"
3. Select Widget Editor
4. Select "Create a new widget", name it whatever and be sure to click "Create a test page"
5. Click the hamburger in the top right and hit enable preview
6. Keep the editor open and return to the sandbox home page. Search for widget in the navigator and select "Widgets" under Service Portal.
7. Select your widget and scroll to the bottom
8. Select "Included in Pages" and click on the created Test Page
9. Finally select try it in the top right and click a link

## Basic usage
A basic functionality of Bootstrap is in HTML where it's "style" can be augmented using its predefined CSS class.

```
<div class="jumbotron">
	<h1>My Page!</h1>
  <p>This uses the "jumbotron" class to create a resizable gray box</p>
</div>
```
Try putting the code above into the HTML section of the widget editor and save. The preview should display it, but an important aspect of bootstrap is that it adapts to various screen sizes. Go to the Test Page (refresh it if nothing displays) we opened previously and play with the windows size. Notice how it reacts and reshapes to the size of the window.

This is more or less how Bootstrap is used, in the following sections we will be covering a few interesting classes it offers. It's important to note that these examples are only a few use cases of Bootstrap and I encourage you to find more pertinent applications that suit your needs.

## Container

```
<div class="container-fluid bg-primary">
	<p>This is a container that will resize to the window resolution</p>
</div>
```

Add this code to our editor. Notice how it will resize with the window. *bg-primary* is a class that colors the container blue. *container-fluid* differs from *container* because it will change to match the full dimension of the window. 

## Rows and Columns
Bootstrap can be used to create dynamically resizing rows and columns in a web browser.

```
<div class="container-fluid bg-primary">
  <div class="row">
    <div class="col-sm-4 text-center">
      <h2>Cats</h2>
      <p>Tabis are cool</p>
    </div>
    <div class="col-sm-4 text-center">
      <h2>Dogs</h2>
      <p>Huskys are cool</p> 
    </div>
    <div class="col-sm-4 text-center">
      <h2>Birds</h2>
      <p>Crows are cool</p>
    </div>
  </div>
</div>
```

Try putting this code into the previously created container in our editor. Again play with it on the test page and notice how the columns stack when the browser window is not wide enough.

There's a few Bootstrap classes being utilized here. *container-fluid* is used to dynamically resize the container to the window size. *row* creates a container that can hold a row of items. *col-sm-4* creates a column entry in a row that dynamically resizes with the windows and stacks on top of each other when the window is too thin. 

Feel free to take a moment to play with these tools. What happens if you add another column? Another row?

## Buttons
Bootstrap can create a variety of button types for us.

```
<button type="button" class="btn">Basic</button>
<button type="button" class="btn btn-primary btn-lg">Colored</button>
```

Dropdown buttons are also possible through bootstrap

```
<div class="container">
	<div class="dropdown">
	    <button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
	      Dropdown button
	    </button>
	    <div class="dropdown-menu">
	      <li><a class="dropdown-item" href="google.com">One</a></li>
	      <li><a class="dropdown-item" href="somewhere.com">Two</a></li>
	      <li><a class="dropdown-item" href="hello.com">Three</a></li>
	    </div>
	</div>
</div>
```

This function utilizes *dropdown*, *dropdown-menu*, and *dropdown-item* to make a dropdown menu with Bootstrap.

# Conclusion
Bootstrap is a versatile tool kit that can create more advanced and dynamic functionality in HTML/CSS simply. A few more uses of Bootstrap includes: alerts, loading spinners, images, cards, badges, and forms. Hopefully you now have an understanding of how to Bootstrap can be used. With this knowledge, I encourage you to explore a few of the references below and see how else Bootstrap can be implemented.

## Referenes
https://hackerthemes.com/bootstrap-cheatsheet
https://www.w3schools.com/bootstrap4/bootstrap_ref_all_classes.asp
