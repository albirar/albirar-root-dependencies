# albirar-root-dependencies
The root properties, dependencies and builds for all projects

## Workflow and Git

All [Albirar projects](https://albirar.cat "albirar") uses the [Gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow "GitFlow workflow")

This parent pom includes a fully configured [jgit-flow-plugin](https://bitbucket.org/atlassian/jgit-flow/wiki/Home "jgit-flow plugin") to enforce the use of git workflow through maven.

### New feature

* `mvn jgitflow:feature-start`
* Coding and commiting
* Testing
*  `mvn jgitflow:feature-finish`

### New hotfix

* `mvn jgitflow:hotfix-start`
* Coding and commiting
* Testing
*  `mvn jgitflow:hotfix-finish`

### New release

* `mvn jgitflow:release-start`
* Testing, amending and commit
* QA if needed
*  `mvn jgitflow:release-finish`

## Nexus deploying

Nexus deploying enable disposing the projects at Maven Central. The pom contains all the needed to support this tasks.

In all operations, the profile *nexus* should be used:

```bash
mvn -P nexus ...
```

And then any of the available nexus plugin goal:

* Use `deploy` instead of `nexus-staging:deploy`, so any plugin attached to `deploy` phase are executed, included the `nexus-staging:deploy` goal
* `nexus-staging:rc-list` to show the current staged repositories and to get the ID of the current project to deploy
* `nexus-staging:rc-close -DstagingRepositoryId=...`
* `nexus-staging:release -DstagingRepositoryId=...`

### Deploying SNAPSHOT

At any branch that contains SNAPSHOT version of the project, a deploying to nexus:

```bash
mvn -P nexus clean install deploy
```

No further goals of nexus plugin should to be called, because the SNAPSHOT process doesn't need to close or release.