# ARIA Best Practices

Don’t use ARIA on everything. Too much of something is not good. There are only rare situations where HTML is not enough. In those situations, using ARIA is advised. In other situations, when the use of a clean and semantically correct HTML structure can provide a solution, usage of ARIA is strongly discouraged, due to its non-homogenous support among browsers and screen readers.

ARIA provides HTML attributes that allow adding specific semantic meaning to existing HTML elements.
* Role attributes add or override a semantic role of an element.
 * `<span role="button">`
 * Adding a role will not change the look or behavior of an element for people **not** using assistive technology.
 * ARIA adds nothing to default semantics of most HTML elements
   * "Changing the role of an element does not add behaviors, properties or states to the role used."

* `aria-*` attributes provide statuses to the current semantic role.
 * `<span role="button" aria-pressed="true">`

## ARIA Roles
 Roles define what an element of a region does. The role attribute on element provides an informative description of the role, the context of the role, and supported states and properties, among other things. Roles are important because they give assistive technologies information about how to handle the element it is attached to. More information available in ARIA [documentation](https://www.w3.org/TR/wai-aria/#usage_intro).

## ARIA Property and states
These are the characteristics and current conditions of components and are closely associated with roles. They are both `aria-` prefixed attributes but have subtle differences in meaning. There is overlap between them but, simply put, a property describes the characteristics of a component while a state describes the current condition. Properties, like `aria-labelledby`,are characterized by being less likely to change during the life-cycle of the application while states, like `aria-checked` may change frequently.
More information available in ARIA [documentation](https://www.w3.org/TR/wai-aria/#introstates).

## The Five Rules of ARIA Use
1. If you can use a native HTML element or attribute with the semantics and behavior you require **already built in**, instead of re-purposing an element and adding an ARIA role, state or property to make it accessible, **then do so.**
   * Example:
   ```HTML
   <span class="link" onclick="..." role="link">
       Google
   </span>
   ```
   * Despite that screen readers announce this element as a link, using ARIA in this situation over the proper `<a>` tag leads to missing standard functionality and issues like the element not being focusable, the need for custom JavaScript, and the browser history may be broken.
  
2. Do not change native semantics, unless you really have to.
   * Do not put a role in an element where the semantic meaning is overwritten:
     ```HTML
     <h2 role="tab">Heading Tab</h2>
     ```
   * Do, instead, wrap it in a generic element like `<div>` and assign the role to the generic element:
     ```HTML
     <div role="tab">
         <h2>Heading Tab</h2>
     </div>
     ```
3. All interactive ARIA controls must be usable with the keyboard.
   * Click, tap, drag and drop, slide, and scroll must all have an equivalent action that can be performed using a keyboard.
   * All interactive widgets must be scripted to respond to standard keystrokes or keystroke combinations where applicable.
4. Do not use `role="presentation"` or `aria-hidden="true"` on a **focusable** element.
   * Using either of these will result in some users focusing on 'nothing'.
5. All interactive elements must have an [accessible name](http://www.w3.org/TR/accname-aam-1.1/#dfn-accessible-name).
   * An interactive element only has an accessible name when its Accessibility API accessible name (or equivalent) has a value. ([Examples](https://w3c.github.io/using-aria/#fifthrule))

## Other Notes
In general, it is better practice to not treat users who use accessibility tools differently than those who do not. For example, it is questionable to use code like
```HTML
<button aria-label="Dear screen reader user, please do not use this functionality, it is not meant for you">
  Zoom image
</button>
```
and use `aria-label` to override the a zoom button's functionality.

## In Summary
* ARIA doesn't make things behave differently
* **No** ARIA is better than **bad** ARIA
* Avoid redundancy (see Doc Conformance)
* Add appropriate labeling but avoid mislabeling

## Resources and Helpful Links
[Authoring Practices](https://www.w3.org/TR/wai-aria-practices/#read_me_first) <br>
[ARIA Roles](https://www.w3.org/TR/wai-aria/#roles) <br>
[States and Properties](https://www.w3.org/TR/wai-aria/#states_and_properties) <br>
[Doc Conformance](https://www.w3.org/TR/html-aria/#docconformance) <br>
[Using ARIA](https://w3c.github.io/using-aria/) <br>
[Bad Practices](https://www.accessibility-developer-guide.com/knowledge/aria/bad-practices/)\* <br>
[Best Practices](https://www.mediacurrent.com/blog/wai-aria-attributes-best-practices/)\* <br>

---
\* Not official W3C documentation
