# Accessibility 

Accessibility (often abbreviated to A11y) means enabling as many people as possible to use Web sites, even when those people's abilities are limited in some way.

https://developer.mozilla.org/en-US/docs/Web/Accessibility

Contents:
- What is accessibility?
  - People with visual impairments 
  - People with hearing impairments 
  - People with mobility impairments 
  - People with cognitive impairments 
- HTML: A good basis for accessibility
  - Semantic markup
  - Text Content
  - Using clear language
  - UI Controls 
  - Building accessibility back in 
  - Meaningful text labels 
  - Accessible Data Tables
  - Text alternatives (alt)
  - Link Styling
- CSS and JavaScript accessibility best practices
  - CSS 
  - JavaScript
- WAI-ARIA basics
- Accessible Multimedia
- Mobile Accessibility 




## What is accessibility? 

Accessibility is the practice of making your websites usable by as many people as possible. I.e. those with disability, those using a mobile, or those with a slow network connection. 

Building accessible sites benefit everyone:
- Semantic HTML, which improves accessibility, also improves SEO, making your site more findable.
- Caring about accessibility demonstrates good ethics and morals, which improves your public image.
- Other good practices that improve accessibility also make your site more usable by other groups, such as mobile phone users or those on low network speed. In fact, everyone can benefit from many such improvements.
- It is also the law in some places

People with Visual Impairments:
Often use screen magnifiers (either physical or software zoom capabilities, i.e. most browsers have zoom). Some users rely on screen readers.

Some screen reader examples include:
- Paid commercial products, like JAWS (Windows) and Dolphin Screen Reader (Windows).
- Free products, like NVDA (Windows), ChromeVox (Chrome), and Orca (Linux).
- Software built into the operating system, like VoiceOver (macOS, iPadOS, iOS), Narrator (Windows), ChromeVox (on Chrome OS), and TalkBack (Android).

Types of Impairments: 
1. Visual:
  - World Health Organization estimates that "285 million people are estimated to be visually impaired worldwide: 39 million are blind and 246 million have low vision." A large and significant population of users — almost the same size as the population of the United States of America.
2. People with hearing impairments: 
  - People have various levels of hearing loss ranging from mild to profound. Although some do use AT (assistive devices), they are not widespread.
  - To provide access, textual alternatives must be provided. Videos should be manually captioned, and transcripts should be provided for audio content. "466 million people worldwide have disabling hearing loss", says the World Health Organization.
3. People with mobility impairments: 
  - These people have disabilities concerning movement. Some people might have difficulty making the exact hand movements required to use a mouse
  - The way this usually affects web development work is the requirement that controls be accessible by the keyboard. Can you use the Tab key to move between the different controls of a web form, for example?
4. People with cognitive impairments: 
  - Cognitive impairment refers to a broad range of disabilities, from people with intellectual disabilities who have the most-limited capabilities, to all of us as we age and have difficulty thinking and remembering. The range includes people with mental illnesses, such as depression and schizophrenia. It also includes people with learning disabilities, such as dyslexia and attention deficit hyperactivity disorder. 
  - Importantly, though there is a lot of diversity within clinical definitions of cognitive impairments, people with them experience a common set of functional problems. These include difficulty with understanding content, remembering how to complete tasks, and confusion caused by inconsistent webpage layouts.
  - A good foundation of accessibility for people with cognitive impairments includes:
    - Delivering content in more than one way, such as by text-to-speech or by video.
    - Easily understood content, such as text written using plain-language standards.
    - Focusing attention on important content.
    - Minimizing distractions, such as unnecessary content or advertisements.
    - Consistent webpage layout and navigation.
    - Familiar elements, such as underlined links blue when not visited and purple when visited.
    - Dividing processes into logical, essential steps with progress indicators.
    - Website authentication as easy as possible without compromising security.
    - Making forms easy to complete, such as with clear error messages and simple error recovery.

When planning your project, factor accessibility testing into your testing regime, just like testing for any other important target audience segment (e.g., target desktop or mobile browsers). 
doing some testing with disabled user groups to see how well more complex site features work for them. For example:
- Is my date picker widget usable by people using screen readers?
- If content updates dynamically, do visually impaired people know about it?
- Are my UI buttons accessible using the keyboard and on touch interfaces?

