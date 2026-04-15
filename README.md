# CMS Content for opendata.swiss

This is one of three repositories that contain the content for the opendata.swiss website. Each corresponds to one of three environments:

| Environment | Repo                                                              |
|-------------|-------------------------------------------------------------------|
| TEST        | https://github.com/opendata-swiss/opendata-swiss-cms-content-test |
| INT         | https://github.com/opendata-swiss/opendata-swiss-cms-content-int  |
| PROD        | https://github.com/opendata-swiss/opendata-swiss-cms-content      |

Each one is its own independent repository as far as GitHub is concerned, but they share the same content. As a minimum safety measure, their default branches are protected against direct pushes, requiring pull requests to be opened.

In principle, it should be possible to migrate the content from PROD to INT. At least until we will at some point need to rewrite history to remove some sensitive data from PROD.

TEST is a little different because it contains test data for testing the CMS. 
When content should be synchronised with INT/PROD, make sure to keep the TEST content intact.

## Working with the content from a single local environment

1. Clone the TEST environment:

    ```bash
    git clone git@github.com:opendata-swiss/opendata-swiss-cms-content-test.git
    ``` 
2. Add remotes for INT and PROD:

    ```bash
    git remote add int git@github.com:opendata-swiss/opendata-swiss-cms-content-int.git
    git remote add prod git@github.com:opendata-swiss/opendata-swiss-cms-content.git
    ```

If you wish to create a new branch to INT or PROD, you can do so by branching off the corresponding remote and then pushing slightly different:

```bash
# Add -c only on first switch, to create a new local branch
git switch -c int/main
# Create a new branch for INT
git switch -c int/my-branch
# Make changes
# ...
# Push to INT
git push int HEAD:my-branch
```

The last push is important. A standard `git push` would push to the default remote, which in this scenario would be `test`.
