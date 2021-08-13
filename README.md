Deploy a [DigitalOcean App Platform](https://www.digitalocean.com/products/app-platform/) app using GitHub Actions.

 - Auto-deploy your app from source on commit, while allowing you to run tests or perform other operations before.

## Example

 Add your `.do/app.yaml`:

**Note that you should not configure `deploy_on_push: true` for this workflow.**

```yaml
name: sample-golang
services:
- name: web
  git:
    repo_clone_url: https://github.com/digitalocean/sample-golang.git
    branch: main
```

Create a `.github/workflows/main.yml`:

```yaml
on:
  push:
    branches:
      - master
jobs:
  deploy:
    runs-on: ubuntu-latest
    name: Deploy App
    steps:
    - name: Checkout code
      uses: actions/checkout@v2
    - name: DigitalOcean App Platform deployment
      uses: digitalocean/app_action@main
      with:
        app_name: sample-golang
        token: ${{ secrets.DIGITALOCEAN_ACCESS_TOKEN }}
```

## How its using DigitalOcean App Platform App Actions?

This example is using [DigitalOcean App Platform App Actions](https://github.com/digitalocean/app_action) in the .github/workflows/main.yml file to auto-deploy your app.

```yaml
- name: DigitalOcean App Platform deployment
  uses: digitalocean/app_action@main
  with:
    app_name: sample-golang
    token: ${{ secrets.DIGITALOCEAN_ACCESS_TOKEN }}
```