# GitHub Pages Multi-page CMS

A browser-based static CMS for GitHub Pages. It lets you create an unlimited page tree and publish real `.html` files to a GitHub repository.

## Structure

- Top-level pages = **Main Links**
- Children of a page = **Sublinks** in that page's sidebar
- Children can themselves have children, so the tree can be deeper than one level.
- `cms.json` stores the editable site structure.
- `index.html` is the generated page for the page whose slug is `home`.
- Other pages are generated under `pages/<slug>.html`.
- Every generated page contains the common header, main navigation, contextual sidebar, and its own content.

## Quick start

1. Create an empty GitHub repository and enable GitHub Pages from the `main` branch/root.
2. Upload `admin.html` to the repository. You can also upload the placeholder `index.html`.
3. Open `https://YOUR-USER.github.io/YOUR-REPO/admin.html`.
4. Enter your owner, repository, branch and a fine-grained GitHub token with **Contents: Read and write** permission.
5. Click **Load sample** to see the page tree, or **Load site** if `cms.json` already exists.
6. Use **+ Main link/page** to create a top-level page.
7. Select a page and use **+ Sublink/page** to create a child under it.
8. Edit the slug, browser title, heading and HTML content.
9. Click **Preview**.
10. Click **Publish to GitHub**.

## Example

If the tree is:

```text
Home
About
  Team
  History
Services
  Web Development
  Consulting
Contact
```

The generated files are:

```text
index.html
pages/about.html
pages/team.html
pages/history.html
pages/services.html
pages/web-development.html
pages/consulting.html
pages/contact.html
cms.json
```

The top navigation is:

```text
Home | About | Services | Contact
```

When `About` is opened, its sidebar contains:

```text
Team
History
```

When `Services` is opened, its sidebar contains:

```text
Web Development
Consulting
```

## Important GitHub token note

The token is entered into the browser and used directly against the GitHub API. Do not put the token in `admin.html`, commit it to the repository, or share it. For a public production CMS, replace the personal token flow with GitHub OAuth or a GitHub App/backend.

## Editing HTML

The page body accepts HTML intentionally. This makes the CMS useful for static sites without needing a server. The generated HTML is static, so published pages continue to work even when the CMS page is not open.

## Limitations of this browser-only version

Publishing uses the GitHub Contents API and may create several commits (manifest + each page + deletions). It is designed to be simple and GitHub-Pages-friendly. A production version can use the Git Git Data API to publish the entire tree as one atomic commit, plus GitHub OAuth/GitHub App authentication, media upload, revision management, drafts and reusable templates.
