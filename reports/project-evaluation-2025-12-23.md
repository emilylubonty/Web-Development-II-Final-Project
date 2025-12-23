# Project evaluation report: House M.D. Meme Collection

**Generated:** December 23, 2025 at 3:03 PM ET

## Summary

This report identifies issues found in the project beyond the three previously noted problems (tag format, unclosed `<p>` tags, email input attributes). Issues are categorized by severity and include suggested fixes.

## Previously identified issues (confirmed)

### 1. Tag format uses single strings instead of arrays

**Location:** All blog post front matter
**Files affected:** [chicken.md](content/blog/chicken/chicken.md), [liver.md](content/blog/liver/liver.md), [globalmouse.md](content/blog/globalmouse/globalmouse.md), [squeakypost.md](content/blog/squeaky/squeakypost.md), [bromantic.md](content/blog/bromance/bromantic.md)

**Current:**

```yaml
tags: chaos
```

**Suggested fix:**

```yaml
tags:
  - chaos
```

### 2. Broken HTML: unclosed `<p>` tags in about.md

**Location:** [about.md:10-16](content/about.md#L10-L16)

**Current:**

```html
<div class="about-me">
 <p>
 Hi!
 <p>
 I'm Emily, a computer programming student at Raritan Valley Community College.
 <p>
 This website's purpose was to experiment with image generation using Google Gemini.
 It also serves as a personal fan site for one of my favorite shows, House M.D.
</div>
```

**Suggested fix:**

```html
<div class="about-me">
 <p>Hi!</p>
 <p>I'm Emily, a computer programming student at Raritan Valley Community College.</p>
 <p>This website's purpose was to experiment with image generation using Google Gemini.
 It also serves as a personal fan site for one of my favorite shows, House M.D.</p>
</div>
```

### 3. Form errors: email input uses wrong attributes

**Location:** [about.md:26](content/about.md#L26)

**Current:**

```html
<input type="text" id="comment-email" email="email" placeholder="Your email">
```

**Suggested fix:**

```html
<input type="email" id="comment-email" name="email" placeholder="Your email">
```

## Additional issues found

### High priority

#### 4. Nested `<p>` tag inside `<p>` in footer (invalid HTML)

**Location:** [base.njk:64-68](_includes/layouts/base.njk#L64-L68)

**Current:**

```html
<footer>
 <p>
  <em>Built with <a href="https://www.11ty.dev/">{{ eleventy.generator }}</a></em>
  <p> 2025 Emily Lubonty </p>
 </p>
</footer>
```

**Issue:** A `<p>` element cannot contain another `<p>` element. This is invalid HTML and browsers will auto-close the first `<p>` unexpectedly.

**Suggested fix:**

```html
<footer>
 <p><em>Built with <a href="https://www.11ty.dev/">{{ eleventy.generator }}</a></em></p>
 <p>&copy; 2025 Emily Lubonty</p>
</footer>
```

#### 5. Missing `name` attribute on form - Netlify forms require it

**Location:** [about.md:21](content/about.md#L21)

**Current:**

```html
<form class="comment-box" method="POST" netlify="true">
```

**Issue:** Netlify forms require a `name` attribute to identify the form in the Netlify dashboard. The attribute should also be `data-netlify="true"` (with `data-` prefix) for proper HTML5 validity.

**Suggested fix:**

```html
<form class="comment-box" name="contact" method="POST" data-netlify="true">
```

#### 6. RSS feed metadata not updated from template defaults

**Location:** [eleventy.config.js:80-88](eleventy.config.js#L80-L88)

**Current:**

```javascript
metadata: {
 language: "en",
 title: "Blog Title",
 subtitle: "This is a longer description about your blog.",
 base: "https://example.com/",
 author: {
  name: "Your Name"
 }
}
```

**Issue:** The feed plugin still uses placeholder values from the starter template instead of the actual site metadata.

**Suggested fix:**

```javascript
metadata: {
 language: "en",
 title: "House M.D. Memes",
 subtitle: "A blog dedicated to AI generated memes based on the TV show House M.D.",
 base: "https://housemdmemes.com/",
 author: {
  name: "Emily Lubonty"
 }
}
```

### Medium priority

#### 7. Invalid CSS pseudo-class syntax

**Location:** [index.css:271-273](css/index.css#L271-L273)

**Current:**

```css
.home-link:link(:visited) {
 color: var(--text-color-link);
}
```

**Issue:** `:link(:visited)` is invalid CSS syntax. These are separate pseudo-classes that cannot be nested this way.

**Suggested fix:**

```css
.home-link:visited {
 color: var(--text-color-link);
}
```

#### 8. Image filename case mismatch

**Location:** [squeakypost.md:8](content/blog/squeaky/squeakypost.md#L8)

**Current:**

```html
<img src="./gemini_mouse_bites.png" alt="...">
```

**Actual filename:** `Gemini_Mouse_Bites.png` (capital G and M)

**Issue:** Case-sensitive file systems (Linux servers, some macOS configurations) will return a 404 for this image. It may work locally but fail in production.

**Suggested fix:**

```html
<img src="./Gemini_Mouse_Bites.png" alt="...">
```

#### 9. Typo in description

**Location:** [liver.md:4](content/blog/liver/liver.md#L4)

**Current:**

```yaml
description: This post involves House diagnosing a patiet
```

**Suggested fix:**

```yaml
description: This post involves House diagnosing a patient
```

#### 10. Mismatched label `for` attribute

**Location:** [about.md:25-26](content/about.md#L25-L26)

**Current:**

```html
<label for="email">Email</label>
<input type="text" id="comment-email" ...>
```

**Issue:** The `for="email"` doesn't match the input's `id="comment-email"`, breaking the label-input association for accessibility.

**Suggested fix:**

```html
<label for="comment-email">Email</label>
<input type="email" id="comment-email" name="email" placeholder="Your email">
```

### Low priority

#### 11. Empty line at start of base.njk

**Location:** [base.njk:1](_includes/layouts/base.njk#L1)

**Issue:** There's a blank line before the `<!doctype html>` declaration. While browsers handle this gracefully, it's not best practice.

**Suggested fix:** Remove the empty first line so `<!doctype html>` is on line 1.

#### 12. Inconsistent indentation in about.md form

**Location:** [about.md:21-32](content/about.md#L21-L32)

**Issue:** Mixed use of tabs and spaces within the form markup makes the code harder to read and maintain.

**Suggested fix:** Use consistent 2-space indentation throughout the form.

#### 13. Future date on blog post

**Location:** [squeakypost.md:5](content/blog/squeaky/squeakypost.md#L5)

**Current:**

```yaml
date: 2025-12-17
```

**Issue:** This date is in the past now, but depending on when the site was built, this post may have been dated in the future. Not necessarily an error, but worth noting for chronological accuracy.

## Strengths observed

- Well-organized directory structure following Eleventy conventions
- Effective use of glassmorphism CSS with modern `color-mix()` function
- Thoughtful colorblind-safe color palette
- Good accessibility features (skip link, visually-hidden class, semantic HTML)
- Proper use of variable fonts with `font-display: swap`
- Dark mode support via `prefers-color-scheme`
- Co-located images with blog posts (good content organization)
- Featured post functionality implemented correctly

## Areas for improvement

- Form validation and accessibility (missing `required` attributes, no error messaging)
- Consider adding `width` and `height` attributes to images to prevent layout shift
- The CSS input styling only targets `input[type="text"]` - should also style `input[type="email"]` once the type is fixed
