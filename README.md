# HTML Concepts

1. [Semantic HTML](#semantic-html)
2. [HTML Document Structure](#html-document-structure)
3. [Meta Tags](#meta-tags)
4. [Forms and Input Types](#forms-and-input-types)
5. [Accessibility (a11y)](#accessibility-a11y)
6. [Script and Style Loading](#script-and-style-loading)
7. [Images and Media](#images-and-media)
8. [Links and Navigation](#links-and-navigation)
9. [Tables](#tables)
10. [Data Attributes](#data-attributes)
11. [Content Embedding](#content-embedding)
12. [Interactive Attributes](#interactive-attributes)
13. [HTML APIs that Senior Devs Should Know](#html-apis-that-senior-devs-should-know)
14. [Performance Considerations](#performance-considerations)
15. [SEO Essentials](#seo-essentials)

# Semantic HTML

Semantic HTML means using elements that describe the *meaning* of the content, not just its appearance. A `<nav>` tells the browser, screen readers, and search engines "this is navigation." A `<div>` tells them nothing.

### Why it matters

- **Accessibility** — screen readers use semantic elements to help visually impaired users navigate. A `<nav>` is announced as navigation. A `<div>` is just "group."
- **SEO** — search engines give more weight to content inside `<article>`, `<main>`, and heading tags than content inside generic `<div>`s.
- **Readability** — `<header>`, `<aside>`, `<footer>` immediately tell other developers what a section does. `<div class="header">` requires reading the class name.

### Semantic vs Non-semantic elements

```html
<!-- Non-semantic — tells you nothing about the content -->
<div class="header">
  <div class="nav">
    <div class="nav-item">Home</div>
  </div>
</div>
<div class="main-content">
  <div class="article">
    <div class="article-header">My Blog Post</div>
    <div class="article-body">Content here...</div>
  </div>
  <div class="sidebar">Related links</div>
</div>
<div class="footer">© 2025</div>

<!-- Semantic — meaning is built into the tags -->
<header>
  <nav>
    <a href="/">Home</a>
  </nav>
</header>
<main>
  <article>
    <h1>My Blog Post</h1>
    <p>Content here...</p>
  </article>
  <aside>Related links</aside>
</main>
<footer>© 2025</footer>
```

### Structural elements

**`<header>`** — introductory content or navigation links. Can be used multiple times (page header, article header, section header).

**`<nav>`** — major navigation blocks. Don't use for every group of links — only primary navigation, table of contents, or breadcrumbs.

**`<main>`** — the dominant content of the page. Only ONE `<main>` per page. Excludes headers, footers, sidebars, and navigation.

**`<footer>`** — closing content. Like `<header>`, can be used at page level or inside `<article>` and `<section>`.

**`<aside>`** — content tangentially related to the surrounding content. Sidebars, pull quotes, related links, advertisements.

### Content elements

**`<article>`** — self-contained content that could stand on its own. Blog posts, news articles, forum posts, comments, product cards. Ask yourself: "Would this make sense if I syndicated it to another site?" If yes, use `<article>`.

**`<section>`** — a thematic grouping of content, typically with a heading. Chapters, tabbed panels, different sections of a homepage. If you just need a wrapper for styling, use `<div>` instead.

**`<article>` vs `<section>` vs `<div>`:**

```html
<!-- article — self-contained, could be reused elsewhere -->
<article>
  <h2>How Closures Work in JavaScript</h2>
  <p>A closure is created when...</p>
</article>

<!-- section — thematic grouping within a page -->
<section>
  <h2>Our Services</h2>
  <p>We offer web development, design, and consulting.</p>
</section>

<!-- div — no semantic meaning, just a container for styling -->
<div class="card-grid">
  <article class="card">...</article>
  <article class="card">...</article>
</div>
```

### Other useful semantic elements

```html
<!-- figure + figcaption — self-contained content with a caption -->
<figure>
  <img src="chart.png" alt="Revenue growth chart for Q3 2025" />
  <figcaption>Revenue grew 23% in Q3 2025 compared to Q2.</figcaption>
</figure>

<!-- time — machine-readable date/time -->
<p>Published on <time datetime="2025-03-15">March 15, 2025</time></p>

<!-- mark — highlighted/relevant text -->
<p>Search results for "closure": A <mark>closure</mark> is created when...</p>

<!-- abbr — abbreviation with full form -->
<p>Use <abbr title="Hyper Text Markup Language">HTML</abbr> for structure.</p>

<!-- details + summary — native accordion, no JS needed -->
<details>
  <summary>What is a closure?</summary>
  <p>A closure is a function that retains access to its lexical scope...</p>
</details>

<!-- address — contact information -->
<address>
  Contact us at <a href="mailto:info@example.com">info@example.com</a>
</address>

<!-- blockquote + cite -->
<blockquote cite="https://example.com/article">
  <p>The best way to predict the future is to create it.</p>
</blockquote>
```

# HTML Document Structure

### The minimal valid HTML document

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Page Title</title>
</head>
<body>
  <!-- Content goes here -->
</body>
</html>
```

Every line here has a purpose:

### DOCTYPE

```html
<!DOCTYPE html>
```

Tells the browser to render the page in **standards mode** instead of quirks mode. Without it, browsers fall back to legacy rendering behavior for backward compatibility, which can cause inconsistent styling and layout across browsers.

This is not an HTML tag — it's an instruction to the browser. In HTML5, this is the only DOCTYPE you need. Older versions of HTML had long, complex DOCTYPE declarations.

### html element with lang

```html
<html lang="en">
```

The `lang` attribute tells browsers and screen readers what language the content is in. Screen readers use this to switch pronunciation rules. Search engines use it for language-specific results. Browser translation features use it to detect the source language.

```html
<!-- For specific regions -->
<html lang="en-US">
<html lang="en-GB">
<html lang="ta">  <!-- Tamil -->

<!-- For multilingual content, override at element level -->
<html lang="en">
  <body>
    <p>This is English content.</p>
    <p lang="ta">இது தமிழ் உள்ளடக்கம்.</p>
  </body>
</html>
```

### head element

The `<head>` contains metadata about the document — information *about* the page, not content *on* the page. Nothing inside `<head>` is visible to the user (except `<title>` which shows in the browser tab).

**Essential head elements:**

```html
<head>
  <!-- Character encoding — must be within first 1024 bytes -->
  <meta charset="UTF-8" />

  <!-- Viewport — essential for responsive design -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- Page title — shows in browser tab, search results, bookmarks -->
  <title>My Website — Home</title>

  <!-- CSS -->
  <link rel="stylesheet" href="styles.css" />

  <!-- Favicon -->
  <link rel="icon" href="/favicon.ico" />
</head>
```

**`<meta charset="UTF-8">`** — defines character encoding. UTF-8 supports virtually all characters and symbols worldwide. Without it, special characters might display as garbled text.

**`<meta name="viewport">`** — controls how the page scales on mobile devices. Without it, mobile browsers render the page at desktop width and zoom out, making text tiny. `width=device-width` sets the viewport to the device's width. `initial-scale=1.0` sets the initial zoom level.

### How the browser parses HTML

The browser reads HTML top to bottom and builds the DOM tree incrementally:

```
1. Receives HTML bytes from server
2. Converts bytes to characters (using charset)
3. Tokenizes characters into HTML tags
4. Builds DOM tree node by node
5. When it encounters CSS → builds CSSOM
6. When it encounters JS → (may) pause DOM building to execute
7. Combines DOM + CSSOM → Render Tree
8. Layout → Paint → Composite → Pixels on screen
```

This is why the order of elements in `<head>` matters — CSS and JS loading can block rendering (covered in Script and Style Loading section).

# Meta Tags

Meta tags provide metadata about the HTML document. They live in `<head>` and are not visible on the page, but browsers, search engines, and social media platforms use them.

### Essential meta tags

```html
<!-- Character encoding -->
<meta charset="UTF-8" />

<!-- Responsive design -->
<meta name="viewport" content="width=device-width, initial-scale=1.0" />

<!-- Page description — shows in search results under the title -->
<meta name="description" content="Learn JavaScript concepts with clear 
  explanations and code examples. A senior frontend engineer's reference." />

<!-- Author -->
<meta name="author" content="Akshai" />
```

### SEO meta tags

```html
<!-- Control search engine indexing -->
<meta name="robots" content="index, follow" />      <!-- default: index and follow links -->
<meta name="robots" content="noindex, nofollow" />   <!-- hide from search + don't follow links -->
<meta name="robots" content="noindex, follow" />     <!-- hide from search but follow links -->

<!-- Canonical URL — tells search engines which URL is the "official" version -->
<!-- Prevents duplicate content issues -->
<link rel="canonical" href="https://example.com/blog/closures" />
```

### Open Graph tags — social media sharing

When you share a link on LinkedIn, Facebook, Slack, or WhatsApp, these tags control what shows up in the preview card:

```html
<meta property="og:title" content="Understanding Closures in JavaScript" />
<meta property="og:description" content="A deep dive into how closures work..." />
<meta property="og:image" content="https://example.com/images/closures-og.png" />
<meta property="og:url" content="https://example.com/blog/closures" />
<meta property="og:type" content="article" />
<meta property="og:site_name" content="JS Concepts" />
```

📢 NOTES:

> `og:image` should be at least 1200×630 pixels for best display across platforms. Without Open Graph tags, platforms will try to auto-generate a preview — usually poorly.

### Twitter Card tags

```html
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="Understanding Closures in JavaScript" />
<meta name="twitter:description" content="A deep dive into how closures work..." />
<meta name="twitter:image" content="https://example.com/images/closures-twitter.png" />
```

### Other useful meta tags

```html
<!-- Theme color — colors the browser toolbar on mobile -->
<meta name="theme-color" content="#1a1a2e" />

<!-- Prevent automatic phone number detection on iOS -->
<meta name="format-detection" content="telephone=no" />

<!-- HTTP equiv — rarely needed but good to know -->
<!-- Auto-refresh page every 30 seconds -->
<meta http-equiv="refresh" content="30" />

<!-- Redirect after 3 seconds -->
<meta http-equiv="refresh" content="3;url=https://example.com/new-page" />

<!-- Content Security Policy (basic) -->
<meta http-equiv="Content-Security-Policy" content="default-src 'self'" />
```

# Forms and Input Types

Forms are how users send data to servers. As a frontend developer, you interact with forms constantly — login pages, search bars, checkout flows, settings panels.

### Basic form structure

```html
<form action="/api/submit" method="POST">
  <label for="username">Username</label>
  <input type="text" id="username" name="username" required />

  <label for="email">Email</label>
  <input type="email" id="email" name="email" required />

  <button type="submit">Submit</button>
</form>
```

**`action`** — URL where form data is sent. In React/SPA apps, you usually prevent default and handle submission in JS.

**`method`** — GET (data in URL query string, for searches/filters) or POST (data in request body, for creating/updating).

**`name`** — the key used when form data is submitted. Without `name`, the input's value won't be included in the form data.

### The label-input connection

```html
<!-- Explicit association using for/id — recommended -->
<label for="email">Email</label>
<input type="email" id="email" name="email" />

<!-- Implicit association by nesting — also works -->
<label>
  Email
  <input type="email" name="email" />
</label>
```

Why this matters: clicking the label focuses/activates the input. Screen readers announce the label when the input is focused. Without this association, screen reader users don't know what an input is for. This is one of the most common accessibility failures on the web.

### Input types

```html
<!-- Text inputs -->
<input type="text" />          <!-- generic text -->
<input type="email" />         <!-- email validation + mobile keyboard -->
<input type="password" />      <!-- masked characters -->
<input type="number" />        <!-- numeric keyboard + spin buttons -->
<input type="tel" />           <!-- phone keyboard on mobile — no validation -->
<input type="url" />           <!-- URL validation -->
<input type="search" />        <!-- search field with clear button in some browsers -->

<!-- Date and time -->
<input type="date" />          <!-- date picker -->
<input type="time" />          <!-- time picker -->
<input type="datetime-local" /><!-- date + time picker -->
<input type="month" />         <!-- month/year picker -->
<input type="week" />          <!-- week picker -->

<!-- Selection -->
<input type="checkbox" />      <!-- multiple selection -->
<input type="radio" />         <!-- single selection within a group -->
<input type="range" />         <!-- slider -->
<input type="color" />         <!-- color picker -->

<!-- File -->
<input type="file" />                          <!-- single file -->
<input type="file" multiple />                 <!-- multiple files -->
<input type="file" accept=".pdf,.doc" />       <!-- restrict file types -->
<input type="file" accept="image/*" />         <!-- any image -->

<!-- Hidden -->
<input type="hidden" name="csrf" value="token123" />  <!-- not visible, sent with form -->
```

📢 NOTES:

> Using the correct `type` is not just about validation — it changes the keyboard on mobile devices. `type="email"` shows `@` and `.com` keys. `type="tel"` shows the phone dialpad. `type="number"` shows a numeric keypad. This significantly improves mobile UX.

### Validation attributes

```html
<!-- Required field -->
<input type="text" required />

<!-- Min/max for numbers and dates -->
<input type="number" min="0" max="100" step="5" />
<input type="date" min="2025-01-01" max="2025-12-31" />

<!-- Length constraints -->
<input type="text" minlength="3" maxlength="50" />

<!-- Pattern — regex validation -->
<input type="text" pattern="[A-Za-z]{3,}" title="At least 3 letters" />

<!-- Custom validation message -->
<input type="email" required 
  oninvalid="this.setCustomValidity('Please enter a valid email')"
  oninput="this.setCustomValidity('')" />
```

### select, textarea, fieldset

```html
<!-- Dropdown -->
<label for="country">Country</label>
<select id="country" name="country">
  <option value="">Select a country</option>
  <option value="IN">India</option>
  <option value="US">United States</option>
  <optgroup label="Europe">
    <option value="UK">United Kingdom</option>
    <option value="DE">Germany</option>
  </optgroup>
</select>

<!-- Multi-line text -->
<label for="bio">Bio</label>
<textarea id="bio" name="bio" rows="4" cols="50" 
  placeholder="Tell us about yourself..."></textarea>

<!-- Grouping related inputs -->
<fieldset>
  <legend>Shipping Address</legend>
  <label for="street">Street</label>
  <input type="text" id="street" name="street" />
  <label for="city">City</label>
  <input type="text" id="city" name="city" />
</fieldset>
```

`<fieldset>` groups related inputs visually and semantically. `<legend>` provides the group's label. Screen readers announce the legend when entering the group, giving users context.

### datalist — autocomplete suggestions

```html
<label for="framework">Favorite Framework</label>
<input list="frameworks" id="framework" name="framework" />

<datalist id="frameworks">
  <option value="React" />
  <option value="Vue" />
  <option value="Angular" />
  <option value="Svelte" />
</datalist>
```

Unlike `<select>`, the user can still type a custom value. The `<datalist>` provides suggestions, not restrictions.

### output element

```html
<form oninput="result.value = parseInt(a.value) + parseInt(b.value)">
  <input type="range" id="a" value="50" /> +
  <input type="number" id="b" value="25" /> =
  <output name="result" for="a b">75</output>
</form>
```

### Form submission and enctype

```html
<!-- Default: URL-encoded (key=value&key=value) -->
<form method="POST" enctype="application/x-www-form-urlencoded">

<!-- For file uploads — MUST use this enctype -->
<form method="POST" enctype="multipart/form-data">
  <input type="file" name="avatar" />
</form>

<!-- Plain text — rarely used -->
<form method="POST" enctype="text/plain">
```

### FormData API

```javascript
const form = document.querySelector("form");

form.addEventListener("submit", (e) => {
  e.preventDefault();

  const formData = new FormData(form);

  // Access values
  formData.get("username");        // value of input[name="username"]
  formData.getAll("hobbies");      // all values for multi-select/checkboxes

  // Iterate
  for (const [key, value] of formData) {
    console.log(`${key}: ${value}`);
  }

  // Send with fetch
  fetch("/api/submit", {
    method: "POST",
    body: formData,  // Content-Type is set automatically
  });

  // Convert to plain object
  const data = Object.fromEntries(formData);
});
```

# Accessibility (a11y)

Accessibility means making your website usable by everyone, including people who use screen readers, keyboard-only navigation, or have visual, motor, or cognitive disabilities. It's not optional — it's a legal requirement in many countries and a professional responsibility.

### The first rule of ARIA

> If you can use a native HTML element that already has the semantics and behavior you need, do that instead of adding ARIA. Don't do this:

```html
<!-- BAD — reinventing a button -->
<div role="button" tabindex="0" onclick="submit()" 
  onkeydown="if(event.key==='Enter') submit()">
  Submit
</div>

<!-- GOOD — just use a button -->
<button onclick="submit()">Submit</button>
```

A `<button>` already has the correct role, keyboard handling (Enter and Space), focus behavior, and screen reader announcement. Using a `<div>` with ARIA means you have to manually recreate all of that.

### ARIA roles

Roles tell assistive technology what an element *is*:

```html
<!-- Landmark roles — usually better to use semantic HTML instead -->
<div role="navigation">   <!-- use <nav> instead -->
<div role="main">          <!-- use <main> instead -->
<div role="banner">        <!-- use <header> instead -->
<div role="contentinfo">   <!-- use <footer> instead -->

<!-- Widget roles — for custom interactive components -->
<div role="tablist">
  <button role="tab" aria-selected="true">Tab 1</button>
  <button role="tab" aria-selected="false">Tab 2</button>
</div>
<div role="tabpanel">Tab 1 content</div>

<!-- Other useful roles -->
<div role="alert">Form submitted successfully!</div>  <!-- announced immediately -->
<div role="status">3 items in cart</div>               <!-- announced politely -->
<div role="dialog" aria-labelledby="title">...</div>   <!-- modal dialog -->
<ul role="list">  <!-- restores list semantics in Safari when list-style: none -->
```

### ARIA attributes

```html
<!-- aria-label — provides a label when visible text isn't available -->
<button aria-label="Close dialog">✕</button>
<nav aria-label="Main navigation">...</nav>

<!-- aria-labelledby — references another element as the label -->
<h2 id="section-title">User Settings</h2>
<form aria-labelledby="section-title">...</form>

<!-- aria-describedby — additional description -->
<input type="password" id="pw" aria-describedby="pw-hint" />
<p id="pw-hint">Must be at least 8 characters with one number.</p>

<!-- aria-hidden — hides from screen readers but still visible -->
<span aria-hidden="true">★</span>  <!-- decorative star icon -->
<span class="sr-only">Favorited</span>  <!-- text only screen readers see -->

<!-- aria-live — announces dynamic content changes -->
<div aria-live="polite">3 results found</div>  <!-- waits for pause in speech -->
<div aria-live="assertive">Error: connection lost</div>  <!-- interrupts immediately -->

<!-- aria-expanded — toggle state -->
<button aria-expanded="false" aria-controls="menu">Menu</button>
<ul id="menu" hidden>...</ul>

<!-- aria-required vs required -->
<input required />                  <!-- native: prevents form submission -->
<input aria-required="true" />      <!-- ARIA: only announces to screen readers -->
<!-- Use native required when possible — it does both -->

<!-- aria-disabled vs disabled -->
<button disabled>Submit</button>              <!-- native: not clickable, not focusable -->
<button aria-disabled="true">Submit</button>  <!-- ARIA: still focusable, announced as disabled -->
<!-- Use aria-disabled when you want disabled users to still find the element -->
```

### Alt text for images

```html
<!-- Informative image — describe what it shows -->
<img src="chart.png" alt="Bar chart showing 23% revenue growth in Q3 2025" />

<!-- Decorative image — empty alt to hide from screen readers -->
<img src="divider.png" alt="" />

<!-- Image as a link — describe the destination, not the image -->
<a href="/home">
  <img src="logo.png" alt="Company homepage" />
</a>

<!-- Complex image — use figure + figcaption or aria-describedby -->
<figure>
  <img src="architecture.png" alt="System architecture overview" 
    aria-describedby="arch-desc" />
  <figcaption id="arch-desc">
    The system consists of a React frontend, Node.js API layer, 
    and PostgreSQL database with Redis caching.
  </figcaption>
</figure>
```

### Keyboard navigation

```html
<!-- tabindex controls focus order -->
<button>First</button>              <!-- tabindex=0 by default -->
<div tabindex="0">Focusable div</div>  <!-- added to tab order -->
<div tabindex="-1">Programmatic only</div>  <!-- focusable via JS, not Tab -->
<!-- AVOID positive tabindex (1, 2, 3...) — it overrides natural order -->

<!-- Skip link — lets keyboard users skip past navigation -->
<body>
  <a href="#main-content" class="skip-link">Skip to main content</a>
  <nav><!-- long navigation --></nav>
  <main id="main-content"><!-- content --></main>
</body>

<style>
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  z-index: 100;
}
.skip-link:focus {
  top: 0;  /* visible only when focused via Tab */
}
</style>
```

### Focus trapping in modals

When a modal is open, Tab should cycle within the modal only — not escape to the content behind it:

```javascript
function trapFocus(modal) {
  const focusable = modal.querySelectorAll(
    'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
  );
  const first = focusable[0];
  const last = focusable[focusable.length - 1];

  modal.addEventListener("keydown", (e) => {
    if (e.key !== "Tab") return;

    if (e.shiftKey) {
      // Shift+Tab — if on first element, wrap to last
      if (document.activeElement === first) {
        e.preventDefault();
        last.focus();
      }
    } else {
      // Tab — if on last element, wrap to first
      if (document.activeElement === last) {
        e.preventDefault();
        first.focus();
      }
    }
  });

  first.focus(); // focus first element when modal opens
}
```

📢 NOTES:

> The native `<dialog>` element with `showModal()` handles focus trapping automatically. Use it instead of building your own modal when possible.

### Screen reader only text

```css
/* Content visible only to screen readers */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border-width: 0;
}
```

```html
<button>
  <svg><!-- icon --></svg>
  <span class="sr-only">Delete item</span>
</button>
```

### Color contrast

WCAG (Web Content Accessibility Guidelines) defines contrast ratios:

- **AA (minimum):** 4.5:1 for normal text, 3:1 for large text (18px+ bold or 24px+)
- **AAA (enhanced):** 7:1 for normal text, 4.5:1 for large text

```html
<!-- Check contrast: https://webaim.org/resources/contrastchecker/ -->

<!-- BAD contrast -->
<p style="color: #999; background: #fff;">Hard to read</p>  <!-- ratio ~2.8:1 -->

<!-- GOOD contrast -->
<p style="color: #595959; background: #fff;">Easy to read</p>  <!-- ratio ~7:1 -->
```

📢 NOTES:

> Never rely on color alone to convey information. Always pair it with text, icons, or patterns:

```html
<!-- BAD — color is the only indicator -->
<span style="color: red;">Error</span>
<span style="color: green;">Success</span>

<!-- GOOD — icon + text + color -->
<span style="color: red;">❌ Error: Email is required</span>
<span style="color: green;">✅ Success: Form submitted</span>
```

### The accessibility tree

The browser builds an accessibility tree from the DOM — a simplified version that screen readers use. It only contains semantically relevant information:

```html
<nav aria-label="Main">
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>
```

```
Accessibility tree:
navigation "Main"
  list
    listitem
      link "Home"
    listitem
      link "About"
```

You can inspect the accessibility tree in Chrome DevTools → Elements → Accessibility pane.

# Script and Style Loading

How and where you load CSS and JavaScript directly impacts page rendering speed.

### CSS loading — render blocking

```html
<!-- CSS blocks rendering — browser won't paint until CSS is downloaded and parsed -->
<head>
  <link rel="stylesheet" href="styles.css" />
  <!-- Browser: "I need to know how everything looks before I show anything" -->
</head>
```

This is why you should put CSS in the `<head>` — the browser needs it before it can render. But it also means large CSS files delay first paint.

**Strategies to reduce CSS blocking:**

```html
<!-- Critical CSS inlined — instant first paint for above-the-fold content -->
<head>
  <style>
    /* Only the CSS needed for initial viewport */
    body { font-family: sans-serif; margin: 0; }
    .hero { height: 100vh; display: flex; }
  </style>
  
  <!-- Non-critical CSS loaded asynchronously -->
  <link rel="preload" href="full-styles.css" as="style" 
    onload="this.onload=null;this.rel='stylesheet'" />
</head>

<!-- Media-specific CSS — only blocks rendering for matching media -->
<link rel="stylesheet" href="print.css" media="print" />        <!-- doesn't block screen render -->
<link rel="stylesheet" href="mobile.css" media="(max-width: 768px)" /> <!-- blocks only on mobile -->
```

### JavaScript loading — three modes

**Default `<script>` — blocks everything:**

```html
<head>
  <script src="app.js"></script>
  <!-- Browser stops parsing HTML, downloads JS, executes JS, then resumes HTML -->
</head>
```

```
HTML parsing:  ████████░░░░░░░░░░░░████████████
JS download:          ████████
JS execute:                   ████
                     ↑ HTML blocked here
```

**`<script defer>` — download in parallel, execute after HTML is parsed:**

```html
<head>
  <script defer src="app.js"></script>
  <script defer src="analytics.js"></script>
</head>
```

```
HTML parsing:  ██████████████████████████████████
JS download:      ████████
JS execute:                                      ████
                                                ↑ after DOMContentLoaded
```

- Downloads in parallel with HTML parsing — no blocking
- Executes after HTML is fully parsed, before `DOMContentLoaded`
- **Maintains order** — `app.js` always runs before `analytics.js`
- Only works with external scripts (not inline)

**`<script async>` — download in parallel, execute immediately when ready:**

```html
<head>
  <script async src="analytics.js"></script>
  <script async src="chat-widget.js"></script>
</head>
```

```
HTML parsing:  ████████████░░░░██████████████████
JS download:      ████████
JS execute:               ████
                         ↑ executes as soon as downloaded, pausing HTML
```

- Downloads in parallel with HTML parsing
- Executes immediately when download finishes — pauses HTML parsing briefly
- **No guaranteed order** — whichever downloads first runs first
- Only works with external scripts (not inline)

**`<script type="module">` — deferred by default:**

```html
<script type="module" src="app.js"></script>
```

- Behaves like `defer` by default (downloads in parallel, executes after parsing)
- Can also use `async` to execute immediately: `<script type="module" async>`
- Enables `import`/`export` syntax
- Always in strict mode
- Executed only once even if imported multiple times

### When to use which

```
Scenario                              | Use
--------------------------------------|------------------
Your main app bundle                  | defer
Independent third-party (analytics)   | async
Module-based application              | type="module"
Inline script that needs DOM          | defer or end of body
Critical above-the-fold JS            | inline <script> in head
```

### Where to place scripts

```html
<!-- Option 1: In head with defer (modern, recommended) -->
<head>
  <script defer src="app.js"></script>
</head>
<body>
  <!-- HTML content -->
</body>

<!-- Option 2: End of body (traditional, still works) -->
<body>
  <!-- HTML content -->
  <script src="app.js"></script>
</body>
```

Both achieve the same result — JS runs after HTML is parsed. `defer` in the `<head>` is preferred because the browser starts downloading earlier.

### Resource hints

```html
<!-- preload — download this NOW, I need it soon -->
<link rel="preload" href="critical-font.woff2" as="font" type="font/woff2" crossorigin />
<link rel="preload" href="hero-image.webp" as="image" />

<!-- prefetch — download this in idle time, I'll need it on the NEXT page -->
<link rel="prefetch" href="/about-page-bundle.js" />

<!-- preconnect — establish connection early (DNS + TCP + TLS) -->
<link rel="preconnect" href="https://api.example.com" />
<link rel="preconnect" href="https://fonts.googleapis.com" />

<!-- dns-prefetch — resolve DNS only (lighter than preconnect) -->
<link rel="dns-prefetch" href="https://analytics.example.com" />

<!-- modulepreload — preload ES modules -->
<link rel="modulepreload" href="./utils.js" />
```

**preload vs prefetch:**
- `preload` = "I need this on THIS page, download it NOW with high priority"
- `prefetch` = "I might need this on the NEXT page, download it when you're idle"

# Images and Media

### img element — the essentials

```html
<img 
  src="photo.jpg" 
  alt="Sunset over Marina Beach in Chennai"
  width="800" 
  height="600"
  loading="lazy"
  decoding="async"
/>
```

**`alt`** — already covered in accessibility section. Required for every image.

**`width` and `height`** — set these in HTML even if you resize with CSS. The browser uses the aspect ratio to reserve space before the image loads, preventing layout shift (CLS — Cumulative Layout Shift, a Core Web Vital).

**`loading="lazy"`** — defers loading until the image is near the viewport. Don't use on above-the-fold images — those should load immediately.

**`decoding="async"`** — tells the browser it can decode the image off the main thread, preventing jank.

### Responsive images with srcset and sizes

```html
<!-- Resolution switching — same image, different sizes -->
<img 
  src="photo-800.jpg"
  srcset="
    photo-400.jpg 400w,
    photo-800.jpg 800w,
    photo-1200.jpg 1200w
  "
  sizes="
    (max-width: 600px) 400px,
    (max-width: 1000px) 800px,
    1200px
  "
  alt="Landscape photo"
/>
```

`srcset` tells the browser what images are available and their widths. `sizes` tells the browser how wide the image will be displayed at different viewport widths. The browser then picks the best image — you don't choose, the browser does.

### picture element — art direction and format switching

```html
<!-- Serve different images at different breakpoints -->
<picture>
  <source media="(max-width: 600px)" srcset="photo-mobile.jpg" />
  <source media="(max-width: 1000px)" srcset="photo-tablet.jpg" />
  <img src="photo-desktop.jpg" alt="Landscape photo" />
</picture>

<!-- Serve modern formats with fallback -->
<picture>
  <source srcset="photo.avif" type="image/avif" />
  <source srcset="photo.webp" type="image/webp" />
  <img src="photo.jpg" alt="Landscape photo" />  <!-- fallback for old browsers -->
</picture>
```

The browser uses the first `<source>` it supports. The `<img>` is always required as the fallback.

### Image formats — when to use which

```
Format | Best for                        | Transparency | Animation | Size
-------|----------------------------------|-------------|-----------|--------
JPEG   | Photos, complex images          | ❌          | ❌        | Medium
PNG    | Icons, screenshots, transparency | ✅          | ❌        | Large
WebP   | Everything (modern replacement) | ✅          | ✅        | Small
AVIF   | Everything (newest, smallest)   | ✅          | ✅        | Smallest
SVG    | Icons, logos, simple graphics    | ✅          | ✅(CSS/JS)| Tiny
GIF    | Simple animations (legacy)      | ✅(1-bit)   | ✅        | Large
```

In practice: use SVG for icons and logos, WebP or AVIF for photos with a JPEG fallback, and avoid PNG for photos.

### Video and audio

```html
<!-- Video with multiple sources and subtitles -->
<video 
  controls 
  width="720"
  poster="thumbnail.jpg"
  preload="metadata"
>
  <source src="video.webm" type="video/webm" />
  <source src="video.mp4" type="video/mp4" />
  <track 
    kind="subtitles" 
    src="captions-en.vtt" 
    srclang="en" 
    label="English" 
    default 
  />
  Your browser doesn't support video.
</video>

<!-- Audio -->
<audio controls preload="none">
  <source src="podcast.ogg" type="audio/ogg" />
  <source src="podcast.mp3" type="audio/mpeg" />
  Your browser doesn't support audio.
</audio>
```

**`preload` values:**
- `none` — don't preload anything (saves bandwidth)
- `metadata` — only load duration, dimensions (recommended default)
- `auto` — browser decides (may download entire file)

### Canvas vs SVG

```
Feature    | Canvas                    | SVG
-----------|---------------------------|---------------------------
Type       | Bitmap (pixels)           | Vector (math)
Rendering  | JavaScript API            | DOM elements
Scaling    | Blurry when scaled up     | Sharp at any size
Events     | One event on whole canvas | Events per element
Performance| Better for many objects   | Better for few complex shapes
Use case   | Games, data viz, photos   | Icons, logos, charts, maps
Access     | getContext("2d")          | CSS and JS on each element
```

# Links and Navigation

### The anchor element

```html
<!-- Basic link -->
<a href="https://example.com">Visit Example</a>

<!-- Open in new tab -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
  Visit Example
</a>

<!-- Anchor link — scroll to element with matching id -->
<a href="#section-2">Jump to Section 2</a>
<section id="section-2">...</section>

<!-- Download link -->
<a href="/files/report.pdf" download>Download Report</a>
<a href="/files/report.pdf" download="Q3-Report-2025.pdf">Download Report</a>

<!-- Email and phone -->
<a href="mailto:akshai@example.com">Email us</a>
<a href="tel:+911234567890">Call us</a>
```

### rel="noopener noreferrer" — why it matters

```html
<a href="https://external-site.com" target="_blank" rel="noopener noreferrer">
  External Link
</a>
```

Without `rel="noopener"`, the opened page has access to your page via `window.opener`. A malicious site could redirect your page: `window.opener.location = "https://phishing-site.com"`.

`noopener` — prevents the new page from accessing `window.opener`.
`noreferrer` — also prevents sending the Referer header (the external site won't know where the traffic came from).

📢 NOTES:

> Modern browsers (2021+) automatically apply `noopener` behavior for `target="_blank"` links. But explicitly adding it ensures compatibility with older browsers and makes your intent clear.

### Link vs Button — when to use which

```html
<!-- Link — navigates to another page or resource -->
<a href="/about">About Us</a>

<!-- Button — performs an action (submit, toggle, delete, open modal) -->
<button onclick="deleteItem()">Delete</button>
```

The rule: if clicking it takes you somewhere, use `<a>`. If clicking it does something, use `<button>`.

```html
<!-- BAD — these are actions, not navigation -->
<a href="#" onclick="submitForm()">Submit</a>
<a href="javascript:void(0)" onclick="openModal()">Open</a>

<!-- GOOD -->
<button onclick="submitForm()">Submit</button>
<button onclick="openModal()">Open</button>
```

Why it matters: `<a>` and `<button>` have different keyboard behavior (Enter vs Enter+Space), different ARIA roles (link vs button), and different screen reader announcements. Using the wrong one confuses assistive technology users.

### rel attribute values

```html
<a rel="nofollow" href="...">         <!-- tells search engines not to follow this link -->
<a rel="sponsored" href="...">        <!-- paid/sponsored link -->
<a rel="ugc" href="...">              <!-- user-generated content (comments, forums) -->
<a rel="noopener" href="..." target="_blank">  <!-- security for external links -->
<a rel="noreferrer" href="...">       <!-- don't send Referer header -->
<a rel="external" href="...">         <!-- indicates external link -->
```

# Tables

Tables are for tabular data — data that has a relationship between rows and columns. Do NOT use tables for page layout.

### Proper table structure

```html
<table>
  <caption>Quarterly Revenue (in thousands)</caption>
  
  <thead>
    <tr>
      <th scope="col">Quarter</th>
      <th scope="col">Revenue</th>
      <th scope="col">Growth</th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <th scope="row">Q1 2025</th>
      <td>$450</td>
      <td>+12%</td>
    </tr>
    <tr>
      <th scope="row">Q2 2025</th>
      <td>$520</td>
      <td>+15%</td>
    </tr>
  </tbody>
  
  <tfoot>
    <tr>
      <th scope="row">Total</th>
      <td>$970</td>
      <td>+13.5%</td>
    </tr>
  </tfoot>
</table>
```

**`<caption>`** — describes the table. Screen readers announce it before reading the table. Like `alt` for images but for tables.

**`<thead>`, `<tbody>`, `<tfoot>`** — semantic grouping. Helps screen readers, allows independent scrolling of body, and `<tfoot>` can render at the bottom even if placed before `<tbody>` in markup.

**`scope`** — tells screen readers whether a header applies to its column (`col`) or row (`row`). Without it, screen readers may not correctly associate data cells with their headers.

### Spanning rows and columns

```html
<table>
  <tr>
    <th colspan="2">Full Name</th>  <!-- spans 2 columns -->
    <th>Age</th>
  </tr>
  <tr>
    <td>First</td>
    <td>Last</td>
    <td rowspan="2">28</td>  <!-- spans 2 rows -->
  </tr>
  <tr>
    <td>Akshai</td>
    <td>TR</td>
  </tr>
</table>
```

# Data Attributes

Data attributes let you store custom data on HTML elements without using non-standard attributes or extra JavaScript variables.

### Syntax and access

```html
<article 
  data-id="42"
  data-category="javascript"
  data-author-name="Akshai"
  data-is-featured="true"
>
  <h2>Understanding Closures</h2>
</article>
```

```javascript
const article = document.querySelector("article");

// Access via dataset — camelCase conversion
article.dataset.id;          // "42" (always a string)
article.dataset.category;    // "javascript"
article.dataset.authorName;  // "Akshai" (data-author-name → authorName)
article.dataset.isFeatured;  // "true" (string, not boolean)

// Set data attributes
article.dataset.views = "1500";
// Result: <article data-views="1500" ...>

// Remove
delete article.dataset.views;

// Check existence
"category" in article.dataset; // true
```

📢 NOTES:

> Data attributes are always strings. If you store numbers or booleans, you'll need to convert them:

```javascript
const id = Number(article.dataset.id);            // 42
const featured = article.dataset.isFeatured === "true"; // true
```

### CSS access

```css
/* Select by data attribute */
[data-category="javascript"] {
  border-left: 3px solid yellow;
}

[data-is-featured="true"] {
  background: #f0f0f0;
}

/* Display data attribute content */
[data-tooltip]:hover::after {
  content: attr(data-tooltip);
  position: absolute;
  background: #333;
  color: white;
  padding: 4px 8px;
}
```

```html
<button data-tooltip="Click to save your changes">Save</button>
```

### When to use data attributes vs alternatives

```
Need                          | Use
------------------------------|----------------------------
Store data for JS             | data-* attributes
Style variations              | CSS classes
Unique identifier             | id
Accessibility info            | ARIA attributes
Form data to submit           | name attribute + hidden inputs
Application state             | JavaScript variables / state management
```

# Content Embedding

### iframe

```html
<!-- Basic iframe -->
<iframe 
  src="https://example.com" 
  width="600" 
  height="400"
  title="Example website"
></iframe>

<!-- YouTube embed -->
<iframe 
  src="https://www.youtube.com/embed/VIDEO_ID"
  width="560" 
  height="315"
  title="Video title"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope"
  allowfullscreen
></iframe>

<!-- Google Maps embed -->
<iframe 
  src="https://www.google.com/maps/embed?pb=..."
  width="600"
  height="450"
  style="border:0;"
  allowfullscreen
  loading="lazy"
  referrerpolicy="no-referrer-when-downgrade"
  title="Office location map"
></iframe>
```

### iframe security — sandbox

```html
<!-- Full sandbox — disables everything -->
<iframe src="untrusted.html" sandbox></iframe>

<!-- Selective permissions -->
<iframe src="widget.html" sandbox="
  allow-scripts
  allow-same-origin
  allow-forms
  allow-popups
"></iframe>
```

**Sandbox permissions:**
- `allow-scripts` — lets the iframe run JavaScript
- `allow-same-origin` — lets the iframe access its own origin's cookies/storage
- `allow-forms` — lets forms submit inside the iframe
- `allow-popups` — lets the iframe open new windows
- `allow-modals` — lets the iframe use `alert()`, `confirm()`, `prompt()`
- `allow-top-navigation` — lets the iframe navigate the parent page (dangerous)

📢 NOTES:

> Never use `allow-scripts` and `allow-same-origin` together on untrusted content — the script could remove the sandbox attribute entirely.

### Clickjacking protection

Clickjacking is when a malicious site embeds your site in an invisible iframe and tricks users into clicking on it. Prevent this with:

```html
<!-- HTTP Header (preferred) -->
<!-- X-Frame-Options: DENY -->
<!-- X-Frame-Options: SAMEORIGIN -->

<!-- CSP alternative -->
<!-- Content-Security-Policy: frame-ancestors 'none' -->
<!-- Content-Security-Policy: frame-ancestors 'self' -->
```

### srcdoc — inline HTML content

```html
<iframe srcdoc="
  <h1>Hello from inline HTML</h1>
  <p>This content is embedded directly, no external URL needed.</p>
" title="Inline content"></iframe>
```

Useful for sandboxed previews — like showing rendered HTML in a code playground.

# Interactive Attributes

### contenteditable

```html
<!-- Makes any element editable -->
<div contenteditable="true">
  Click here and start typing...
</div>

<!-- Useful for rich text editors -->
<article contenteditable="true" id="editor">
  <h2>Edit this heading</h2>
  <p>And this paragraph too.</p>
</article>
```

```javascript
const editor = document.getElementById("editor");
editor.addEventListener("input", () => {
  console.log(editor.innerHTML); // get the edited HTML
});
```

### draggable

```html
<!-- Make an element draggable -->
<div draggable="true" id="drag-item">Drag me</div>
<div id="drop-zone">Drop here</div>
```

```javascript
const item = document.getElementById("drag-item");
const zone = document.getElementById("drop-zone");

item.addEventListener("dragstart", (e) => {
  e.dataTransfer.setData("text/plain", e.target.id);
});

zone.addEventListener("dragover", (e) => {
  e.preventDefault(); // required to allow drop
});

zone.addEventListener("drop", (e) => {
  e.preventDefault();
  const id = e.dataTransfer.getData("text/plain");
  zone.appendChild(document.getElementById(id));
});
```

### hidden attribute

```html
<!-- hidden — removed from rendering AND accessibility tree -->
<div hidden>Not visible, not accessible</div>

<!-- versus CSS display: none — same visual effect -->
<div style="display: none;">Not visible, not accessible</div>

<!-- versus aria-hidden — visible but hidden from screen readers -->
<div aria-hidden="true">Visible but screen readers skip this</div>

<!-- versus visibility: hidden — invisible but takes up space -->
<div style="visibility: hidden;">Invisible but space reserved</div>

<!-- versus opacity: 0 — invisible but takes up space AND is interactive -->
<div style="opacity: 0;">Invisible but clickable</div>
```

**Choosing the right method:**

```
Method              | Visible | Takes space | Accessible | Interactive
--------------------|---------|-------------|------------|------------
hidden              | ❌      | ❌          | ❌         | ❌
display: none       | ❌      | ❌          | ❌         | ❌
aria-hidden="true"  | ✅      | ✅          | ❌         | ✅
visibility: hidden  | ❌      | ✅          | ❌         | ❌
opacity: 0          | ❌      | ✅          | ✅         | ✅
```

### Other attributes

```html
<!-- spellcheck -->
<textarea spellcheck="true">Check my spelling</textarea>
<input type="text" spellcheck="false" />  <!-- disable for code/IDs -->

<!-- translate -->
<p translate="no">Akshai TR</p>  <!-- don't translate proper nouns -->

<!-- autocomplete -->
<input type="email" autocomplete="email" />
<input type="text" autocomplete="given-name" />
<input type="text" autocomplete="off" />  <!-- disable autofill -->

<!-- inputmode — controls virtual keyboard WITHOUT validation -->
<input type="text" inputmode="numeric" />    <!-- number pad -->
<input type="text" inputmode="decimal" />    <!-- number pad with decimal -->
<input type="text" inputmode="tel" />        <!-- phone pad -->
<input type="text" inputmode="email" />      <!-- email keyboard -->
<input type="text" inputmode="url" />        <!-- URL keyboard -->
<input type="text" inputmode="search" />     <!-- search keyboard -->
```

📢 NOTES:

> `inputmode` is different from `type`. `type="number"` adds validation and spinner buttons. `inputmode="numeric"` only changes the keyboard — useful when you want a numeric keyboard for inputs like OTP codes or ZIP codes that aren't truly "numbers."

# HTML APIs that Senior Devs Should Know

### dialog element — native modal

```html
<dialog id="myDialog">
  <h2>Confirm Action</h2>
  <p>Are you sure you want to delete this item?</p>
  <form method="dialog">
    <button value="cancel">Cancel</button>
    <button value="confirm">Confirm</button>
  </form>
</dialog>

<button onclick="document.getElementById('myDialog').showModal()">
  Delete Item
</button>
```

```javascript
const dialog = document.getElementById("myDialog");

// showModal() — opens with backdrop, traps focus, closes with Escape
dialog.showModal();

// show() — opens without backdrop, no focus trapping
dialog.show();

// Close programmatically
dialog.close();

// Listen for close
dialog.addEventListener("close", () => {
  console.log(dialog.returnValue); // "cancel" or "confirm"
});
```

**Why use native `<dialog>` over a custom modal:**
- Focus trapping is automatic
- Escape key closes it automatically
- The `::backdrop` pseudo-element provides a native overlay
- The `returnValue` gives you the user's choice
- Proper accessibility — announced as a dialog by screen readers

```css
dialog::backdrop {
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(4px);
}
```

### template element — hidden reusable markup

```html
<!-- Not rendered, not in the DOM until you clone it -->
<template id="card-template">
  <div class="card">
    <h3 class="card-title"></h3>
    <p class="card-body"></p>
  </div>
</template>
```

```javascript
const template = document.getElementById("card-template");

function createCard(title, body) {
  const clone = template.content.cloneNode(true); // deep clone
  clone.querySelector(".card-title").textContent = title;
  clone.querySelector(".card-body").textContent = body;
  document.getElementById("container").appendChild(clone);
}

createCard("Closures", "A function that remembers its scope...");
createCard("Promises", "Represents an async operation...");
```

Content inside `<template>` is parsed but not rendered — images don't load, scripts don't run. It's truly inert until cloned.

### Popover API — native popover without JS

```html
<!-- Toggle button and popover — no JavaScript needed -->
<button popovertarget="my-popover">Toggle Popover</button>

<div id="my-popover" popover>
  <p>This is a popover! Click outside to dismiss.</p>
</div>
```

**Popover types:**

```html
<!-- auto (default) — closes when clicking outside or pressing Escape -->
<div popover="auto">Light dismiss popover</div>

<!-- manual — only closes via JS or toggle button -->
<div popover="manual">Must be explicitly closed</div>
```

```javascript
const popover = document.getElementById("my-popover");
popover.showPopover();
popover.hidePopover();
popover.togglePopover();
```

**Why use native popover over custom implementations:**
- Light dismiss (click outside to close) is built-in
- Escape key handling is automatic
- Placed on the top layer — no z-index battles
- Accessible by default

### details and summary — native accordion

```html
<details>
  <summary>What is a closure?</summary>
  <p>A closure is a function that retains access to its lexical scope 
  even after the outer function has finished executing.</p>
</details>

<details open>  <!-- open by default -->
  <summary>What is hoisting?</summary>
  <p>Hoisting is JavaScript's behavior of moving declarations to the 
  top of their scope during compilation.</p>
</details>
```

```javascript
// Listen for toggle
const details = document.querySelector("details");
details.addEventListener("toggle", () => {
  console.log(details.open ? "Opened" : "Closed");
});
```

No CSS or JavaScript needed for basic show/hide behavior. Style the `<summary>` marker with `summary::marker` or `summary::-webkit-details-marker`.

### Web Components basics

```html
<!-- Using a web component -->
<user-card name="Akshai" role="Frontend Engineer"></user-card>
```

```javascript
class UserCard extends HTMLElement {
  constructor() {
    super();
    
    // Attach shadow DOM — encapsulated styles
    const shadow = this.attachShadow({ mode: "open" });
    
    shadow.innerHTML = `
      <style>
        .card {
          padding: 16px;
          border: 1px solid #ddd;
          border-radius: 8px;
        }
        .name { font-weight: bold; }
      </style>
      <div class="card">
        <p class="name">${this.getAttribute("name")}</p>
        <p class="role">${this.getAttribute("role")}</p>
      </div>
    `;
  }

  // Lifecycle callbacks
  connectedCallback() { }    // element added to DOM
  disconnectedCallback() { } // element removed from DOM
  attributeChangedCallback(name, oldVal, newVal) { } // attribute changed

  static get observedAttributes() {
    return ["name", "role"]; // which attributes to watch
  }
}

// Register the custom element
customElements.define("user-card", UserCard);
```

**slot element — content projection:**

```html
<!-- Definition -->
<template id="card-template">
  <div class="card">
    <slot name="title">Default title</slot>
    <slot>Default content</slot>  <!-- unnamed = default slot -->
  </div>
</template>

<!-- Usage -->
<user-card>
  <h2 slot="title">Akshai</h2>
  <p>Frontend Engineer with 8 years of experience.</p>
</user-card>
```

# Performance Considerations

### Critical Rendering Path

The sequence of steps the browser takes to convert HTML, CSS, and JS into pixels on screen:

```
HTML → DOM Tree
                  ↘
                    Render Tree → Layout → Paint → Composite → Pixels
                  ↗
CSS  → CSSOM Tree

JavaScript can modify both DOM and CSSOM at any point
```

**What blocks rendering:**
- CSS blocks rendering — browser won't paint until CSSOM is built
- JavaScript blocks HTML parsing (unless defer/async)
- JavaScript can't run until CSSOM is ready (it might read styles)

**Optimization goal:** minimize the time between first byte received and first meaningful paint.

### Resource hints (recap with performance context)

```html
<head>
  <!-- 1. preconnect to critical third parties FIRST -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://api.example.com" />
  
  <!-- 2. preload critical resources -->
  <link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin />
  <link rel="preload" href="/css/critical.css" as="style" />
  
  <!-- 3. CSS -->
  <link rel="stylesheet" href="/css/critical.css" />
  
  <!-- 4. prefetch next-page resources (low priority) -->
  <link rel="prefetch" href="/js/about-page.js" />
  
  <!-- 5. deferred scripts -->
  <script defer src="/js/app.js"></script>
</head>
```

### Lazy loading

```html
<!-- Images — native lazy loading -->
<img src="photo.jpg" alt="..." loading="lazy" />

<!-- iframe — also supports lazy loading -->
<iframe src="https://youtube.com/embed/..." loading="lazy"></iframe>

<!-- DON'T lazy load above-the-fold content -->
<!-- Hero image should load immediately -->
<img src="hero.jpg" alt="..." fetchpriority="high" />
```

### fetchpriority

```html
<!-- High priority — critical above-the-fold image -->
<img src="hero.jpg" fetchpriority="high" alt="..." />

<!-- Low priority — below-the-fold images -->
<img src="footer-image.jpg" fetchpriority="low" alt="..." loading="lazy" />

<!-- High priority — critical script -->
<script src="app.js" fetchpriority="high"></script>

<!-- Low priority — analytics -->
<script src="analytics.js" fetchpriority="low" async></script>
```

### Reducing DOM complexity

```html
<!-- BAD — deeply nested, excessive DOM nodes -->
<div class="wrapper">
  <div class="container">
    <div class="row">
      <div class="col">
        <div class="card">
          <div class="card-inner">
            <div class="card-content">
              <p>Hello</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- GOOD — flat structure -->
<article class="card">
  <p>Hello</p>
</article>
```

**Why DOM size matters:**
- More nodes = slower style calculations
- More depth = longer selector matching
- More nodes = more memory usage
- Large DOMs slow down `querySelectorAll`, layout, and garbage collection
- Recommended: under 1500 nodes total, max depth of 32, max 60 children per node

### Preload scanner

The browser has a preload scanner that looks ahead in the HTML for resources to download early, even while the main parser is blocked by JavaScript. It finds `<img>`, `<link>`, `<script>` tags and starts downloading them.

Resources loaded via JavaScript (like background images in CSS or dynamically inserted scripts) are invisible to the preload scanner — they start downloading later. This is why critical resources should be in HTML, not generated by JS.

# SEO Essentials

### Heading hierarchy

```html
<!-- GOOD — logical nesting, one h1 -->
<h1>JavaScript Concepts</h1>
  <h2>Closures</h2>
    <h3>Lexical Scope</h3>
    <h3>Practical Uses</h3>
  <h2>Promises</h2>
    <h3>Promise.all()</h3>

<!-- BAD — skipping levels, multiple h1s -->
<h1>JavaScript</h1>
<h1>Concepts</h1>          <!-- two h1s -->
<h4>Closures</h4>          <!-- skipped h2 and h3 -->
```

One `<h1>` per page. Don't skip heading levels. Headings create a document outline that search engines and screen readers use to understand content structure.

### Canonical URLs

```html
<!-- Tells search engines which URL is the authoritative version -->
<link rel="canonical" href="https://example.com/blog/closures" />
```

Prevents duplicate content penalties when the same content is accessible via multiple URLs:
- `https://example.com/blog/closures`
- `https://example.com/blog/closures?ref=twitter`
- `https://www.example.com/blog/closures`
- `http://example.com/blog/closures`

### Structured data with JSON-LD

```html
<!-- Tells search engines what type of content this is -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Understanding Closures in JavaScript",
  "author": {
    "@type": "Person",
    "name": "Akshai"
  },
  "datePublished": "2025-03-15",
  "description": "A deep dive into JavaScript closures..."
}
</script>
```

This enables rich results in Google — article cards, FAQ dropdowns, recipe cards, star ratings, etc.

**FAQ structured data:**

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is a closure in JavaScript?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "A closure is a function that retains access to its lexical scope..."
      }
    }
  ]
}
</script>
```

### Multilingual sites

```html
<!-- Tell search engines about language alternatives -->
<link rel="alternate" hreflang="en" href="https://example.com/en/closures" />
<link rel="alternate" hreflang="ta" href="https://example.com/ta/closures" />
<link rel="alternate" hreflang="x-default" href="https://example.com/closures" />
```

`x-default` is the fallback for users whose language isn't specifically targeted.

### Social sharing tags (recap)

```html
<head>
  <title>Understanding Closures | JS Concepts</title>
  <meta name="description" content="A deep dive into JavaScript closures..." />
  
  <!-- Open Graph (Facebook, LinkedIn, WhatsApp) -->
  <meta property="og:title" content="Understanding Closures in JavaScript" />
  <meta property="og:description" content="A deep dive..." />
  <meta property="og:image" content="https://example.com/og-image.png" />
  <meta property="og:url" content="https://example.com/blog/closures" />
  
  <!-- Twitter -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content="Understanding Closures in JavaScript" />
  <meta name="twitter:description" content="A deep dive..." />
  <meta name="twitter:image" content="https://example.com/twitter-image.png" />
  
  <!-- Canonical -->
  <link rel="canonical" href="https://example.com/blog/closures" />
</head>
```

### robots.txt and sitemap

These aren't HTML tags, but they work alongside your HTML for SEO:

```
# robots.txt — tells crawlers what to index
User-agent: *
Allow: /
Disallow: /admin/
Disallow: /api/
Sitemap: https://example.com/sitemap.xml
```

```xml
<!-- sitemap.xml — lists all indexable pages -->
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/blog/closures</loc>
    <lastmod>2025-03-15</lastmod>
    <priority>0.8</priority>
  </url>
</urlset>
```
