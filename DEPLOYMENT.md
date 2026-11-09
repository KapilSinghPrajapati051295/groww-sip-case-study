# Git + GitHub Pages — exact steps

Use one **public repository**. This package intentionally avoids API keys and personal data. The project folder is named `groww-sip-case-study`.

## 1. Create a new empty repository

On https://github.com/new create a **Public** repository named `groww-sip-case-study`. Do **not** initialise it with README, `.gitignore`, or license; the package already has a README.

## 2. Push from a terminal (Git Bash, VS Code Terminal, PowerShell)

Open a terminal *inside the extracted* `groww-sip-case-study` directory:

```bash
git init
git branch -M main
git add .
git commit -m "Build Groww SIP continuation case study submission"
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/groww-sip-case-study.git
git push -u origin main
```

Replace `YOUR_GITHUB_USERNAME` with the real owner name. Authenticate using Git Credential Manager/browser when prompted. If `origin` already exists: `git remote set-url origin https://github.com/YOUR_GITHUB_USERNAME/groww-sip-case-study.git`.

## 3. Turn on GitHub Pages

Repo → **Settings** → **Pages** → Source `Deploy from a branch` → Branch `main` → Folder `/docs` → **Save**. Publishing is asynchronous; only treat the URLs as live **after opening and testing them in an incognito browser**. GitHub Pages publication source `/docs` on a public branch is supported by GitHub.

## 4. Copy these *actual* verified links into the submission form

Base: `https://YOUR_GITHUB_USERNAME.github.io/groww-sip-case-study/`

- **AI Discovery Engine**: `[base]engine/` (also explain workflow in slide 3)
- **Deployed AI-native MVP demo**: `[base]mvp/`
- **AI Evidence Log**: `[base]evidence-log/`
- **PDF upload**: `deck/NL_Groww_10_Slides.pdf` from your local extracted project.

Open all three links and test both apps on mobile or incognito; verify no 404s. These are **templates** until the repository has been published.

## 5. Put public links in the deck, then rebuild final PDF

Open `deck/build_deck.py`, change the top-level `URLS` dictionary to the confirmed URLs. Run:

```bash
python deck/build_deck.py
libreoffice -env:UserInstallation=file:///tmp/lo_groww_publish --headless --convert-to pdf --outdir deck deck/NL_Groww.pptx
```

Rename `deck/NL_Groww.pdf` to `deck/NL_Groww_10_Slides.pdf` and submit this refreshed PDF. Commit and push the refreshed deck artifacts too if you want download links from the repo.

## 6. If you want to update the repo later

```bash
git add .
git commit -m "Update submission artifacts and live links"
git push
```

**Privacy and truthfulness:** do not claim the generated feedback is observed public data, pretend fictional interviews were conducted, or describe the deterministic MVP as a live generative model. They are clearly labelled study demonstrations throughout the package.
