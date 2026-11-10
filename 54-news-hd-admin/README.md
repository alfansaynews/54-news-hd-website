# 54 News HD Admin Panel

A standalone HTML admin panel that updates a separate public website repository through the GitHub Contents API. No Supabase, Firebase, server, or build step is used.

## 1. Configure the public website repository

1. Create a GitHub repository, for example `54-news-hd-website`.
2. Upload all files from the `54-news-hd-website` folder in this package, keeping the `assets` folder.
3. In the repository, open **Settings → Pages**.
4. Select **Deploy from a branch**, choose `main` and `/ (root)`, then save.
5. Wait for GitHub Pages to publish the site.

The website uses:
- `index.html` — channel home page and YouTube playlist
- `article.html` — individual story page
- `posts.json` — articles
- `ticker.json` — breaking news headlines
- `manifest.json`, `sw.js`, `assets/icon.svg` — PWA support

## 2. Create a fine-grained token

In GitHub: **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.

Recommended settings:
- Resource owner: your GitHub account (or the organization that owns the website repository)
- Repository access: **Only select repositories** → select only `54-news-hd-website`
- Repository permissions: **Contents → Read and write**
- No other permissions are required for this panel.

Set an expiry date and keep the token private. If it is exposed, revoke it immediately and create a new one.

## 3. Publish the admin panel in its own repository

1. Create a second repository, for example `54-news-hd-admin`.
2. Upload `admin.html` and this README.
3. Enable GitHub Pages for this admin repository using `main` and `/ (root)`.
4. Open the admin page over HTTPS.
5. Enter the website repository owner, repository name, branch (`main`) and the fine-grained token.
6. Click **Connect & load content**.

The token is kept in the current browser page session only; it is not written into the HTML or committed to GitHub. Do not use this as a shared public admin login. Anyone who can use the panel and has the token can edit the website repository. Use a dedicated limited token and sign out/close the tab when finished.

## 4. Admin features

- Add, edit and delete articles.
- Set article status to Published or Draft.
- Add a short summary, full article, date and image URL.
- Add or update ticker headlines (one per line).
- Changes are committed directly to the website repository using GitHub's API.

## Notes and limitations

- This is a static-site solution. GitHub is the content store; there is no separate database.
- The browser needs internet access to contact `api.github.com`.
- GitHub Pages deployment may take a short time after a commit. Visitors may need to refresh.
- Image URLs must be publicly accessible HTTPS URLs. The admin panel stores the URL; it does not upload image files.
- The YouTube playlist is embedded. Autoplay with sound may be blocked by the visitor's browser.
- GitHub Pages does not provide private admin authentication. Protect the admin repository/page as appropriate and never embed a token in source code.
- For organization repositories, the token may require organization approval.
