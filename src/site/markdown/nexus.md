# Nexus deploying

Nexus deploying enable disposing the projects at Maven Central. The pom contains all the needed to support this tasks.

<u>In all operations, the profile *nexus* should be used:</u>

```bash
mvn -P nexus ...
```

And then any of the available nexus plugin goal:

* Use `deploy` instead of `nexus-staging:deploy`, so any plugin attached to `deploy` phase are executed, included the `nexus-staging:deploy` goal
* `nexus-staging:rc-list` to show the current staged repositories and to get the ID of the current project to deploy
* `nexus-staging:rc-close -DstagingRepositoryId=...`
* `nexus-staging:release -DstagingRepositoryId=...`

## Deploying SNAPSHOT

At any branch that contains SNAPSHOT version of the project, a deploying to nexus:

```bash
mvn -P nexus clean install deploy
```

No further goals of nexus plugin should to be called, because the SNAPSHOT process doesn't need to close or release.

## Deploying Release

The deploying release has some validations at nexus, so no invalid projects are released to MAVEN central.

The process is divided in some steps:

1. Deploy to nexus (staging)
2. Close the staged repository
3. Release the closed repository (if all validations are ok)

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
