# Submission Notes

What was the hardest part of setting up the CI pipeline?

The hardest part was getting the GitHub Actions workflow to run successfully the first time. A couple of the jobs failed because of missing dependencies and small configuration issues, so I went through the workflow step by step and verified each stage. Having Claude explain the workflow made it much easier to understand what each job was doing instead of just copying the YAML.

What did the Docker health check catch that curl on the host didn't?

The Docker health check verified that the application was actually healthy from inside the container, including its dependencies. A simple curl from the host only confirmed that the API endpoint responded, but it didn't tell me whether the container itself was considered healthy or if the supporting services were available.

One specific thing Claude generated that you changed — and why.

Claude initially generated a CI workflow with a few extra steps that weren't necessary for this project. I removed the unnecessary parts and kept the workflow focused on linting, testing, security scanning, and validation so it was easier to understand and maintain. I also reviewed each section before committing to make sure I knew what it was doing.

What would you add to the pipeline if you had another hour?

I would add automatic code coverage reporting and a deployment stage that runs only after the main branch passes all checks. I would also add dependency caching to reduce build time and a PR template so reviewers have a consistent checklist before approving changes.
