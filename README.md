# House M.D. Meme Collection

A web project showcasing AI-generated memes based on the TV show House M.D., created using Google Gemini.

## About

This website shares a curated collection of AI-generated memes inspired by the medical drama House M.D. Each meme has been ranked based on humor and relevance to the show.

## Project Structure

- **`content/`** - Main content files and blog posts
  - `blog/` - Individual blog post entries
  - `index.njk` - Homepage template
  - `about.md` - About page
- **`_includes/`** - Reusable template components
  - `layouts/` - Page layout templates (base, home, post)
  - `postslist.njk` - Blog post list component
- **`_data/`** - Data files and configuration
- **`css/`** - Stylesheets
  - `index.css` - Main styles with Cabin font, House M.D. color scheme, and glassmorphism effects
  - `message-box.css` - Message box styling
  - `prism-diff.css` - Code syntax highlighting
- **`fonts/`** - Custom fonts (Cabin variable font with variable weights and stretches)
- **`public/`** - Static assets that are copied to output

## Tech Stack

- **Static Site Generator:** Eleventy (11ty)
- **Templating:** Nunjucks
- **Styling:** CSS with House M.D.-inspired color scheme and glassmorphism effects
- **Font:** Cabin variable font
- **Deployment:** Netlify & Vercel ready

## Getting Started

### Installation

```bash
npm install
```

### Development

```bash
npm start
```

This will start the Eleventy development server with live reload.

### Build

```bash
npm run build
```

Generates the static site in the output directory.

## Configuration

- `eleventy.config.js` - Main Eleventy configuration
- `netlify.toml` - Netlify deployment settings
- `vercel.json` - Vercel deployment settings

## Features

- **Responsive design** with mobile-first approach
- **Dark mode support** with House M.D.-inspired clinical blue theme
- **Colorblind-safe color palette** (blues, teals, warm accents)
- **Featured post** callout on the homepage
- **Contact box** with styled form inputs/textarea/button
- **Accessible navigation** with proper semantic HTML
- **Tag-based post organization** for easy browsing
- **Custom variable font** (served from `fonts/` via passthrough)
- **WCAG AA compliant** contrast ratios for accessibility

## Homepage sections

- Welcome glass panel with intro text
- Featured Post block (pulls the first `featured: true` post)
- Suggestion box form for visitor ideas

## License

See LICENSE file for details.
