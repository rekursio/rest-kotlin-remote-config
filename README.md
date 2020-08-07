# REST Kotlin remote configurations
This project holds all common configuration for any Rekursio REST Kotlin project. Here we define **dependencies** and **project common configurations**.

# Dependencies
Before publishing a new tag is recommended to check all declared dependencies and to upgrade previous dependencies to the most recent version of each library.

To do so there is a sample project that uses all declared dependencies and Gradle plugins and includes a version check plugin

## Check declared dependencies
To check the dependencies are well-defined just build the example project:

`<...>/rest-kotlin-remote-config/example ./gradlew`

If the process ends successfully all declared dependencies and Gradle plugins are correct.

## Check upgrades
To check if there are libraries that can be upgraded just execute the *dependencyUpdates* Gradle task in the example project:

`<...>/rest-kotlin-remote-config/example ./gradlew dependencyUpdates`

The result will show a report with the libraries that can be upgraded

# Apply private files
To apply the dependencies, configurations and flavours in project from a private repository you must import the `private-repos.gradle` file in your project and apply it you your project `build.gradle` file:

`apply from: 'private-repos.gradle'`

if you have the file locally, or you can fetch it using:

`apply from: 'https://raw.githubusercontent.com/rekursio/rest-kotlin-remote-config/main/private-repos.gradle'`

It contains two functions `bitbucket` and `github` to retrieve files from private repositories for each service.
Both functions receive the same parameters:
 
*  `organization`: Repository owner name
*  `repository`: Repository name
*  `file path`: Path inside the repository of the file to retrieve
*  `tag`: Tag or commit reference to retrieve a specific revision of the file

## GitHub
For GitHub private projects, create a personal access token from GitHub and define `PRIVATE_REPOS_GITHUB_ACCESS_TOKEN` value in your `~/.gradle/gradle.proporties` file

```
PRIVATE_REPOS_GITHUB_ACCESS_TOKEN = <access token>
```

## Bitbucket
For Bitbucket, you must define both `PRIVATE_REPOS_BITBUCKET_USERNAME` and `PRIVATE_REPOS_BITBUCKET_PASSWORD` values in your `~/.gradle/gradle.proporties` file

```
PRIVATE_REPOS_BITBUCKET_USERNAME = <email>
PRIVATE_REPOS_BITBUCKET_PASSWORD = <password>
```

Then apply the configuration from Bitbucket private repository:

`apply from: bitbucket('rekursio, 'rest-kotlin-remote-config', <file path>, <tag or commit>)` 




Then apply the configuration from GitHub private repository:

`apply from: github('rekursio, 'rest-kotlin-remote-config', <file path>, <tag or commit>)`