## HTML: A good basis for accessibility 

A great deal of web content can be made accessible just by making sure the correct Hypertext Markup Language elements are used for the correct purpose at all times, the importance of using semantic HTML. I.e.
````js
// you can make a button like so:
<div>play video</div>

// but using it semantically will come with defaults built-in for keyboard accessibility and more suitable styling 
<button>play video</button>
````

Semantic markup also offers:
- Better on mobile - lighter in file size than non-semantic, and easier to make responsive 
- Good for SEO - search engines give importance to keywords inside headings, links, etc. 

Text content:
- One of the best accessibility aids a screen reader user can have is an excellent content structure with headings, paragraphs, lists, etc.

Using clear language: 
you should use clear language that is not overly complex and doesn't use unnecessary jargon or slang terms. This benefits all readers. You should try to avoid using language and characters that don't get read out clearly by the screen reader. For example:
- Don't use dashes if you can avoid it. Instead of writing 5–7, write 5 to 7.
- Expand abbreviations — instead of writing Jan, write January.
- Expand acronyms, at least once or twice, then use the tag to describe them.

#### UI Controls:
By UI controls, we mean the main parts of web documents that users interact with — most commonly buttons, links, and form controls.

By default, browsers allow them to be manipulated by the keyboard (i.e. by pressing 'tab')
You essentially get this behavior for free, just by using the appropriate elements.

Building keyboard accessibility back in: 
Here we've given our fake <div> buttons the ability to be focused (including via tab) by giving each one the attribute tabindex="0":
````js
// 
<div data-message="This is from the first button" tabindex="0">Click me!</div>
<div data-message="This is from the second button" tabindex="0">Click me too!</div>
<div data-message="This is from the third button" tabindex="0">And me!</div>

// allow us to activate them via the Enter/Return key. To do that, we had to add the following bit of JavaScript trickery:
document.onkeydown = function(e) {
  if(e.key === "Enter") { // The Enter/Return key
    document.activeElement.click();
  }
};
````

Better to just use the right element for the right job in the first place.

Meaningful text labels:
````js
// Make sure your labels make sense out of context, read on their own, as well as in the context of the paragraph they are in. For example, the following shows an example of good link text:
<p>Whales are really awesome creatures. <a href="whales.html">Find out more about whales</a>.</p>
//but this is bad link text:
<p>Whales are really awesome creatures. To find more out about whales, <a href="whales.html">click here</a>.</p>
````

Form labels are also important for giving you a clue about what you need to enter into each form input. Here is a good example: 
````js
// the 'for="name"' in label links it to the input
<div>
  <label for="name">Fill in your name:</label>
  <input type="text" id="name" name="name">
</div>
````
With code like this, the label will be clearly associated with the input; the description will be more like "Fill in your name: edit text." when read by the screen reader. 

Accessible Data Tables:
You can create a basic data table like so:
````js
<table>
  <tr>
    <td>Name</td>
    <td>Age</td>
    <td>Gender</td>
  </tr>
    <tr>
    <td>Gabriel</td>
    <td>13</td>
    <td>Male</td>
  </tr>
</table>
````

However a better way is to use table headers <th> and <caption>, which provide groupings of data for the screen reader. An example: https://github.com/mdn/learning-area/blob/main/css/styling-boxes/styling-tables/punk-bands-complete.html


Text Alternatives:
alt text will be read allowed by a screen reader. 
One thing to consider is whether your images have meaning inside your content, or whether they are purely for visual decoration, and thus have no meaning. If they are decorative, it is better to write an empty text as a value for alt attribute

If you do want to provide extra contextual information, you should put it in the text surrounding the image, or inside a title attribute, as shown below. In this case, most screen readers will read out the alt text, the title attribute, and the filename.

````js
<img src="dinosaur.png"
     alt="A red Tyrannosaurus Rex: A two legged dinosaur standing upright like a human, with small arms, and a large head with lots of sharp teeth.">

<img src="dinosaur.png"
     alt="A red Tyrannosaurus Rex: A two legged dinosaur standing upright like a human, with small arms, and a large head with lots of sharp teeth."
     title="The Mozilla red dinosaur">
