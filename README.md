> An example of versioning with [mike](https://github.com/jimporter/mike) for MkDocs

## First commit

1. create mkdocs.yml

    ```yaml
    site_name: mike version for mkdocs

    theme:
    name: material

    plugins:
    - search

    extra:
    version:
        provider: mike
    
    nav:
    - Home: index.md
    - Content: content.md
    ```

2. git commit all changes

3. git checkout new branch v1.x

4. create first version: `mike deploy v1.x`

5. back to master and `mike deploy v2.x`, now you get two versions.

6. set default version: `mike set-default v2.x`

7. preview: `mike serve`


## Push to github

- `git push origin master`
- `git push origin gh-pages`
- `git push origin v1.x`

## Github action

Create `.github/workflows/mkdocs.yml`, ensure correct branch and version, `v1.x` be equal to branch [v1.x](https://github.com/luolingchun/mkdocs-version-demo/blob/v1.x/.github/workflows/mkdocs.yml) and `v2.x` be equal to branch [master](https://github.com/luolingchun/mkdocs-version-demo/blob/master/.github/workflows/mkdocs.yml) in this demo.

```yml
# This is a basic workflow to help you get started with Actions

name: mkdocs

# Controls when the action will run. 
on:
  # Triggers the workflow on push or pull request events but only for the master branch
  push:
    branches: [ master ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - run: pip install mkdocs-material mike mkdocstrings[python]
      - name: Build docs
        run: |
          git config --local user.email "action@github.com"
          git config --local user.name "GitHub Action"
          git fetch origin gh-pages:gh-pages
          mike deploy v2.x
          git push origin gh-pages

```