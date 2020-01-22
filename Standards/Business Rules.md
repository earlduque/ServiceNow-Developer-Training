# Business Rules Standards

+ If possible, use conditions in Business Rules
+ Do not use `current.update()` in a Business Rule script
+ Just like `current.update()`, do not script a Business Rule that may accidentally activate itself again upon running
+ It is preferred to use Script Includes rather than Global Business Rules
