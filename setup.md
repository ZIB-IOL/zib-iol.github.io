# Setup

## GitHub Pages

The site is served automatically from the `main` branch of `ZIB-IOL/zib-iol.github.io`.

## GitHub Action: `fetch-blog.yml`

Runs daily (06:17 UTC), on push to `main`, and on manual dispatch. It:

1. **Fetches the blog feed** from `https://www.pokutta.com/blog/feed.xml` (Atom), converts the latest 5 posts to `blog-feed.json`
2. **Fetches GitHub org stats** (member count, repo count) from the GitHub API, writes to `org-stats.json`
3. **Auto-commits** if either file changed

### Required secret: `ORG_TOKEN`

The default `GITHUB_TOKEN` can only see public org members and public repos. To get accurate counts, the Action uses a fine-grained PAT stored as the repository secret `ORG_TOKEN`.

**Token scope** (fine-grained PAT):

| Setting | Value |
|---------|-------|
| Resource owner | `ZIB-IOL` |
| Repository access | All repositories (needed for repo count) |
| Organization permissions > Members | **Read** |
| Repository permissions > Contents | **Read and write** (to push `org-stats.json`) |
| Repository permissions > Metadata | **Read** (to count repos) |

**To rotate the token:**

1. Go to GitHub > Settings > Developer settings > Fine-grained tokens
2. Regenerate or create a new token with the scopes above
3. Update the secret:
   ```
   gh secret set ORG_TOKEN --repo ZIB-IOL/zib-iol.github.io
   ```
   (paste the new token when prompted)

## Local development

```
cd zib-iol.github.io
python3 -m http.server 8000
# open http://localhost:8000
```

## Fonts

JetBrains Mono (OFL license), self-hosted in `fonts/`. No external font dependencies.
