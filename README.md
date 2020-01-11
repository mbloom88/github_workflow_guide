# Github Workflow Guide

## Markdown
A markdown tutorial can be found [here](https://guides.github.com/features/mastering-markdown/) for ".md" files.

## Version Control
Version control follows the [Semantic Versioning](https://semver.org/) nomenclature (MAJOR.MINOR.PATCH).

1. MAJOR version when you make incompatible API changes,
1. MINOR version when you add functionality in a backwards compatible manner, and
1. PATCH version when you make backwards compatible bug fixes.

Additional labels for pre-release and build metadata are available as extensions to the format listed above.

## Branching Model
Development follows a [branching model](https://nvie.com/posts/a-successful-git-branching-model/) that uses the following branches:

Branch Name | Branches From | Merges Into | Purpose
------------|---------------|-------------|--------
master | - | - | The main branch where the source code of HEAD always reflects a production-ready state.
develop | master | - | The main branch where the source code of HEAD always reflects a state with the latest delivered development changes for the next release. Some would call this the “integration branch”. When the source code in the develop branch reaches a stable point and is ready to be released, all of the changes should be merged back into master somehow (Release branch) and then tagged with a release number.
