# Avoid duplicate action triggering

I thin ideally we would want to run the CI on all `push` and `pull_request` events.

* The `push` trigger will run the CI if someone pushes to the repository, accepts a pull-request, makes a change through the UI of GitHub.
* The `pull_request` trigger will run the CI when someone send a Pull-Request.
* 

If someone sends a PR from another repo
