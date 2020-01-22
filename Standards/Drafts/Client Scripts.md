# Client Script Standards

+ Use Client Scripts to validate user input
+ When possible, use a UI Policy to set field attributes to mandatory, read-only, or visible rather than a Client Script
+ Do not create Global Client Scripts, instead create them on Base Tables that can be inherited for all child/extending tables
+ If possible, avoid DOM Manipulation
+ Do not use `GlideRecord` in Client Scripts, it is preferred to use `GlideAjax` instead
