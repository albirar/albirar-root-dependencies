# Workflow and Git

All [Albirar projects](https://albirar.cat "albirar") uses the [Gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow "GitFlow workflow") as strategy to manage the development process.

This parent pom includes a fully configured [jgit-flow-plugin](https://bitbucket.org/atlassian/jgit-flow/wiki/Home "jgit-flow plugin") to enforce the use of git workflow through maven.

## New feature

* `mvn jgitflow:feature-start`
* Coding and commiting
* Testing
* `mvn jgitflow:feature-finish`

## New hotfix

* `mvn jgitflow:hotfix-start`
* Coding and commiting
* Testing
* `mvn jgitflow:hotfix-finish`

## New release

* `mvn jgitflow:release-start`
* Testing, amending and commit
* QA if needed
* `mvn jgitflow:release-finish`