````

Link Styling: 
- Link text color, like all text, has to be significantly different from the background color (a 4.5:1 contrast). 
- links should visually be significantly different from non-linking text, with a minimum contrast requirement of 3:1 between link text and surrounding text and between default, visited, and focus/active states and a 4:5 contrast between all those state colors and the background color.

External links and linking to non-HTML resources
- Links that open in a new tab or window via the target="_blank" declaration and links to whose href value points to a file resource should include an indicator about the behavior that will occur when the link is activated.

i.e: 
````js
<a target="_blank" href="https://www.wikipedia.org/">Wikipedia (opens in a new window)</a>
<a target="_blank" href="2017-annual-report.ppt">2017 Annual Report (PowerPoint)</a>
````


## CSS and JavaScript accessibility best practices 

CSS and JavaScript, when used properly, also have the potential to allow for accessible web experiences ... or they can significantly harm accessibility if misused.

#### CSS:

Correct semantics and user expectation.
It is possible to use CSS to make any HTML element look like anything, but this doesn't mean that you should. you should use the appropriate semantic element for the job, whenever possible.

As an example, a screen reader user can't navigate a page via heading elements if the developer hasn't appropriately used heading elements to markup the content. By the same token, a heading loses its visual purpose if you style it so it doesn't look like a heading.

The rule of thumb is that you can update the styling of a page feature to fit in your design, but don't change it so much that it no longer looks or behaves as expected. 

They have suggestions here for specific elements: https://developer.mozilla.org/en-US/docs/Learn/Accessibility/CSS_and_JavaScript

you shouldn't use visibility:hidden or display:none, because they do hide content from screen readers. Unless of course, there is a good reason why you want this content to be hidden from screen readers.

Accept that users can override your styles. They can do it in firefox, IE, or using extensions in Chrome, Safari, Opera 

#### JavaScript

JavaScript can also break accessibility, depending on how it is used.

There is no rule that says all content has to be 100% accessible to all people — you just need to do what you can, and make your apps as accessible as possible.

Complex functionality like 3D games are not so easy to make accessible — a complex 3D game created using WebGL will be rendered on a <canvas> element, which has no facility at this time to provide text alternatives or other information for severely visually impaired users to make use of. 

Arguably the main audience isn't blind people, but to make it more accessible, you could implement keyboard controls so it is usable by non-mouse users, and make the color scheme contrasting enough to be usable by those with color deficiencies.

The problem with too much JavaScript:
Sometimes you'll see a website where everything has been done with JavaScript — the HTML has been generated by JavaScript, the CSS has been generated by JavaScript, etc. This has all kinds of accessibility and other issues associated with it, so it is not advised.

Sometimes when using javascript, you'll need to use some WAI-ARIA attributes in to help solve accessibility problems caused by areas of content constantly updating without a page reload (screen readers won't pick this up or alert users to it by default).

#### Other JavaScript accessibility concerns

mouse-specific events: 
The main example you'll come across is mouse-specific events like mouseover, mouseout, dblclick, etc. Functionality that runs in response to these events will not be accessible using other mechanisms, like keyboard controls.

To mitigate such problems, you should double up these events with similar events that can be activated by other means (so-called device-independent event handlers) — focus and blur would provide accessibility for keyboard users.

````js
imgThumb.onmouseover = showImg;
imgThumb.onmouseout = hideImg;

// This can be done by tabbing over the image, because we've included tabindex="0" on it.
imgThumb.onfocus = showImg;
imgThumb.onblur = hideImg;
````

## WAI-ARIA basics

(Web Accessibility Initiative - Accessible Rich Internet Applications) 

You should only use WAI-ARIA when you need to! Ideally, you should always use native HTML features to provide the semantics required by screenreaders to tell their users what is going on.

sometimes making complex UI controls that involve unsemantic HTML and dynamic JavaScript-updated content can be difficult. WAI-ARIA is a technology that can help with such problems by adding in further semantics that browsers and assistive technologies can recognize and use to let users know what is going on

HTML5 introduced a number of semantic elements to define common page features (<nav>, <footer>, etc.) Before these were available, developers would use <div>s with IDs or classes, e.g. <div class="nav">, but these were problematic, as there was no easy way to easily find a specific page feature such as the main navigation programmatically.

