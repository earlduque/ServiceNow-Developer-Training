# Scripting Standards

### GlideRecords

- Do not name your GlideRecord instantiations as simply `gr` as this may conflict with other running GlideRecords.
- Instead, name them something like `table_gr` or `function_gr`
- Remove logging and unnecessary comments prior to promoting toward production
- Do not use client-side GlideRecords, instead use GlideAjax
- For complex GlideRecord queries, it is preferred to generate encoded query strings through the list filter and using that with `addEncodedQuery`, rather than using a series of `addQuery` and `addOrCondition`.

### GlideAjax

- Only return information that is going to be used by the client.

### General

- Avoid naming globally used variables as `i` as that may conflict with other scripts running.
- Make code easy to read with appropriate white-space, indentation, and comments
- When appropriate, verify that variables and fields have a value before using them
- Avoid using hard-coded values
