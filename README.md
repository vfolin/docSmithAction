# docSmithAction

This GitHub Action automates the process of exporting selected code and documentation files from your repository to an AWS S3 bucket. 
It also generates and uploads the repository structure, commit history, and the diff of the latest commit as artifacts and to S3. 
This is useful for tracking changes, backing up important files, and integrating with external systems that require up-to-date repository data.

Add this file to your repository at the path `.github/workflows/use-export.yml`, then update the placeholders with your own settings.

```yaml
name: Use Export Changes

on:
  push:
    branches:
      - main
    paths-ignore:
      - '.github/workflows/**'
  pull_request:
    branches:
      - main
  workflow_dispatch:

jobs:
  call-export:
    uses: vfolin/docSmithAction/.github/workflows/export_changes.yml@main
    with:
      bucket_name: <YOUR_BUCKET_NAME>
      aws_region: <YOUR_AWS_REGION>
      include_code: 'folder1,folder2, file1.py, file2.py'
      include_documentation: 'folder3, README.md'
    secrets:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```
