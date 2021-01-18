# albirar-root-dependencies
The root properties, dependencies and builds for all projects.

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

### Deploying Release

The deploying release has some validations at nexus, so no invalid projects are released to MAVEN central.

The steps to release are:

* Deploy to nexus (staging)
* Close the staged repository
* Release the closed repository (if all validations are ok)

After a while (can be 24 hours) the new artifact will be at Maven Central.

Goals to release:

**Deploy**


```bash
mvn -P nexus clean install deploy
```

**Get the staging repository ID**

```bash
mvn -P nexus nexus-staging:rc-list
```

The new stagged repository should to be show, we need the repository ID, the code that appears at first column.

**Try to close**

The process to close the repository make all the validation needed to pass verification rules. If validation isn't pass, the repository remains open.

```bash
mvn -P nexus nexus-staging:rc-close -DstagingRepositoryId=repoId
```

Where `repoId` is the repository id listed before.

If the process ends successfully, the deploying is validated and can be released.

If the process ends with error, the message show the problem to be corrected. Correct it and try to close another time.

**Release the artifact**

Once the repository was successfully closed, the artifact can be released:

```bash
mvn -P nexus nexus-staging:release -DstagingRepositoryId=repoId
```

Where `repoId` is the repository id to release.

If all is OK, the new version of artifact is published at sonatype repositories and, after a while, they be appear on Maven Central.

## Documenting project

Any project that should to publish documentation, should to use the Maven site plugin.

The site will be published with github pages, so as site is for project, the site is published at branch `gh-pages`.





