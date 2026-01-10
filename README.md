# Portable Generator Guide

An independent educational website providing clear, practical guides on portable generators, generator sizing, safety, and real-world use cases.

**Live Site:** <https://portablegenguide.com/>

## Features

### Generator Size Calculator

- Interactive wattage calculator that estimates required generator size based on real appliances
- Accounts for running watts and startup surge requirements
- Includes custom appliance input for advanced users
- Provides buying recommendations based on calculated power needs

### Educational Content

- Comprehensive guides covering generator fundamentals, safety, and use cases
- Articles covering portable vs standby generators, inverter vs conventional types, and fuel options
- Safety checklists and carbon monoxide awareness

### Search & Navigation

- Full-text search functionality
- Organized content sections: Guides, Use Cases, Safety, Tools
- Breadcrumb navigation and table of contents

## Tech Stack

- **Static Site Generator:** Hugo (v0.130+)
- **Theme:** PaperMod (customized)
- **Styling:** Tailwind CSS
- **JavaScript:** Vanilla ES6+ (no frameworks)
- **Schema Markup:** JSON-LD structured data
- **Analytics:** Google Analytics

## Project Structure

```
.
├── archetypes/          # Hugo content templates
├── assets/js/           # JavaScript files
├── content/             # Site content (Markdown)
│   ├── generator-sizes/ # Generator size guides
│   ├── posts/           # Articles and guides
│   └── tools/           # Calculator and tool pages
├── data/                # YAML data files
│   ├── appliances.yml   # Appliance wattage data
│   └── generator_size_profiles.yaml  # Generator size profiles
├── layouts/             # Hugo templates
│   ├── partials/        # Reusable template components
│   └── shortcodes/      # Custom shortcodes
└── static/              # Static assets (favicons, ads.txt)
```

## Published Articles

| Title | Link | Published |
|-------|-------|----------|
| Gas vs Dual Fuel Generators: Which Is Better for Your Use Case? | [gas-vs-dual-fuel-generators](/posts/gas-vs-dual-fuel-generators/) | 2026-01-06 |
| Portable Generator for RV Use: Power Requirements Explained | [portable-generator-for-rv](/posts/portable-generator-for-rv/) | 2026-01-05 |
| Portable Generator for Camping: What Size and Noise Level Do You Really Need? | [portable-generator-for-camping](/posts/portable-generator-for-camping/) | 2026-01-05 |
| Portable Generator Noise Levels Explained: How Loud Is Too Loud? | [portable-generator-noise-levels](/posts/portable-generator-noise-levels/) | 2026-01-05 |
| Best Generator for Refrigerator: How to Choose the Right Backup Power | [best-generator-for-refrigerator](/posts/best-generator-for-refrigerator/) | 2026-01-01 |
| Can a Generator Damage Electronics? What You Need to Know | [can-a-generator-damage-electronics](/posts/can-a-generator-damage-electronics/) | 2025-12-31 |
| Can You Use a Generator Indoors? Why It's Dangerous and What to Do Instead | [can-you-use-a-generator-indoors](/posts/can-you-use-a-generator-indoors/) | 2025-12-31 |
| Portable vs Standby Generator: Which Is Right for You? | [portable-vs-standby-generator](/posts/portable-vs-standby-generator/) | 2025-12-23 |
| Best Portable Generator for Home Backup: How to Choose the Right One | [best-portable-generator-for-home-backup](/posts/best-portable-generator-for-home-backup/) | 2025-12-23 |
| Best Generator for Apartment Power Outage: What Works and What to Avoid | [best-generator-for-apartment-power-outage](/posts/best-generator-for-apartment-power-outage/) | 2025-12-24 |
| Can You Use a Generator in the Rain? | [can-you-use-a-generator-in-the-rain](/posts/can-you-use-a-generator-in-the-rain/) | 2025-12-24 |
| How Long Can a Portable Generator Run Continuously? | [how-long-can-a-portable-generator-run-continuously](/posts/how-long-can-a-portable-generator-run-continuously/) | 2025-12-25 |
| Portable Generator Safety Checklist | [portable-generator-safety-checklist](/posts/portable-generator-safety-checklist/) | 2025-12-22 |
| Inverter vs Conventional Generator: What's the Difference? | [inverter-vs-conventional-generator](/posts/inverter-vs-conventional-generator/) | 2025-12-22 |
| Generator Carbon Monoxide Risks: Why It's Dangerous and How to Stay Safe | [generator-carbon-monoxide-risks](/posts/generator-carbon-monoxide-risks/) | 2025-12-28 |
| How Many Watts Do I Need for a Portable Generator? | [how-many-watts-do-i-need-for-a-portable-generator](/posts/how-many-watts-do-i-need-for-a-portable-generator/) | 2025-12-26 |
| What Can a Portable Generator Power? | [what-can-a-portable-generator-power](/posts/what-can-a-portable-generator-power/) | 2025-12-21 |
| How Does a Portable Generator Work? | [how-does-a-portable-generator-work](/posts/how-does-a-portable-generator-work/) | 2025-12-21 |
| What Is a Portable Generator? | [what-is-a-portable-generator](/posts/what-is-a-portable-generator/) | 2025-12-20 |


## Getting Started

### Prerequisites

- Hugo Extended (v0.130 or later)
- Node.js (for Tailwind CSS, if needed)
- Git

### Installation

1. Clone the repository:

```bash
git clone https://github.com/canhetingsky/portable-generator-site.git
cd portable-generator-site
```

1. Install the PaperMod theme (submodule):

```bash
git submodule update --init --recursive
```

### Development

Start the development server with hot reload:

```bash
hugo server -D
```

Start with navigation to changed files:

```bash
hugo server --buildDrafts --navigateToChanged
```

The site will be available at `http://localhost:1313`

### Building for Production

Build the static site to `public/` directory:

```bash
hugo
```

## Code Style Guidelines

### Hugo Templates

- Use Hugo template syntax: `{{ variable }}` and `{{ function }}`
- 4-space indentation for HTML/Templates
- Comments: Use `{{/* comment */}}` format
- Partial calls: `{{ partial "path/to/partial.html" . }}`

### HTML/Structuring

- Semantic HTML5 elements
- Tailwind CSS utility classes
- Data attributes for JavaScript hooks: `data-name`, `data-value`
- Accessible markup with proper ARIA labels

### JavaScript

- Modern ES6+ syntax
- camelCase for variables/functions
- JSDoc comments for functions
- XSS prevention: `escapeHtml(text)` for user input

### YAML Data Files

- 2-space indentation
- snake_case for keys (e.g., `running_watts`, `starting_watts`)
- Group related data with categories

## Contributing

Contributions are welcome! Please ensure:

1. Code follows the established style guidelines
2. Run `hugo` to build the site locally before submitting
3. Test any calculator changes thoroughly
4. Update documentation for new features

## License

This project uses the PaperMod theme under its respective license. Content is original and independently created.

## Important Disclaimer

This site is for educational purposes only. Always follow manufacturer instructions and consult qualified professionals when working with generators. Improper use can cause serious injury or death.
