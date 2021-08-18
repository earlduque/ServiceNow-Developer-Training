# Catalog Item Standards

Request catalogs and their catalog items (forms) are used to describe, support, and request services from service providers. 
 
### Catalog Item Style Guide 

- Use your company provided style guide to design catalog items. 

### Request Catalog Style Guide

This style guide is a set of standards to help the information technology community develop ServiceNow Request Catalog items.

This style guide follows:
- The Associated Press (AP) style guide and The Chicago Manual of Style, which UC Davis Strategic Communication follows
- ServiceNow product documentation
 
#### Audience 

- Staff who have oversight and content management responsibilities for ServiceNow
- IT community developers who work on ServiceNow modules, applications, and system components utilizing the Item Designer

#### Purpose

The Request Catalog is for service offerings. Services offerings may include both products and services.

#### Request Item Writing Tips

- **Avoid capitalizing every word in a header, question or phrase**. The first letter of the first word of variables in a catalog item should be capitalized (i.e. Phone number). Capitalize professional titles, organizations, and other proper nouns, but in general, avoid the use of caps.
- **Avoid the use of acronyms**. If an acronym is required, the full name should be written out the first time it is used with its corresponding acronym in parenthesis (i.e. Associated Press (AP)).
- **Use clear and concise language**. For variable questions, typically verbs are not necessary. (i.e. “Requestor’s job title” rather than “Enter the requestor’s job title.”)

#### General Formatting

A cascading style sheet (CSS) has been created that adheres to University guidelines. This style sheet applies standard formatting to all aspects of the Service Hub, including the public-facing Knowledge Base.
- Font Tags - Do not change or insert Font Tags into any allowable HTML field. This erroneous code diminishes the set standards. Bold or italic may be used for impact on the content it references.
- Phone numbers - Use the traditional formatting convention for phone numbers:
    - Area code followed by 7 digits; (NPA) NXX-XXXX where NPA is the area code and NXX-XXXX is the subscriber number
    - Area code wrapped in parentheses "( )"
    - The subscriber number is separated by a hyphen ("-")
- Dates - Use International Organization for Standardization (ISO) format:
    - Four-digit year first, followed by month, then day: YYYY-MM-DD
    - With each separated by a hyphen ("-")
    - Numbers less than 10 preceded by a leading zero
    - Years expressed as "0" prior to year 1 and as "-1" for the year prior to year 0 (and so forth)
 
 #### Form Design Guidelines

1. **Standard content blocks**. All request forms should maintain the three content block standard.
    1. Customer Information – This section captures the customer's details including contact method, department, and any relevant authorization information. This serves as validation of who is entering information into the form. There are two variable sets available for this block, one with Request on behalf of, and one without.  This section includes the following standard fields.
        1. Primary Contact - UI policy to auto-populate with CAS authentication
        2. Email – auto-populates
        3. Telephone – auto-populates
        4. Request on behalf of – optional field
    2. Request Information – This is the body of the form. The variables in this block must be held in containers.  The number of questions in this block is determined by the requirements of the request.
    3. Additional Information – This content block is for supplemental information such as attachments or additional information that are not captured in the body of the form. There are two variable sets available, Include Billing and Exclude Billing.  Do not use the Additional Information variable set if the RITM workflow is completely automated. The customer may assume that information entered will be reviewed.                 
2. **Variable sets**. Variable sets are standard sets of fields that can be used across multiple forms. Using variable sets keep forms standardized and make for a consistent user experience. They should be used whenever possible. 
3. **Agreement checkbox**. Include this checkbox on impactful items that deal with matters such as account cancellation or finances. A script has been developed and is available which inactivates the "Submit" button unless the agreement is checked/acknowledged.
4. **Columns**. Column usage will be up to the form designer's discretion, but here are some general guidelines:
    1. Fields that trigger/reveal other fields should generally be two columns, revealing the other field either below or to the right of the first field.
    2. Most multi line text fields should be one column spanning the width of the page.
    3. Single line text fields will generally be one column, spanning half the page.
5. **Drop downs**. If a drop down field is mandatory, it should default to "None" so the requester must choose one of the options before submission is allowed. If a drop down field is not mandatory, a "None" option is not needed.
6. **Multi line vs Single line** Question dependent, but multi lines should only be used for lengthy questions such as asking for additional detail.

#### Guide to Usability

- **Tooltips** (rollover or hover functionality) are the primary method used for "help text." The majority of variables in a form will require a tooltip; the exception to this standard is when the variable name is its definition.
- **More information** should be used sparingly in support of more complicated content within the variable. This is a secondary solution to the tooltip. More information appears in grey under the input field. Do not include information directed to an individual or group, requirements, or terms and conditions. 
- **Common variables** used in form design:
    - Select Box - drop down menu item to be used in cases of a single item needing to be selected from a list of items.
    - Yes / No - a select box variable type used for questions with a Yes or No answer.
    - Check Boxes - individual options that are true or false. These should be used in a vertical alignment.
    - Radio buttons - should be used in cases where one of four options, or less, need to be selected. Best practice is to use this when all options need to visible on the form.
    - Submit button - located in the lower left corner for web submission forms.

A complete list of variable types can found [here](https://docs.servicenow.com/bundle/jakarta-servicenow-platform/page/administer/wizards/task/t_DefineAVariable.html).