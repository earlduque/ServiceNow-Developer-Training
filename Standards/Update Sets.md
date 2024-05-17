# Update Sets 

Remember: different companies do things differently! The below doesn't necessarily apply to every dev team.

### Update Set Naming Conventions 

Use a consistent naming convention for update sets. 

- Never set the update set for Global Default to complete
- Create at least one local update set and switch from the Global update set to the local one before beginning work.  
- At a minimum, update sets must have a unique name that identifies the originating campus organization, concise description, and implementation sequence. A reference to the project requirement is also recommended to ensure traceability to customer requirements such as:  
org_reference_desc_seq/date 
  - org: Primary developer organizational acronym  
  - reference: External reference number  
  - desc: Short description  
  - seq/date: (optional) Sequence number or version or date 
  - Example: DA STRY0001234 Incident Hotfix 3 2020.01.12 
- The standard date format is YYYY.MM.DD. 
- Do not use the word “default” anywhere in your update set name 

### Good Practices for Update Sets 
 
- Never delete an Update Set. (Some companies delete them in production though, YMMV)
- Never re-open previously completed update sets. Create new ones instead. 
  - Why? If another instance has retrieved your update set already then it will never try to retrieve your newly "updated" update set, resulting in desynced update sets.
- Never manually merge update sets. Utilize batch functionality instead. 
- Before completing an update set, review the update set to ensure that the only updates included pertain to the desired work. 
- Preview update sets before committing them. 
- Identify dependencies between update sets. Follow naming conventions standards to specify the correct order for migrating them to the next instance. 
- Remove all debugging scripts and system properties before marking an update set as Complete. 
- In the dev instance, completed update sets should never be placed into a batch after it has been completed 
- Do not transfer updates between update sets manually. Seek administrative assistance when update sets contain incorrect updates. 
- Test your work before you complete your update set. 

### Instance Administrators

- When preparing for production release, batch all updates for that release together
- When pulling to production, delete all irrelevant update sets from the loaded table
