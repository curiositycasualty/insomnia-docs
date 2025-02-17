---
layout: article-detail
title:  Continuous Integration
category: "Inso CLI"
category-url: inso-cli
---

Inso CLI has been designed to run in a CI environment, disabling prompts, and providing exit codes to pass or fail the CI workflow.

An example workflow run in Github Actions is as follows and performs the following:

1. Checkout
2. Install NodeJS
3. Install Inso CLI
4. Run linting
5. Run unit tests
6. Generate a declaractive configuration file

If any of these steps fail, the GitHub workflow will as well.

```yaml
# .github/workflows/test.yml

name: Test

jobs:
  Linux:
    name: Validate API spec
    runs-on: ubuntu-latest
    steps:
      - name: Checkout branch
        uses: actions/checkout@v1
      - name: Install NodeJS
        uses: actions/setup-node@v1
      - name: Install inso
        run: npm install -g insomnia-inso
      - name: Lint
        run: inso lint spec "Designer Demo" --ci
      - name: Run test suites
        run: inso run test "Designer Demo" --env UnitTest --ci
      - name: Generate declarative config
        run: inso generate config "Designer Demo" --type declarative --ci
```
