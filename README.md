# Dettonville.org Documentation & Infrastructure

This repository serves as the authoritative source for the Dettonville Project's infrastructure documentation, configuration standards, and automation lifecycle tools.

## Development & Testing
To build the site locally for testing and verification:

```bash
hugo serve --gc --minify --disableFastRender
```

## Deployment Workflow
Deployment is fully automated via GitHub Actions. There is no manual `deploy.sh` script; the build process is triggered natively by source control events.

1. **Commit & Push:** Make your changes to the `main` branch.
2. **Automated Pipeline:** The `.github/workflows/hugo.yml` action automatically triggers on every push to `main`.
3. **Build:** The CI runner compiles the site using Hugo.
4. **Publish:** The generated static assets are automatically pushed to the `gh-pages` branch, which serves the live production site.



## Repository Architecture
* **`main`**: Primary source for content, Hugo configuration, and templates.
* **`gh-pages`**: Production artifact branch. This branch contains only the generated static HTML/CSS/JS and is updated automatically by the GitHub Actions pipeline.

## LLM-Integrated Maintenance
This site is designed to be maintained via LLM agents. Automation agents should:
1.  **Monitor Infrastructure Repos:** Watch for changes in `dettonville/` infrastructure repositories.
2.  **Generate Documentation:** Automatically update content under `/content/` to reflect new feature enablement or inventory shifts.
3.  **Sync:** Push updates to `main`, triggering the automated build pipeline described above.

---

## Roadmap & TODOs
See the [TODO.md](TODO.md) file for upcoming platform improvements, theme migration plans, and content refactoring milestones.

## Code of Conduct
This project follows the Ansible project's [Code of Conduct](https://docs.ansible.com/ansible/devel/community/code_of_conduct.html). Please read and familiarize yourself with this document before contributing.

## More Information
- [Ansible Collection overview](https://github.com/ansible-collections/overview)
- [Ansible User guide](https://docs.ansible.com/ansible/latest/user_guide/index.html)
- [Dettonville Ansible Git Inventory Module](https://github.com/dettonville/ansible-git-inventory)
