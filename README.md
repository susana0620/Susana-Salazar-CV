# Susana-Salazar-CV
CV
name: Build and Deploy
env:
  CI: false
  GITHUB_USERNAME: ${{ github.repository_owner }}
  REACT_APP_GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} # This is automatically set by Github Actions
  USE_GITHUB_DATA: "true"
on:
  push:
    branches:
      - master
  schedule:
    - cron: "0 12 * * 1" # see https://docs.github.com/en/actions/reference/events-that-trigger-workflows#scheduled-events
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout 🛎️
        uses: actions/checkout@v2 # If you're using actions/checkout@v2 you must set persist-credentials to false in most cases for the deployment to work correctly.
        with:
          persist-credentials: false

      - name: Install and Build 🔧 # Build the Project
        run: |
          npm install
          npm run build
      - name: Deploy 🚀
        uses: JamesIves/github-pages-deploy-action@releases/v3
        with:
          GITHUB_TOKEN : ${{ secrets.GITHUB_TOKEN }} # This is provided by GitHub.
          BRANCH: gh-pages # The branch the action should deploy to.
          FOLDER: build # The folder the action should deploy.
