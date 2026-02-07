# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is an independent educational website about portable generators built with Hugo static site generator. The site provides guides, calculators, and safety information about portable generators.

**Live Site:** https://portablegenguide.com/

## Common Commands

### Development
```bash
# Start dev server with hot reload (serves at http://localhost:1313)
hugo server -D

# Start dev server with navigation to changed files
hugo server --buildDrafts --navigateToChanged

# Initialize theme submodules (if needed)
git submodule update --init --recursive
```

### Building
```bash
# Production build to public/ directory
hugo

# Clean build (removes old files)
hugo --cleanDestinationDir
```

## Project Structure

```
portable-generator-site/
├── archetypes/          # Hugo default templates (default.md)
├── assets/              # Custom JavaScript (generator-size.js)
├── content/             # Site content in Markdown
│   ├── generator-sizes/ # Generator size category pages
│   ├── posts/          # Articles and guides
│   └── tools/          # Calculator/tool pages (generator-size.md)
├── data/
│   ├── appliances.yml          # Appliance wattage database
│   └── generator_size_profiles.yaml  # Generator size mappings & profiles
├── layouts/             # Override/custom templates
│   ├── partials/       # Reusable components + schema templates + tool templates
│   ├── tools/single.html  # Page layout for tools
│   └── shortcodes/     # Custom Hugo shortcodes
├── static/              # Static assets (favicons, ads.txt)
├── hugo.toml            # Hugo configuration
├── themes/              # PaperMod theme (git submodule)
└── public/              # Generated site (gitignored)
```

## Architecture

### Theme: PaperMod (Customized)

The site uses the PaperMod theme as a git submodule. Customizations are made through:
- `layouts/` - Override theme templates
- `layouts/partials/extend_head.html` - Add Tailwind CSS, KaTeX, AdSense, Clarity analytics, schema markup
- `layouts/partials/extend_footer.html` - Custom footer scripts

### Generator Size Calculator

The calculator is a key feature that estimates generator power requirements:

**Data Flow:**
1. `data/appliances.yml` - Contains appliance categories, names, running_watts, and starting_watts
2. `data/generator_size_profiles.yaml` - Maps calculated wattage to generator size profiles (ultraLight, basic, popular, power, wholeHome)
3. `layouts/partials/tools/generator-size-calculator.html` - The calculator UI template with embedded JavaScript
4. `content/tools/generator-size.md` - Page that renders the calculator

**Calculator Logic:**
- Total Running Load = sum of all selected appliances' running_watts
- Peak Surge = Total Running + max(starting_increment for all appliances)
- Recommended Size = Peak Surge × 1.2 (20% safety margin)

**Calculator Modes:**
- `simple` - Shows only common appliances, links to full calculator
- `full` - Shows all appliances, custom appliance input, detailed recommendations

### Schema Markup (JSON-LD)

Structured data for SEO is managed through:
- `layouts/partials/schema/` - Individual schema templates
- Page frontmatter `custom.schema` array specifies which schemas to include
- `extend_head.html` dynamically loads schemas based on page config

### Tailwind CSS Integration

Tailwind is conditionally loaded via `layouts/partials/extend_head.html`:
- Only loads when page has `custom.use_tailwindcss: true` in frontmatter
- Includes dark mode support (`media` based on system preference)
- Custom CSS fixes list styling that Tailwind resets

### Content Structure

**Posts:** Individual articles in `content/posts/` with frontmatter including title, date, description, tags.

**Generator Sizes:** Category pages in `content/generator-sizes/` for different wattage ranges.

**Tools:** Interactive calculator pages in `content/tools/`.

## Key Configuration Files

### hugo.toml
- baseURL, title, theme settings
- Google Analytics ID
- Menu structure (Calculator, Guides, Use Cases, Safety, About)
- Output formats: home includes JSON for search functionality

### data/appliances.yml
- Appliance wattage data structure:
  ```yaml
  - category: 'Category Name'
    common: true  # Whether to show in simple mode
    items:
      - name: 'Appliance Name'
        running_watts: 100
        starting_watts: 200
        common: true  # Individual item visibility
  ```

### data/generator_size_profiles.yaml
- Profiles contain min/max wattage ranges, recommendations, suitableFor, notSuitableFor, proTip
- Dynamically sorted by `min` value in template (no hardcoded order)

## Custom Shortcodes

- `{{< recent-posts >}}` - Displays recent articles
- `{{< generator-wattage-calculator >}}` - Embeds wattage calculator
- `{{< generator-runtime-calculator >}}` - Embeds runtime calculator
- `{{< watt-converter >}}` - Watt conversion tool

## Content Frontmatter Patterns

```yaml
---
title: "Page Title"
description: "Page description"
date: 2025-01-01
draft: false
tags: ['tag1', 'tag2']
custom:
    use_tailwindcss: true
    schema:
        - schema-website
---
```

## Analytics Integration

- Google Analytics: G-7XRR67NZEE
- Microsoft Clarity: urvo8kt7wv
- Google AdSense: ca-pub-9852687911329503

All configured in `layouts/partials/extend_head.html`.

## JavaScript Notes

- Vanilla ES6+, no frameworks
- Calculator JavaScript is embedded in `layouts/partials/tools/generator-size-calculator.html`
- Uses `data-*` attributes for DOM interaction (e.g., `data-run`, `data-start`)
- XSS prevention: `escapeHtml()` function for user input
- Hugo data accessed via `{{ .Site.Data.generator_size_profiles | jsonify | safeJS }}`

## Math Rendering

KaTeX is conditionally loaded for pages with `custom.math: true` in frontmatter.