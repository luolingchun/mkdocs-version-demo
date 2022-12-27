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

