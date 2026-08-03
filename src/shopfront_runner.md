# Vender shopfront_runner

## Overview

Vender shopfront (CI/CD) and shopfront-react (CI) automatically test and deploy using GitHub Actions.

Unfortunately, money isn't free. To avoid accruing unnecessary costs, and to allow for more flexibility, shopfront-runner was created.

Vender shopfront-runner is a Python project that automatically creates self-hosted runners, commanded by a GitHub webhook. The runners are ephemeral, so data does not persist with each one.

