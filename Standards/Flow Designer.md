# Flow Designer Standards

- Since flows are not tied to tables/records like workflows are, they can be easily configured to run in any situation. That being said, always approach flow triggers with the perspective of "do not allow this to run unless absolutely needed" or else many flow contexts will accidentally be created.
- Do not edit base system actions and flows. Editing these will cause them to not immediately receive future updates from ServiceNow.
- Flows should be within scoped applications whenever possible (not Global).
- When possible use IntegrationHub to handle authentications instead of recreating your own
- Never test flows in a production environment
- Never develop flows in a production environment
- Do not create conflicting logic with already active business rules and workflows