Developers quite often rely on JavaScript libraries that generate such controls as a series of nested <div>s or table elements with classnames, which are then styled using CSS and controlled using JavaScript.

#### Enter WAI-ARIA

Web Accessibility Initiative - Accessible Rich Internet Applications is a specification written by the W3C, defining a set of additional HTML attributes that can be applied to elements to provide additional semantics and improve accessibility wherever it is lacking. There are three main features defined in the spec:
- Roles: These define what an element is or does. Many of these are so-called landmark roles, which largely duplicate the semantic value of HTML5 structural elements e.g. role="navigation" (<nav>), but there are also others that describe different pages structures, such as role="banner", role="search", role="tablist", role="tab", etc., which are commonly found in UIs.
- Properties: These define properties of elements, which can be used to give them extra meaning or semantics. As an example, aria-required="true" specifies that a form input needs to be filled in order to be valid, whereas aria-labelledby="label" allows you to put an ID on an element, then reference it as being the label for anything else on the page, including multiple elements, which is not possible using <label for="input">
- States: Special properties that define the current conditions of elements, such as aria-disabled="true", which specifies to a screenreader that a form input is currently disabled. States differ from properties in that properties don't change throughout the lifecycle of an app, whereas states can change, generally programmatically via JavaScript. 

Where is WAI-ARIA supported? 
Not easy to answer because: 
- There are a lot of features in the WAI-ARIA spec.
- There are many combinations of operating system, browser, and screenreader to consider.

When should you use WAI-ARIA? 
1. Signposts/Landmarks: ARIA's role attribute values can act as landmarks that either replicate the semantics of HTML5 elements (e.g. <nav>), or go beyond HTML5 semantics to provide signposts to different functional areas, e.g search, tablist, tab, listbox, etc.
2. Dynamic content updates: Screenreaders tend to have difficulty with reporting constantly changing content; with ARIA we can use aria-live to inform screenreader users when an area of content is updated, e.g. via XMLHttpRequest, or DOM APIs.
3. Enhancing keyboard accessibility: There are built-in HTML elements that have native keyboard accessibility; when other elements are used along with JavaScript to simulate similar interactions, keyboard accessibility and screenreader reporting suffers as a result. Where this is unavoidable, WAI-ARIA provides a means to allow other elements to receive focus (using tabindex).
4. Accessibility of non-semantic controls: When a series of nested <div>s along with CSS/JavaScript is used to create a complex UI-feature, or a native control is greatly enhanced/changed via JavaScript, accessibility can suffer — screenreader users will find it difficult to work out what the feature does if there are no semantics or other clues. In these situations, ARIA can help to provide what's missing with a combination of roles like button, listbox, or tablist, and properties like aria-required or aria-posinset to provide further clues as to functionality.

Practical implementations: 
https://developer.mozilla.org/en-US/docs/Learn/Accessibility/WAI-ARIA_basics#practical_wai-aria_implementations


## Accessible Multimedia

Multimedia can also create accessibility problems - video, audio, and image content need proper textual alternatives. 

1. Simple Images
  - Ensure where possible visual content has an alternative text available for screenreaders to pick up and read to their users. 
