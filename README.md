# HTML Concepts

## Table of Contents

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
14. [Web Storage](#web-storage)
15. [Performance Considerations](#performance-considerations)
16. [Security](#security)
17. [SEO Essentials](#seo-essentials)
18. [Progressive Web Apps (PWA) Basics](#progressive-web-apps-pwa-basics)

---

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

<!-- dl, dt, dd — description list (glossaries, metadata, key-value pairs) -->
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language — the structure of web pages.</dd>
  <dt>CSS</dt>
  <dd>Cascading Style Sheets — the presentation of web pages.</dd>
</dl>
```

---

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

**Standards mode** — the browser follows the W3C/CSS specifications correctly. Box model works as expected, CSS layout rules are applied consistently.

**Quirks mode** — the browser mimics old IE5/Netscape-era behavior. The biggest difference is the box model: in quirks mode, `width` includes padding and border. CSS behaves unpredictably.

You can check which mode a page is using:

```javascript
document.compatMode
// "CSS1Compat" = standards mode
// "BackCompat" = quirks mode
```

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
  <link rel="icon" href="/favicon.ico" sizes="32x32" />
  <link rel="icon" href="/favicon.svg" type="image/svg+xml" />
  <link rel="apple-touch-icon" href="/apple-touch-icon.png" />
</head>
```

**`<meta charset="UTF-8">`** — defines character encoding. UTF-8 supports virtually all characters and symbols worldwide. Without it, special characters might display as garbled text. Must be within the first 1024 bytes of the document — the browser needs to know the encoding before it can correctly read anything else.

**`<meta name="viewport">`** — controls how the page scales on mobile devices. Without it, mobile browsers render the page at desktop width and zoom out, making text tiny. `width=device-width` sets the viewport to the device's width. `initial-scale=1.0` sets the initial zoom level.

### Viewport deep dive

```html
<!-- Standard — use this for 99% of cases -->
<meta name="viewport" content="width=device-width, initial-scale=1.0" />

<!-- Prevent user zoom (BAD for accessibility — avoid) -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />

<!-- Allow zoom but set limits -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=5.0" />

<!-- For full-screen apps that extend under the notch (iPhone) -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
```

📢 NOTES:

> Never disable user zoom (`user-scalable=no` or `maximum-scale=1.0`) unless you have a very specific reason (like a full-screen game). Users with low vision rely on zoom to read content. WCAG considers disabling zoom an accessibility failure.

> `viewport-fit=cover` is needed when you want content to extend behind the iPhone notch/dynamic island. Pair it with `env(safe-area-inset-*)` CSS values to prevent content from going under the notch.

### Favicon best practices

```html
<head>
  <!-- Standard favicon -->
  <link rel="icon" href="/favicon.ico" sizes="32x32" />

  <!-- SVG favicon (modern browsers — supports dark mode) -->
  <link rel="icon" href="/favicon.svg" type="image/svg+xml" />

  <!-- Apple touch icon (iOS home screen — 180×180px, no transparency) -->
  <link rel="apple-touch-icon" href="/apple-touch-icon.png" />

  <!-- Web app manifest (PWA) -->
  <link rel="manifest" href="/manifest.json" />
</head>
```

SVG favicons can adapt to dark mode:

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100">
  <style>
    circle { fill: #4A90D9; }
    @media (prefers-color-scheme: dark) {
      circle { fill: #7AB8FF; }
    }
  </style>
  <circle cx="50" cy="50" r="45" />
</svg>
```

### How the browser parses HTML — the Critical Rendering Path

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

**Step 1-2:** The server sends raw bytes. The browser uses `<meta charset="UTF-8">` to know how to decode those bytes into readable characters.

**Step 3-4:** The HTML parser reads characters and tokenizes them into tags (start tags, end tags, text content), then assembles those tokens into the DOM tree — a tree structure of nodes with parent-child relationships. This is the DOM you interact with in JavaScript.

**Step 5:** When the parser hits a `<link rel="stylesheet">` or `<style>` block, the browser builds the CSSOM — a tree of all styles with computed values after cascade, specificity, and inheritance are resolved. CSS is render-blocking — the browser won't paint until the CSSOM is complete, because showing unstyled content and then reflowing would be a terrible user experience (Flash of Unstyled Content — FOUC).

**Step 6:** When the parser hits a `<script>` tag (without `defer` or `async`), it stops building the DOM, downloads the script (if external), waits for CSSOM to be ready, executes the script, then resumes parsing. This is why script placement matters.

**Step 7:** The DOM and CSSOM combine into the Render Tree — only visible elements. `<head>`, `<script>`, and elements with `display: none` are excluded. Elements with `visibility: hidden` ARE included (they take up space).

**Step 8:** Layout calculates exact position and size of every element. Paint fills in pixels (colors, text, borders, shadows). Composite combines painted layers using the GPU for the final image on screen.

```
Most expensive ←————————————→ Least expensive
Layout (Reflow) → Paint → Composite

Changing width/margin    → triggers all three
Changing color/shadow    → triggers paint + composite
Changing transform/opacity → triggers only composite (cheapest)
```

This is why CSS animations should use `transform` and `opacity` — they skip the expensive layout and paint steps.

---

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
```

**`index` / `noindex`** — should this page appear in search results?

**`follow` / `nofollow`** — should the crawler follow the links on this page?

When to use: `noindex, nofollow` for admin pages, login pages, staging environments. `noindex, follow` for paginated pages like `/blog?page=5` — you don't want page 5 in search results but you want Google to discover the actual articles through the links.

```html
<!-- Canonical URL — tells search engines which URL is the "official" version -->
<link rel="canonical" href="https://example.com/blog/closures" />
```

Prevents duplicate content penalties when the same content is accessible via multiple URLs (`?ref=twitter`, `www` vs non-`www`, `http` vs `https`). Google consolidates all ranking signals into the canonical URL.

### Open Graph tags — social media sharing

When you share a link on LinkedIn, Facebook, Slack, or WhatsApp, the platform fetches your page and reads these tags to build the preview card:

```html
<meta property="og:title" content="Understanding Closures in JavaScript" />
<meta property="og:description" content="A deep dive into how closures work..." />
<meta property="og:image" content="https://example.com/images/closures-og.png" />
<meta property="og:url" content="https://example.com/blog/closures" />
<meta property="og:type" content="article" />
<meta property="og:site_name" content="JS Concepts" />
```

Without these tags, platforms try to auto-generate a preview — usually poorly.

📢 NOTES:

> `og:image` should be at least 1200×630 pixels for best display across platforms. Must be a full absolute URL, not a relative path. Test your tags with Facebook's Sharing Debugger, LinkedIn's Post Inspector, or Twitter's Card Validator.

### Twitter Card tags

```html
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="Understanding Closures in JavaScript" />
<meta name="twitter:description" content="A deep dive into how closures work..." />
<meta name="twitter:image" content="https://example.com/images/closures-twitter.png" />
```

If Twitter card tags are missing, Twitter falls back to Open Graph tags.

### Other useful meta tags

```html
<!-- Theme color — colors the browser toolbar on mobile -->
<meta name="theme-color" content="#1a1a2e" />
<meta name="theme-color" content="#ffffff" media="(prefers-color-scheme: light)" />
<meta name="theme-color" content="#1a1a2e" media="(prefers-color-scheme: dark)" />

<!-- Prevent automatic phone number detection on iOS -->
<meta name="format-detection" content="telephone=no" />

<!-- HTTP equiv — rarely needed but good to know -->
<meta http-equiv="refresh" content="30" />  <!-- auto-refresh every 30 seconds -->
<meta http-equiv="refresh" content="3;url=https://example.com/new-page" /> <!-- redirect after 3s -->

<!-- Content Security Policy (basic) -->
<meta http-equiv="Content-Security-Policy" content="default-src 'self'" />
```

---

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
<input type="email" />         <!-- email validation + mobile @ keyboard -->
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

### Radio button groups

```html
<!-- Radio buttons MUST share the same name to form a group -->
<fieldset>
  <legend>Preferred contact method</legend>

  <label>
    <input type="radio" name="contact" value="email" checked />
    Email
  </label>

  <label>
    <input type="radio" name="contact" value="phone" />
    Phone
  </label>

  <label>
    <input type="radio" name="contact" value="sms" />
    SMS
  </label>
</fieldset>
```

The `name` attribute groups radio buttons together — selecting one deselects the others in the same group. Without matching `name` values, they act as independent checkboxes.

### Checkbox groups

```html
<fieldset>
  <legend>Select your skills</legend>

  <label>
    <input type="checkbox" name="skills" value="html" />
    HTML
  </label>

  <label>
    <input type="checkbox" name="skills" value="css" />
    CSS
  </label>

  <label>
    <input type="checkbox" name="skills" value="javascript" />
    JavaScript
  </label>
</fieldset>
```

Unlike radio buttons, multiple checkboxes can be selected. Use the same `name` when they're logically a group — `FormData.getAll("skills")` returns all checked values.

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

---

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

### Live regions — strategies

```html
<!-- Status messages — polite, waits for user to finish reading -->
<div role="status" aria-live="polite">
  Search found 42 results
</div>

<!-- Error alerts — assertive, interrupts immediately -->
<div role="alert" aria-live="assertive">
  Session expired. Please log in again.
</div>

<!-- Log — new entries are announced, old ones aren't re-read -->
<div role="log" aria-live="polite">
  <p>User joined the chat</p>
</div>

<!-- aria-atomic — read the ENTIRE region when any part changes -->
<div aria-live="polite" aria-atomic="true">
  Your cart: 3 items, $45.00 total
  <!-- When total changes, the ENTIRE sentence is re-read, not just the number -->
</div>
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
```

```css
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  z-index: 100;
}
.skip-link:focus {
  top: 0;  /* visible only when focused via Tab */
}
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
      if (document.activeElement === first) {
        e.preventDefault();
        last.focus();
      }
    } else {
      if (document.activeElement === last) {
        e.preventDefault();
        first.focus();
      }
    }
  });

  first.focus();
}
```

📢 NOTES:

> The native `<dialog>` element with `showModal()` handles focus trapping automatically. Use it instead of building your own modal when possible.

### Screen reader only text

```css
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

📢 NOTES:

> Never rely on color alone to convey information. Always pair it with text, icons, or patterns:

```html
<!-- BAD — color is the only indicator -->
<span style="color: red;">Error</span>

<!-- GOOD — icon + text + color -->
<span style="color: red;">❌ Error: Email is required</span>
```

### The accessibility tree

The browser builds an accessibility tree from the DOM — a simplified version that screen readers use:

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

Inspect it in Chrome DevTools → Elements → Accessibility pane.

---

# Script and Style Loading

How and where you load CSS and JavaScript directly impacts page rendering speed.

### CSS loading — render blocking

```html
<head>
  <link rel="stylesheet" href="styles.css" />
  <!-- Browser won't paint ANYTHING until this CSS is downloaded and parsed -->
</head>
```

**Strategies to reduce CSS blocking:**

```html
<head>
  <!-- Critical CSS inlined — instant first paint for above-the-fold content -->
  <style>
    body { font-family: sans-serif; margin: 0; }
    .hero { height: 100vh; display: flex; }
  </style>

  <!-- Non-critical CSS loaded asynchronously -->
  <link rel="preload" href="full-styles.css" as="style"
    onload="this.onload=null;this.rel='stylesheet'" />

  <!-- Media-specific CSS — only blocks rendering for matching media -->
  <link rel="stylesheet" href="print.css" media="print" />
  <link rel="stylesheet" href="mobile.css" media="(max-width: 768px)" />
</head>
```

### JavaScript loading — three modes

**Default `<script>` — blocks everything:**

```html
<script src="app.js"></script>
<!-- Browser stops parsing HTML → downloads JS → executes JS → resumes HTML -->
```

```
HTML parsing:  ████████░░░░░░░░░░░░████████████
JS download:          ████████
JS execute:                   ████
                     ↑ HTML blocked here
```

**`<script defer>` — download in parallel, execute after HTML is parsed:**

```html
<script defer src="app.js"></script>
<script defer src="analytics.js"></script>
```

```
HTML parsing:  ██████████████████████████████████
JS download:      ████████
JS execute:                                      ████
                                                ↑ after parsing, maintains order
```

**`<script async>` — download in parallel, execute immediately when ready:**

```html
<script async src="analytics.js"></script>
```

```
HTML parsing:  ████████████░░░░██████████████████
JS download:      ████████
JS execute:               ████
                         ↑ executes whenever ready, no guaranteed order
```

**`<script type="module">` — deferred by default:**

```html
<script type="module" src="app.js"></script>
```

Behaves like `defer`, enables `import`/`export`, always strict mode, executed only once.

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

### Resource hints

```html
<!-- preload — download NOW, need it soon (high priority) -->
<link rel="preload" href="critical-font.woff2" as="font" type="font/woff2" crossorigin />
<link rel="preload" href="hero-image.webp" as="image" />

<!-- prefetch — download in idle time, need it on NEXT page (low priority) -->
<link rel="prefetch" href="/about-page-bundle.js" />

<!-- preconnect — establish connection early (DNS + TCP + TLS) -->
<link rel="preconnect" href="https://api.example.com" />
<link rel="preconnect" href="https://fonts.googleapis.com" />

<!-- dns-prefetch — resolve DNS only (lighter than preconnect) -->
<link rel="dns-prefetch" href="https://analytics.example.com" />

<!-- modulepreload — preload ES modules -->
<link rel="modulepreload" href="./utils.js" />
```

---

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

**`width` and `height`** — set these in HTML even if you resize with CSS. The browser uses the aspect ratio to reserve space before the image loads, preventing layout shift (CLS).

**`loading="lazy"`** — defers loading until near the viewport. Don't use on above-the-fold images.

**`decoding="async"`** — decode the image off the main thread, preventing jank.

### Responsive images with srcset and sizes

```html
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

`srcset` tells the browser what's available. `sizes` tells it how wide the image will display. The browser picks the best match.

### picture element — art direction and format switching

```html
<!-- Serve modern formats with fallback -->
<picture>
  <source srcset="photo.avif" type="image/avif" />
  <source srcset="photo.webp" type="image/webp" />
  <img src="photo.jpg" alt="Landscape photo" />
</picture>

<!-- Different images at different breakpoints -->
<picture>
  <source media="(max-width: 600px)" srcset="photo-mobile.jpg" />
  <source media="(max-width: 1000px)" srcset="photo-tablet.jpg" />
  <img src="photo-desktop.jpg" alt="Landscape photo" />
</picture>
```

### Image formats

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

In practice: SVG for icons/logos, WebP/AVIF for photos with JPEG fallback, avoid PNG for photos.

### Video and audio

```html
<video controls width="720" poster="thumbnail.jpg" preload="metadata">
  <source src="video.webm" type="video/webm" />
  <source src="video.mp4" type="video/mp4" />
  <track kind="subtitles" src="captions-en.vtt" srclang="en" label="English" default />
  Your browser doesn't support video.
</video>

<audio controls preload="none">
  <source src="podcast.ogg" type="audio/ogg" />
  <source src="podcast.mp3" type="audio/mpeg" />
</audio>
```

`preload`: `none` (saves bandwidth), `metadata` (duration/dimensions only — recommended), `auto` (browser decides).

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
```

---

# Links and Navigation

```html
<!-- Basic link -->
<a href="https://example.com">Visit Example</a>

<!-- Open in new tab — always add rel for security -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
  Visit Example
</a>

<!-- Anchor link — scroll to element -->
<a href="#section-2">Jump to Section 2</a>

<!-- Download link -->
<a href="/files/report.pdf" download="Q3-Report.pdf">Download Report</a>

<!-- Email and phone -->
<a href="mailto:akshai@example.com">Email us</a>
<a href="tel:+911234567890">Call us</a>
```

### rel="noopener noreferrer"

Without `noopener`, the opened page can access your page via `window.opener` and redirect it to a phishing site. `noreferrer` also prevents sending the Referer header. Modern browsers apply `noopener` automatically for `target="_blank"`, but explicit is safer.

### Link vs Button

If clicking it takes you somewhere → `<a>`. If clicking it does something → `<button>`.

```html
<!-- BAD -->
<a href="#" onclick="submitForm()">Submit</a>
<a href="javascript:void(0)" onclick="openModal()">Open</a>

<!-- GOOD -->
<button onclick="submitForm()">Submit</button>
<button onclick="openModal()">Open</button>
```

They have different keyboard behavior (Enter vs Enter+Space), different ARIA roles, and different screen reader announcements.

### rel attribute values

```html
<a rel="nofollow" href="...">     <!-- search engines won't follow -->
<a rel="sponsored" href="...">    <!-- paid link -->
<a rel="ugc" href="...">          <!-- user-generated content -->
<a rel="noopener" href="..." target="_blank">  <!-- security -->
<a rel="noreferrer" href="...">   <!-- no Referer header -->
<a rel="external" href="...">     <!-- external link -->
```

---

# Tables

Tables are for tabular data only — never for page layout.

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

`<caption>` describes the table for screen readers. `scope` tells screen readers whether a header applies to its column or row. `<thead>`, `<tbody>`, `<tfoot>` provide semantic grouping.

### Spanning

```html
<th colspan="2">Full Name</th>  <!-- spans 2 columns -->
<td rowspan="2">28</td>         <!-- spans 2 rows -->
```

---

# Data Attributes

Store custom data on HTML elements:

```html
<article data-id="42" data-category="javascript" data-author-name="Akshai">
  <h2>Understanding Closures</h2>
</article>
```

```javascript
const article = document.querySelector("article");

article.dataset.id;          // "42" (always a string)
article.dataset.category;    // "javascript"
article.dataset.authorName;  // "Akshai" (data-author-name → camelCase)

article.dataset.views = "1500";  // set
delete article.dataset.views;    // remove
```

```css
[data-category="javascript"] { border-left: 3px solid yellow; }

[data-tooltip]:hover::after {
  content: attr(data-tooltip);
  position: absolute;
  background: #333;
  color: white;
  padding: 4px 8px;
}
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

---

# Content Embedding

### iframe

```html
<iframe src="https://example.com" width="600" height="400" title="Example website"></iframe>

<!-- YouTube embed -->
<iframe src="https://www.youtube.com/embed/VIDEO_ID" width="560" height="315"
  title="Video title" allow="accelerometer; autoplay; clipboard-write; encrypted-media"
  allowfullscreen loading="lazy"></iframe>
```

### iframe security — sandbox

```html
<!-- Full sandbox — disables everything -->
<iframe src="untrusted.html" sandbox></iframe>

<!-- Selective permissions -->
<iframe src="widget.html" sandbox="allow-scripts allow-same-origin allow-forms allow-popups"></iframe>
```

📢 NOTES:

> Never use `allow-scripts` and `allow-same-origin` together on untrusted content — the script could remove the sandbox entirely.

### Clickjacking protection

```
HTTP headers (preferred):
X-Frame-Options: DENY
X-Frame-Options: SAMEORIGIN
Content-Security-Policy: frame-ancestors 'none'
Content-Security-Policy: frame-ancestors 'self'
```

### srcdoc — inline HTML

```html
<iframe srcdoc="<h1>Hello</h1><p>Inline HTML content</p>" title="Preview"></iframe>
```

---

# Interactive Attributes

### contenteditable

```html
<div contenteditable="true">Click here and start typing...</div>
```

```javascript
document.getElementById("editor").addEventListener("input", () => {
  console.log(editor.innerHTML);
});
```

### draggable

```html
<div draggable="true" id="drag-item">Drag me</div>
<div id="drop-zone">Drop here</div>
```

```javascript
item.addEventListener("dragstart", (e) => e.dataTransfer.setData("text/plain", e.target.id));
zone.addEventListener("dragover", (e) => e.preventDefault());
zone.addEventListener("drop", (e) => {
  e.preventDefault();
  zone.appendChild(document.getElementById(e.dataTransfer.getData("text/plain")));
});
```

### hidden attribute — ways to hide elements

```html
<div hidden>hidden attribute</div>
<div style="display: none;">display none</div>
<div aria-hidden="true">aria-hidden</div>
<div style="visibility: hidden;">visibility hidden</div>
<div style="opacity: 0;">opacity zero</div>
```

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
<textarea spellcheck="true">Check my spelling</textarea>
<input type="text" spellcheck="false" />  <!-- disable for code/IDs -->

<p translate="no">Akshai TR</p>  <!-- don't translate proper nouns -->

<input type="email" autocomplete="email" />
<input type="text" autocomplete="given-name" />
<input type="text" autocomplete="off" />

<!-- inputmode — controls virtual keyboard WITHOUT validation -->
<input type="text" inputmode="numeric" />  <!-- number pad for OTP/ZIP -->
<input type="text" inputmode="decimal" />  <!-- number pad with decimal -->
<input type="text" inputmode="tel" />      <!-- phone pad -->
<input type="text" inputmode="url" />      <!-- URL keyboard -->
```

📢 NOTES:

> `inputmode` is different from `type`. `type="number"` adds validation and spinner buttons. `inputmode="numeric"` only changes the keyboard — useful for OTP codes or ZIP codes that aren't truly "numbers."

---

# HTML APIs that Senior Devs Should Know

### dialog — native modal

```html
<dialog id="myDialog">
  <h2>Confirm Action</h2>
  <p>Are you sure?</p>
  <form method="dialog">
    <button value="cancel">Cancel</button>
    <button value="confirm">Confirm</button>
  </form>
</dialog>

<button onclick="document.getElementById('myDialog').showModal()">Delete</button>
```

```javascript
const dialog = document.getElementById("myDialog");
dialog.showModal();  // opens with backdrop, traps focus, Escape closes
dialog.show();       // opens without backdrop
dialog.close();
dialog.addEventListener("close", () => console.log(dialog.returnValue));
```

```css
dialog::backdrop {
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(4px);
}
```

Native `<dialog>` gives you focus trapping, Escape key, backdrop, and accessibility for free.

### template — hidden reusable markup

```html
<template id="card-template">
  <div class="card">
    <h3 class="card-title"></h3>
    <p class="card-body"></p>
  </div>
</template>
```

```javascript
const template = document.getElementById("card-template");
const clone = template.content.cloneNode(true);
clone.querySelector(".card-title").textContent = "Closures";
document.getElementById("container").appendChild(clone);
```

Content inside `<template>` is parsed but not rendered — images don't load, scripts don't run.

### Popover API — native popover without JS

```html
<button popovertarget="my-popover">Toggle Popover</button>
<div id="my-popover" popover>
  <p>Click outside to dismiss.</p>
</div>
```

```html
<div popover="auto">Light dismiss (click outside or Escape)</div>
<div popover="manual">Must be explicitly closed</div>
```

Native popovers: light dismiss built-in, top layer (no z-index battles), accessible by default.

### details and summary — native accordion

```html
<details>
  <summary>What is a closure?</summary>
  <p>A closure is a function that retains access to its lexical scope...</p>
</details>

<details open>  <!-- open by default -->
  <summary>What is hoisting?</summary>
  <p>Hoisting moves declarations to the top of their scope...</p>
</details>
```

No CSS or JavaScript needed for basic show/hide behavior.

### Web Components

```javascript
class UserCard extends HTMLElement {
  constructor() {
    super();
    const shadow = this.attachShadow({ mode: "open" });
    shadow.innerHTML = `
      <style>
        .card { padding: 16px; border: 1px solid #ddd; border-radius: 8px; }
      </style>
      <div class="card">
        <p><strong>${this.getAttribute("name")}</strong></p>
        <p>${this.getAttribute("role")}</p>
      </div>
    `;
  }

  connectedCallback() { }
  disconnectedCallback() { }
  attributeChangedCallback(name, oldVal, newVal) { }
  static get observedAttributes() { return ["name", "role"]; }
}

customElements.define("user-card", UserCard);
```

```html
<user-card name="Akshai" role="Frontend Engineer"></user-card>
```

**Slot — content projection:**

```html
<template id="card-template">
  <div class="card">
    <slot name="title">Default title</slot>
    <slot>Default content</slot>
  </div>
</template>
```

---

# Web Storage

### localStorage — persistent key-value storage

```javascript
// Store data — persists across browser sessions (until explicitly cleared)
localStorage.setItem("theme", "dark");
localStorage.setItem("user", JSON.stringify({ name: "Akshai", age: 28 }));

// Read data
localStorage.getItem("theme");  // "dark"
JSON.parse(localStorage.getItem("user"));  // { name: "Akshai", age: 28 }

// Remove
localStorage.removeItem("theme");

// Clear all
localStorage.clear();

// Storage limit: ~5-10MB per origin
// Synchronous API — blocks the main thread on large reads/writes
```

### sessionStorage — per-tab, cleared when tab closes

```javascript
// Same API as localStorage, but data is scoped to the tab
sessionStorage.setItem("scrollPosition", "500");
sessionStorage.getItem("scrollPosition");  // "500"
// Data is lost when the tab is closed
// Each tab has its own independent sessionStorage
```

### When to use which

```
Storage             | Persists     | Scope       | Size    | Use case
--------------------|-------------|-------------|---------|---------------------------
localStorage        | Forever      | All tabs    | ~5-10MB | Theme, language, user prefs
sessionStorage      | Until tab close | Per tab  | ~5-10MB | Form drafts, scroll position
Cookies             | Configurable | All tabs    | ~4KB    | Auth tokens, server-readable
IndexedDB           | Forever      | All tabs    | Large   | Offline data, large datasets
```

### IndexedDB — structured client-side database

```javascript
// Open a database
const request = indexedDB.open("MyApp", 1);

request.onupgradeneeded = (event) => {
  const db = event.target.result;
  const store = db.createObjectStore("users", { keyPath: "id", autoIncrement: true });
  store.createIndex("email", "email", { unique: true });
};

request.onsuccess = (event) => {
  const db = event.target.result;

  // Add data
  const tx = db.transaction("users", "readwrite");
  tx.objectStore("users").add({ name: "Akshai", email: "akshai@email.com" });

  // Read data
  const readTx = db.transaction("users", "readonly");
  const getReq = readTx.objectStore("users").get(1);
  getReq.onsuccess = () => console.log(getReq.result);
};
```

IndexedDB is complex — in practice, use a wrapper library like `idb` (by Jake Archibald) or Dexie.js.

### Storage events — cross-tab communication

```javascript
// Fires when another tab changes localStorage (not the current tab)
window.addEventListener("storage", (event) => {
  console.log(`Key: ${event.key}, Old: ${event.oldValue}, New: ${event.newValue}`);
});

// Use case: user logs out in one tab → all tabs respond
```

---

# Performance Considerations

### Core Web Vitals

Google uses these three metrics for search ranking:

**LCP (Largest Contentful Paint)** — how long until the largest visible element renders. Target: under 2.5 seconds.

How to fix: preload the LCP image with `fetchpriority="high"`, inline critical CSS, use server-side rendering.

```html
<link rel="preload" href="/hero.webp" as="image" fetchpriority="high" />
<img src="/hero.webp" alt="..." fetchpriority="high" />
```

**INP (Interaction to Next Paint)** — how long until the page responds to user interaction. Target: under 200ms.

How to fix: break up long JavaScript tasks, debounce event handlers, minimize DOM size.

**CLS (Cumulative Layout Shift)** — how much the layout shifts unexpectedly during loading. Target: under 0.1.

How to fix:

```html
<!-- Always set width and height on images -->
<img src="photo.jpg" width="800" height="600" alt="..." />

<!-- Reserve space for dynamic content -->
<div style="min-height: 250px;">
  <!-- ad or dynamic content loads here -->
</div>
```

### Resource loading optimization

```html
<head>
  <!-- 1. Preconnect to critical third parties -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://api.example.com" />

  <!-- 2. Preload critical resources -->
  <link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin />

  <!-- 3. CSS -->
  <link rel="stylesheet" href="/css/critical.css" />

  <!-- 4. Prefetch next-page resources -->
  <link rel="prefetch" href="/js/about-page.js" />

  <!-- 5. Deferred scripts -->
  <script defer src="/js/app.js"></script>
</head>
```

### Lazy loading

```html
<img src="photo.jpg" alt="..." loading="lazy" />
<iframe src="https://youtube.com/embed/..." loading="lazy"></iframe>

<!-- DON'T lazy load above-the-fold content -->
<img src="hero.jpg" alt="..." fetchpriority="high" />
```

### fetchpriority

```html
<img src="hero.jpg" fetchpriority="high" alt="..." />       <!-- critical -->
<img src="footer.jpg" fetchpriority="low" alt="..." loading="lazy" />  <!-- non-critical -->
<script src="app.js" fetchpriority="high"></script>
<script src="analytics.js" fetchpriority="low" async></script>
```

### DOM complexity

```html
<!-- BAD — deeply nested -->
<div><div><div><div><div><p>Hello</p></div></div></div></div></div>

<!-- GOOD — flat -->
<article class="card"><p>Hello</p></article>
```

Recommendations: under 1500 nodes total, max depth of 32, max 60 children per node.

### Preload scanner

The browser has a preload scanner that looks ahead for resources to download early, even while the main parser is blocked by JavaScript. Resources loaded via JS (dynamically inserted scripts, CSS background images) are invisible to it. Keep critical resources in HTML.

---

# Security

### Content Security Policy (CSP)

CSP tells the browser what resources are allowed to load and from where. It prevents XSS (Cross-Site Scripting) attacks by blocking unauthorized scripts.

```html
<!-- Via meta tag (limited) -->
<meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self' https://cdn.example.com; style-src 'self' 'unsafe-inline'" />
```

```
# Via HTTP header (preferred — more complete)
Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.example.com; img-src *; style-src 'self' 'unsafe-inline'
```

Common directives:

```
default-src 'self'                    — only allow resources from same origin
script-src 'self' https://cdn.com    — scripts from self and cdn.com only
style-src 'self' 'unsafe-inline'     — styles from self + inline styles
img-src *                             — images from anywhere
font-src 'self' https://fonts.com   — fonts from self and fonts.com
connect-src 'self' https://api.com   — fetch/XHR to self and api.com
frame-src 'none'                      — no iframes allowed
```

### Subresource Integrity (SRI)

Ensures CDN-loaded scripts haven't been tampered with:

```html
<script src="https://cdn.example.com/library.js"
  integrity="sha384-oqVuAfXRKap7fdgcCY5uykM6+R9GqQ8K/uxAUhk7wYR28+"
  crossorigin="anonymous"></script>
```

If the file's hash doesn't match the `integrity` attribute, the browser refuses to execute it. Generate hashes with `openssl dgst -sha384 -binary file.js | base64`.

### rel="noopener" for target="_blank"

Already covered in Links section — prevents the opened page from accessing `window.opener`.

### Referrer Policy

```html
<meta name="referrer" content="strict-origin-when-cross-origin" />
```

Controls how much URL information is sent in the Referer header:

```
no-referrer              — never send Referer
origin                    — send only the origin (https://example.com), not the full path
strict-origin-when-cross-origin — full URL to same origin, only origin to cross-origin (recommended default)
```

---

# SEO Essentials

### Heading hierarchy

```html
<!-- GOOD -->
<h1>JavaScript Concepts</h1>
  <h2>Closures</h2>
    <h3>Lexical Scope</h3>
  <h2>Promises</h2>

<!-- BAD -->
<h1>JavaScript</h1>
<h1>Concepts</h1>    <!-- two h1s -->
<h4>Closures</h4>    <!-- skipped h2 and h3 -->
```

One `<h1>` per page. Don't skip heading levels.

### Canonical URLs

```html
<link rel="canonical" href="https://example.com/blog/closures" />
```

Prevents duplicate content penalties when content is at multiple URLs.

### Structured data with JSON-LD

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Understanding Closures in JavaScript",
  "author": { "@type": "Person", "name": "Akshai" },
  "datePublished": "2025-03-15",
  "description": "A deep dive into JavaScript closures..."
}
</script>
```

Enables rich results in Google — article cards, FAQ dropdowns, star ratings.

**FAQ structured data:**

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "What is a closure?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "A closure is a function that retains access to its lexical scope..."
    }
  }]
}
</script>
```

**Breadcrumb structured data:**

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    { "@type": "ListItem", "position": 1, "name": "Home", "item": "https://example.com" },
    { "@type": "ListItem", "position": 2, "name": "Blog", "item": "https://example.com/blog" },
    { "@type": "ListItem", "position": 3, "name": "Understanding Closures" }
  ]
}
</script>
```

### Multilingual sites

```html
<link rel="alternate" hreflang="en" href="https://example.com/en/closures" />
<link rel="alternate" hreflang="ta" href="https://example.com/ta/closures" />
<link rel="alternate" hreflang="x-default" href="https://example.com/closures" />
```

### Social sharing tags

```html
<head>
  <title>Understanding Closures | JS Concepts</title>
  <meta name="description" content="A deep dive into JavaScript closures..." />

  <!-- Open Graph -->
  <meta property="og:title" content="Understanding Closures in JavaScript" />
  <meta property="og:description" content="A deep dive..." />
  <meta property="og:image" content="https://example.com/og-image.png" />
  <meta property="og:url" content="https://example.com/blog/closures" />

  <!-- Twitter -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content="Understanding Closures in JavaScript" />
  <meta name="twitter:image" content="https://example.com/twitter-image.png" />

  <link rel="canonical" href="https://example.com/blog/closures" />
</head>
```

### robots.txt and sitemap

```
# robots.txt
User-agent: *
Allow: /
Disallow: /admin/
Disallow: /api/
Sitemap: https://example.com/sitemap.xml
```

```xml
<!-- sitemap.xml -->
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/blog/closures</loc>
    <lastmod>2025-03-15</lastmod>
    <priority>0.8</priority>
  </url>
</urlset>
```

---

# Progressive Web Apps (PWA) Basics

### Web App Manifest

The manifest tells the browser how your app should behave when installed on a device:

```html
<link rel="manifest" href="/manifest.json" />
```

```json
{
  "name": "JS Concepts",
  "short_name": "JS",
  "description": "JavaScript concepts reference",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#4A90D9",
  "icons": [
    { "src": "/icon-192.png", "sizes": "192x192", "type": "image/png" },
    { "src": "/icon-512.png", "sizes": "512x512", "type": "image/png" }
  ]
}
```

`display` options: `browser` (normal tab), `standalone` (looks like a native app — no browser UI), `fullscreen` (no status bar), `minimal-ui` (minimal browser controls).

### Service Worker — basics

A Service Worker is a script that runs in the background, separate from the web page. It can intercept network requests, cache resources, and enable offline functionality.

```javascript
// Register in your main JS
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js')
    .then(reg => console.log('SW registered'))
    .catch(err => console.log('SW registration failed'));
}
```

```javascript
// sw.js — basic cache-first strategy
const CACHE_NAME = 'v1';
const URLS_TO_CACHE = ['/', '/styles.css', '/app.js', '/offline.html'];

// Install — cache core assets
self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => cache.addAll(URLS_TO_CACHE))
  );
});

// Fetch — serve from cache, fallback to network
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request)
      .then(response => response || fetch(event.request))
      .catch(() => caches.match('/offline.html'))
  );
});
```

### Meta tags for mobile app experience

```html
<!-- iOS status bar appearance -->
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
<meta name="apple-mobile-web-app-title" content="JS Concepts" />

<!-- Theme color (already covered but critical for PWA) -->
<meta name="theme-color" content="#4A90D9" />

<!-- Splash screen icon for iOS -->
<link rel="apple-touch-startup-image" href="/splash.png" />
```

### PWA installability requirements

For Chrome to show the "Add to Home Screen" prompt:

1. Valid `manifest.json` with `name`, `icons` (192px + 512px), `start_url`, `display`
2. Served over HTTPS
3. Registered Service Worker with a fetch handler
4. The user has interacted with the site sufficiently
