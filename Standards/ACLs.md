# ACL standards

- __Understand how ACLs are evaluated and in what order they are run before attempting to configure ACLs__
- Never leave anything in the script field if the ACL's advanced field is false.
- Understand that ACLs impact instance performance, the more complex the query and the more that are running, the slower the interaction will be.
- **Whenever possible**, a matching Before Business Rule Query should be created for every ACL that is designed to remove records from a person's view.