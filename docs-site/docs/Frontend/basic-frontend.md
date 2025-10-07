
# Frontend Development

## Quick Access to hightlights

➡️ [Quick BootStrap Style for Dashboard](#10-dbc-for-python-dash)

--- 




## 1. Rapid Website Development
Quick Start:
    Quickly build a website based on the Flask web framework.
- Frontend Stack: HTML, CSS, JavaScript correspond to Content, Presentation, and Behavior respectively.
- Web Frameworks
- MySQL Database: Storing data

In-depth Learning:
    Django framework

```python
from flask import Flask

app = Flask(__name__)


# Creates a mapping between the URL /show/info and the function index()
# When a user visits /show/info in the browser, the website automatically executes index
@app.route("/show/info")
def index():
    return "China Unicom" # Example text, "中国联通" means "China Unicom"


if __name__ == "__main__":
    app.run()
```

> In PyCharm, selecting "disconnect" is a pseudo-disconnect; the Python interpreter is still running. Use the following method to query and kill the background process.

```Shell

netstat -ano | findstr 5000  ## Flask uses port 5000
taskkill /pid  xxxxx /f\
```
## 2. Tags Recognizable by Browsers
Tags are divided into basic attributes (can modify simple style effects) and event attributes (directly set the code to respond to events).
Single tags (<tag/>) and double tags (<tag>...</tag>).
Comment: ``
### 2.0 br and hr
```HTML

<br/>   -----Line break
<hr/>   -----Horizontal rule
```
### 2.1 Encoding and `title` (`<head>`)
```HTML

<meta charset="UTF-8">
<title>My Unicom</title> ```
```
### 2.2 Headings

```html
<h1>Level 1 Heading</h1>
<h2>Level 2 Heading</h2>
<h3>Level 3 Heading</h3>
<h4>Level 4 Heading</h4>
<h5 align="left">Level 5 Heading</h5>
```
### 2.3 div, span, and p
```HTML

<div>Content</div>

<span>sfsaf</span>

<p>Paragraph tag</p>
```
- `div` takes up the whole line [Block-level tag].
- `span` takes up as much space as its content [Inline tag].
- `p` defaults to having one empty line above and below the paragraph (if space exists, it won't add more).
> Note: These two tags are quite plain + CSS styles. You can use the browser's inspect tool to see if a tag is block-level or inline.

### 2.4 Hyperlinks
```HTML

# Open in the current page
<a href="[www.amazon.com](https://www.amazon.com)">Click to jump</a>
# Open in a new tab
<a href="[www.amazon.com](https://www.amazon.com)" target="_blank">Click to jump</a>
```
### 2.5 Images
```HTML
<img src="image_address" />
```
```HTML
-Displaying your own images
	Create a static directory in the project; images need to be placed in static.
<img src="/static/xiaogong.png" />
```
Regarding setting image height and width:
```HTML
<img src="/static/xiaogong.png" style="height:100px; width:200px" />
<img src="/static/xiaogong.png" style="height:10%; width:20%" />
```
Summary of Basic HTML Tags
- Tags learned
- Classification
```HTML
- Block-level tags
	<h1></h1>
	<div></div>
  <p></p>
  <hr/>
  <ul></ul>
  <ol></ol>
  <table></table>
- Inline tags
	<span></span>
	<a></a>
	<img />
  <br/>
```
Nesting
```HTML
<div>
    <span></span>
    <a>
    	<img />
    </a>
</div>
```
### 2.6 List Tags
```HTML
-Unordered list
<ul>
    <li>ATT</li>      <li>T-mobile</li>
    <li>Mint</li>
</ul>
-Ordered list
<ol>
    <li>ATT</li>
    <li>T-mobile</li>
    <li>Mint</li>
</ol>
```
### 2.7 Tables
(Note: The image link from the original document web_notes.assets/image-20221126223534030.png will not work here unless the image is accessible at this path relative to where the Markdown is rendered.)
```HTML
<table>
    <tr> <th>ID</th><th>name</th><th>age</th></tr>  <tr> <td>1</td><td>jay</td><td>18</td> </tr>   </table>
```
Table row and column spanning:
```HTML
// Set attribute colspan="2"  to span two columns
// Set attribute rowspan="2"  to span two rows
```
Case Study: User List
```HTML
<h1>User List</h1>

<table border="1">
  <thead>
    <tr>
      <th>name</th>
      <th>photo</th>
      <th>moreInfo</th>
      <th>Operate</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>jay</td>
      <td><img src="/static/xiaogong.png" style="height: 50px;" alt="User Photo"></td>
      <td><a href="[https://www.baidu.com/](https://www.baidu.com/)" target="_blank" >View Details</a></td>  <td>Edit Delete</td>
    </tr>
  </tbody>
</table>
```
### 2.8 Input Series (7 types)
```HTML
- Inline tags
<input type="text">
<input type="password">
<input type="file">

- Radio buttons (use name='n1' to group them)
<input type="radio" name="gender" value="1">male
<input type="radio" name="gender" value="2">female

- Checkboxes
<input type="checkbox">basketball
<input type="checkbox">football
<input type="checkbox">tennis

<input type="button" value="Submit"> <input type="submit" value="Submit"> ```
```
### 2.9 Dropdown Lists

```html
<select>
    <option value="beijing">Beijing</option>
    <option value="shanghai">Shanghai</option>
    <option value="shenzhen">Shenzhen</option>
</select>
-Multiple selection
<select multiple>
    <option value="beijing">Beijing</option>
    <option value="shanghai">Shanghai</option>
    <option value="shenzhen">Shenzhen</option>
</select>
### 2.10 Multiline Text (Textarea)
```HTML
<textarea rows="10"></textarea>
```
### 2.11 Special Characters
(e.g., &lt; for <, &gt; for >, &amp; for &, &nbsp; for non-breaking space)

### 2.12 iframe Tag
(The iframe tag is used to embed another HTML document within the current page.)

### 2.13 form Tag *********
```HTML
<form action="submit_url" method="post">
    Username: <input type="text" name="username" value="default"/>
    Password: <input type="password" name="password" value="1323123">

    Country: <select name="country" id="country_select">
            <option value="">--Select Country--</option>
            <option value="china">China</option>
            </select>
    <input type="submit" value="Register">
</form>
```

Summary and Supplement
Website Request Flow
(Browser -> Request -> Server -> Response -> Browser)

Network Requests
- Typing an address in the browser URL bar and pressing Enter initiates a visit.
```txt
The browser sends data, essentially a string:
"GET /explore HTTP/1.1\r\nHost: [www.baidu.com](https://www.baidu.com)\r\n..." (Simplified example)
"POST /submit_form HTTP/1.1\r\nHost: [www.example.com](https://www.example.com)\r\nContent-Type: application/x-www-form-urlencoded\r\n\r\nname=xxx&age=19" (Simplified example)
```
- When the browser sends a request to the backend:

  - GET Request

    - Phenomenon: GET request, navigates, passes data to the backend appended to the URL.
        ```txt
        [https://www.baidu.com/web?query=request&age=19&name=xxx](https://www.baidu.com/web?query=request&age=19&name=xxx)
        ```
        Note: GET request data is visible in the URL.
 - POST Request
    - Phenomenon: Submitted data is not in the URL, but in the request body.

## Case Study: User Registration
Data on the page that needs to be submitted to the backend:

- Wrap the data-containing tags within a form tag.
  - Submission method: `method="get"` or `method="post"`
  - Submission address: `action="xx/xx/xx"`
  - There must be a submit input tag (`<input type="submit">`) inside the form.
- Tags inside the form: `<input>`, `<select>`, `<textarea>`
  - Must have a `name` attribute: `<input type="text" name="username">`
## HTML Summary
1. Terminology
```HTML
-HTML Tags: HyperText Markup Language
```
2.  HTML Tags - Default Styles, can be modified to look better.
3.  HTML is independent of programming languages.
- Java + HTML
- C# + HTML
- Python + HTML
- PHP + HTML
4. Reminder: There are many more tags, but the ones covered encompass 90% of development scenarios.
## 3. CSS Styles
CSS (Cascading Style Sheets) is specifically used to beautify tags.

- Basic CSS: Write simple pages, understand, and modify.
- Modules: Adjust and modify.
### 3.1 Quick Introduction
1. Inline Styles (On the tag)
Set "key:value; key:value;" in the tag's `style` attribute.

```HTML

<img src="..." style="height:100px;" /> <div style="color:red;">China Unicom</div>
```
2. In the `<head>` tag using `<style>` tags (*)
CSS
```css
Format:
<style>
selector {
    key: value value;
    ...
}
</style>
```
```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
        .c1{
            color:red;
        }
    </style>
</head>
<body>
<h1 class="c1">China Unicom</h1>
<h3>China Mobile</h3>
<div>
    <span style="color:darkred">Time:</span>
</div>
    ...
</body>
</html>
```
3. Writing Styles in an External File (*)
Write CSS styles in a separate `.css` file and then reference it using the `<link>` tag.

```CSS

--- common.css
.c1{
    color:red;
}
.c2{
    height:100px;
}
```
```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <link rel='stylesheet' type="text/css" href="common.css">
</head>
<body>
<h1 class="c1">China Unicom</h1>
<h3>China Mobile</h3>
<div>
    <span style="color:darkred">Time:</span>
</div>
    ...
</body>
</html>
```
### 3.2 CSS Selectors
- ID Selector (uses the `id` attribute value)

```CSS
#c1{
    color:red;
}
```
```HTML
<div id='c1'></div>
```
- Class Selector (most common)

```CSS
.c1{
    color:red;
}
```

```HTML
<div class='c1'></div>
```
- Tag Name Selector (applies CSS to all instances of a specific tag)
```CSS
li{
	color:red;
}
```
```HTML
<li>Item</li>
```
- Attribute Selector
```CSS
.c1[xx="456"]{
    color:cadetblue;
}
```
```HTML
<h3 class="c1" xx="456">China Mobile</h3>
```
- Descendant Selector

```CSS
/* Selects all <li> descendants of elements with class="yy" */
.yy li{
    color: pink;
}

/* Selects all direct <a> children of elements with class="yy" */
.yy > a{
    color: red;
}
```
```HTML
<div class="yy">
  <a>Baidu</a>
  <div>
      <a>Google</a>
  </div>
  <li>USA</li>
</div>
```
- Regarding selectors:
```txt
Commonly used: Class selector, Tag selector, Descendant selector
Less used: Attribute selector, ID selector
```
Regarding multiple styles and overriding issues:
```txt
In CSS files, later rules override earlier ones (for the same specificity).
```
Supplement: To prevent a style from being overridden, add `!important`.

```CSS
.c1{
    color:red !important;
}
.c1[xx="456"]{
    color:cadetblue; /* This will be overridden by the !important rule */
}
```
### 3.3 Styles
1. Height and Width
```CSS

.c1{
    height: 100px;
    width: 50%;
}
```
- Width supports percentages.
- Inline tags: Ineffective by default for height and width.
- Block-level tags: Effective by default (takes up full width, even if empty space remains on the right).
2. Block-level and Inline Tags
- Block-level
- Inline
- CSS style to change display behavior: `display:inline-block`;
```CSS
 <style>
    .c1{
       display:inline-block;
    }
</style>
```
```HTML
<div style="display: inline;">zh</div>  <span style="display: block;">us</span>  
```
Note: `block` and `inline-block` are commonly used.

3. Font and Color
- Color
- Size
- Weight (boldness)
- Family (style)
- CSS
```css
<style>
    .c3{
        color: #00FF7F; /* SpringGreen */
        font-size: 58px;
        font-weight: 400; /* Normal weight */
        font-family: "Microsoft YaHei", sans-serif; /* Font family */
    }
</style>
```
4. Text Alignment
```CSS
.c4{
    height: 50px;
    width: 200px;
    border: 1px solid red;

    text-align: center; /* Horizontal centering */
    line-height: 50px; /* Vertical centering (if height is known and text is single-line) */
}
```
5. Float
```HTML

<span>Left side</span>
<span style="float:right">Right side</span>
```
`div` is a block-level tag by default (takes full width). If a float style is added, multiple divs can exist on one line (content dictates width).
If a tag is floated, it is removed from the normal document flow.

```HTML

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
  <style>
    .item{
      float: left;
      width:280px;
      height:170px;
      border:1px solid  red;
    }
  </style>
</head>
<body>

<div style="background-color: dodgerblue">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  <div class="item">4</div>
  <div style="clear: both"></div> </div>
<div>Has it come out?</div> </body>
</html>
```
To bring elements back into the normal flow after floated elements:

```HTML
<div style="clear: both"></div>
```
6. Padding (Inner Margin)
Padding: Distance from the content inside a block to its border.

```CSS

padding-top: 20px;
padding: 20px 10px 20px 10px; /* top right bottom left */
```
7. Margin (Outer Margin)
```CSS

margin-top:20px;
margin: 20px 10px 20px 10px; /* top right bottom left */
```
8. div Centering
To center a block-level element (like a div) that has a defined width:

```CSS
.centered-div {
    width: 80%; /* or any specific width */
    margin-left:auto;
    margin-right:auto;
}
```
This can be shortened to:

```CSS

.centered-div {
    width: 80%;
    margin: 0 auto; /* 0 for top/bottom, auto for left/right */
}
```
9. Removing Hyperlink Underline
```CSS

a {
    text-decoration: none;
}
```
10. Removing List Markers
```CSS

ul{
	list-style:none;
}
ol{
    list-style:none; /* Also works for ordered lists if numbers are not desired */
}
```
11. Table Thin Lines (Collapsed Borders)
```CSS

table{
	border: 1px solid black;
	border-collapse:collapse;  /* Merges adjacent borders */
}
td, th {
	border: 1px solid black;
    padding: 5px; /* Add some padding for better readability */
}
```
CSS Summary
- The `body` tag has a default margin, causing white space around the page. How to remove it:
```CSS

body{
    margin:0;
}
```
- Content Centering:
  - Text centering (text will be centered within its container):
```CSS

.text-center {
    text-align:center;
}
```
- Block/Region centering (element must have a width + margin-left:auto; margin-right:auto;):
``` CSS

.container{
    width: 1226px; /* Example width */
    margin: 0 auto; /* 0 for top/bottom, auto for left/right */
}
```
- A parent element without height or width can be "stretched" by its children.
- If floats are used, remember to clear them to prevent layout issues. A common way is to add an element with clear: both; or use a clearfix method.
- Layout Division:
## 4. CSS Case Studies
### 4.1 Content Review
- HTML Tags
```txt
h1-h6 / div / span / a / img / ul / ol / li / table / input / form / etc.
```
- CSS Styles
  - Referencing: Inline, in <head>, external file.
  - CSS Properties:
```txt
height / width / display (block, inline, inline-block) / float (and clear:both) / font properties / text-align / padding, margin
```
- Page Layout
```txt
Divide the visible page into many small regions based on what you see, then populate them.
```
### 4.2 Case Study: Two-Level Menu
#### 4.2.1 Dividing Areas
(This image likely shows the menu divided into logo, menu items, and search areas.)

#### 4.2.2 Building the Skeleton
```HTML

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Two-Level Menu</title>
  <style>
    body{
      margin: 0;
    }
    .subheader{
      height: 100px;
      background-color: white;
      border-bottom: 1px solid #e0e0e0; /* Added for visual separation */
    }
    .container{
      width: 1128px;
      margin: 0 auto;
    }
    .subheader .logo{
      width: 234px; /* Adjust as needed */
      height: 100px;
      float: left;
      /* For vertical alignment of logo image if needed */
      display: flex;
      align-items: center;
    }
    .subheader .menu-list{
      /* width: auto; /* Adjust as needed, or let content define it */
      height: 100px;
      float: left;
      line-height: 100px; /* For vertical alignment of text menu items */
    }
    .subheader .search{
      /* width: auto; /* Adjust as needed */
      height: 100px;
      float: right;
      /* For vertical alignment of search content if needed */
      display: flex;
      align-items: center;
      padding-right: 20px; /* Example padding */
    }
  </style>
</head>
<body>
<div class="subheader">
  <div class="container">
    <div class="logo"> Logo Area </div>
    <div class="menu-list"> Menu List Area </div>
    <div class="search"> Search Area </div>
    <div style="clear:both;"></div>
  </div>
</div>
</body>
</html>
```

CSS Case Study Summary
- `<a>` tags are inline elements; by default, margins and explicit height/width might not apply as expected. Use `display: inline-block`; or `display: block`; if you need to control these properties.
- Vertical Centering:
  - Single-line text: Set `line-height` equal to the container's `height`.
  - Images/Blocks: Can use padding, flexbox (align-items: center;), or adjust margins.
- `<a>` tags have a default underline. Remove it with `text-decoration: none`;.
- The `:hover` pseudo-class is used to apply styles when the mouse cursor is over an element:
```CSS

.c1:hover{
	/* styles for .c1 on hover */
}
a:hover{
    /* styles for a on hover */
}
```
#### 4.4 Recommended Area (Example Section)
(This image likely shows a section of a webpage with product recommendations or featured content.)

A common style used in such areas might be for overlay effects or image opacity.

CSS Opacity Summary
CSS
## 5. Advanced CSS Concepts
### 5.1 `:hove` (Pseudo-class)
Already covered: applies styles when the mouse is over an element.

```CSS

.c1:hover{
    display:none; /* Example: hide element on hover */
}
```
### 5.2 `:after` (Pseudo-element)
Adds content after the content of the selected element.

```CSS

.c1:after{
	content: " - Suffix"; /* Adds text after .c1's content */
    color: gray;
}
```
An important application is the clearfix hack (equivalent to `<div style="clear: both"></div>`for containing floats):

```CSS

.clearfix:after{
    content: ""; /* Content must be set, even if empty */
    display: block;
    clear: both;
}
```
Usage:

```HTML

<div class="clearfix">
    <div style="float:left;">Floated</div>
    </div>
```
### 5.3 position Property
Controls the type of positioning method used for an element.

- `fixed`: Positioned relative to the viewport (browser window). It stays in the same place even when the page is scrolled.
- `relative`: Positioned relative to its normal position. Offsetting (`top`, `right`,` bottom`, `left`) will move it from this normal position, but without affecting the flow of other elements. Also creates a new positioning context for `absolute` children.
- `absolute`: Positioned relative to the nearest positioned ancestor (an ancestor with` position` other than `static`). If no positioned ancestor exists, it uses the document body (initial containing block) and moves along with page scrolling.
#### 1. `fixed` Positioning
Case Study: "Back to Top" Button
```HTML

<style>
     .back-to-top{
        position:fixed;
        width: 60px;
        height: 60px;
        border: 1px solid red;
        background-color: lightgray; /* Added for visibility */
        text-align: center; /* For text inside */
        line-height: 60px; /* For vertical text alignment */
        right: 20px; /* Distance from right edge */
        bottom: 20px; /* Distance from bottom edge */
        text-decoration: none; /* If it's an anchor */
        color: black; /* If it's an anchor */
        z-index: 100; /* Ensure it's above other content */
    }
</style>
<a href="#" class="back-to-top">Top</a> ```
```
#### Case Study: Dialog Box / Modal
Fixed positioning is often used for modal dialogs that overlay the page content.
```css
.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.5); /* Semi-transparent background */
    display: flex; /* For centering the modal content */
    justify-content: center;
    align-items: center;
    z-index: 1000; /* Ensure it's on top */
}
.modal-content {
    background-color: white;
    padding: 20px;
    border-radius: 5px;
    width: 300px; /* Example width */
}
```
#### 2. `relative` & `absolute` Positioning
An element with `position: relative`; is positioned according to the normal flow of the document. Then, offset properties (`top`, `right`, `bottom`, `left`) are applied relative to itself without affecting other elements.
An element with `position: absolute`; is removed from the normal document flow. It's positioned relative to its nearest positioned ancestor. If none exists, it's positioned relative to the initial containing block (often the `<html>` element).
#### Case Study: Xiaomi Mall Download App Popup
(This often involves an icon or button that, when hovered or clicked, shows a QR code or download link positioned absolutely relative to the icon/button which might be relatively positioned.)

```HTML

<style>
    .download-container {
        position: relative; /* Establishes positioning context for .popup */
        display: inline-block; /* Or block, depending on layout */
    }
    .download-trigger {
        padding: 10px;
        border: 1px solid #ccc;
        cursor: pointer;
    }
    .download-popup {
        position: absolute;
        bottom: 100%; /* Position above the trigger */
        left: 50%; /* Start from center of trigger */
        transform: translateX(-50%); /* Adjust to truly center */
        border: 1px solid #ccc;
        background-color: white;
        padding: 15px;
        display: none; /* Hidden by default */
        width: 200px; /* Example width */
        box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        z-index: 10; /* Ensure it's above other elements if needed */
    }
    .download-container:hover .download-popup {
        display: block; /* Show on hover */
    }
</style>

<div class="download-container">
    <div class="download-trigger">Download App</div>
    <div class="download-popup">
        <p>Scan to download</p>
    </div>
</div>
```

### 5.4 border Property
```CSS

.c1{
    border: 2px solid red; /* width style color */
    border-left: 3px dotted blue; /* Specific side */
    /* border-left-color: transparent; -- Makes border invisible but occupies space */
}
```
### 5.5 background-color Property
Sets the background color of an element.

```CSS

.element-with-bg {
    background-color: red;
}
```
## 6. Bootstrap
[Bootstrap](https://getbootstrap.com/docs/5.3/getting-started/introduction/) is a popular pre-built CSS framework.
Code path example: `E:\Projects\bootstrap_learn` (This is a local path from the notes)

- Download Bootstrap.
- Usage:
  - Include Bootstrap CSS (and optionally JS) in your page.
  - Write HTML according to Bootstrap's predefined classes and structure, then customize as needed.
  - icons [https://icons.getbootstrap.com/](https://icons.getbootstrap.com/)
  - bootstrap 5 cheetsheet [https://bootstrap-cheatsheet.themeselection.com/](https://bootstrap-cheatsheet.themeselection.com/)
  - offical cheatsheet [https://getbootstrap.com/docs/5.0/examples/cheatsheet/}](https://getbootstrap.com/docs/5.0/examples/cheatsheet/)
### 6.1 Navigation (Navs, Navbar)
Bootstrap provides components for various navigation styles.
Reference: [docs ref](https://getbootstrap.com/docs/3.4/components/#navs) (Using v3.4 link from notes)

### 6.2 Grid System
Bootstrap's grid system allows you to create responsive layouts.

- It divides the screen/container into 12 columns.
- Categories:
  - Responsive (adapts to screen width):
```txt
.col-lg-* (for large desktops, >=1200px, though original note says 1170px which might be container width)
.col-md-* (for medium desktops, >=992px, original note says 970px)
.col-sm-* (for tablets, >=768px, original note says 750px)
.col-xs-* (for phones, <768px)
```
- Non-responsive (or always stacked on extra-small screens if only col-xs-* is used):
```HTML

<div class="row">
    <div class="col-xs-6" style="background-color: #f0f0f0;">Column 1 (6 units)</div>
    <div class="col-xs-6" style="background-color: #d0d0d0;">Column 2 (6 units)</div>
</div>
```
Column Offsetting: Moves columns to the right.
```HTML

<div class="row">
    <div class="col-md-4 col-md-offset-2" style="background-color: #f0f0f0;">4 units, offset by 2</div>
</div>
```
Reference: [https://getbootstrap.com/docs/3.4/css/#grid](https://getbootstrap.com/docs/3.4/css/#grid)

### 6.3 `container` and `container-fluid`
`.container`: Fixed width, responsive container. Its `max-width` changes at different breakpoints.
```HTML

<div class="container">
    <div class="row">
        <div class="col-sm-9">Left side (9 units)</div>
        <div class="col-sm-3">Right side (3 units)</div>
    </div>
</div>
```
`.container-fluid`: Full width container, spanning the entire width of the viewport.
```HTML

<div class="container-fluid">
    <div class="row">
        <div class="col-sm-9">Left side (9 units)</div>
        <div class="col-sm-3">Right side (3 units)</div>
    </div>
</div>
```
### 6.4 Panels
Panels are used to put content in a bordered box with some padding.
Reference: [https://getbootstrap.com/docs/3.4/components/#panels](https://getbootstrap.com/docs/3.4/components/#panels)


### 6.5 Icons
- Bootstrap provides a limited set of icons (Glyphicons in v3).
- For more icons, use Font Awesome. Reference: [https://fontawesome.com/v4/](https://fontawesome.com/v4/) (Original note links to a Chinese mirror: [https://fontawesome.dashgame.com/](https://fontawesome.dashgame.com/))
  - Download Font Awesome.
  - Include its CSS in your page.
  - Use by adding `<i>` tags with appropriate classes (e.g., `<i class="fa fa-user"></i>`).
### 6.6 Bootstrap JavaScript Dependencies
Many Bootstrap components (like dropdowns, modals, carousels) rely on JavaScript and jQuery.

Download jQuery and include it in your page before Bootstrap's JavaScript file.
Include Bootstrap's JavaScript file (`bootstrap.min.js` or `bootstrap.js`).
<!-- end list -->

HTML
```HTML
<script src="path/to/jquery.min.js"></script>
<script src="path/to/bootstrap.min.js"></script>
```

## 7. Preliminary Discussion on JavaScript
- HTML: Structure
- CSS: Presentation
- JavaScript: Behavior, Dynamics
  - A programming language.
  - Libraries (modules, jQuery is a JavaScript library).
## 8. JavaScript for the Frontend
- JavaScript is a programming language; the browser acts as its interpreter. It's a weakly-typed language (variable types can change), unlike Java which is strongly-typed (variable type is fixed at definition).

- Three main characteristics:
  - Interactivity: Responds to user actions.
  - Security: Not allowed to directly access the local hard disk (for web pages running in a browser sandbox).
  - Cross-platform: Runs on various browsers and operating systems.
- DOM (Document Object Model) and BOM (Browser Object Model)
```txt
These are like built-in modules in a programming language.
For example, in Python, modules like re, random, time, json.
```
- DOM represents the HTML document structure as a tree of objects.
- BOM allows JavaScript to interact with the browser (e.g., window, history, location).
- jQuery
```txt
This is like a third-party module in a programming language.
For example, Python libraries like requests, openpyxl.
```
jQuery simplifies HTML DOM tree traversal and manipulation, as well as event handling, animation, and Ajax.

- Instance / Example

```HTML

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JS Example</title>
    <style>
        .menus{
            width: 200px;
            border: 1px solid red;
        }
        .menus .header{
            background-color: gold;
            padding: 10px; /* Adjusted padding */
            cursor: pointer; /* Indicates clickable */
        }
        .menus .item {
            padding: 10px;
            border-top: 1px solid #eee; /* Separator */
        }
    </style>
</head>
<body>
    <div class="menus">
        <div class="header" onclick="myFunc()">Header (Click Me)</div>
        <div class="item">Content</div>
    </div>

    <script type="text/javascript">
        function myFunc() {
            // alert("Hello there!");
            var proceed = confirm("Continue?"); // Returns true or false
            if (proceed) {
                console.log("User clicked OK");
            } else {
                console.log("User clicked Cancel");
            }
        }
    </script>
</body>
</html>
```

Frontend Trinity:

- HTML: The "body" / structure.
- CSS: The "clothes" / presentation.
- JavaScript: The "soul" / dynamic behavior.
### 8.1 JavaScript Core Concepts
#### 1.1 Code Position
JavaScript code can be placed in:

1. `<head>` section
2. `<body> `section (often at the end, before `</body>`, for better performance as HTML loads first).
   

#### 1.2 JS Code Forms
- Can be written inline within the HTML file (inside `<script>` tags).
- Can be in an external `.js` file, linked using the `src` attribute of the `<script>` tag.

```HTML
<script src="path/to/your/script.js"></script>
```
#### 1.3 Comments
- HTML comments:
- CSS comments (within `<style>` tags or `.css` files):
```CSS
.class-name {
	
}
/* This is a CSS comment */
```

- JavaScript comments (within `<script>` tags or .js files):

```javaScript

// This is a single-line JavaScript comment
/* This is a
   multi-line JavaScript comment */
```

#### 1.4 Variables
- JavaScript variable definition (using `var`, `let`, or `const`):
```JavaScript

var name = "jianxu"; // 'var' is function-scoped or globally-scoped
let age = 30;       // 'let' is block-scoped (preferred for most cases)
const PI = 3.14;    // 'const' is for constants, block-scoped, cannot be reassigned

console.log(name);
console.log(age);
console.log(PI);
```
#### 1.5 Relational Operators
Similar to Java, but with an additional strict equality operator `=== `and strict inequality` !==`.

`==` (loose equality, performs type coercion)
`!= `(loose inequality)
`===` (strict equality, compares value and type, no type coercion)
`!==` (strict inequality)
`>` (greater than)
`<` (less than)
`>=` (greater than or equal to)
`<=` (less than or equal to)
#### 1.6 Logical Operators
Similar to Java. In JavaScript, all variables can be treated as boolean in a logical context.
"Falsy" values: `0`, `null`, `undefined`, `""` (empty string), `NaN`, `false`. All other values are "truthy".

`&&` (logical AND)
`|| `(logical OR)
`!` (logical NOT)
#### 1.7 Arrays
JavaScript arrays can hold elements of different types.

```JavaScript

var arr = []; // Empty array
var arr1 = [1, true, "abc", null]; // Array with mixed types

// In JavaScript, if you assign a value to an array index beyond its current length,
// the array will automatically expand to accommodate it.
var sparseArray = [];
sparseArray[0] = "first";
sparseArray[2] = "third"; // sparseArray is now ["first", undefined, "third"]
console.log(sparseArray.length); // Output: 3
```
```JavaScript

// Definition
var v1 = [11, 22, 33, 44];
var v2 = new Array(11, 22, 33, 44); // Another way to define
var v3 = Array(5); // Creates an empty array with length 5

// Operations
v1[1] = "jianxu"; // Modify element at index 1: [11, "jianxu", 33, 44]

v1.push("newEnd");  // Add to end (append): [11, "jianxu", 33, 44, "newEnd"]
v1.unshift('newStart'); // Add to beginning: ["newStart", 11, "jianxu", 33, 44, "newEnd"]

// splice(startIndex, deleteCount, item1, item2, ...)
v1.splice(1, 0, "zg"); // Insert "zg" at index 1 without deleting: ["newStart", "zg", 11, "jianxu", 33, 44, "newEnd"]

var removedLast = v1.pop(); // Remove from end
var removedFirst = v1.shift(); // Remove from beginning
var removedItems = v1.splice(2, 1); // Remove 1 element starting at index 2
```
```JavaScript

// Iterating through an array
var v1 = [11, 22, 33, 44];

// for...in loop (iterates over enumerable property names, including array indices)
// Generally not recommended for arrays if order is critical or if array might have non-integer keys.
console.log("Using for...in:");
for (var idx in v1) {
	console.log(idx + ": " + v1[idx]); // idx will be "0", "1", "2", "3" (strings)
}

// Standard for loop (preferred for arrays)
console.log("Using standard for loop:");
for (var i = 0; i < v1.length; i++) {
    console.log(i + ": " + v1[i]);
}

// forEach loop (ES5+)
console.log("Using forEach:");
v1.forEach(function(element, index) {
    console.log(index + ": " + element);
});

// for...of loop (ES6+) (iterates over values)
console.log("Using for...of:");
for (var value of v1) {
    console.log(value);
}
```
Note: `break` and `continue` work within loops as expected.

Case Study: Dynamically Populating a List
```HTML

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Dynamic List</title>
</head>
<body>
<ul id="city">
</ul>

<script type="text/javascript">
    var city_list = ['Beijing', "Shanghai", 'Shenzhen'];
    var parentTag = document.getElementById("city"); // Get the <ul> element once

    for (var idx in city_list) { // Using for...in here, but for...of or a standard for loop is often preferred for arrays
        var txt = city_list[idx];

        // Create an <li> tag (DOM manipulation)
        var tag = document.createElement("li");
        // Set the text content of the <li> tag
        tag.innerText = txt; // or tag.textContent = txt;

        // Add the new <li> to the <ul> tag (DOM manipulation)
        parentTag.appendChild(tag);
    }
</script>
</body>
</html>
```
#### 1.8 Functions
Declaration Format 1 (Function Declaration):

```JavaScript

function functionName(param1, param2) {  // Parameters don't need types
	// function body
    return param1 + param2;
}

var result = functionName(5, 3); // result will be 8
```
Declaration Format 2 (Function Expression):

```JavaScript

var functionName = function(param1, param2) {
    // function body
    return param1 * param2;
};

// Example
var fun1 = function (a, b) {
    alert("Function with parameters: " + a + " and " + b);
    return a + b;
};
fun1(1, 2);
```
JavaScript does not support function overloading in the same way as languages like Java or C++. If you define two functions with the same name, the later definition will overwrite the earlier one.

`arguments` object (Implicit Parameter):
Inside any `function` (not arrow functions), there's an `arguments` object which is an array-like object containing all arguments passed to the function, regardless of the named parameters.

```JavaScript

function displayArgs(a) {
    console.log("Number of arguments passed: " + arguments.length); // e.g., 3
    console.log("First argument: " + arguments[0]); // e.g., 1 (which is 'a')
    console.log("Second argument: " + arguments[1]); // e.g., "b"
    console.log("Third argument: " + arguments[2]); // e.g., "c"
}
displayArgs(1, "b", "c");

function sumAll() {
    var result = 0;
    for (var i = 0; i < arguments.length; i++) {
        if (typeof arguments[i] === "number") { // Use === for strict type checking
            result += arguments[i];
        }
    }
    return result;
}
var total = sumAll(1, 2, 3, "abc", 4, 5); // total will be 15
console.log(total);
```
#### 1.9 JS Custom Objects (Similar to creating classes/objects in Java)
Object Definition (Constructor Style - less common for simple objects now):

```JavaScript

var myObject = new Object();     // Object instance (empty object)
myObject.propertyName = "value"; // Define a property
myObject.methodName = function() { // Define a method
    console.log("Method called, property is: " + this.propertyName);
};

// Accessing object members:
console.log(myObject.propertyName);
myObject.methodName();
```
Object Literal Notation (More common and preferred for simple objects):

```JavaScript

var myLiteralObject = {}; // Empty object

var person = {
    firstName: "John",            // Property
    lastName: "Doe",              // Property
    age: 30,
    fullName: function() {        // Method
        return this.firstName + " " + this.lastName;
    },
    greet: function() {
        console.log("Hello, my name is " + this.fullName() + " and I am " + this.age + " years old.");
    }
};

console.log(person.firstName);
console.log(person.fullName());
person.greet();
```
####1.10 String Type
``` JavaScript

// Declaration
var greeting = "Hello, World!";
var name = 'JavaScript'; // Single or double quotes can be used

// Common string properties and methods
var myString = "  中国联通  "; // "中国联通" means "China Unicom"

console.log("Length: " + myString.length); // Includes leading/trailing spaces

// Accessing characters
console.log("Character at index 3: " + myString.charAt(3)); // "国" (index 3 because of leading spaces)
console.log("Character using bracket notation: " + myString[3]); // Same as charAt(3)

// Trimming whitespace
var trimmedString = myString.trim(); // Removes leading and trailing whitespace: "中国联通"
console.log("Trimmed: '" + trimmedString + "'");

// Substring (substring(startIndex, endIndex) - endIndex is not included)
var sub = trimmedString.substring(0, 2); // "中国" (characters at index 0 and 1)
console.log("Substring(0,2): " + sub);

// Other useful methods:
console.log("Uppercase: " + trimmedString.toUpperCase());
console.log("Lowercase: " + trimmedString.toLowerCase());
console.log("Index of '联通': " + trimmedString.indexOf("联通")); // Returns starting index or -1 if not found
console.log("Includes '国': " + trimmedString.includes("国")); // ES6: returns true/false
var words = "apple,banana,orange".split(','); // ["apple", "banana", "orange"]
console.log("Split: " + words);
```
Case Study: Marquee Effect (Simple Text Animation)
```HTML

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Marquee Effect</title>
</head>
<body>

<span id="txt">Welcome to this place for a tour! </span> <script type="text/javascript">
    var intervalId; // To store the interval ID for potential clearing

    function startMarquee() {
        // 1. Find the tag's content in HTML (DOM)
        var tag = document.getElementById("txt");
        var dataString = tag.innerText;

        // 2. Animate: Move the first character to the end of the string
        if (dataString.length > 0) {
            var firstChar = dataString[0];
            var otherString = dataString.substring(1); // Get the rest of the string
            var newTxt = otherString + firstChar;

            // 3. Update in HTML
            tag.innerText = newTxt;
        }
    }

    // JavaScript timer: execute the show function every 1000 milliseconds (1 second)
    intervalId = setInterval(startMarquee, 300); // Changed to 300ms for smoother effect

    // To stop the marquee (optional):
    // clearInterval(intervalId);
</script>

</body>
</html>
```
#### 1.11 Conditional Statements
```JavaScript

var age = 20;

if (age >= 18) {
    console.log("Adult");
} else {
    console.log("Minor");
}

var score = 85;
if (score >= 90) {
    console.log("Grade A");
} else if (score >= 80) {
    console.log("Grade B");
} else if (score >= 70) {
    console.log("Grade C");
} else {
    console.log("Grade D or F");
}

// Switch statement
var day = new Date().getDay(); // 0 (Sunday) to 6 (Saturday)
var dayName;
switch (day) {
    case 0: dayName = "Sunday"; break;
    case 1: dayName = "Monday"; break;
    case 2: dayName = "Tuesday"; break;
    case 3: dayName = "Wednesday"; break;
    case 4: dayName = "Thursday"; break;
    case 5: dayName = "Friday"; break;
    case 6: dayName = "Saturday"; break;
    default: dayName = "Unknown";
}
console.log("Today is " + dayName);
```
#### 8.2 JS Events
Events are actions that occur in the browser, like a user clicking a button, a page finishing loading, or an input field losing focus. JavaScript can "listen" for these events and execute code in response.

1. `onload` Event
Fires when the entire page (including all dependent resources like stylesheets and images) has finished loading. Typically used on the `<body>` or `window` object.

Static registration (HTML attribute):

```HTML

<body onload="onloadFun();">
    <script type="text/javascript">
        function onloadFun() {
            alert("Page fully loaded (static registration).");
        }
    </script>
</body>
```
Dynamic registration (JavaScript):

```HTML

<head>
    <meta charset="UTF-8">
    <title>Onload Event</title>
  <script type="text/javascript">
      // onload event method
      function handlePageLoad() {
        alert("Page fully loaded (dynamic registration via function).");
      }

      // onload event dynamic registration, common practice:
      window.onload = function () {
        // This function will execute when the page is fully loaded.
        // It's good practice to put DOM manipulation code here or after the DOM is loaded.
        alert("Page fully loaded (dynamic registration via anonymous function).");
        // You could also call another function:
        // handlePageLoad();
      };
      // Note: Assigning to window.onload multiple times will overwrite previous assignments.
      // For multiple onload handlers, use addEventListener:
      // window.addEventListener('load', function() { alert("Listener 1 loaded!"); });
      // window.addEventListener('load', function() { alert("Listener 2 loaded!"); });
  </script>
</head>
<body>
    Content of the page.
</body>

```
2. `onclick` Event
Fires when an element is clicked.

Static registration (HTML attribute):

```HTML

<button onclick="onclickFun();">Button One (Static)</button>
<script>
    function onclickFun() {
        alert("Static onclick event triggered for Button One.");
    }
</script>
```
Dynamic registration (JavaScript):
```HTML

<button id="btn02">Button Two (Dynamic)</button>

<script type="text/javascript">
    // It's best to ensure the DOM is loaded before trying to attach events to elements.
    window.onload  = function () {
        // 1. Get the DOM element
        var btnObj = document.getElementById("btn02");

        if (btnObj) { // Check if the element exists
            // 2. Assign the event handler: element.eventname = function(){}
            btnObj.onclick = function () {
                alert("Dynamic onclick event triggered for Button Two.");
            };
        } else {
            console.error("Element with ID 'btn02' not found.");
        }
    };
</script>
```
3. `onblur` Event
Fires when an element loses focus (e.g., clicking outside an input field after clicking into it).

```HTML
Password: <input id="password" type="password">

<script type="text/javascript">
    window.onload = function () {
        var pwdObj = document.getElementById("password");
        if (pwdObj) {
            pwdObj.onblur = function () {
                console.log("Password field lost focus (onblur event).");
                // Example: Validate input when focus is lost
                if (this.value.length < 6 && this.value.length > 0) {
                    alert("Password should be at least 6 characters long.");
                }
            };
        }
    };
</script>
```
4. `onchange` Event
Fires when the value of an element (like `<input>`, `<select>`, `<textarea>`) has been changed. For text inputs and textareas, it usually fires when the element loses focus after its value has been modified. For select boxes, radio buttons, and checkboxes, it fires immediately after the selection changes.

```HTML

<select id="mySelect">
    <option value="1">Option 1</option>
    <option value="2">Option 2</option>
</select>
<input type="text" id="myText" placeholder="Type and then click away">

<script>
    window.onload = function() {
        var selectEl = document.getElementById("mySelect");
        var textEl = document.getElementById("myText");

        if (selectEl) {
            selectEl.onchange = function() {
                console.log("Select value changed to: " + this.value);
            };
        }
        if (textEl) {
            textEl.onchange = function() {
                console.log("Text input value changed to: " + this.value);
            };
        }
    };
</script>
```
5. `onsubmit` Event
Fires when a form is submitted. It's often used to validate form data before sending it to the server. If the event handler returns `false`, the form submission is cancelled.

Static registration:
```HTML
<form action="[http://example.com/submit](http://example.com/submit)" method="get" onsubmit="return onSubmitFunStatic();">
    Username: <input type="text" name="username" id="userStatic">
    <input type="submit" value="Submit Static">
</form>
<script>
    function onSubmitFunStatic() {
        var username = document.getElementById("userStatic").value;
        if (username.trim() === "") {
            alert("Username cannot be empty (static validation).");
            return false; // Prevents form submission
        }
        alert("Static form submitting...");
        return true; // Allows form submission
    }
</script>
```
Dynamic registration:

```HTML

<form action="[http://example.com/submit](http://example.com/submit)" method="get" id="form01">
    Password: <input id="passwordDynamic" type="password" name="password">
    <input type="submit" value="Submit Dynamic">
</form>
<script type="text/javascript">
    window.onload = function () {
        var formObj = document.getElementById("form01");
        if (formObj) {
            formObj.onsubmit = function () {
                // Example validation
                var password = document.getElementById("passwordDynamic").value;
                if (password.length < 6) {
                    alert("Password too short (dynamic validation). Submission blocked.");
                    return false; // Prevents submission if validation fails
                }
                alert("Dynamic form submitting...");
                return true; // Allows submission if validation passes
            };
        }
    };
</script>
```
### 8.3 DOM (Document Object Model)
(This image likely depicts the DOM tree structure: `window` at the top, then `document`, then HTML elements like `head`, `body`, etc., forming a hierarchy.)

The DOM is an API (Application Programming Interface) for HTML and XML documents. It defines the logical structure of documents and the way a document is accessed and manipulated. With the DOM, programmers can create and build documents, navigate their structure, and add, modify, or delete elements and content.

```JavaScript

// Get an element by its ID
var myElement = document.getElementById("myId");

if (myElement) {
    // Get the text content of the element
    var text = myElement.innerText; // Or .textContent for better standard compliance
    console.log("Original text: " + text);

    // Modify the text content of the element
    myElement.innerText = "Hello, DOM!"; // Or .textContent

    // Modify HTML content
    // myElement.innerHTML = "<strong>Important!</strong> Hello, DOM!";
}

// Create a new element
var newP = document.createElement("p");
newP.innerText = "This is a new paragraph.";

// Append the new element to an existing one (e.g., the body)
document.body.appendChild(newP);

// Get elements by tag name (returns an HTMLCollection)
var allDivs = document.getElementsByTagName("div");
for (var i = 0; i < allDivs.length; i++) {
    // allDivs[i].style.border = "1px solid blue"; // Example: add border to all divs
}

// Get elements by class name (returns an HTMLCollection)
var items = document.getElementsByClassName("item");

// Get elements by CSS selector (more versatile)
var firstItem = document.querySelector(".item"); // Returns the first match
var allItems = document.querySelectorAll(".item"); // Returns a NodeList of all matches
```


#### 2.1 Event Binding (Reiteration and Alternatives)
Note: The DOM provides many operations. While powerful, direct DOM manipulation can be verbose.
```txt
DOM can achieve many functionalities, but it can be cumbersome.
Modern web development often uses libraries/frameworks like jQuery, Vue.js, or React for more efficient and declarative DOM manipulation and event handling.
```
Standard DOM Event Handling (preferred over `on<event>` properties for multiple handlers):
`element.addEventListener(eventType, handlerFunction, useCapture);`
`element.removeEventListener(eventType, handlerFunction, useCapture);`

#### 2.2 Common Attributes and Methods of Nodes (Elements)
- `innerText`: Gets/sets the text content of an element, excluding HTML tags. Browser differences exist; textContent is more standard and generally preferred for getting/setting only text.
- `innerHTML`: Gets/sets the HTML content (including tags) within an element.
- `appendChild()` and `createElement()` methods are often used together to dynamically add elements to the DOM.
Example:

```HTML

<div id="container">
    <p>First paragraph.</p>
</div>
<script>
    var container = document.getElementById("container");
    if (container) {
        console.log("innerHTML:", container.innerHTML); // "<p>First paragraph.</p>"
        console.log("innerText:", container.innerText); // "First paragraph." (may vary slightly by browser)
        console.log("textContent:", container.textContent); // "First paragraph." (more consistent)

        var newSpan = document.createElement("span");
        newSpan.textContent = " A new span!";
        newSpan.style.color = "green";

        var pInContainer = container.querySelector("p");
        if (pInContainer) {
            pInContainer.appendChild(newSpan); // Adds span inside the paragraph
        }

        // container.innerHTML += "<p>Another paragraph added via innerHTML.</p>"; // Re-parses content
    }
</script>
```
### 8.4 Knowledge Review (General IT Concepts)
- Encoding Related:
```txt
When a file is saved, it uses a certain encoding. To open it correctly, the same encoding must be used; otherwise, Mojibake (garbled characters) will occur.
Characters are essentially stored as 01010101 at the lowest level.
Character-to-binary mapping relationships (encodings):
    - ASCII encoding: 256 mappings (mostly for English).
    - GB2312, GBK: Chinese and some Asian countries [Chinese characters typically 2 bytes].
    - Unicode: A standard for encoding most of the world's writing systems. UCS-2/UCS-4 are specific Unicode encodings.
    - UTF-8 encoding: A variable-width Unicode encoding [In UTF-8, Chinese characters typically occupy 3 bytes, but can be more].

Python interpreter default encoding is often UTF-8.
HTML pages should declare their encoding: <meta charset="UTF-8">
```
- Computer Units:
```txt
Bit (b) / Byte (B) / Kilobyte (KB) / Megabyte (MB) / Gigabyte (GB) / Terabyte (TB)
1 Byte = 8 Bits
1 KB = 1024 Bytes (in computing, though sometimes 1000 is used for storage marketing)
1 MB = 1024 KB
...
```

- String Formatting (Python examples from notes):

```Python

# Python string formatting examples (not JavaScript, but included in original notes)
name_py = "jianxu"
age_py = 33

# Method 1: .format()
v1_py = "I am {}, and my age is {}".format(name_py, age_py)  # Recommended in older Python
print(v1_py)

# Method 2: f-strings (Python 3.6+)
v2_py = f"I am {name_py}, and my age is {age_py}" # Current recommendation
print(v2_py)

# Method 3: % operator (older style)
v3_py = "I am %s, and my age is %d" % (name_py, age_py)
print(v3_py)
```
### 8.5 jQuery
jQuery is a fast, small, and feature-rich JavaScript library. It makes things like HTML document traversal and manipulation, event handling, animation, and Ajax much simpler with an easy-to-use API that works across a multitude of browsers.

- Based on jQuery, you can develop your own functionalities.
- Many existing tools/plugins rely on jQuery (e.g., some Bootstrap dynamic effects).
- A jQuery object is an array-like object containing DOM elements, augmented with jQuery's own methods.
### 1. Quick Start
Download jQuery:
Official site: [jquery.com](https://jquery.com/)
CDN link from notes: [https://code.jquery.com/jquery-3.6.0.min.js](https://code.jquery.com/jquery-3.6.0.min.js) (This is a specific version)

Apply jQuery (Include it in your HTML):

```HTML

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery Quick Start</title>
</head>
<body>

<h1 id="txt">China Unicom</h1>

<script src="static/jquery-3.6.0.min.js"></script> <script type="text/javascript">
    // Utilize jQuery functionalities to achieve effects

    // 1. Find the tag with id=txt (jQuery selector)
    // The $ sign is an alias for jQuery
    var $myHeading = $("#txt"); // $myHeading is now a jQuery object

    // 2. Modify its content using a jQuery method
    $myHeading.text("USA Unicom"); // Changed content
</script>

</body>
</html>
```
### 2. `$` is the jQuery Core Function (and Alias)
The `$` symbol is typically an alias for the `jQuery` function. It's the entry point for most jQuery operations.
`$(selector):` Selects DOM elements.
`$(htmlString)`: Creates DOM elements from an HTML string.
`$(domElement)`: Wraps a DOM element in a jQuery object.
`$(function() { ... })`: A shorthand for `$(document).ready(function() { ... })`; which executes code once the DOM is fully loaded and ready for manipulation.

### 3. jQuery Object and DOM Object Conversion
- jQuery Object to DOM Object: A jQuery object is array-like. To get the underlying DOM element, you can use array indexing or the `.get() `method.
```JavaScript

var $jqObject = $("#myElement"); // jQuery object
var domElement1 = $jqObject[0];    // DOM element
var domElement2 = $jqObject.get(0); // DOM element
// Now you can use DOM properties/methods on domElement1 or domElement2
// e.g., console.log(domElement1.id);
```
- DOM Object to jQuery Object: Wrap the DOM element with $(...).
```JavaScript

var domElement = document.getElementById("myElement"); // DOM element
var $jqObject = $(domElement); // jQuery object
// Now you can use jQuery methods on $jqObject
// e.g., $jqObject.hide();
```
### 4. Selector Types
jQuery uses CSS-like selectors to find elements in the DOM.

1. Basic Selectors (Directly find tags)
- ID Selector: `$("#txt")` (Selects the element with `id="txt"`)
- Class Selector: `$(".c1")` (Selects all elements with `class="c1"`)
- Tag Selector: `$("div")` (Selects all `<div> `elements)
- Descendant Selector: `$("div span")` (Selects all `<span>` elements that are descendants of `<div>` elements)
- Child Selector: `$("ul > li") `(Selects all `<li>` elements that are direct children of` <ul> `elements)
- Multiple Selector: `$(".c1, #c2, div")` (Selects elements matching any of these selectors)
- Attribute Selector: `$("input[name='n1']` (Selects `<input>` elements with `name="n1"`)
  - `$("a[href^='http']")` (Links starting with http)
  - `$("img[src$='.png']")` (Images ending with .png)
  - `$("input[type='text']")`
Creating tags: `$("<li>New List Item</li>")` or `$("<li>").text("New List Item")`

2. Hierarchy / Traversing Selectors
These methods allow you to navigate the DOM tree relative to already selected elements.

- Siblings:

```JavaScript

$("#c1").prev()          // The immediately preceding sibling of #c1
$("#c1").next()          // The immediately following sibling of #c1
$("#c1").siblings()      // All siblings of #c1
$("#c1").siblings(".active") // All siblings of #c1 with class "active"
// $("#c1").next().next() // Next's next sibling
```
- Parent(s) / Children / Descendants:

```JavaScript

$("#c1").parent()             // The direct parent of #c1
$("#c1").parents()            // All ancestors of #c1 up to <html>
$("#c1").parents(".container")// All ancestors of #c1 with class "container"
// $("#c1").parent().parent() // Grandparent of #c1

$("#c1").children()           // All direct children of #c1
$("#c1").children(".p10")     // All direct children of #c1 with class="p10"

$("#c1").find(".p10")         // All descendants (children, grandchildren, etc.) of #c1 with class="p10"
$("#c1").find("div")          // All <div> descendants of #c1
```
Case Study: Menu Toggle (Accordion Style)
```HTML

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery Menu Toggle</title>
    <style>
        .my_menu {
            width: 200px;
            border: 1px solid #ccc; /* Lightened border */
        }
        .my_menu .item .header{ /* Target header specifically within item */
            background-color: gold;
            padding: 10px 5px;
            cursor: pointer;
            border-bottom: 1px solid #eee; /* Separator */
        }
        .my_menu .item:last-child .header { /* Remove bottom border from last header */
            border-bottom: none;
        }
        .my_menu .item .content a { /* Target links within content */
            display: block;
            padding: 8px 10px; /* Adjusted padding */
            border-bottom: 1px dotted #ddd; /* Lightened border */
            text-decoration: none;
            color: #333;
        }
        .my_menu .item .content a:last-child {
            border-bottom: none;
        }
        .my_menu .item .content a:hover {
            background-color: #f0f0f0;
        }
        .hide { /* Utility class to hide elements */
            display: none;
        }
    </style>
</head>
<body>

<div class="my_menu">
    <div class="item">
        <div class="header">Shanghai</div> <div class="content hide">
            <a>Pudong</a>
            <a>Xuhui</a>
            <a>Jing'an</a>
        </div>
    </div>
    <div class="item">
        <div class="header">Beijing</div>
        <div class="content hide">
            <a>Haidian</a>
            <a>Chaoyang</a>
            <a>Xicheng</a>
        </div>
    </div>
</div>

<script src="static/jquery-3.6.0.min.js"></script> <script>
    $(document).ready(function() { // Ensures DOM is ready
        $(".my_menu .item .header").click(function() {
            // 'this' refers to the clicked .header DOM element
            var $currentHeader = $(this);
            var $currentContent = $currentHeader.next(".content");

            // Toggle the current content
            $currentContent.slideToggle(); // jQuery animation for smooth toggle

            // Optional: Hide other open content sections (accordion effect)
            $(".my_menu .item .content").not($currentContent).slideUp();
        });
    });

    /*
    // Original function (can be replaced by the jQuery version above)
    function clickMe(self) { // self is the DOM element
        // $(self) -> jQuery object for the clicked header
        // .removeClass("hide") removes the class
        var $content = $(self).next(); // Get the .content div sibling
        var hasHide = $content.hasClass("hide");

        if (hasHide) {
            $content.removeClass("hide"); // Show
            // Simultaneously hide other open sections
            $(self).parent().siblings().find(".content").addClass("hide");
        } else {
            $content.addClass("hide"); // Hide
        }
    }
    */
</script>
</body>
</html>
```
### 5. Style Operations
jQuery provides methods to easily manipulate CSS classes and styles.

- Class Manipulation:
  - `addClass("className")`: Adds one or more classes.
  - `removeClass("className")`: Removes one or more classes.
  - `toggleClass("className")`: Toggles a class (adds if not present, removes if present).
  - `hasClass("className")`: Checks if an element has a specific class (returns true or false).
- Direct CSS Manipulation:
- `.css("propertyName")`: Gets the value of a CSS property.
- `.css("propertyName", "value")`: Sets a single CSS property.
- `.css({ "propertyName1": "value1", "propertyName2": "value2" })`: Sets multiple CSS properties. <!-- end list -->
```JavaScript

$("#myDiv").addClass("highlighted important");
$("#myDiv").removeClass("oldClass");
$("#myDiv").toggleClass("active");

if ($("#myDiv").hasClass("active")) {
    console.log("It's active!");
}

// Get CSS property
var bgColor = $("#myDiv").css("background-color");
console.log(bgColor);

// Set CSS property
$("#myDiv").css("color", "blue");
$("#myDiv").css({
    "font-weight": "bold",
    "padding": "20px"
});
```
- Appending/Prepending Content:
```JavaScript

var newLi = $("<li>New item</li>");
$("#view").append(newLi);    // Appends newLi as the last child of #view (e.g., an <ul>)
$("#view").prepend(newLi);   // Prepends newLi as the first child of #view
// Other methods: .before(), .after(), .appendTo(), .prependTo()
```

### 6. Events in jQuery
jQuery simplifies event handling.
Common event methods: `.click(), .dblclick(), .hover(), .mousedown(), .mouseup(), .mouseenter(), .mouseleave(), .mousemove(), .focus(), .blur(), .change(), .submit(), .keydown(), .keyup(), .keypress().`

Event Binding with `.on() `(Recommended for flexibility and dynamic elements):
The `.on()` method attaches one or more event handlers for the selected elements and child elements.
Syntax: `$(selector).on(events, selector, handler);`

- `events`: One or more space-separated event types (e.g., "click", "mouseover keydown").
- `selector` (optional): A selector string to filter the descendants of the selected elements that trigger the event. If `null` or omitted, the event is always triggered when it reaches the selected element.
- `handler`: A function to execute when the event is triggered.
<!-- end list -->

```JavaScript
$(document).ready(function() {
    // Direct binding to existing h5 elements
    // $("h5").click(function () {
    // 	alert('h5 click event == .click() method binding');
    // });

    // Event delegation using .on() for h5 elements, including those added later
    // This binds the event to #panel, but only triggers if the click originated from an h5 inside #panel
    $("#panel").on("click", "h5", function () {
        alert('h5 click event == .on() method binding (delegated)');
        $(this).css("color", "red"); // 'this' refers to the clicked h5
    });

    // Add a new h5 element to the panel dynamically
    <span class="math-inline">\('<h5 class\="head"\>What is jQuery? \(Dynamically Added\)</h5\>'\)\.appendTo\(</span>("#panel"));

    // Triggering an event
    // $("button").click(function () {
    // 	$("h5").first().click(); // Triggers the click event on the first h5
    // });

    // Mouse events
    // $("#panel").on("mouseover", "h5", function () {
    // 	console.log("Mouse entered h5: " + $(this).text());
    // });
    // $("#panel").on("mouseout", "h5", function () {
    // 	console.log("Mouse left h5: " + $(this).text());
    // });

    // .bind() is an older way, .on() is preferred.
    // $("h5").bind("click mouseover mouseout", function () {
    // 	console.log("This is a bind-bound event for: " + $(this).text());
    // });

    // .one() binds an event handler that executes at most once per element per event type.
    // $("#panel").one("click", "h5", function () {
    // 	console.log("This h5 one-time click event for: " + $(this).text());
    // });

    // To unbind events: .off()
    // $("#panel").off("click", "h5"); // Removes the specific delegated click handler
});
```
```HTML
<div id="panel" style="border:1px solid green; padding:10px;">
    <h5>What is HTML?</h5>
    <h5>What is CSS?</h5>
</div>
<button id="triggerButton">Trigger Click on First H5</button>
<button id="addButton">Add New H5</button>

<script>
$(document).ready(function() {
    $("#panel").on("click", "h5", function() {
        alert('Clicked: ' + $(this).text());
        $(this).toggleClass('highlight');
    });

    $("#addButton").click(function() {
        <span class="math-inline">\('<h5 class\="new"\>What is JavaScript? \(New\)</h5\>'\)\.appendTo\(</span>("#panel"));
    });

    $("#triggerButton").click(function() {
        $("#panel h5:first-child").trigger("click"); // Programmatically trigger click
    });
});
</script>
<style>.highlight { background-color: yellow; }</style>
```
Inside an event handler, `$(this)` refers to the jQuery object for the DOM element that triggered the event.

```HTML

<ul>
    <li>Beijing</li>
    <li>Shanghai</li>
    <li>Guangzhou</li>
</ul>
<script>
    $(document).ready(function() {
        $("li").click(function() {
            // When an <li> is clicked, this function executes.
            // $(this) refers to the specific <li> that was clicked.
            console.log("You clicked: " + $(this).text());
            $(this).css("color", "blue");
        });
    });
</script>
```
Removing elements in jQuery:

```HTML

<div id="c1" style="border:1px solid red; padding:10px;">Content to be removed</div>
<button id="removeBtn">Remove Div</button>
<script>
    $(document).ready(function() {
        $("#removeBtn").click(function() {
            $("#c1").remove(); // Removes the element #c1 from the DOM
            console.log("Div #c1 removed.");
        });
    });
</script>
```
- `$(function(){ ... });` is a shorthand for `$(document).ready(function(){ ... })`;. It ensures that the code inside it runs only after the entire DOM (the page structure) is fully loaded and ready to be manipulated. This prevents errors that might occur if you try to access or modify elements that haven't been created yet.
```HTML

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document Ready Example</title>
</head>
<body>

<ul>
    <li>Beijing</li>
    <li>Shanghai</li>
    <li>Guangzhou</li>
</ul>

<script src="static/jquery-3.6.0.min.js"></script>
<script>
    $(function() {
        // This code runs after the DOM is ready.
        $("li").click(function() {
            // $(this) refers to the clicked <li> element.
            $(this).remove(); // Removes the clicked <li>
            console.log($(this).text() + " removed.");
        });
        console.log("DOM is ready, event handlers attached.");
    });
</script>
</body>
</html>
```

## 9. XML (Extensible Markup Language)
### 1. Introduction


- What is XML? XML stands for Extensible Markup Language.
- Purpose: It was designed to store and transport data. It's self-descriptive.
- Key Characteristics:
  - XML is not a replacement for HTML. HTML is for displaying data; XML is for carrying data.
  - XML tags are not predefined. You must define your own tags.
  - XML is case sensitive. <Message> is different from <message>.
  - All XML elements must have a closing tag.
  - XML documents must have one root element.
  - Attribute values must always be quoted.
  - XML preserves white space.
- Example:
```XML
<?xml version="1.0" encoding="UTF-8"?>
<note>
    <to>Tove</to>
    <from>Jani</from>
    <heading>Reminder</heading>
    <body>Don't forget me this weekend!</body>
</note>
```
> XML is often used in configuration files, for data exchange between applications (e.g., web services like SOAP), and as a base for other markup languages (e.g., SVG, RSS). While JSON has become more popular for data interchange on the web due to its simplicity and direct mapping to JavaScript objects, XML still has its uses.


## 10. DBC for Python Dash
### What is BDC for Python Dash?

**BDC (Big Data Components)** for Python Dash is an open-source extension package that enhances the Dash framework with advanced UI elements, layout capabilities, and interactive data components. It is designed to accelerate the development of big-data dashboards and analytical applications with minimal code.

---

### Advantages of Using Dash Bootstrap Components
Using DBC offers several key benefits for Dash developers:

- **Rapid UI Development**: Quickly create good-looking, responsive layouts using pre-built components like navbars, cards, alerts, and modals.
- **Bootstrap Styling**: Easily apply Bootstrap themes and styling to your Dash app for a professional and modern appearance. There are many free and paid Bootstrap themes available (like Bootswatch themes that DBC makes easy to use).
- **Responsive Design**: Components are inherently responsive, meaning your Dash app will adapt to different screen sizes (desktops, tablets, mobiles) with minimal extra effort.
- **Simplified Layouts**: Provides powerful layout components like `Row`, `Col`, and `Container` that leverage Bootstrap's responsive grid system, making complex page structures manageable in Python.
-** Theming**: Comes with support for all the standard Bootstrap themes and makes it easy to switch between them or use custom Bootstrap themes.
- **Reduced CSS/JS**: Minimizes the need to write custom CSS or JavaScript for common UI patterns and styling.
- **Community and Documentation**: Benefits from the vast Bootstrap community and resources, in addition to DBC's own helpful documentation.

---

### Basic Functions and Components
DBC provides a wide array of components that mirror those available in Bootstrap. Some of the core functionalities and commonly used components include:

- Layout Components:
  - `dbc.Container`: For wrapping page content, can be fixed-width or fluid.
  - `dbc.Row`: Creates horizontal groups of columns.
  - `dbc.Col`: The fundamental building block for layouts, creating columns within rows. You can specify widths for different screen sizes (e.g., `sm=6, md=4`).
- Content Components:
  - `dbc.Alert`: For displaying contextual feedback messages.
  - `dbc.Badge`: Small count and labeling components.
  - `dbc.Card`: A flexible and extensible content container with options for headers, footers, images, and body content.
  - `dbc.ListGroup`: For displaying series of content.
  - `dbc.Table`: For styling HTML tables.
- Interactive Components:
  - `dbc.Button` and dbc.ButtonGroup: For actions and grouping buttons.
  - `dbc.DropdownMen`u: For displaying a list of links or actions in a dropdown.
  - `dbc.Input`, dbc.Textarea, dbc.Checkbox, dbc.RadioItems, dbc.Select: A suite of form components.
  - `dbc.Modal`: For creating dialog prompts.
  - `dbc.Nav`, `dbc.NavbarSimple`, `dbc.NavbarBrand`, `dbc.NavItem`, `dbc.NavLink`: For creating navigation bars and menus.
  - `dbc.Pagination`: For navigating through paged content.
  - `dbc.Progress`: For displaying progress bars.
  - `dbc.Spinner`: To indicate a loading state.
  - `dbc.Tabs`: For organizing content into different sections.
  - `dbc.Toast:` For showing unobtrusive notifications.
- Utilities:
  - DBC also makes it easy to use Bootstrap's utility classes for things like spacing, alignment, colors, and visibility directly through component properties or by assigning them to className.
To use these, you typically import `dash_bootstrap_components as dbc` and then instantiate components like `dbc.Button("Click me!", color="primary")`.

---

### Official Website

- 👉 [https://bdc.dash-docs.io/](https://bdc.dash-docs.io/)  
(If official site changes, you can also check [https://github.com/BDC-Development/bdc-dash](https://github.com/BDC-Development/bdc-dash))
- icons [https://icons.getbootstrap.com/](https://icons.getbootstrap.com/)
- bootstrap 5 cheetsheet [https://bootstrap-cheatsheet.themeselection.com/](https://bootstrap-cheatsheet.themeselection.com/)
- offical cheatsheet [https://getbootstrap.com/docs/5.0/examples/cheatsheet/}](https://getbootstrap.com/docs/5.0/examples/cheatsheet/)
---

### Quick Installation

```bash
pip install bdc-dash
```

Example
```python
from dash import Dash, html
from bdc_dash.components import Sidebar, Topbar

app = Dash(__name__)
app.layout = html.Div([
    Topbar(title="My Dashboard"),
    Sidebar(items=["Home", "Analytics", "Settings"]),
    html.Div("Main Content Area")
])

if __name__ == "__main__":
    app.run_server(debug=True)
```