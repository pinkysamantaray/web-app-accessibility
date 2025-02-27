# Digital Accessibility: Why It Matters and How to Get It Right

## Table of Contents

- [Why Accessibility Matters](#why-accessibility-matters)
- [A History of Advocacy](#a-history-of-advocacy)
- [Myths About Accessibility](#myths-about-accessibility)
- [Key Accessibility Considerations](#key-accessibility-considerations)
- [Web Standards and Guidelines](#web-standards-and-guidelines)
- [Semantic HTML and Best Practices](#semantic-html-and-best-practices)
- [Media Accessibility](#media-accessibility)
- [Reducing Motion and Improving Color Contrast](#reducing-motion-and-improving-color-contrast)
- [Testing Accessibility](#testing-accessibility)
- [Building Accessibility Culture in Teams](#building-accessibility-culture-in-teams)
- [Final Thoughts](#final-thoughts)

## Why Accessibility Matters

Digital accessibility is about removing barriers for people with disabilities, ensuring that everyone has equal access to information and digital services. It benefits not just users with disabilities but also businesses, government organizations, and media platforms. The motivation for accessibility extends beyond compliance—it fosters innovation, improves user experience, and makes digital spaces more inclusive.

### The Business Case for Accessibility

Many organizations, from e-commerce to banking and government services, are embracing accessibility. Prioritizing accessibility can:

- Enhance customer reach
- Improve SEO
- Strengthen brand reputation
- Reduce legal risks
- Drive innovation

[The Business Case for Digital Accessibility](https://www.w3.org/WAI/business-case/) explores these advantages in depth.

### Digital Accessibility Is for Everyone

A common misconception is that accessibility only benefits screen reader users. In reality, accessible web applications accommodate users with different needs, including those who rely on voice commands, screen magnifiers, keyboards, and switch devices.

> *"Accessibility is foundational. Disability is a part of life."*

## A History of Advocacy

The fight for disability rights in the U.S. has a long history, with key moments such as:

- **The Capitol Crawl (1990):** Hundreds of disabled Americans crawled up the steps of the U.S. Capitol to advocate for the Americans with Disabilities Act (ADA).  
- **[National Federation of the Blind v. Target Corp.](https://en.wikipedia.org/wiki/National_Federation_of_the_Blind_v._Target_Corp.)**: A landmark case that reinforced the importance of web accessibility.

## Myths About Accessibility

- **"100% accessible websites exist."** Accessibility is a continuous process, not a one-time achievement.
- **"It’s too expensive."** Accessibility investments pay off through better usability and broader customer reach.
- **"Screen readers can’t handle JavaScript."** Modern assistive technologies fully support JavaScript.

## Key Accessibility Considerations

### Privacy Matters

Screen reader detection can invade privacy, as some users prefer to navigate without being identified. [Here’s why detecting screen readers is problematic.](https://www.marcozehe.de/why-screen-reader-detection-on-the-web-is-a-bad-thing/)

### Benefits Beyond Accessibility

- **SEO:** Proper semantic structure improves search engine rankings.
- **Performance:** Faster-loading sites benefit all users.
- **Security:** Inaccessible authentication methods can compromise user privacy (e.g., forcing blind users to disclose their PIN to someone else).
- **Business Growth:** Inclusive design improves customer retention and satisfaction.

## Web Standards and Guidelines

Understanding accessibility standards is crucial:

- **A11y:** Short for "accessibility."
- **WCAG (Web Content Accessibility Guidelines) 2.2:** Defines levels of conformance (A, AA, AAA). [Learn more](https://www.w3.org/WAI/standards-guidelines/wcag/)
- **ARIA (Accessible Rich Internet Applications):** Helps improve web app accessibility. [ARIA examples](https://dequeuniversity.com/library/)
- **Design Personas:**
  - [Stanford Accessibility Personas](https://uit.stanford.edu/accessibility/design-personas)
  - [UK Government Accessibility Personas](https://alphagov.github.io/accessibility-personas/)
  - [Figma Community Accessibility Personas](https://www.figma.com/community/file/1002739809764461819/accessibility-personas)

### Platform-Specific Accessibility

Different operating systems have unique accessibility tools:
- **Apple:** VoiceOver
- **Windows:** NVDA (free, open-source)
- **Android:** TalkBack

## Semantic HTML and Best Practices

Using semantic HTML enhances accessibility: (Readability, Predictability & Adaptability)
- **Proper headings (`h1-h6`)** for structure.
- **Landmark elements (`header`, `nav`, `main`, etc.)** for navigation.
- **Descriptive alt text** for images. 
- **Skip-links** to improve keyboard navigation. [skip-links](https://dequeuniversity.com/rules/axe/4.10/skip-link) allow keyboard users to jump directly to main content
- **Accessible Names and Descriptions** Names are always announced. 
    For example, the accessible name for a `<button>`, `<a>`, or `<td>` comes from the text between the opening and closing tags. 
    Other elements, such as form `<textarea>`, `<fieldset>`, and `<table>` get their accessible name from the content of associated elements; for these elements, the accessible name comes from the `<label>` with a for attribute, `<legend>`, and `<caption>` respectively. 
    aria-label(if the default is missing) and aria-labelledby/aria-describedby(reference to an entire template) attributes, and Fallback names derived from titles(mouse hover) and placeholders
    ```
    <span
      role="checkbox"
      aria-checked="false"
      tabindex="0"
      aria-labelledby="tac"></span>
    <span id="tac">I agree to the Terms and Conditions.</span>
    ```
    
    > [!INFO]
    > [ARIA prohibited items](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-label#associated_roles)

> [!TIP]
> Helpful resouces: https://www.w3.org/TR/accname-1.2/, https://www.w3.org/WAI/ARIA/apg/practices/names-and-descriptions/.
    
- **Lists**: Use `ul` and `ol` for lists instead of non-semantic elements like `div` or `span`.
- **Avoid "div soup"**: Use semantic elements instead of excessive `div` elements for better readability
- **Form accessibility**:
  - Ensure `label` elements are correctly associated with `input` fields using `for` attributes.
  - Use `fieldset` and `legend` for grouping related form controls.
- **Focus management**:
  - Visible Focus with contrast, outline
  - Focus order: ensure users can navigate via keyboard by using `tabindex` (-1/0/1-5.../) correctly. 
  - Prevent keyboard traps by allowing easy exit from modal dialogs.
  - example: [Svelte Actions use:trapFocus](https://svelte.dev/tutorial/svelte/actions) 
- **Inert attribute**: Use `inert` to make off-screen elements non-focusable, improving user navigation.
- **CSS Accessibility**:
  - three states of hidden elements:
  - Hidden for Everyone: (visibility: hidden or display: none) 
  - Hidden for Visual Users: 
    - Utilize `.sr-only` classes (e.g., in Tailwind) for screen reader-only content.
    - using specific CSS techniques, like positioning the element off-screen. This is often used for providing additional context to screen reader users, such as hidden headings that provide structure and orientation. 
  - Hidden for Screen Readers: aria-hidden="true". This is handy for situations where visual elements are purely decorative and do not provide additional information, such as icons used alongside text labels.
 - Ensure hover effects do not rely solely on color to convey information.
- **ARIA live regions**: Implement [ARIA live regions](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions) attributes for dynamically updating content, such as notifications or search results(aria-live="off/polite/assertive")
  ```
  <div id="announce" aria-live="polite">
    <p>You have a new message!</p>
  </div>
  ```
- Element level vs. page level language `lang="fr"` for Voice Over
- clear and constructive error messages
- visual aids with icons
  ```
  <a href="report.pdf">
    <img src="pdf-icon.png" alt="" aria-hidden="true">
    Download Report (PDF)
  </a>
  <a href="report.doc">
    <img src="word-icon.png" alt="" aria-hidden="true">
    Download Report (DOC)
  </a>
  ```


## Media Accessibility

### Image Alt Text

Use alt attributes correctly:
- [An alt Decision Tree](https://www.w3.org/WAI/tutorials/images/decision-tree/)
- **Decorative images:** Use `alt=""` to skip over them.
- **AI-generated alt text:** Consider tools like [alttext.ai](https://alttext.ai/).
- **Background images:** Use ARIA attributes to describe them.
  ```
  <div id="fooSection" style="background-image: foo.jpg">
    <!-- Text alternative for the background image on div#fooSection -->
    <span role="img" aria-label="fooSection"></span>

    <h2>My heading</h2>
    <p>Some more text</p>
    <a href="foo.html">Call to action</a>
  <div>
  ```

### Transcripts and Captions

Ensuring accessibility for audio and video content:

- **Use closed captions** for videos. 
    - **Pre-recorded videos:** Require captions.
    - **Live videos:** Need real-time captions.
    - **No spoken dialogue?** No captions necessary.
    
- **Provide transcripts** for audio content.
- **Avoid reliance on auto-generated captions** as they may be inaccurate.

[HTML5 video caption demo](https://codepen.io/JediLin/pen/jpzgpv)

## Reducing Motion and Improving Color Contrast

- **Reduced Motion:** Implement `prefers-reduced-motion` media queries to accommodate users sensitive to motion.
- **Dark Mode Support:** Utilize `prefers-color-scheme` for adaptive themes.
- **Color Contrast:** Ensure WCAG-compliant contrast ratios for readability. [accessible color contrast](https://www.w3.org/WAI/WCAG22/quickref/?versions=2.0#qr-visual-audio-contrast-contrast)

> [!WARNING]
> Avoid going dark with anti patterns.

## Testing Accessibility
How to Test a website:
  - Use default browser tools, Google Lighthouse (Built into Chrome DevTools), example: [cursorless](https://www.cursorless.org/docs/)
  - WAVE (Web Accessibility Evaluation Tool) – https://wave.webaim.org
  - Plugins like:
    - Accessibility Insights for Web by Microsoft > Ad hoc tools
    - WAVE Evaluation Tool
    - axe Accessibility Checker (Browser Extension) – https://www.deque.com/axe/
    

Automated tools help, but human testing is essential.

- **Automated checks:** HTML validation, form labels, focus management.
- **Manual testing:** Screen readers, keyboard navigation, color contrast testing, testing reflow by zooming to 200%
- **Useful tools:**
  - DevTools: [Chrome Accessibility DevTools](https://developer.chrome.com/docs/devtools/accessibility/)
  - [Cypress-axe](https://github.com/component-driven/cypress-axe)
  - [Accessibility Insights for Web](https://accessibilityinsights.io/)
  - [Chakra UI](https://www.chakra-ui.com/) - A React component library focused on accessibility.
  - [AssistivLabs](https://assistivlabs.com/) - Test with real assistive technologies in the cloud.
  - [Deque University](https://dequeuniversity.com/) - Training and tools for digital accessibility.
  - [Web Accessibility Checklist](https://dequeuniversity.com/checklists/web/) - A checklist for accessibility compliance.
  - [The Accessibility Developer Guide](https://www.accessibility-developer-guide.com/)
  - Enterprise support([AccessiWay](https://www.accessiway.com/), example: [Sezane](https://www.sezane.com/nl-nl) )

## Building Accessibility Culture in Teams

- **Adopt "No Mouse" Days** to encourage keyboard navigation.
- **Make accessibility part of the development process.** part of the definition of done, Access-debt, PR reviews
- **Break down accessibility work into phases.** smaller, solvable parts in phases, Build in iteration, continuous process
- **Ensure accountability:** Who is responsible if legal issues arise? convince leadership and business stakeholders

> *"Accessibility compliance is a constant work in progress."*

## Final Thoughts

Accessible design isn’t just a legal requirement—it’s a fundamental part of creating inclusive, user-friendly digital experiences. By prioritizing accessibility, we can build a web that works for everyone.

---

*Some notes derived from accessibility courses by Marcy Sutton.*

