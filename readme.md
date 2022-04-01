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
- WAI-ARIA basics




### What is accessibility? 

Accessibility is the practice of making your websites usable by as many people as possible. I.e. those with disability, those using a mobile, or those with a slow network connection. 

Building accessible sites benefit everyone:
- Semantic HTML, which improves accessibility, also improves SEO, making your site more findable.
- Caring about accessibility demonstrates good ethics and morals, which improves your public image.
- Other good practices that improve accessibility also make your site more usable by other groups, such as mobile phone users or those on low network speed. In fact, everyone can benefit from many such improvements.
- Did we mention it is also the law in some places?

People with Visual Impairments:
Often use screen magnifiers (either physical o rsoftware zoom capabilities, i.e. most browsers have zoom). Some users rely on screen readers.

Some screen reader examples include:
- Paid commercial products, like JAWS (Windows) and Dolphin Screen Reader (Windows).
- Free products, like NVDA (Windows), ChromeVox (Chrome), and Orca (Linux).
- Software built into the operating system, like VoiceOver (macOS, iPadOS, iOS), Narrator (Windows), ChromeVox (on Chrome OS), and TalkBack (Android).

World Health Organization estimates that "285 million people are estimated to be visually impaired worldwide: 39 million are blind and 246 million have low vision." A large and significant population of users to — almost the same size as the population of the United States of America.

People with hearing impairments: 
People have various levels of hearing loss ranging from mild to profound. Although some do use AT (assistive devices), they are not widespread.

To provide access, textual alternatives must be provided. Videos should be manually captioned, and transcripts should be provided for audio content. "466 million people worldwide have disabling hearing loss", says the World Health Organization.

People with mobility impairments: 
These people have disabilities concerning movement. Some people might have difficulty making the exact hand movements required to use a mouse

The way this usually affects web development work is the requirement that controls be accessible by the keyboard. Can you use the Tab key to move between the different controls of a web form, for example?

People with cognitive impairments: 
Cognitive impairment refers to a broad range of disabilities, from people with intellectual disabilities who have the most-limited capabilities, to all of us as we age and have difficulty thinking and remembering. The range includes people with mental illnesses, such as depression and schizophrenia. It also includes people with learning disabilities, such as dyslexia and attention deficit hyperactivity disorder. Importantly, though there is a lot of diversity within clinical definitions of cognitive impairments, people with them experience a common set of functional problems. These include difficulty with understanding content, remembering how to complete tasks, and confusion caused by inconsistent webpage layouts.

A good foundation of accessibility for people with cognitive impairments includes:
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

### HTML: A good basis for accessibility 

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
you should use clear language that is not overly complex and doesn't use unnecessary jargon or slang terms. This benefits all readers. ou should try to avoid using language and characters that don't get read out clearly by the screen reader. For example:
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

If you do want to provide extra contextual information, you should put it in the text surrounding the image, or inside a title attribute, as shown above. In this case, most screen readers will read out the alt text, the title attribute, and the filename.

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


## WAI-ARIA basics 

