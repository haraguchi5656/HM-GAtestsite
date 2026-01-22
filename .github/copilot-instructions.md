# HM-GAtestsite Copilot Instructions

## Project Overview
A static HTML test site (GTM GA4 Test) hosted on GitHub Pages. Purpose: validate Google Tag Manager (GTM) and Google Analytics 4 (GA4) tracking implementation. The site features Western calendar (西暦) and Japanese calendar (和暦) conversion tables targeting Japanese users.

## Architecture & Structure

### Page Structure
- **index.html**: Main landing page with calendar conversion tables
- **pages/content.html**: Historical content about Japanese calendar
- **pages/sitemap.html**: Site navigation map
- **pages/privacy-policy.html**: Privacy disclosure
- **pages/site-policy.html**: Site terms
- **pages/accessibility-policy.html**: Accessibility standards
- **assets/style.css**: Centralized stylesheet (all pages reference)

### Repeated Patterns
Each HTML page follows **identical structure**:
1. Consistent `<head>` meta tags (charset, viewport, OG tags)
2. Link to external stylesheet: `<link rel="stylesheet" href="...assets/style.css">`
3. GTM container script ID: `GTM-TXDWCBH2` (inline in every page)
4. Japanese language (`lang="ja"`) throughout
5. OGPimage.png referenced in all OG meta tags

## Key Implementation Details

### Google Tag Manager Integration
- **GTM Container ID**: `GTM-TXDWCBH2`
- **Placement**: Inline GTM script in every page's `<head>` section (lines 20-24 in each file)
- **Data Layer**: Uses standard `dataLayer` variable with `gtm.start` event
- **Design Pattern**: Duplicate GTM code across pages (not externalized) - maintain this pattern for consistency

### Styling Approach
- **External CSS file**: `assets/style.css` - ALL pages reference this single file
- **No page-level `<style>` tags**: CSS is centralized for maintainability
- **CSS Framework**: Vanilla CSS with mobile-first responsive design
- **Color Scheme**:
  - Primary: #2c3e50 (dark slate - headers)
  - Secondary: #34495e (slightly lighter slate)
  - Neutral: #bdc3c7 (light gray - borders)
  - Background: #f5f5f5 (off-white)

### Shared Layout Classes
```css
.container { max-width: 900px; /* centered layout */ }
.section { margin-bottom: 25-40px; /* consistent spacing */ }
h2 { border-bottom: 2px solid #bdc3c7; /* divider pattern */ }
table { width: 100%; border-collapse: collapse; /* data tables */ }
.nav-button { /* consistent call-to-action buttons */ }
```

### Mobile-First Responsive Design
- **Default (Mobile)**: 320px viewport
- **Tablet breakpoint**: `@media (min-width: 768px)`
- **Desktop breakpoint**: `@media (min-width: 1200px)`
- All responsive rules defined in `assets/style.css`

## Development Conventions

### Content Updates
1. **Maintain parallel structure**: Always update all pages that share meta descriptions
2. **Meta description**: Identical across all pages ("西暦・和暦の対照表。過去30年分を掲載。GTM・GA4の動作検証用テストサイト")
3. **Keep OG tags synchronized**: og:url must match actual page URL; og:title/description per page
4. **HTML Validation**: Ensure meta tags and structure mirror existing pages exactly
5. **CSS Updates**: Edit `assets/style.css` only - never add `<style>` tags to individual pages

### No Build Process
- Static HTML delivered as-is
- No build tools, npm scripts, or preprocessing required
- Direct file editing → Git commit → GitHub Pages automatic deployment

### File Organization
```
HM-GAtestsite/
├── index.html                              (← root landing page)
├── pages/                                  (← policy & content pages)
│   ├── content.html
│   ├── sitemap.html
│   ├── privacy-policy.html
│   ├── site-policy.html
│   └── accessibility-policy.html
├── assets/
│   └── style.css                          (← centralized stylesheet)
├── .github/
│   └── copilot-instructions.md            (← this file)
├── .gitignore
└── README.md                              (← optional project documentation)
```

### Path References
- **From index.html (root)**: `<a href="pages/content.html">`
- **From pages/* (subfolder)**: 
  - To index.html: `<a href="../index.html">`
  - To other pages: `<a href="sitemap.html">` (same folder)
  - To CSS: `<link rel="stylesheet" href="../assets/style.css">`

### Testing/Validation
- **GTM Validation**: Use Google Tag Manager Preview/Debug mode with container ID GTM-TXDWCBH2
- **GA4 Events**: Verify dataLayer events fire on page load (`event: 'gtm.js'`)
- **Cross-page consistency**: Check that all 6 pages reference stylesheet correctly
- **Responsive testing**: Verify at 320px, 768px, 1200px viewport widths
- **Accessibility**: Review semantic HTML (`lang="ja"`, proper heading hierarchy)
- **Link validation**: Ensure all relative paths are correct (especially pages/.. references)

## Common Tasks

### Adding a New Page
1. Create new file in `pages/` folder (e.g., `pages/new-page.html`)
2. Copy HTML structure from existing page (e.g., `pages/content.html`)
3. Update `<title>`, meta description, og:title, og:url
4. **Ensure external CSS link**: `<link rel="stylesheet" href="../assets/style.css">`
5. Keep GTM script ID and dataLayer intact
6. Add link to `pages/sitemap.html` for navigation
7. **Do NOT include `<style>` tag** - all CSS is in assets/style.css

### Updating Shared Meta Description
- **Search string**: "西暦・和暦の対照表。過去30年分を掲載。GTM・GA4の動作検証用テストサイト"
- **Files affected**: All 6 HTML pages (index.html + pages/*.html)
- **Use multi-replace** to update all instances simultaneously

### Modifying CSS
- **Always edit**: `assets/style.css` only
- Verify color values match (#2c3e50, #34495e, #bdc3c7, #f5f5f5)
- Test responsive design at viewport widths: 320px, 768px, 1200px
- Changes automatically apply to all pages

### Updating Links After Folder Reorganization
- **Root page (index.html)**: `pages/` + filename
  - Example: `<a href="pages/content.html">`
- **Pages folder (pages/*.html)**: `../` + filename or relative
  - Example: `<a href="../index.html">` or `<a href="content.html">`

### Adding Page-Specific Styles (if needed)
If page-specific styles are required, create a `<style>` tag in that page's `<head>` AFTER the CSS link:
```html
<link rel="stylesheet" href="../assets/style.css">
<style>
  /* page-specific overrides only */
</style>
```

## Key Files Reference
- [index.html](../index.html) - Primary landing/reference for structure
- [pages/sitemap.html](../pages/sitemap.html) - Navigation hub; update when adding pages
- [pages/content.html](../pages/content.html) - Content page example
- [assets/style.css](../assets/style.css) - **Centralized stylesheet for all pages**
- [.github/copilot-instructions.md](.github/copilot-instructions.md) - This file
