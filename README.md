# Orbit space quiz

A ten-question space exploration quiz with answer explanations, progress and
score tracking, final accuracy, and replay. It supports keyboard answers
(`1`-`4`), light and dark appearance, narrow screens, and reduced motion.

## Run locally

Clone or download this repository, then open `index.html` directly in a modern
browser (a `file://` URL). No server, build command, package installation, or
external resources are needed: all HTML, CSS, JavaScript, and SVG artwork live
in that file.

## GitHub Pages

The workflow in [`.github/workflows/pages.yml`](.github/workflows/pages.yml)
runs only after a push to the default branch, currently `main`, including a
merged pull request. It copies `index.html` into a staging directory, uploads
that directory as a Pages artifact, and deploys it to the `github-pages`
environment. There is no build step because the site is already static.
Pull requests and feature-branch pushes do not deploy.

Before the first deployment, a repository administrator must:

1. Open **Settings > Pages > Build and deployment** and select **GitHub Actions**
   as the source.
2. Ensure GitHub Actions is enabled and repository or organization policies allow
   `actions/checkout`, `actions/configure-pages`, `actions/upload-pages-artifact`,
   `actions/deploy-pages`, and their nested actions.
3. Allow the workflow's `GITHUB_TOKEN` permissions: `contents: read`,
   `pages: write`, and `id-token: write`. No personal access token or custom
   secret is needed.
4. Ensure any `github-pages` environment deployment rules permit `main`; if
   required reviewers are configured, approve deployments when ready.

The workflow does not enable Pages or change its settings. Configure Pages
before merging the deployment pull request; merging triggers the first run.
If the default branch is renamed, update the workflow's branch filter.

With the standard project-site configuration, the site will be available at
<https://jeongaelee.github.io/space-quiz/> after a successful deployment. The
deployment environment also records the URL returned by Pages.
