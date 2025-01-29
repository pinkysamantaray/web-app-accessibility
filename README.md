# Why
 - To remove barriers to access for people with disabilities
 - Motivation for organizations(government resources, banking and insecure, Ecommerces-groceries? media platforms like audio resources, podcasts, Innovation with D&Inclusion, personal connect like Satya Nadella)
 - The Business Case for Digital Accessibility[https://www.w3.org/WAI/business-case/]
 - Accessibility is not only for screen reader users, although they are important. [Voice over, screen readers, keyboards, switches etc.] Web apps can be made accessible! 


_**Accessibility is foundational. Disability is a part of life**_

America’s long history of advocating for the rights of disabled citizens, highlighting key legislative milestones and activism efforts. but in today's world, further activism may be necessary to ensure compliance and equity in disability rights. (The Capitol Crawl in 1972. In March 12, 1990 when hundreds of disabled Americans began dragging themselves up as many of the three hundred and sixty five steps of the US Capitol building as their strength would allow)

[National Federation of the Blind v. Target Corp.](https://en.wikipedia.org/wiki/National_Federation_of_the_Blind_v._Target_Corp.)

### Myths: 
- 100% accessible
- Cost
- Tech: Screen readers use JavaScript! 


### Considerations: 
_Privacy issues and why we shouldn’t detect screen readers. [It would take away the one place where blind people can navigate around relatively undetected](https://www.marcozehe.de/why-screen-reader-detection-on-the-web-is-a-bad-thing/)_

### Positives and overlaps: 
* when a webpage contains a semantic structure and actual text content in it (think alternative text for images), it's easier for search engines to detect what's on it and improve searchability.
* The faster a site loads, the quicker people can interact with it. 
* Security: Inaccessible user interfaces can be a security issue. Think of a blind person not being able to log into a form or use an ATM without help. It would be an insecure practice to have to share your PIN or other personal details with someone else.
* practice in domain use cases: government procurement, education software, banking software, etc. for better customer/business growth

# Design personas:
* https://uit.stanford.edu/accessibility/design-personas
* https://alphagov.github.io/accessibility-personas/
* https://www.figma.com/community/file/1002739809764461819/accessibility-personas

# Web Standards and Definitions
- A11y(numeronym for accessibility), 
- WCAG(web content accessibility guidelines) 2.2(developed in the open on GitHub, backwards-compatible)[https://www.w3.org/WAI/standards-guidelines/wcag/] Levels of Conformance A, AA, AAA, 
- ARIA(Accessible Rich Internet Applications)[https://www.w3.org/TR/wai-aria-1.2/], [https://www.w3.org/WAI/ARIA/apg/patterns/]
- WebAIM[https://webaim.org/articles/](explores screen readers, platforms through real surveys, and feedbacks),
- MDN[https://developer.mozilla.org/en-US/docs/Web/Accessibility], 
- web.dev[https://web.dev/accessibility]
- Deque University ARIA Examples[https://dequeuniversity.com/library/]

#### Platform Accessibility APIs: Apple, windows, Android each have their own APIs. 
- Screen readers: VoiceOver in Mac-iOS, NVDA in windows(free, open-source)
- Voice over in webkit is different to the read aloud in browsers in Mac.


#### The Accessibility Tree: a tree structure created with accessibility APIs and web browsers to expose relevant accessibility information
examples: https://target.com



# Semantic HTML basics 
* Use of headings h1-h6
* Skip Links ex: #header, #content, (navigate through sections), good for SEOs, good for overall structure of the page
* Element level vs. page level language `lang="fr"` for VO
* Accessible names: 
    Names are always announced, 
    For example, the accessible name for a `<button>`, `<a>`, or `<td>` comes from the text between the opening and closing tags. 
    Other elements, such as form `<textarea>`, `<fieldset>`, and `<table>` get their accessible name from the content of associated elements; for these elements, the accessible name comes from the `<label>` with a for attribute, `<legend>`, and `<caption>` respectively. 
    aria-label(if the default is missing) and aria-labelledby/aria-describedby(reference to an entire template) attributes, and even title(mouse hover) and placeholder
    https://www.w3.org/TR/accname-1.2/
* lists: yes to `ul` `ol`, `datalist`: no 
* landmark elements like section, nav, headers etc, props like aria-label, aria-labelledby, aria-hidden, avoid DIV Soup
* Use of dialog, modal, overlays(preventing keyboard and screen reader interaction with elements in the background. role, focusable and labeled CTAs)
* the property **role** > \
    `<button>`  implicit 'button' role \
    `<div role="button">` explicit 'button' role 
* tabindex 0(focusable) and -1(not focusable); TabIndex 0-5..order > focus management on dynamic content through JS 
* ARIA live regions provide a way to programmatically expose dynamic content changes(hydration) in a way that can be announced by assistive technologies[https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions] ex: amazon search box
* The 'inert' attribute > makes the browser ignore input events sent by the user, including focus-related events and events from assistive technologies.
* WCAG actually mentions 18pt text, which is a unit we don’t use on the web. 18pt = 24px
* CSS ex: .sr-only in Tailwind, 
* some tools:
    - [Web Accessibility Checklist](https://dequeuniversity.com/checklists/web/)
    - Will your code work with assistive technologies?[https://a11ysupport.io/]
    - [Chakra ui](https://www.chakra-ui.com/)
    - [AssistivLabs](https://assistivlabs.com/) to run screen readers in the cloud

 
### image alt text
- Skipping over images with empty alt="" like decorative image
- [An alt Decision Tree](https://www.w3.org/WAI/tutorials/images/decision-tree/)
- use of AI tools: https://alttext.ai/
- for background images, have a hidden block or template with an ID describing the background through aria-labelledby that ID, set on the div with background image

### Transcripts and Closed Captions for audio video or media contents
Descriptive transcripts for example with videos include visual information needed to understand the content.
For example for a video with no communication(background music), no caption is needed.
but for a Live or pre-recorded video, caption is required.

Things to consider: Don’t rely on auto-generated captions, don't write unnecessary long descriptions, don't hide
example: [HTML5 video caption/subtitle demo](https://codepen.io/JediLin/pen/jpzgpv)

### Reduce motion 
[prefers-reduced-motion](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion)
Non-animated by default, only moving if the setting exists and is unchecked (leveraging prefers-reduced-motion: no-preference)

    CSS:
    @media (prefers-reduced-motion: no-preference) {
        .mask {
            /* do animation stuff */
        }
    }
    Animated by default, stopping movement if the setting exists and is checked (using prefers-reduced-motion: reduce)
    @media (prefers-reduced-motion: reduce) {
        .mask {
            /* turn animations off */
            animation: none;
            transition: none;
        }
    }

    JS:
    const motionQuery = matchMedia('(prefers-reduced-motion: no-preference)');
    let userPrefersMotion = true;
    function handleReduceMotionChanged() {
        console.log(motionQuery.matches);
        if (motionQuery.matches) {
        /* adjust 'transition' or 'animation' properties */
        userPrefersMotion = true;
        } else {
        /* standard motion */
        userPrefersMotion = false;
        }
    }
    motionQuery.addEventListener('change', handleReduceMotionChanged);
    handleReduceMotionChanged(); // trigger once on load

### Color Scheme 
    CSS:
    @media (prefers-color-scheme: dark) {
        .theme-a.adaptive {
            background: #753;
            color: #dcb;
            outline: 5px dashed #000;
        }
    }

    JS:
    const darkModeQuery = matchMedia('(prefers-color-scheme: dark)');
    let userPrefersDarkMode = true;
    
    function handleDarkModeChanged() {
        if (darkModeQuery.matches) {
        /* adjust color and other theme style properties */
        userPrefersDarkMode = true;
        } else {
        /* standard theme */
        userPrefersDarkMode = false;
        }
    }
    darkModeQuery.addEventListener('change', handleDarkModeChanged);
    handleDarkModeChanged();

### Color contrast 
[Use of distinguishable colors](https://www.w3.org/WAI/WCAG22/quickref/?versions=2.0#qr-visual-audio-contrast-contrast)


<br/>

# Testing a11y
* Mindful on:
    What can be automated(HTML/ARIA validation, Form labels, Color contrast, Accessible names, Focus management,Specifying a language), 
    and what can’t be(Focus order, Text alternative quality, Screen reader testing, Contrast over images/gradients)
* Approach: Linting, Unit tests(Jest, Jest DOM, Testing Library), Integration testing([Cypress](https://github.com/component-driven/cypress-axe) or WebdriverIO), E2E testing, actual user testing and feedback for your product
* Keyboard Navigation: tab key, skip links, esc key, use of arrow keys, space key to select/deselect
* Zoom to 200% to check reflow of layouts, components, responsive designs
* Use of voice over screen reader
* Devtools testing - Chrome(Accessibilty Information Tab, lighthouse, [color contrast checker](https://developer.chrome.com/docs/devtools/accessibility/contrast#fix-low-contrast)), firefox(contrast ratio inspector), 
* Visual modes: light/dark, high contrast mode
* Missing transcripts or captions for media contents
* Accessibility Insights for Web from Microsoft is another great tool!


# Working with teams
* Encourage accessibility culture like doing Keyboard Navigation: NO MOUSE days 
* Make accessibility part of the definition of done, Access-debt like tech-debt
* Break problems down into smaller, solvable parts and phases, Build in iteration, continuous process
* PR Reviews are an excellent time to provide accessibility feedback.
* Use consistent tooling and processes across an organization
* Take accountability(if there is a lawsuit, who is responsible?) convince leadership and business stakeholders
* a11y compliant: It's a constant work in progress.




\
\
_Don't try too hard and make accessibility experience hard! Avoid dark anti patterns_

Notes derived from accessibility courses by Marcy Sutton Todd.


[Every HTML element](https://iamwillwang.com/dollar/every-html-element/)