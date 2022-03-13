# Git & Github

Git is a version control system. Github is a Git platform that is free to use.

A repository is a directory where all files and folders needed for a project, including all changes made on them,  are stored.

A commit is a set of changes packaged with a description.

There are always two repositories: one local and one remote.

* Push will push local changes to the remote repo.
* Pull will pull remote changes to the local repo.
* Fetch will pull the information about remote changes, without applying them. This allows you to make changes and later pull.

A branch is a deviation from the main development tree. It's what you would use to add extra features or experiment without affecting the starting code. Once you're done with changes, you can do a pull request, to implement the changes on the branch to main.

## New Repo

* Create a repo on GH first. Get the SSH code for it.
* Get in the local project folder using the terminal.
* Clone the repo with the SSH code using `git clone git@github.com:USER-NAME/REPOSITORY-NAME.git`
* A new folder for the project will now be created locally. Use `git remote -v` to check the GH url of the project from within the local window.
* Create files in the folder, work on the project, make some changes.

## Uploading changes

* Once you have something to upload, stay in the folder and type `git add .` to stage all files.
* Then type this to commit all changes. Add a description. `git commit -m "Edit README.md and hello_world.txt"`
* Use `git push` and get it all done with.
* Other useful commands are `git status` and `git log`.
