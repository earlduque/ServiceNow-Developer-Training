# Catalog Items within ServiceNow

Objective: learn about catalog items, variable sets, variables, UI policies, client scripts, workflows and request items.

Login to your personal developer instance.

## Create the Catalog Item

1. Go to the Catalog Items table (Look for Service Catalog > Open Records > Maintain Items)
2. Hit the "New" button
3. Fill out these values:
    - Name: Tutorial Item
    - Availability: Desktop and Mobile
    - Short description: My test catalog item
4. Right click the header and select "Save"

Your catalog item is now created!

## Add Variable Sets

Variable sets allow you to create a collection of structured variables that can be reused across multiple catalog items. Using variable sets saves time because you do not have to create the same variables individually for many catalog items. From the other Catalog Items tutorial, you saw the "Contact Information" and "Additional Information" variable sets as examples.

To start, your personal instance might not have the "Variable Sets" tab in the Related Lists section at the bottom of the page.

To fix this:

1. Click on the black hamburger menu at the top bar.
2. Go to Configure > Related Lists.
3. Scroll down in the "Available" section until you find "Variable Sets".
4. Select "Variable Sets" and hit the "Add" button (the right arrow).
5. Hit the "Save" button.

You should now be able to add variable sets to your catalog item.

From the Variable Sets tab, click on the "Edit" button and add the "Standard Employee Questions" variable set to your catalog item.

Hit the "Try It" button to preview what your catalog item looks like so far. You should see something like this:
![first-try-it]()

## Add Variables

Service catalog variables allow you to gather information from users. There are many different types of variables you will use when creating catalog items. Here's some of the most common ones:

| Variable         | Functionality                                                                                               |
| ---------------- | ----------------------------------------------------------------------------------------------------------- |
| Check box        | Enable / disable options by selecting and clearing it                                                       |
| Container start  | Define a layout for a container that can hold more variables. This is the start point of a container layout |
| Container end    | The end point of a container layout to close the container                                                  |
| Multi-line text  | Field that lets you enter multiple lines of text                                                            |
| Multiple Choice  | Creates radio buttons for question choices                                                                  |
| Reference        | References a record in another table                                                                        |
| Single-line text | Field to enter a single line of text                                                                        |
| Yes/No           | Choice list with **Yes** and **No** as options                                                              |

Start by adding a Container Start variable to your catalog item:

1. Go to the Variables Tab
2. Click on the "New" button
3. Fill out these values:
    - Type: Container Start
    - Display title: checked
    - Question: Request Information
    - Name: request_information
    - Order: 200
        - as explained in the other Catalog Items tutorial, the "Order" field determines the position of this variable on the catalog item.
4. Hit "Submit"

Click the "Try It" button to see your new Container Start Variable. As you can see, the "Request Information" header appears underneath the Variable Set, since it has a greater Order than the Variable Set's Order (200 vs. 100).

Add the rest of these variables:

1. Variable 1

    - Type: Single Line Text
    - Mandatory: Checked
    - Order: 300
    - Question: Enter your email:
    - Name: enter_your_email

2. Variable 2

    - Type: Reference
    - Mandatory: Checked
    - Order: 400
    - Question: Enter your manager:
    - Name: enter_your_manager
    - Type Specifications > Reference: User [sys_user]

3. Variable 3

    - Type: Yes/No
    - Mandatory: Checked
    - Order: 500
    - Question: Enter if you need additional information:
    - Name: enter_if_your_need_additional_information

4. Variable 4

    - Type: Multi-line text
    - Order: 600
    - Question: Explain your problem:
    - Name: explain_your_problem

5. Variable 5
    - Type: Container End
    - Order: 700

Hit the "Try It" button to see your catalog item so far. It should look something like this:

![second-try-it]()
