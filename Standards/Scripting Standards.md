# Scripting Standards

### GlideRecords

- Do not name your GlideRecord instantiations as simply `gr` as this may conflict with other running GlideRecords.
- Instead, name them something like `table_gr` or `function_gr`
- Remove logging and unnecessary comments prior to promoting toward production
- Do not use client-side GlideRecords, instead use GlideAjax

### GlideAjax

- Only return information that is going to be used by the client.

### General

- Avoid naming globally used variables as `i` as that may conflict with other scripts running.