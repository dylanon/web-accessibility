# Web Content Accessibility Guidelines (WCAG 2.1) Notes

## Overview

- 13 guidelines under four principles (good overview: [Accessibility Principles](https://www.w3.org/WAI/fundamentals/accessibility-principles/))
  - Perceivable
  - Operable
  - Understandable
  - Robust
- Quick reference (“How to Meet WCAG”): [https://www.w3.org/WAI/WCAG21/quickref](https://www.w3.org/WAI/WCAG21/quickref)

## Level A Compliance

### Principle 1 - Perceivable

"Information and user interface components must be presentable to users in ways they can perceive."

#### 1.1 Text alternatives

- "Provide text alternatives for any non-text content so that it can be changed into other forms people need, such as large print, braille, speech, symbols or simpler language."
- Descriptive text should be short - there are techniques for providing long descriptions (see `longdesc`) when necessary, which generally require user action
- Key techniques
  - Images
  - `alt` attribute on `img` elements - short descriptive text, or empty if image is purely decorative and should be ignored by assistive tech
  - `aria-labelled-by` attribute on elements that don’t support `alt`, where existing text on the page can describe the element
  - `aria-label` attribute on elements that don’t support `alt`, where no other text on page can describe the element
  - Forms
    - Label all inputs with `label` element, `for` attribute matching the input's `id` attribute
    - Inputs of type `checkbox` and `radio` should be followed by `label` element - Other input types should be preceded by the `label` element

#### 1.2 Time-based media

- "Provide alternatives for time-based media."
- Key techniques
  - Provide text transcripts for audio-only or video-only content
  - Provide audio description for video-only content

#### 1.3 Adaptable

- "Create content that can be presented in different ways (for example simpler layout) without losing information or structure."
- Can be presented in different ways without losing information
- Key techniques
  - Use semantic markup
    - Break up long lists of `select` element `option`s with the `optgroup` element ([more](https://www.w3.org/WAI/WCAG21/Techniques/html/H85.html))
    - Group checkboxes, radio buttons, and groups of inputs with `fieldset` element ([more](https://www.w3.org/WAI/WCAG21/Techniques/html/H71.html))
      - `legend` should be the first element in the `fieldset` and should provide a text description
    - Use `ol` or `ul` for lists of links to allow users to skip to start or end
    - Use `dl` for lists of information such as key-value pairs (e.g. to list a user's profile information)
  - Associate form controls with labels
  - Associate table data cells with headings
  - Markup content in logical order - do not use CSS layout to change meaning.
    - In most cases source code order should match visual order (e.g. sighted and non-sighted user can review content together without confusion)
  - Also include text description when a sensory characteristic is used to convey meaning (e.g. color, shape, icon)

#### 1.4 Distinguishable

- "Make it easier for users to see and hear content including separating foreground from background."
- Provide additional visual cue when using color to convey information
  - E.g. a link appears blue & is also underlined
- If audio plays for more than 3 seconds, must provide way to turn it off and to control volume

### Principle 2 - Operable

"User interface components and navigation must be operable."

#### 2.1 Keyboard Accessible

- "Make all functionality available from a keyboard."
- All functionality is operable via keyboard (in addition to mouse)
- Does not require specific timing for keyboard use
- Key techniques
  - Proper form labelling ([full list of HTML form controls and how AT determines name/value](https://www.w3.org/WAI/WCAG21/Techniques/html/H91.html#description))
  - Custom controls (e.g. `div` with an action bound on click) must also handle `onkeypress` or `onkeypress`, as well as employ `tabindex` to make the control focusable ([Adding keyboard-accessible actions to static HTML elements](https://www.w3.org/WAI/WCAG21/Techniques/client-side-script/SCR29.html))
  - Keyboard trap - must provide way to close modals, plugins, etc. using only keyboard. Without, app is inoperable for the user.
  - Single-key shortcuts can be disabled, remapped, or are active only when component has focus

#### 2.2 Enough Time

- "Provide users enough time to read and use content."
- Key techniques
  - Avoid time limits (e.g. session, reading content)
    - Must be able to extend limit 10x or disable
    - Exceptions available when changing time limit invalidates the activity or when the activity is real-time
  - Blinking, auto-scrolling, or auto-updating content that auto-plays longer than 5s - can be stopped or paused

#### 2.3 Seizures and Physical Reactions

- "Do not design content in a way that is known to cause seizures or physical reactions."
- Do not include any content that flashes more than 3 times per second

#### 2.4 Navigable

- "Provide ways to help users navigate, find content, and determine where they are."
- A mechanism is available to bypass blocks of content that are repeated on multiple Web pages.
- Key techniques
  - "skip link" at the top of each page to skip to main content
  - All pages have unique descriptive title using the `title` element
  - Pages have a logical tab order that preserves meaning
  - Hidden menus are inserted directly after their trigger in the tab order
  - Link purpose is clear, given the link text and its context (e.g. sentence in which it appears)

#### 2.5 Input Modalities

- "Make it easier for users to operate functionality through various inputs beyond keyboard."
- Users that do not use a mouse or keyboard can interact with the content
- Key techniques
  - A single pointer is sufficient to access the content (e.g. multiple pointers are not necessary)
  - Input is not path-based
  - Pointer based input can be cancelled (see Quick Reference for various acceptable methods)
  - Motion-based input (e.g. shaking, tilting) has conventional input alternative

### Principle 3 - Understandable

"Information and the operation of the user interface must be understandable."

#### 3.1 Readable

- "Make text content readable and understandable."
- Key techniques
  - Set `lang` attribute on the `html` element
    - Helps braille translation software & speech synthesizers (choose correct accent)

#### 3.2 Predictable

- "Make Web pages appear and operate in predictable ways."
- Key techniques
  - Focus events should not trigger a change in context (e.g. new window/tab, form submission) - use "activate" event (space bar or click) instead
  - Do not automatically perform a context change (e.g. form submission) on input (e.g. selecting an option from a dropdown) - instead, allow the user to perform the context change once they are satisfied with their input (e.g. select an option, then press button to submit the form)

#### 3.3 Input Assistance

- "Help users avoid and correct mistakes."
- Key techniques
  - When input errors are detected, the item is identified and the error is described to the user
    - Many ways - can make use of `aria-live` region to announce dynamic errors, show an alert or custom modal (many more accessibility requirements for custom modals), change form labels to indicate where errors have occurred, link to form fields with errors after the submit button (see )
  - Labels and/or instructions are provided for user input
    - All inputs have an associate `label` element
    - Use `fieldset`, `legend` elements to group and describe collections of inputs

### Principle 4 - Robust

"Content must be robust enough that it can be interpreted by a wide variety of user agents, including assistive technologies."

#### 4.1 Compatible

- "Maximize compatibility with current and future user agents, including assistive technologies."
- Key techniques
  - Validate HTML
    - Missing closing tags, duplicate attributes, non-unique `id` attributes prevent effective parsing by AT
  - When creating custom components, `name`, `role`, and `value` can be determined, and AT can track changes to these properties
    - Use aria-\* attributes to indicate state and properties (e.g. a custom toggle component uses `role="button"` to indicate its intended use, `aria-pressed` attribute to indicate its state , and `aria-labelledby` to give it a clear name the user will understand)
