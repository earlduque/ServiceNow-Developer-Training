# Script Include Standards

- Generally speaking, create new script includes for individual applications, catalogs items, or functions.
    - As opposed to one script include for several catalog items, which may cause problems with delegated development.
- Only return information that the calling script will need
- Use JSON.stringify and JSON.parse instead of JSON.encode and JSON.decode
- Use Script Includes instead of Global Business Rules
- Use existing script includes when possible
- Avoid hardcoding values by using System Properties and Messages
- Remove logging and temporary comments before moving to production.
- Copy out-of-box script includes and edit the copy instead of editing the original.