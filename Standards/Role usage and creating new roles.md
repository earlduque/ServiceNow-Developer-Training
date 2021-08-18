# Roles Standards

- Roles should never be assigned directly to users
    - Assign roles to groups then assign members to that group
    - If needed for deployment, utilize the `Add to update set` tool installed in development to add any record relevant to group/role membership:
        - sys_user_group
        - sys_user_grmember
        - sys_group_has_role
        - sys_user_has_role
        - sys_user
        - sys_user_role
- Do not use application roles as a way to be able to edit configurations in production. Files typically included in update sets should follow a developement process (dev to test to production).
- Do not assign roles that would grant configuration access in the production environment unless it is agreed upon that the receiving group and users should have the access.
- Do not add new role inclusions to existing out-of-box roles if those roles are already being utilized elsewhere.
- It is preferred that new roles are created within scoped applications (not Global).
- Do not ever include the admin or security admin role in a group
- Do not grant admin access to other users.