2. Accessible audio and video controls
  - The native HTML5 comes with a set of inbuild controls, however:
    - they are not keyboard-accessible in most browsers (you can't tab between them)
    - different browsers give the native controls differing styling and functionality
  - We can create our custom controls to remedy this
    - there is a guide on how to do this here: https://developer.mozilla.org/en-US/docs/Learn/Accessibility/Multimedia
3. Audio transcripts 
  - to provide deaf people with access to audio content, you need to create text transcripts
4. Video text tracks
  - makes video accessibile for deaf, visually impared
  - the main ones include:
    - captions
    - subtitles
    - descriptions
    - chapter titles


## Mobile Accessibility 

Generally, to make a website accessible and usable on mobile, you just need to follow general good web design and accessibility best practices. 

Special considerations:
1. Control mechanisms: Make sure interface controls such as buttons are accessible (i.e. work with touchscreen)
  - Events can be specific to a certain type of control mechanism (ie mouse-specific events) which can cause accessibility issues
    - i.e. mouse-specific events like 'mousedown' and 'mouseup' create problems - their event handlers will not be invoked using non-mouse controls. 
  - Some events, i.e. the 'click' event is good in terms of accessibility - the associated event handler is invoked by clicking, tabbing and pressing enter, or tapping on a touch screen device
2. User Input: Make user input requirements as painless as possible on mobile (e.g. in forms keep typing to a minimum)
  - minimise the amount of typing needed. instead of getting users to fill out their job title each time using a regular text input, you could instead offer a <select> meun offering the common options.
  - ensure HTML5 form input types such as the date are handled well 
3. Responsive Design: Make sure layouts work on mobile 
  - The practice of making your layouts and other features of your app dynamically change depending on factors like screen size and resolution, so they are usable and accessible to users of different device types 
  - Some common problems for mobile devices:
    - suitability of layouts: a multi-column layout won't work as well on a narrow screen.You can solve this with things like media queries, viewport and flexbox.
    - conserving image sizes downloaded. small screens won't need images as large as desktop counterparts and are more likely to have slow network connections. it is wise to serve smaller images to narrow devices. more info here: https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images
    - some mobile resoltions are very high - SVG images have a small file size and will stay sharp regardless of whatever size is being displayed. 
    - not disabling zoom (never set user-scalable=no). Always ensure resizing is enabled.
    - Keeping menus accessible, i.e. a "hamburger menu" is a common approach 

#### Screen reader testing on Android and iOS:

The most common mobile platforms have fully functional screen readers, which are similar to desktop screenreaders but are operated using touch gestures rather than key combinations. 

The main two are 'TalkBack' on Android and 'VoiceOver' on iOS. 


## Practical Considerations / Summary: 

- HTML Semantics: 
  - Using the correct HTML semantics will give you things for free. You can use a div but you should use a button. 
- Use clear simple language.
- For images:
  - alt text will be read allowed by a screen reader.
  - One thing to consider is whether your images have meaning inside your content, or whether they are purely for visual decoration, and thus have no meaning. If they are decorative, it is better to write an empty text as a value for alt attribute. 
  - If you do want to provide extra contextual information, you should put it in the text surrounding the image, or inside a title attribute. In this case, most screen readers will read out the alt text, the title attribute, and the filename.
- For links:
  - Link text color, like all text, has to be significantly different from the background color (a 4.5:1 contrast). 
  - links should visually be significantly different from non-linking text, with a minimum contrast requirement of 3:1 between link text and surrounding text and between default, visited, and focus/active states and a 4:5 contrast between all those state colors and the background color.
  - Links that open in a new tab or window via the target="_blank" declaration and links to whose href value points to a file resource should include an indicator about the behavior that will occur when the link is activated.
- CSS:
  - It is possible to use CSS to make any HTML element look like anything, but this doesn't mean that you should. you should use the appropriate semantic element for the job, whenever possible.
  - you shouldn't use visibility:hidden or display:none, because they do hide content from screen readers. Unless of course, there is a good reason why you want this content to be hidden from screen readers.
- Javascript:
  - Sometimes when using javascript, you'll need to use some WAI-ARIA attributes in to help solve accessibility problems caused by areas of content constantly updating without a page reload (screen readers won't pick this up or alert users to it by default).
    - You should only use WAI-ARAI when you need to, always preference semantic HTML.
    - WAI-ARIA is a technology that can help with such problems by adding in further semantics that browsers and assistive technologies can recognize and use to let users know what is going on
    - I.e. ARIA's role attribute values can act as landmarks that either replicate the semantics of HTML5 elements (e.g. <nav>), or go beyond HTML5 semantics to provide signposts to different functional areas, e.g search, tablist, tab, listbox, etc.
  - mouse-specific events like mouseover, mouseout, dblclick, etc. Functionality that runs in response to these events will not be accessible using other mechanisms, like keyboard controls or touch screen on a mobile and will need to be accounted for using other ways.
- Add a jest Axe tool to your tests for the different components. Only ~30% of a11y issues are found using this method, but its a start. We should also test our interface with the assistive technologies real users use (i.e. screen readers, mobile) and include people with disabilities in user research. 

