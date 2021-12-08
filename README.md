# GitHub Action to Sync S3 Bucket 🔄

This simple action uses the AWS CLI to sync a directory (either from your repository or generated during your workflow) with a remote S3 bucket.


## Usage

```yaml
name: Upload Website

on:
  push:
    branches:
    - master

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - uses: opn-ooo/opn-s3-action@master
      with:
        args: --acl public-read --follow-symlinks --delete
      env:
        AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET }}
        AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
        AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        AWS_REGION: 'ap-southeast-1'   # optional: defaults to ap-southeast-1
        SOURCE_DIR: 'public'      # optional: defaults to entire repository
        DEST_DIR: 'service-name' 
```