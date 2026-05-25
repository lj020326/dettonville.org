# TODO: Site Evolution & Maintenance Roadmap

## 1. Immediate Theme Migration
- [ ] **Research Replacement:** Transition from the current UIkit-based theme to **[Hugo PaperMod](https://github.com/adityatelange/hugo-PaperMod)** or **[Hugo Book](https://github.com/alex-shpak/hugo-book)**.
    - *Rationale:* PaperMod offers a native, modern, and highly performant dark/light mode toggle with clean CSS variables that avoid the "hardcoded gradient" issues found in your current theme. It is the industry standard for "crisp/professional" tech documentation.

## 2. Content Reworking
- [ ] **Cross-Linking:** Audit all role pages (`ansible/`) to include direct `[Source Code]` links using the `{{ .Site.Params.contentSourceUrl }}` variable.
- [ ] **Example-Driven Refactor:** Convert text-heavy conceptual explanations into "Problem-Solution-Implementation" blocks, linking directly to the actual `inventory/` or `group_vars/` files in your repositories.

## 3. LLM Agent Integration (The Grand Plan)
- [ ] **Agent Workflow:** Develop a dedicated repository for an "Agent-Documentation-Coordinator" that:
    - Watches `dettonville/` infrastructure repositories for `git push` events.
    - Generates summary commits using an LLM.
    - Automates the creation of "Release Feature Highlights" on the `dettonville.org` blog.
- [ ] **Social Synchronization:** Integrate a social-media-post generator that triggers on site deployment to share back-referenced feature updates.

## 4. Technical Debt
- [ ] **GitHub Workflow Update:** Refactor `.github/workflows/*.yml` to remove deprecated `::set-output` commands.
- [ ] **Asset Minification:** Standardize CSS overrides into a single `assets/sass` pipeline to allow for modern Hugo build-time minification.
