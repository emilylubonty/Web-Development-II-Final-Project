# Project fixes complete: House M.D. Meme Collection

**Generated:** December 23, 2025 at 3:24 PM ET

## Summary

All 12 identified issues from the project evaluation have been resolved. This report documents each fix applied and explains why the change was necessary.

## Fixes applied

### 1. Tag format converted to arrays

**Files modified:**

- [chicken.md](../content/blog/chicken/chicken.md)
- [bromantic.md](../content/blog/bromance/bromantic.md)
- [liver.md](../content/blog/liver/liver.md)
- [globalmouse.md](../content/blog/globalmouse/globalmouse.md)
- [squeakypost.md](../content/blog/squeaky/squeakypost.md)

**Change:** Converted `tags: value` to YAML array format:

```yaml
tags:
  - value
```

**Why:** Eleventy's tag system works best with arrays. While single strings may work, arrays provide consistency, allow multiple tags per post, and prevent potential parsing issues.

### 2. Unclosed `<p>` tags fixed

**File modified:** [about.md](../content/about.md)

**Change:** Added closing `</p>` tags to all paragraph elements in the about-me section.

**Why:** Unclosed `<p>` tags create invalid HTML. Browsers attempt to auto-close them, but this can lead to unpredictable DOM structure and styling issues.

### 3. Email input attributes corrected

**File modified:** [about.md](../content/about.md)

**Change:** Changed `type="text" email="email"` to `type="email" name="email"`.

**Why:** The `email` attribute doesn't exist in HTML. The correct approach is `type="email"` for browser validation and `name="email"` for form data submission.

### 4. Nested `<p>` tags in footer fixed

**File modified:** [base.njk](../_includes/layouts/base.njk)

**Change:** Separated the nested paragraph into two sibling `<p>` elements:

```html
<p><em>Built with ...</em></p>
<p>&copy; 2025 Emily Lubonty</p>
```

**Why:** The HTML specification prohibits nesting `<p>` elements inside other `<p>` elements. Browsers auto-close the outer `<p>` when they encounter an inner one, creating malformed markup.

### 5. Netlify form name attribute added

**File modified:** [about.md](../content/about.md)

**Change:** Added `name="contact"` and changed `netlify="true"` to `data-netlify="true"`.

**Why:** Netlify Forms require a `name` attribute to identify submissions in the dashboard. The `data-` prefix ensures valid HTML5 and proper Netlify detection.

### 6. RSS feed metadata updated

**File modified:** [eleventy.config.js](../eleventy.config.js)

**Change:** Updated placeholder values to actual site information:

- Title: "House M.D. Memes"
- Subtitle: "A blog dedicated to AI generated memes based on the TV show House M.D."
- Base URL: "https://housemdmemes.com/"
- Author: "Emily Lubonty"

**Why:** The RSS feed was using default template values ("Blog Title", "example.com", "Your Name"), which would confuse RSS readers and look unprofessional.

### 7. Invalid CSS pseudo-class syntax fixed

**File modified:** [index.css](../css/index.css)

**Change:** Changed `.home-link:link(:visited)` to `.home-link:visited`.

**Why:** `:link(:visited)` is invalid CSS syntax—pseudo-classes cannot be nested this way. The rule was being ignored by browsers entirely.

### 8. Image filename case corrected

**File modified:** [squeakypost.md](../content/blog/squeaky/squeakypost.md)

**Change:** Changed `./gemini_mouse_bites.png` to `./Gemini_Mouse_Bites.png`.

**Why:** The actual filename uses capital letters. Case-sensitive file systems (Linux servers, some macOS) would return a 404 error for the lowercase reference.

### 9. Typo in description fixed

**File modified:** [liver.md](../content/blog/liver/liver.md)

**Change:** Corrected "patiet" to "patient" in the front matter description.

**Why:** Typos in metadata appear in search results, RSS feeds, and social media previews, affecting site professionalism.

### 10. Mismatched label `for` attribute fixed

**File modified:** [about.md](../content/about.md)

**Change:** Changed `for="email"` to `for="comment-email"` to match the input's `id`.

**Why:** The `for` attribute must match the associated input's `id` for accessibility. Screen readers use this association to announce labels when users focus on form fields.

### 11. Empty line before doctype removed

**File modified:** [base.njk](../_includes/layouts/base.njk)

**Change:** Removed the blank line before `<!doctype html>`.

**Why:** While browsers handle this gracefully, the doctype declaration should be the first content in an HTML document. Some older parsers may misinterpret content before the doctype.

### 12. Form indentation normalized

**File modified:** [about.md](../content/about.md)

**Change:** Standardized all form elements to use consistent 2-space indentation.

**Why:** Mixed tabs and spaces make code harder to read and maintain. Consistent indentation improves readability for future edits.

## Verification

To verify the fixes:

```bash
npm start
```

Then check:

- Homepage loads with featured post displayed
- All blog post images load correctly
- About page form displays properly
- RSS feed at `/feed/feed.xml` shows correct metadata
- Footer displays copyright symbol correctly
