# Use CSS within ServiceNow Widgets

Objective: learn how CSS interacts with HTML, how to use CSS within widgets, and the best practices of CSS

## Table of Contents

1. [CSS Basics](#CSS-Basics)
2. [Create the Widget](#Create-the-Widget)
3. [Widget View](#Widget-View)
4. [Add HTML to Your Widget](#Add-HTML-to-Your-Widget)
5. [Add CSS to Your Widget](#Add-CSS-to-Your-Widget)
6. [Resources](#Resources)
7. [Best Practices](#Best-Practices)

## CSS Basics

Cascading Style Sheets (CSS) is a stylesheet language used to describe the
presentation of a document written in HTML. It describes how elements should be
rendered on screen. CSS is used for example, to alter the font, color, size and spacing of your content, split it into multiple columns, or add animations and
other decorative features.

The basic structure of a CSS statement is:

```css
selector {
    property: value;
}
```

In CSS, selectors are used to target the HTML elements on our widgets that we
want to style. There are a wide variety of CSS selectors available, allowing for
fine grained precision when selecting elements to style.

## Create the Widget

Login to the sandbox with your admin credentials via the side door:
https://ucdavisietsand.service-now.com/side_door.do

1. Go to the Service Portal Configuration: https://ucdavisietsand.service-now.com/sp_config
2. Click on Widget Editor
3. Click on "Create a new widget"
4. Name your widget: [your name] Test Widget
5. Select "Create test page"
6. Hit submit
7. Your widget is created!

## Widget View

Only show HTML Template and CSS - SCSS, since Client Script and Server Script
are outside the scope of this tutorial.

Enable preview on your widget by clicking on the 3-bar hamburger menu on the
right and checking "Enable Preview". This will allow you to see what your widget
looks like after you hit Save to whatever changes you've made.

Your widget view should look something like this:
![Initial Widget View](https://github.com/earlduque/ServiceNow-Developer-Training/blob/master/images/initial-widget-view.png)

## Add HTML to Your Widget

Replace the code in HTML Template with this:

```html
<div>
    <h1>Hello, World!</h1>
    <p>
        Cat ipsum dolor sit amet, lick yarn hanging out of own butt pretend you
        want to go out but then don't so jump off balcony, onto stranger's head
        yet i like fish. Jump five feet high and sideways when a shadow moves
        love you, then bite you why use post when this sofa is here spot
        something, big eyes, big eyes, crouch, shake butt, prepare to pounce.
    </p>
</div>

<div>
    <h3>Shopping List:</h3>
    <ul>
        <li>Bananas</li>
        <li>Potatoes</li>
        <li>Rice</li>
    </ul>
    <h3>To Do List:</h3>
    <ol>
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
    </ol>
</div>

<div>
    <p>
        Cat ipsum dolor sit amet, lick <span>yarn</span> hanging out of own butt
        pretend you want to go out but then don't so jump off balcony, onto
        stranger's head yet i like
    </p>
</div>

<a href="#">Link 1</a> <a href="#">Link 2</a> <a href="#">Link 3</a>
```

## Add CSS to Your Widget

### Select by Type

Let's change the text color of "Hello, World!" to red. To do this, we need to
select the `h1` element, and change the `color` property to a `red` value.

Replace the code in CSS - SCSS with this:

```css
h1 {
    color: red;
}
```

Save your widget. The text color of "Hello, World!" should now be red.

Add this statement to your CSS:

```css
div {
    background: pink;
}
```

Save your widget. This changed the background of all of the `div` elements to
pink.

Using elements like `h1`, `h2`, or `p` as a selector is the most generic way to
target HTML elements. Selecting by type means that all elements of
that type will have the specified property.

While this is the easiest way to add CSS to an HTML element, it isn't ideal if,
for example, you would only want one `h1` element to be red. To solve this
problem, you would need to use a more specific CSS selector.

### Select by Class

Add the class `hello` to the first `div` of your HTML:

```html
<div class="hello">...</div>
```

To select by class, you would use this structure:

```css
.class {
    property: value;
}
```

Add this to your CSS:

```css
.hello {
    border: 3px solid blue;
}
```

Save your widget. A blue border should now appear around the first `div`.

Multiple elements in a document can have the same class value, so it's good to
use classes when you want to reuse CSS styles.

### Select by ID

The ID selector consists of a hash/pound symbol (#), followed by the ID name of
a given element. It's the most efficient way to select a single element.

**An ID name must be unique in the document!**

```css
#id {
    property: value;
}
```

Add the id `special` to the second `div` element of your HTML:

```html
<div id="special">...</div>
```

Add this to your CSS:

```css
#special {
    font-size: 30px;
}
```

Save your widget. The font-size of the lists in the second `div` should now be
30px.

### Pseudo-Selectors

These don't select elements, but rather certain parts of elements, or elements
only in certain contexts.

A CSS pseudo-class is a keyword added to the end of a selector, preceded by a
colon (:), which is used to specify that you want to style the selected element
but only when it is in a certain state. For example, you might want to style a
link element only when it is being hovered over by the mouse pointer.

The structure of a pseudo-selector is like:

```css
selector:class {
    property: value;
}
```

Add this to your CSS:

```css
a:hover {
    color: red;
}
```

Save your widget. Now, when you hover over the links at the bottom, they will
change to a red color.

### Combinators and Groups of Selectors

Using one selector at a time is useful, but can be inefficient in some
situations. CSS selectors become even more useful when you start combining them
to perform fine-grained selections. CSS has several ways to select elements
based on how they are related to one another. Some common relationships are
expressed as follows (A and B are any selector from above):

| Name                        | Syntax | Select                                                                                                                             |
| --------------------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| Group of selectors          | A, B   | Any element that matches A and/or B                                                                                                |
| Descendant combinator       | A B    | Any element matching B that is a **descendant** (child, child of child, etc.) of A                                                 |
| Child combinator            | A > B  | Any element matching B that is a **direct** child of A                                                                             |
| Adjacent sibling combinator | A + B  | Any element matching B that is the next **sibling** of an element matching A (the next child of the same parent)                   |
| General sibling combinator  | A ~ B  | Any element matching B that is one of the next **siblings** of an element matching A (one of the next children of the same parent) |

Let's go through these one-by-one to see how they work.

#### Groups of Selectors

You can write groups of selectors separated by commas to apply the same rule to multiple sets of selected elements at once.

Add this to your CSS:

```css
ul,
ol {
    color: purple;
}
```

Save your widget and notice how both the bulleted and numbered lists turned purple.

#### Descendent Combinator

This selector combines two selectors such that elements matched by the second selector are selected if they have an ancestor element matching the first selector.

Add this to your CSS:

```css
ul li {
    text-decoration: underline;
}
```

This statement will make all `li` elements that are descendants of `ul` elements be underlined. Save your widget and notice how the Shopping List is underlined, but the To Do List is not.

#### Child Combinator

Elements matched by the second selector must be the immediate children of the elements matched by the first selector. This is stricter than the descendant combinator, which matches all elements matched by the second selector for which there exists an ancestor element matched by the first selector.

Add this HTML inside of your `#special div` underneath the `ol` :

```html
<div><h3>h3 nested in a div, so not the immediate child of #special</h3></div>
```

Now add this CSS:

```css
#special > h3 {
    color: DodgerBlue;
}
```

Save your widget. Notice how only the `h3` elements "Shopping List" and "To Do List" changed colors, since they are immediate children of the `#special div`.

#### Adjacent Sibling Combinator

This selector matches the second element only if it immediately follows the first element, and both are children of the same parent element.

Add this CSS:

```css
a + a {
    font-size: 20px;
}
```

This statement means for any `a` tag that immediately follows another `a` tag, make the font-size 20px. Save your widget. Notice how the second and third `a` tags now have a font-size of 20px.

#### General Sibling Combinator

This selector matches the second element only if it follows the first element (though not necessarily immediately), and both are children of the same parent element.

Add this to your HTML underneath the links:

```html
<div>
    <span>This is not red.</span>
    <p>Here is a paragraph.</p>
    <code>Here is some code.</code> <span>And here is a red span!</span>
    <code>More code...</code> <span>And this is a red span!</span>
</div>
```

Add this CSS:

```css
p ~ span {
    color: red;
}
```

This statement will make all `spans` that follow `p` elements (not immediately in this case) red. Save your widget to see that this happens.

### Advanced Declarations

#### Multiple Classes

Add this to the end your HTML:

```html
<h2 class="class1">I'm only class1</h2>
<h2 class="class2">I'm only class2</h2>
<h2 class="class1 class2">I have class1 and class2!</h2>
```

In this example, we defined two classes for the last `h2` at the same time. `class1` and `class2` are separate CSS classes, and both of their properties will be applied to this `h2`.

Add this CSS:

```css
.class1 {
    color: darkorange;
}

.class2 {
    border: 10px dotted teal;
}
```

Save your widget. Notice how the last `h2` has both the color and border properties applied to it, compared to the other `h2`s with only a single property (since they only have one class).

What if you want the change the background color of the last `h2` without changing the styles of the other `h2`s? In this case, you want to select the last `h2` element by using the multiple class selector.

To select an HTML element with multiple classes, you use this structure:

```css
.class1.class2 {
    property: value;
}
```

This means to select all elements that have class1 and class2.

Add this to your CSS:

```css
.class1.class2 {
    background: black;
}
```

Save your widget and see how the last `h2` now has a black background.

#### Universal Selector

The syntax of the universal selector is:

```css
* {
    property: value;
}
```

This selector matches elements of any type, meaning that it selects all of the elements on the widget.

To see how it works, add this to your CSS:

```css
* {
    font-family: fantasy;
}
```

Save your widget and notice how the font of everything changed to `fantasy`.

### Final Widget

Here's what your final widget should look like as a reference:

HTML code:

```html
<div class="hello">
    <h1>Hello, World!</h1>
    <p>
        Cat ipsum dolor sit amet, lick yarn hanging out of own butt pretend you
        want to go out but then don't so jump off balcony, onto stranger's head
        yet i like fish. Jump five feet high and sideways when a shadow moves
        love you, then bite you why use post when this sofa is here spot
        something, big eyes, big eyes, crouch, shake butt, prepare to pounce.
    </p>
</div>

<div id="special">
    <h3>Shopping List:</h3>
    <ul>
        <li>Bananas</li>
        <li>Potatoes</li>
        <li>Rice</li>
    </ul>
    <h3>To Do List:</h3>
    <ol>
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
    </ol>
    <div>
        <h3>h3 nested in a div, so not the immediate child of #special</h3>
    </div>
</div>

<div>
    <p>
        Cat ipsum dolor sit amet, lick <span>yarn</span> hanging out of own butt
        pretend you want to go out but then don't so jump off balcony, onto
        stranger's head yet i like
    </p>
</div>

<a href="#">Link 1</a> <a href="#">Link 2</a> <a href="#">Link 3</a>

<div>
    <span>This is not red.</span>
    <p>Here is a paragraph.</p>
    <code>Here is some code.</code> <span>And here is a red span!</span>
    <code>More code...</code> <span>And this is a red span!</span>
</div>

<h2 class="class1">I'm only class1</h2>
<h2 class="class2">I'm only class2</h2>
<h2 class="class1 class2">I have class1 and class2!</h2>
```

CSS code:

```css
h1 {
    color: red;
}

div {
    background: pink;
}

.hello {
    border: 3px solid blue;
}

#special {
    font-size: 30px;
}

a:hover {
    color: red;
}

ul,
ol {
    color: purple;
}

ul li {
    text-decoration: underline;
}

#special > h3 {
    color: Dodgerblue;
}

a + a {
    font-size: 20px;
}

p ~ span {
    color: red;
}

.class1 {
    color: darkorange;
}

.class2 {
    border: 10px dotted teal;
}

.class1.class2 {
    background: black;
}

* {
    font-family: fantasy;
}
```

![Final Widget View](https://github.com/earlduque/ServiceNow-Developer-Training/blob/master/images/final-widget-view.png)

## Resources

Whenever you're stuck on a CSS problem, these resources will probably have the
answer:

-   https://developer.mozilla.org/en-US/docs/Web/CSS
-   https://css-tricks.com/

## Best Practices

1.  Make it Readable

    Good readability of your CSS makes it easier to maintain.

    You could write your CSS like this, with everything on one line:

    ```css
    /* Ignore the second comment. I use the Prettier extension which automatically formats code, but I don't want this code to be formatted to show how unreadable / ugly it is */
    /* prettier-ignore */
    .example {
        background: red; padding: 2em; border: 1px solid black;
    }
    ```

    However, this is hard to read. The best practice is to write each style on its own line like so:

    ```css
    .example {
        background: red;
        padding: 2em;
        border: 1px solid black;
    }
    ```

2.  Organize your CSS in a Top-Down Format

    It is helpful to organize your CSS in a way that lets you quickly and easily find elements of your code. A "Top-Down" format is ordered like so:

    1. Generic elements first (`body`, `a`, `p`, `h1`, etc.)
    2. `.header`
    3. `.nav-menu`
    4. `.main-content`
    5. `.footer`

3.  Combine CSS Elements

    Elements will likely share the same style properties. For example, you might have an `h1` and an `h2` with these styles:

    ```css
    h1 {
        font-family: verdana;
        color: #e1e1e1;
    }

    h2 {
        font-family: verdana;
        color: #e1e1e1;
    }
    ```

    To avoid repeating code, it is best to combine these elements like so:

    ```css
    h1,
    h2 {
        font-family: verdana;
        color: #e1e1e1;
    }
    ```

4.  Use Appropriate Naming Conventions

    CSS allows you to separate the styling and design of the elements from the content of them. You can change the entire design of a widget just by changing the CSS, without changing the HTML.

    So, it's best not to give your CSS classes and ids limiting names. The naming of your CSS elements is based on what they are, not what they give the impression of being like. For example, it's better to use the name `.post-title`, rather than `.post-large-font`.

5.  Avoid Inline Styling

    Inline styles are when you declare the CSS within the HTML. For example,

    ```html
    <p style="background:#ccc; color:#000; border: solid black 1px;"></p>
    ```

    If you had to only use inline styles, your widgets would quickly become bloated and very hard to maintain. This is because inline styles must be applied to every element you want them on. So, the best practice is to keep your HTML and CSS code separate.

6.  Shorthand CSS

    Shorthand CSS allows you to define the same styles in less code. Most properties have shorthand definitions. For example,

    ```css
    img {
        margin-top: 5px;
        margin-right: 10px;
        margin-bottom: 5px;
        margin-left: 10px;
    }
    ```

    is the same as

    ```css
    img {
        margin: 5px 10px;
    }
    ```

    with shorthand notation.

7.  Don't Use `!important`

    When an `!important` rule is used on a style declaration, it overrides any other declarations. This is generally bad practice and should be avoided since it makes debugging more difficult by breaking the natural cascading of your CSS rules.

    It's better to find out why the CSS selector you're trying isn't working than to use a quick fix like `!important`.

8.  Em, Rem, and Pixel

    Some of the units you can style your elements with are `em`, `rem`, and `pixel`. Which one should you use?

    There aren't any specific rules about which ones you should use, but in general:

    | Type | About                                                                                          | Use Case                                                                                                    |
    | ---- | ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
    | em   | The value of 1 em is relative to the font-size of the direct parent                            | em is great for responsiveness                                                                              |
    | rem  | Relative to the font-size of the `<html>` element                                              | Easy to scale all headings and paragraphs on the page                                                       |
    | px   | Pixels give you the most precision but don't offer any scaling when used in responsive designs | They are reliable, easy to understand, and present a good visual connection between value and actual result |
