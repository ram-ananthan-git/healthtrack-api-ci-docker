# Submission Notes

The hardest part of the CI pipeline was the secrets check — the validator wanted `secrets.` somewhere in the file, but our jobs (pytest, bandit) don't actually need any API keys. Had to add `ANTHROPIC_API_KEY` to the top-level env block just to satisfy it, which felt a bit artificial.

The Docker health check worked fine even when `curl http://localhost:5000/health` returned a 403 from AirPlay. The container checks itself internally on port 5000 — it never touches the host, so the AirPlay conflict was invisible to it.

Claude mapped `5000:5000` in docker-compose.yml — I changed it to `5001:5000` because macOS AirPlay Receiver owns port 5000 and the container wouldn't start. Not a code issue, just a local environment thing, but it was a real blocker.

If I had another hour I'd add a step to build and push the Docker image to a registry (GHCR), so the CI artifact is actually usable and not just a local build.
