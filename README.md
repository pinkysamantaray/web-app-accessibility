This is the class notes from [Web App Accessibility (feat. React)](https://frontendmasters.com/courses/react-accessibility/) by Marcy Sutton Todd



# Accessibility is foundational. Disability is a part of life.

America’s long history of advocating for the rights of disabled citizens, highlighting key legislative milestones and activism efforts. but in today's world, further activism may be necessary to ensure compliance and equity in disability rights. (The Capitol Crawl in 1972. In March 12, 1990 when hundreds of disabled Americans began dragging themselves up as many of the three hundred and sixty five steps of the US Capitol building as their strength would allow)

- myths > Screen readers use JavaScript! Web apps can be made accessible! accessibility is not only for screen reader users, although they are important. [Voice over, screen readers, keyboards, switches etc.]

- Privacy issues and why we shouldn’t detect screen readers. https://www.marcozehe.de/why-screen-reader-detection-on-the-web-is-a-bad-thing/ It would take away the one place where blind people can navigate around relatively undetected. 

### positives and overlaps: 
    - when a webpage contains a semantic structure and actual text content in it (think alternative text for images), it's easier for search engines to detect what's on it and improve searchability.
    - The faster a site loads, the quicker people can interact with it. 
    - Security: Inaccessible user interfaces can be a security issue. Think of a blind person not being able to log into a form or use an ATM without help. It would be an insecure practice to have to share your PIN or other personal details with someone else.
    - practice in domain use cases: government procurement, education software, banking software, etc. for better customer/business growth

# Standards and Definitions
- A11y(numeronym for accessibility), 
- WCAG(web content accessibility guidelines) 2.2(developed in the open on GitHub, backwards-compatible)[https://www.w3.org/WAI/standards-guidelines/wcag/], 
- ARIA(Accessible Rich Internet Applications)[https://www.w3.org/TR/wai-aria-1.2/], 
- WebAIM[https://webaim.org/articles/],
- MDN[https://developer.mozilla.org/en-US/docs/Web/Accessibility], 
- web.dev[https://web.dev/accessibility]

#### Platform Accessibility APIs: Apple, windows, Android each have their own APIs. Voice over in webkit is different to the read aloud in browsers in Mac

#### The Accessibility Tree: a tree structure created with accessibility APIs and web browsers to expose relevant accessibility information

# Semantic HTML basics 
    - Element level vs. page level language lang="fr" for VO
    - avoid DIV Soup
    - Use of headings, datalists/lists, landmark elements like section, nav, headers etc, props like aria-label, aria-labelledby, aria-hidden
    - role > 
        <button>  <!-- implicit 'button' role -->
        <div role="button"> <!-- explicit 'button' role -->
    - ARIA live regions provide a way to programmatically expose dynamic content changes in a way that can be announced by assistive technologies[https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions]
    - Skip Links ex: #header, #content, 
    - Tabindex -1 and TabIndex 0-5..order > focus management on dynamic content through JS; 
    - The 'inert' attribute > makes the browser ignore input events sent by the user, including focus-related events and events from assistive technologies.
    - WCAG actually mentions 18pt text, which is a unit we don’t use on the web. 18pt = 24px
    - some tools:
      - Chakra ui[https://www.chakra-ui.com/]
      - Will your code work with assistive technologies?[https://a11ysupport.io/]
      - AssistivLabs to run screen readers in the cloud[https://assistivlabs.com/]
 
### image alt text
    - Skipping over images with empty alt="" like decorative image
    - https://www.w3.org/WAI/tutorials/images/decision-tree/
    - use of AI tools: https://alttext.ai/
    - for background images, have a hidden block or template with an ID describing the background through aria-labelledby that ID, set on the div with background image

### Transcripts and Closed Captions for audio video or media contents

### reduce motion 
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


# Testing a11y
    - use of tab key to navigate, skip links, esc key, use of arrow keys, space key to select/deselect
    - zoom to 200% to check reflow of layouts, components, responsive designs
    - use of voice over screen reader
    - devtools testing - Chrome(Accessibilty Information Tab, lighthouse, color contrast checker), firefox(contrast ratio inspector), 
    - visual modes: light/dark, high contrast mode
    - missing transcripts or captions for media contents
    - Accessibility Insights for Web from Microsoft is another great tool!


# Working with teams
    - keyboard navigation, NO MOUSE days, 
    - Make accessibility part of the definition of done, Access-debt like tech-debt
    - Break problems down into smaller, solvable parts and phases
    - take accountability(if there is a lawsuit, who is responsible?)
    - PR Reviews are an excellent time to provide accessibility feedback.
    - Use consistent tooling and processes across an organization
    - a11y compliant: It's a constant work in progress.

Cheers!
