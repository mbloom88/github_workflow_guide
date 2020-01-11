# Github Workflow Guide

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

### Cloning a Branch from the Remote Repo
When starting out, the following commands can be used to clone a specific project branch from the remote repo.

Console Command | Description
----------------|------------
git fetch --all --tags --prune | Fetch all tags and remotes.
