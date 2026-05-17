### 1、What is accessibility?
Accessibility refers to the ability of everyone, regardless of their physical or mental abilities, to access and use a service.
website：websites can be used by people who are blind or have low vision, and that web content can be read aloud by screen readers.
### 2、what is accessibility testing?

### 3、what is WAI-ARIA?
WAI-ARIA is a technology that can be used to add extra information about the structure and function of a page. This can be especially helpful for users with disabilities who are using assistive technologies.
WAI-ARIA is supported by most modern web browsers, and you can use it to add information such as labels, descriptions, and keyboard shortcuts.
EG: write the page html code, add aria elements , so that screen reader tools can tell people with vision defect the practical meaning of a button 、link

### 4、What is the WCAG?
The WCAG is developed by the World Wide Web Consortium (W3C).
WCAG provides a series of  techniques to ensure that websites and web applications are designed and developed in a way that is perceivable, operable, understandable, and robust for all users. This includes considerations for people with visual, blindness, physical, cognitive, and mental disabilities.
**Perceivable**
- Increased color contrast requirements for non-text elements to improve visibility for users with low vision.
- specifying minimum text size adjustments that don't break the layout to Support for people with low vision who may need larger font sizes by 
**Operable**
- make pointer and touch targets to be larger and more easily accessed, making it easier for users with motor impairments to interact with web content.
- allow for more flexible keyboard shortcuts to Support for users  difficulty holding down keys or performing multiple key presses
**Understandable**
- increased error identification and correction to make it easier for users to understand and fix mistakes.
- providing clear and consistent labels and instructions to help users navigate and understand web content.
**Robust**
- ensuring compatibility with assistive technologies and emerging web technologies to make web content more reliable and accessible over time.
### 5、give a example of accessibility bug using screen reader tool?
in a page, the are several buttons in manu bar. click differ button the main body of this page will change. there are 2 fileds need to input email: email for contact me and email for registry. when screen reader read the email input field, it don't read the title, so people can't distinguish what's practical use

