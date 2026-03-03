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
description: Using Claude Code to build a GitHub Pages template for FTC/FRC teams.
---

**Demo: [https://braineatingmachines.com/pitcrew/](https://braineatingmachines.com/pitcrew/)**

**Repo: [https://github.com/braineatingmachines/pitcrew/](https://github.com/braineatingmachines/pitcrew/)**

Since working with my [FLL team](/lego-robotics/), I've been looking at growth gaps between FLL and FTC to better equip students for higher-level teams. Conversations with teachers point to students struggling to articulate their designs and models for 3D modeling and printing, or to document their CNC work. While browsing team websites and forum posts about FTC and FRC, I realized a lot of teams build their websites using WordPress. WordPress is a great CMS with good plugins and templates — a solid choice if you are a business. For a cash-strapped robotics team, though, it is just another line item on the monthly expense sheet. For a team that already writes code and hosts it on GitHub, [GitHub Pages](https://pages.github.com) is the perfect fit — host your team’s website directly from a repository. 

Enter Claude Code to build a template in Jekyll + GitHub Pages. I summoned ChatGPT and Claude to review team websites and document a list of features in order of usage, that should be available on such a template. After multiple rounds of review, I combined the notes and created a `SPEC.md` & `CLAUDE.md` file for Claude Code to build the template. At the end of each session, these files are updated and committed as part of the codebase.

## Feedback Update - Adding a Wizard
After the template was released, I saw 3 forks from different teams, but did not see a fully deployed site. The common feedback from all 3 teams was the apprehension to edit the mountain of `yml` files to add the data. Teams were aware about the work, but were not very familiar with the file format and process. I've added a startup wizard that helps you with the initial configuration. It's controlled by a config parameter in `_config.yml` | `startup_wizard: true`. 

The wizard allows you to choose your team colors and provides a simple interface to capture basic data about the team, sponsors and events. As you walk through it step-by-step, it captures the data in browser memory, and at the end of the wizard, gives you the data files for download that you replace in your own repository and push to github.

![/assets/images/posts/pitcrew-wizard.png](/assets/images/posts/pitcrew-wizard.png)

---
## Files for Claude

### SPEC.md

> Live from [braineatingmachines/pitcrew](https://github.com/braineatingmachines/pitcrew/blob/main/SPEC.md)

<div id="spec-embed"><em>Loading SPEC.md...</em></div>

---

### CLAUDE.md

> Live from [braineatingmachines/pitcrew](https://github.com/braineatingmachines/pitcrew/blob/main/CLAUDE.md)

<div id="claude-embed"><em>Loading CLAUDE.md...</em></div>

<script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
<script>
[
  { url: 'https://raw.githubusercontent.com/braineatingmachines/pitcrew/main/SPEC.md', id: 'spec-embed' },
  { url: 'https://raw.githubusercontent.com/braineatingmachines/pitcrew/main/CLAUDE.md', id: 'claude-embed' }
].forEach(function(f) {
  fetch(f.url)
    .then(function(r) { return r.text(); })
    .then(function(t) { document.getElementById(f.id).innerHTML = marked.parse(t); });
});
</script>