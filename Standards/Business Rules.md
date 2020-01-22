# Business Rules Standards

+ If possible, use conditions in Business Rules
+ Do not use `current.update()` in a Business Rule script
+ Just like `current.update()`, do not script a Business Rule that may accidentally activate itself again upon running
+ Do not create Global Business Rules, it is preferred to use Script Includes instead.
+ Understand if you intend for other Business Rules to run due to the running of this Business Rule.
+ Use Business Rules to validate input on top of Client Scripts/UI Policies since fields can be editable outside of fields.