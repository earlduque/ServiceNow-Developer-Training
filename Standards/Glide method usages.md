# Glide Method usages

### GlideRecord
- Use when attempting to get information from specific records
- Don't use for attempting to do calculations on groups of records, use GlideAggregate instead
- Only use on server scripts (usable in client scripts but do not do this, opt for GlideAjax instead)

### GlideAggregate
- Use when doing calculations on groups of records
- Only use on server scripts

### GlideAjax
- Use when you need information from the server after the client has finished loading the page
- Only use on client scripts

### GlideElement
- Used to operate on fields of the currently selected GlideRecord
- Only use on server scripts

### GlideSystem
- Use to get information from the system
- Only use on server scripts

### GlideDateTime
- Use to perform date-time operations
- Only use on server scripts

### GlideUser
- Use when getting session infromation about the current logged-in user
- Only use on client scripts