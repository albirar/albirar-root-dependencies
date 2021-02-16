# Workflow and Git

All [Albirar projects](https://albirar.cat) uses the [Gitflow workflow](https://guides.github.com/introduction/flow/) as strategy to manage the development process. See also [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/).

This parent pom includes a fully configured [gitflow-maven-plugin](https://aleksandr-m.github.io/gitflow-maven-plugin/index.html "gitflow-maven-plugin") to enforce operations of git workflow through maven.

## Main branches

In our workflow with git, two branches holds the production code and the development code:

* `master` hold the production code
* `develop` hold the development code (new features)

When a new hotfix is added to `master`, also should to be added to develop. In other words, develop holds the master and any new development for new features.

## Summary of gitflow operations

1. New feature
2. Hotfix
3. New release

### New feature

Any new feature should to be developed at a specific branch, not in development branch. A new feature should to be added with:

* `mvn gitflow:feature-start`
* Coding and commiting
* Testing
* `mvn gitflow:feature-finish`

This goal create a new branch from develop, and name it with the following composition:

```
current_development_version_without_snapshot + feature_name + "-SNAPSHOT"
```

If the current development version is `1.5.10-SNAPSHOT` and the new feature is `locales`, the new pom version is:

```
1.5.10-locales-SNAPSHOT
```

And the new created branch for developing this new feature is:

```
feature/locales
```

When the feature is completely implemented, the command to finish is:

```bash
mvn gitflow:feature-finish
```

Then, this branch is merged out with develop and pom version is changed to `1.5.10-SNAPSHOT` to left develop with the current development version.

### New hotfix

* `mvn gitflow:hotfix-start`
* Coding and commiting
* Testing
* `mvn gitflow:hotfix-finish`

In this case, the origin branch is `master`. If I suppose that pom version of `master` is `1.0.1`, a new branch is created with name `hotfix/1.0.2` and the pom version in that branch is changed to `1.0.2-SNAPSHOT`.

When hotfix is implemented, the command to finish is:

```bash
mvn gitflow:hotfix-finish
```

The hotfix branch is merged into master, the master pom version is changed to `1.0.2`.

Also, the master branch is merged into develop and pom version is changed to `1.0.2-SNAPSHOT`

A new tag is created with name `v1.0.2` pointing to `master` HEAD.

### New release

* `mvn gitflow:release-start`
* Testing, amending and commit
* QA if needed
* `mvn gitflow:release-finish`

When a group of features should to be released, a new `release` should to be made.

Suppose that master pom version is `1.4.1`, and development pom version is `1.5.0-SNAPSHOT`.

The command to start the release process is:

```bash
mvn gitflow:release-start
```

A new branch is created from `develop`, with the name: `release/1.5.0`, the pom version for this branch is `1.5.0-SNAPSHOT`.

After test and QA acceptations, the release can be finished:

```bash
mvn gitflow:release-finish
```

The release branch is merged with master, the master pom version is set to `1.5.0`, a new tag is created with name `v1.5.0` pointing to `master` HEAD.

The release branch is merged, also, with develop, and the develop pom version is set to `1.6.0-SNAPSHOT`.

## Summary of pom versioning

### New feature

Only add new feature code to develop!

**Scenario before feature:**

`develop`: `1.5.0-SNAPSHOT`

`master`: `1.4.44`

`tag`: `v1.4.44`

**Scenario after feature**

`develop`: `1.5.0-SNAPSHOT`

`master`: `1.4.44`

`tag`: `v1.4.44`

### New hotfix

Add new hotfix code to master and develop!

**Scenario before hotfix:**

`develop`: `1.6.0-SNAPSHOT`

`master`: `1.5.0`

`tag`: `v1.5.0`

**Scenario after hotfix**

`develop`: `1.6.0-SNAPSHOT`

`master`: `1.5.1`

`tag`: `v1.5.1`

### New release

Put the develop code to master!

**Scenario before release:**

`develop`: `1.5.0-SNAPSHOT`

`master`: `1.4.44`

`tag`: `v1.4.44`

**Scenario after release**

`develop`: `1.6.0-SNAPSHOT`

`master`: `1.5.0`

`tag`: `v1.5.0`