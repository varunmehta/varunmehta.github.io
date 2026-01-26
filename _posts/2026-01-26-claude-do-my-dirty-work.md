---
title: "Making Claude do my dirty work"
layout: post
date: 2026-01-26
image: https://upload.wikimedia.org/wikipedia/commons/b/b0/Claude_AI_symbol.svg
headerImage: true
tag:
- robotics
- FLL
- lego
- technical
- jekyll
star: false
hidden: false
category: blog
author: varunmehta
description: Extract the SVG from llsp3, and embed in README file.
---

**Demo: [https://braineatingmachines.com/pitcrew/](https://braineatingmachines.com/pitcrew/)**

**Repo: [https://github.com/braineatingmachines/pitcrew/](https://github.com/braineatingmachines/pitcrew/)**

Since working with my [FLL team](/lego-robotics/), I've been looking at growth gaps between FLL and FTC, to better equip students to a higher level team. Correspondence with teachers points towards students not being able to articulate their designs and models for 3D modelling and printing or just create a new CNC part. While browsing through multiple websites and forum/Facebook posts around FTC and FRC, I realized a lot of teams build their websites using WordPress. WordPress is a great CMS tool with good plugins and templates. It is a good tool to build your web presence if you are a business. For a cash-strapped robotics team, it is an additional line item on your monthly expense sheet.

As a team that writes code and hosts it on GitHub, [GitHub Pages](https://pages.github.com) is the perfect place to host your team’s website, directly from a repository on GitHub. I decided to leverage Claude Code, and build a template in Jekyll + GitHub Pages.

I asked ChatGPT and Claude to review some of the existing team websites, and come back with a list of features that should be available on such a template. After a series of back and forth I combined all the notes and created a master prompt for Claude Code to build the template. 

> ## AGENT PROMPT: FTC/FRC Robotics Portfolio Website Template
> 
> ### Role
> 
> You are an autonomous senior full-stack engineer and technical writer tasked with building a **production-ready, reusable website template** for **FIRST FTC/FRC robotics teams**.
> 
> The output must be a **Jekyll-based static site** hosted on **GitHub Pages**, designed for **students and mentors with little to no coding experience**.
> 
> Your goal is to produce a repository that teams can fork and immediately use.
> 
> ### High-Level Goals
> 
> 1. Markdown-first editing (no HTML required for content authors)
> 2. Season-aware structure (FTC/FRC school-year seasons like `2025–2026`)
> 3. Configuration-driven behavior via `_config.yml`
> 4. Automated workflows using GitHub Actions
> 5. Clean, modern, responsive UI using Tailwind CSS
> 6. Long-term maintainability across many seasons
> 7. Accessibility-first, toggleable accessibility mode
> 
> ### Core Constraints (Non-Negotiable)
> 
> * **All content pages must be Markdown**
> * Contributors should only need:
>   * A text editor
>   * Basic Markdown knowledge
> * Feature toggles must live in `_config.yml`
> * No manual copy/paste when seasons change
> * No local Python execution required
> * GitHub Pages compatibility
> 
> ### Technology Stack
> 
> * Static Site Generator: **Jekyll**
> * Hosting: **GitHub Pages**
> * Styling: **Tailwind CSS**
> * Data files: YAML (`_data/`)
> * Automation: **GitHub Actions**
> * JS: Minimal, progressive enhancement only
> 
> ### Repository Structure (Target)
> 
> ```
> /
> ├── _config.yml
> ├── _layouts/
> ├── _includes/
> ├── _data/
> │   ├── team.yml
> │   ├── mentors.yml
> │   ├── alumni.yml
> │   ├── events.yml
> │   └── socials.yml
> ├── _posts/                 # Blog / News
> ├── docs/                   # ReadTheDocs-style documentation
> ├── seasons/
> │   ├── 2025-2026/
> │   │   ├── robot.md
> │   │   ├── team.yml
> │   │   ├── outreach.md
> │   │   ├── gallery.md
> │   │   ├── code.md
> │   │   ├── cad.md
> │   │   └── docs/
> │   └── 2024-2025/
> ├── assets/
> │   ├── images/
> │   ├── models/
> │   └── css/
> ├── .github/workflows/
> └── README.md
> ```
> 
> ### Configuration System (`_config.yml`)
> 
> All major behavior must be configurable here.
> 
> #### Required Sections
> 
> ```yaml
> site:
>   team_name:
>   team_number:
>   program: FTC | FRC
>   current_season: 2025-2026
> 
> theme:
>   colors:
>     primary:
>     secondary:
>     accent:
>   dark_mode: true # Adopt system settings, and can also be toggled on the UI too
> 
> features:
>   blog: true
>   docs: true
>   cad_viewer: true
>   circuit_viewer: true
>   code_links: true
>   data_visualizations: true
>   alumni_auto_archive: true
>   accessibility_toggle: true
> 
> socials:
>   instagram:
>   github:
>   youtube:
>   donorschoose:
>   other:
> ```
> 
> ### Navigation
> 
> * Top navigation bar
> * Left: team logo
> * Right: navigation links
> * Mobile-responsive hamburger menu
> * Navigation items configurable via `_config.yml`
> 
> ### Home Page
> 
> The home page is a **composite of reusable sections**, each backed by Markdown.
> 
> #### Required Sections
> 
> 1. **Hero / Current Season Overview**
>     * Game name
>     * Robot name
>     * Season year
>     * Image or video
> 
> 2. **Join the Team**
>     * Short paragraph
>     * CTA button
>     * External form link
> 
> 3. **Calendar of Events**
>     * Past and upcoming events
>     * Powered by YAML data
> 
> 4. **Scrimmage Hosting**
>     * Conditionally visible
>     * Event details + registration link
> 
> 5. **Featured Content**
>     * Awards, outreach, or blog highlight
> 
> ### Pages to Implement
> 
> * About
>   * Team history
>   * Timeline
>   * Mentors
> 
> * Sponsorship
>   * Sponsor tiers
>   * Logos
>   * Call-to-action
> 
> * Awards
>   * Season-filtered
>   * FTC/FRC standard awards
> 
> * Contact
>   * Contact links or form
> 
> * Team Handbook
>   * Markdown-based
>   * Printable layout
> 
> * News / Blog
>   * Markdown posts
>   * Tags & categories
> 
> * Archive
>   * Auto-generated by season
> 
> * Alumni
>   * Powered by `_data/team.yml`
>   * Auto-move students to alumni based on graduation year
> 
> ### Season-Aware Content System (Critical)
> 
> FTC/FRC seasons run **Aug–Jun** and must be treated as first-class entities.
> 
> #### Requirements
> 
> * All robot, outreach, team, and documentation content lives under `/seasons/{season}/`
> * Changing seasons requires **only** updating `current_season` in `_config.yml`
> * Older seasons automatically appear under Archive
> * No manual file movement
> 
> ### Media & Visualization Features
> 
> #### Required
> 
> * Image galleries
> * YouTube embeds
> * GitHub repo links
> * CAD viewer (glTF / STL preferred)
> * Circuit schematic display (SVG or PDF)
> 
> #### Optional Enhancements
> 
> * Match statistics
> * Outreach metrics
> * Award timelines
> 
> ### Documentation Section (Docs)
> 
> * Styled like **ReadTheDocs v2** ~ check exisiting Jekyll templates and see if you can borrow from there 
> * Sidebar navigation
> * Markdown-only
> * Teaching-focused templates
> * Per-season documentation support
> 
> ### MESGRO Integration
> 
> * Port MESGRO converters from:
>   [https://github.com/aojedao/MESGRO](https://github.com/aojedao/MESGRO)
> * Run converters via **GitHub Actions**
> * No local Python execution
> * Document usage clearly
> 
> ### Accessibility (Optional)
> 
> Implement an **Accessibility Mode Toggle Button**:
> 
> #### Requirements
> 
> * Visible toggle button in header or footer
> * When enabled:
> 
>   * Switch to high-contrast color palette
>   * Increase base font size
>   * Improve focus outlines
>   * Disable motion/animations
> * Accessibility styles must be implemented via **CSS class switch**
> * Colors must still derive from `_config.yml`
> 
> ### Footer
> 
> * Social media icons
> * Fundraising links
> * Config-driven visibility
> * FTC/FRC-appropriate disclaimers
> 
> ### Automation (GitHub Actions)
> 
> Implement workflows for:
> 
> 1. Build & deploy to GitHub Pages
> 2. Alumni auto-archival (graduation-year based, cron job runs on July 1st)
> 3. Season rollover checks
> 4. MESGRO content processing
> 
> ### Bonus Features (Strongly Encouraged)
> 
> * “Judge Mode” page highlighting:
>   * Robot
>   * Awards
>   * Outreach
>   * Engineering docs
> * Outreach impact metrics page
> * Client-side search (blog + docs)
> * Season comparison pages
> * Accessibility compliance checks
> 
> ### Definition of Done
> 
> The project is complete when:
> 
> * A team can fork the repo
> * Change `_config.yml`
> * Add Markdown files
> * Push to GitHub
> * And immediately have a polished, accessible FTC/FRC website
> 
> No web development knowledge required.
> 
> **Begin by scaffolding the repository, configuration system, layouts, and automation.**