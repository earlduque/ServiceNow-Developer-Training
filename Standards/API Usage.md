# API Usage Standards

## Outbound

- Outbound calls to external APIs via REST, SOAP, or other methods are allowed.
- Do not store API keys in plain-text on scriptable records, instead put them in system properties.
- Intentionally rate limit outbound calls that occur rapidly (several per second). Make sure these calls are condition-based for when they occur instead of timer based.
- Do not use ServiceNow to call an external API to check for updates rapidly. If you need live updates, attempt to create an inbound integration that is triggered by the external system, instead of polling for updates.
- Prefer creating outbound service records that are called in script rather than creating an entire outbound call in individual scripts.

## Inbound

- Do NOT create an unauthenticated API for inbound calls
- Always prefer to use a more secure authentication method like OAuth 2.0 over a simple username/password authentication
- Do not store API keys in plain-text on scripts or table records, instead put them in system properties.
- Do not create or configure table APIs for campus-used tables unless approved by the campus TAG or IET Service Management (eg. the incident table).
- Some tables have ACLs or Business Rules that intend to restrict some information that is accessible (eg. incident, sc_req_item, sysapproval_approver, sc_task, x_uocd2_business_m_case, etc.). Always use discretion when divulging information on these tables for an API. Always program to satisfy that these ACLs and rules are not broken.