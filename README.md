# CodeDirector — public site (Privacy Policy + Terms)

Static pages published via **GitHub Pages** to give the CodeDirector app a public
Privacy Policy and Terms of Service URL — required for the TikTok Content Posting
API app review and the YouTube API project.

```
index.html    → landing page
privacy.html  → Privacy Policy   (paste this URL into the TikTok/Google review)
terms.html    → Terms of Service
.nojekyll     → serve the HTML as-is (no Jekyll processing)
```

## Publish it (one time)

`gh` CLI is not installed, so use the web UI once to create the repo, then push.

### 1. Create an EMPTY public repo on GitHub

Go to <https://github.com/new> and create:

- **Repository name:** `codedirector-site`
- **Visibility:** **Public** (Pages needs public, unless you have GitHub Pro)
- Do **not** add a README / .gitignore / license (this folder already has files)

### 2. Push this folder

From `D:\projects\codedirector-site` (PowerShell):

```powershell
git init
git branch -M main
git add .
git commit -m "Add CodeDirector site: privacy policy + terms"
git remote add origin https://github.com/tptindev/codedirector-site.git
git push -u origin main
```

### 3. Turn on GitHub Pages

In the new repo: **Settings → Pages**

- **Source:** *Deploy from a branch*
- **Branch:** `main`  •  **Folder:** `/ (root)`  → **Save**

Wait ~1 minute. Your public URLs will be:

| Page            | URL                                                        |
| --------------- | ---------------------------------------------------------- |
| Home            | `https://tptindev.github.io/codedirector-site/`            |
| Privacy Policy  | `https://tptindev.github.io/codedirector-site/privacy.html`|
| Terms of Service| `https://tptindev.github.io/codedirector-site/terms.html`  |

### 4. Use the URLs

Paste the **Privacy Policy** URL (and Terms URL) into:

- TikTok for Developers → your app → basic info + review submission
- Google Cloud Console → OAuth consent screen → app privacy/terms links

## Alternative: `gh` CLI

If you install GitHub CLI (`winget install GitHub.cli`), steps 1–2 collapse to:

```powershell
gh auth login
gh repo create codedirector-site --public --source=. --remote=origin --push
```

Then enable Pages (step 3) — or:

```powershell
gh api -X POST repos/tptindev/codedirector-site/pages -f "source[branch]=main" -f "source[path]=/"
```

## Editing later

Change the HTML, then:

```powershell
git add . ; git commit -m "Update legal pages" ; git push
```

Pages redeploys automatically within a minute.

---

**Note:** the contact email in the pages is `tptin.dev@gmail.com` (from your git
config). Swap it in `privacy.html` / `terms.html` if you want a different address.
The pages state CodeDirector is not affiliated with TikTok/Google/YouTube — keep
that line; reviewers look for it.
