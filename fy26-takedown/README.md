# FY26 Final Take Down Targets — deploy package

Static HTML served with nginx in Docker. Ready for **DigitalOcean App Platform**, **Container Registry + Droplet**, or any host that runs containers.

## What’s in here

| File | Purpose |
|------|---------|
| `index.html` | App (copy of `../deals-in-flight.html` in this repo) |
| `Dockerfile` | nginx Alpine image, listens on **8080** |
| `nginx.conf` | Serves `index.html` at `/` |

## Run locally

From **this directory** (`fy26-takedown`):

```bash
docker build -t fy26-takedown .
docker run --rm -p 8080:8080 fy26-takedown
```

Open http://localhost:8080

## DigitalOcean App Platform (recommended)

1. Push this repo to GitHub/GitLab/Bitbucket.
2. In DO: **Create** → **Apps** → **GitHub** (or your provider) → pick the repo.
3. Configure the component:

**Option A — build context is `fy26-takedown` (simplest)**  
   - **Dockerfile path**: `fy26-takedown/Dockerfile`  
   - **Source directory** (if the UI has it): `fy26-takedown`  

**Option B — build context is the repo root**  
   - **Dockerfile path**: `Dockerfile.fy26` (at repository root)  
   - **Context**: `/` (default)

4. Set **HTTP port** / **Public HTTP port** to **8080** (must match the container).
5. Deploy.

## Update the page

Edit `deals-in-flight.html` at the repo root, then refresh the deploy package:

```bash
cp ../deals-in-flight.html ./index.html
```

Commit `index.html` (or the root HTML) and redeploy.

## Notes

- **localStorage** (closed deals, notes) is per **browser + origin** (your deployed HTTPS URL). It does not sync across devices unless you add a backend later.
