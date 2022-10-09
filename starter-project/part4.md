# Part 4 - Continuous Integration and Automated Deployment

Read about [Continuous Integration](https://www.cloudbees.com/continuous-delivery/continuous-integration).

During development of modern software, it is common to use [git flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) or some variant of it for teams to collaborate on changes to their projects.

When changes are made to a git repo, we can automatically perform some actions based on what is being done. Every major git repo host will support either their own Continuous Integration tooling or allow you to hook in your own (such as Jenkins). Your goal should be to never log in to a server yourself to deploy new code.

Using [Github Actions](https://github.com/features/actions), perform the following:

1. When a pull request is submitted against your project's repository, run various tests against your code to verify it is not broken. For example:
    - Unit tests
    - Code linting tests (black for Python formatting, mypy for python type checking)
    - Security auditing tests (bandit for python)
2. When a pull request is approved and merged to the main (or master) branch, perform those tests again.
3. When a tag is pushed to your repo, deploy the software to your hosting environment.
    - There are a few ways to go about this. For now, just use a basic semantic versioning schema. For example: pushing tag `v0.1.0` would deploy to your hosting environment.
    - Ensure tags that do not fit the schema you set (in the above example, tags starting with `v`) do not deploy.
    - The deployment methodology between each company and team may differ. For example, a merge to master may deploy to a development environment. Or a pull request may deploy that branch to an entirely new environment created just for that PR. For now, keep it simple.
4. For this project, simply run ansible as your deployment step. You should be able to define in your ansible vars which tag from your git repo to deploy.
    - Ensure any secrets (ssh keys, api keys) are not available to the public. Ensure these keys are not available to any CI tools (including actions) in pull requests. This prevents credential leakage.
5. Develop a new feature and deploy it!

### Acceptance Criteria
1. Pull requests against your repo get scanned or tested automatically.
2. Merges to your main/master branch are scanned or tested in the same way.
3. Tags pushed to your repo are deployed automatically.

---

[Continue to Part 5](part5.md)