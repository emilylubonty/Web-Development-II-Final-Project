# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

House M.D. Meme Collection - An Eleventy v3 static site showcasing AI-generated memes from the TV show House M.D. Built from the `eleventy-base-blog` starter template with custom theming and features.

## Commands

```bash
npm install          # Install dependencies
npm start            # Dev server with live reload (localhost:8080)
npm run build        # Production build to _site/
npm run debug        # Build with Eleventy debug output
npm run debugstart   # Dev server with debug output
```

## Architecture

### Directory structure

- `content/` - Source content (input directory)
  - `blog/` - Blog posts organized in subdirectories with co-located images
  - `index.njk` - Homepage with featured post logic
  - `about.md` - About page with Netlify contact form
- `_includes/layouts/` - Nunjucks layout templates (base, home, post)
- `_data/` - Global data files (metadata.js, eleventyDataSchema.js)
- `_config/filters.js` - Custom Luxon date filters and collection helpers
- `css/` - Stylesheets (passthrough copied)
- `fonts/` - Cabin variable font (passthrough copied)
- `public/` - Static assets copied to root of output
- `_site/` - Build output (gitignored)

### Content patterns

Blog posts use directory data file inheritance:
- `content/blog/blog.11tydata.js` applies `tags: ["posts"]` and `layout: layouts/post.njk` to all posts
- Posts can add `featured: true` in front matter to appear in homepage featured section
- Images are co-located with posts (e.g., `content/blog/chicken/Gemini_House_Chicken.png`)

### Key customizations from base template

- **Featured post system**: Homepage loops through `collections.posts` looking for `featured: true`
- **Glassmorphism CSS**: `.glass-container` class with backdrop-filter blur and color-mix()
- **House M.D. theme**: Clinical blue palette in CSS custom properties, colorblind-safe colors
- **Variable font**: Cabin with width and weight axes (`font-weight: 100-900`, `font-stretch: 75%-100%`)
- **Contact form**: Netlify form on about page with `.suggestion-box` and `.comment-box` styling

### Configuration notes

- ESM config file (`eleventy.config.js`)
- Input directory is `content/`, includes are at `../_includes`, data at `../_data`
- Draft posts filtered in production via preprocessor (checks `ELEVENTY_RUN_MODE`)
- Image optimization plugin outputs avif, webp, and original formats
- CSS/JS bundling via `eleventy-plugin-bundle` with inlined output

## Deployment

Configured for both Netlify (`netlify.toml`) and Vercel (`vercel.json`). Form submissions require Netlify deployment.
