# Avoid duplicate triggering of Github Actions

I think ideally we would want to run the CI on all `push` and `pull_request` events.

```
on:
  push:
  pull_request:
```

* The `push` trigger will run the CI if someone pushes to the repository, accepts a pull-request, makes a change through the UI of GitHub.
* The `pull_request` trigger will run the CI when someone send a Pull-Request.

* If after sending the initial PR the branch of the PR is updated (by another push) then the CI will be triggered again.

* If someone sends a PR from another repo this all works fine. However, if the PR is sent from the same repository as where the source-code is, then this configuration will trigger the CI twice. Once for the `push` event and once for the `pull_request` event. Any subsequent push to the same branch will also trigger the actions twice.

## Solutions

* Avoid sending PR from the same repo. This is less ideal for projects with multiple maintainers who would like to work on a branch together.
* Limit the triggers. E.g.:

```
on:
  push:
    branches:
      - 'master'
      - 'main'
  pull_request:
```

It will only trigger the GitHub Actions when there is a push to either the master or the main branches (to satisfy both old and new repositories with their default branch) or in a pull-request.

The drawbacks:
    * People who work in a branch on the central repo will have to create a PR before they start seeing the Actions.
    * People who work in different repo, and most likely are less familiar with the project, won't be able to enjoy the actions in their fork. By default GitHub Actions are not enabled in a fork but the forker can enable it and then can enjoy the results of it even before sending a PR. Thereby reducing the noise on the central repo of the project.


