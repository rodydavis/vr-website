# Automatic Online Demo for Flutter Packages

Make sure you are on the dev channel of flutter. And web enabled.

`flutter config —-enable-web`

## Create a folder and cd in to it
`mkdir flutter_awesome_package && cd flutter_awesome_package`

## Create a new flutter package
`flutter create -t package .`

## Create an example
`flutter create example`

## Create a personal access token
Copy the token and paste it in to the repos secret with the key `PERSONAL_TOKEN` 

## Create a git branch
`gh-pages`

## Create a Github Workflow
`main.yml`

Paste the following: 

```
name: github pages

on:
  push:
    branches:
      - master

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2
      - name: Setup Flutter
        uses: subosito/flutter-action@v1
        with:
          channel: ‘dev’
      - name: Install
        run: |
          flutter config —enable-web
          flutter pub get
      - name: Build
        run: cd example && flutter build web
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
#           github_token: ${{ secrets.GITHUB_TOKEN }} # Private Repos Only
          personal_token: ${{ secrets.PERSONAL_TOKEN }}
          publish_dir: ./example/build/web

```