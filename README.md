# Github Workflow Guide

## Getting Started
A quick, 20-minute tutorial can be found [here](https://www.youtube.com/watch?v=0fKg7e37bQE).

## Markdown
A markdown tutorial can be found [here](https://guides.github.com/features/mastering-markdown/) and [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) for ".md" files.

## Version Control
Version control follows the [Semantic Versioning](https://semver.org/) nomenclature (MAJOR.MINOR.PATCH).

1. MAJOR version when you make incompatible API changes,
1. MINOR version when you add functionality in a backwards compatible manner, and
1. PATCH version when you make backwards compatible bug fixes.

Additional labels for pre-release and build metadata are available as extensions to the format listed above.

## Branching Model
Development follows a [Branching Model](https://nvie.com/posts/a-successful-git-branching-model/) that uses the following branches:

| Branch Name | Branches From | Merges Into | Purpose |
|:-----------:|:-------------:|:-----------:|:--------|
| master | - | - | The main branch where the source code of HEAD always reflects a production-ready state.
develop | master | - | The main branch where the source code of HEAD always reflects a state with the latest delivered development changes for the next release. Some would call this the “integration branch”. When the source code in the develop branch reaches a stable point and is ready to be released, all of the changes should be merged back into master somehow (Release branch) and then tagged with a release number. |
| feature | develop | develop | Branch naming convention can be anything except master, develop, release-#, or hotfix-#. Feature branches (or sometimes called topic branches) are used to develop new features for the upcoming or a distant future release. When starting development of a feature, the target release in which this feature will be incorporated may well be unknown at that point. The essence of a feature branch is that it exists as long as the feature is in development, but will eventually be merged back into develop (to definitely add the new feature to the upcoming release) or discarded (in case of a disappointing experiment). Feature branches typically exist in developer repos only, not in origin. |
| release | develop | master, develop | Branch naming convention is release-#. Release branches support preparation of a new production release. They allow for minor bug fixes and preparing meta-data for a release (version number, build dates, etc.). By doing all of this work on a release branch, the develop branch is cleared to receive features for the next big release. The key moment to branch off a new release branch from develop is when develop (almost) reflects the desired state of the new release. At least all features that are targeted for the release-to-be-built must be merged in to develop at this point in time. All features targeted at future releases may not—they must wait until after the release branch is branched off. It is exactly at the start of a release branch that the upcoming release gets assigned a version number—not any earlier. Up until that moment, the develop branch reflected changes for the “next release”, but it is unclear whether that “next release” will eventually become 0.3 or 1.0, until the release branch is started. That decision is made on the start of the release branch and is carried out by the project’s rules on version number bumping. |
| hotfix | master | master, develop | Branch naming convention is hotfix-#. Hotfix branches are very much like release branches in that they are also meant to prepare for a new production release, albeit unplanned. They arise from the necessity to act immediately upon an undesired state of a live production version. When a critical bug in a production version must be resolved immediately, a hotfix branch may be branched off from the corresponding tag on the master branch that marks the production version. The essence is that work of team members (on the develop branch) can continue, while another person is preparing a quick production fix. |

## Project Workflow
Note that commands in this section use angled brackets (e.g. <url>) to signify where the user should fill in the field. The angled brackets should be left out in the actual commands.

### Cloning from a Remote Repo
When starting out, the following commands can be used to clone a specific project branch from the remote repo. Note: It is recommended to first clone the `master` branch and then checkout other branches from there.

| Console Command | Description |
|-----------------|-------------|
| `git fetch --all --tags --prune` | Fetch all tags and remotes. |
| `git clone <remote_repo_url>` | Clone the master branch from the remote repo. |
| `git clone --single-branch --branch <branch> <remote_repo_url>` | Clone a specific branch from the remote repo. |
| `git clone <remote_repo_url> --branch=<tag_name>` | Clone a specific tag from the remote repo. |

### Pull Request from a Working Branch
If a branch has already been cloned to the local workspace from the remote repo, a standard pull request can also be made from the working project directory.

| Console Command | Description |
|-----------------|-------------|
| `git checkout <branch>` | Checkout (or switches to) a desired branch from the remote repo. |
| `git pull` | Pull request from the remote repo into the working project directory. |

### Creating a New Branch
If a new branch needs to be created, the following commands can be used.

| Console Command | Description |
|-----------------|-------------|
| `git checkout <branch_from>` | Checkout the branch that the new branch will branch from. |
| `git checkout -b <branch_name> <branch_from>` | Create the new branch from the root branch that was previously checked out. |

### Committing and Pushing Branch Updates
Once updates have been made to a particular branch, the changes can be pushed to the remote repo.

| Console Command | Description |
|-----------------|-------------|
| `git status` | Receive a list of all local changes made to the working branch. |
| `git add -A` | Add all changes that were made locally to stage for a potential commit to the remote repo. |
| `git add <filepath>` | Add specific changes that were made locally to stage for a potential commit to the remote repo. |
| `git commit -m “update comments”` | Commits changes and adds a comment prior to pushing the local changes to the remote repo. |
| `git push` | Pushes local updates to the remote repo. Note that the push happens to the working branch that was checked out. |

### Merging Branches
If feature, release, or hotfix branches need to be merged back to the master or develop branches, the following commands can be used.

| Console Command | Description |
|-----------------|-------------|
| `git checkout <branch_to_merge_to>` | Checkout the branch that will be merged into from the feature, release, or hotfix branch. |
| `git merge --no-ff <merging_branch>` | Merge the feature, release, or hotfix branch back into the master or develop branch. |
| `git push origin <branch_to_merge_to>` | Push updated branch to the remote repo. |

### Tagging a Release
Tagging is necessary to indicate where releases on the master branch have occurred. To tag a release, the following commands can be used.

| Console Command | Description |
|-----------------|-------------|
| `git checkout master` | Checkout the master branch that will be merged into. |
| ` merge --no-ff release-#` |  Merge the release into the master branch. | 
| `tag -a vX.Y.Z -m "tag comments go here"` | Tag the new release according to the Semantic Versioning process. | 
| `git push --follow-tags` | Push the tag to the remote repo. |

A list of tags can also be found by typing the following.

| Console Command | Description |
|-----------------|-------------|
| `git tag` | Shows all tags on the remote repo. |

### Deleting Branches
If branches need to be deleted (e.g. after merging) the following commands can be made.

| Console Command | Description |
|-----------------|-------------|
| `git branch -d <branch>` | Delete a local branch. |
| `git push <remote_repo_url> --delete <branch>` | Relete a specfic branch in the remote repo. |

## Changelogs
Changelogs should always be included with every release. A breakdown on what is included in a typical changelog can be found [here](https://keepachangelog.com/en/1.0.0/) and an example CHANGELOG.md can be found at this [Github repo](https://github.com/olivierlacan/keep-a-changelog/blob/master/CHANGELOG.md).  

## Useful Github Resources
* [Essential git commands every developer should know](https://dev.to/dhruv/essential-git-commands-every-developer-should-know-2fl)
* [Start a new git repository](https://kbroman.org/github_tutorial/pages/init.html)
