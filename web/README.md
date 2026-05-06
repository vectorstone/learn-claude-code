# Web app

This app is a static-exported Next.js site that can be deployed to GitHub Pages.

## Local development

```bash
npm ci
npm run dev
```

Open http://localhost:3000.

## Build

```bash
npm run build
```

The static output is generated in `out/`.

## Deploy to GitHub Pages

This repository includes `.github/workflows/deploy-pages.yml`.

### 1. Enable GitHub Pages

In the GitHub repository:

- Go to **Settings -> Pages**
- Set **Source** to **GitHub Actions**

### 2. Push to `main`

Any push to `main` will:

- install dependencies in `web/`
- run `npm run build`
- upload `web/out`
- deploy it to GitHub Pages

### 3. Configure a custom domain

For GitHub Pages deployed via **custom workflows / GitHub Actions**, configure the domain in GitHub settings instead of committing a `CNAME` file.

In **Settings -> Pages**:

- set **Custom domain** to your domain, for example `docs.example.com`
- enable **Enforce HTTPS** after DNS has propagated

DNS setup:

- for a subdomain like `docs.example.com`, create a `CNAME` record pointing to `<your-github-username>.github.io`
- for an apex/root domain like `example.com`, use GitHub Pages `A` records, and usually add `www` as a `CNAME` to `<your-github-username>.github.io`

## Notes

- The app uses `output: "export"` and `trailingSlash: true` in `next.config.ts`
- The root route redirects to `/en/`
- This setup is intended for custom-domain or user-site style hosting from the domain root
- If you later want to serve it under a repository subpath such as `/repo-name/`, you will need additional `basePath` / `assetPrefix` adjustments
