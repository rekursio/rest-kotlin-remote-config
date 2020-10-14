# GitHub Packages

Here you can find all the configuration needed to publish and consume packages from GitHub packages repository.

## Publishing a package to GitHub Packages

To publish a package first create a `library-configuration.gradle` file with the following configuration:

```groovy
ext {
    github_owner = <GitHub project owner>
    github_project = <GitHub project name>

    version_major = x
    version_minor = x
    version_patch = x

    version_name = "${version_major}.${version_minor}.${version_patch}-SNAPSHOT"
}
``` 

Then add the next configuration to your project `build.gradle` file

```groovy
buildscript {
    apply from: 'library-configuration.gradle'
    apply from: 'https://raw.githubusercontent.com/rekursio/rest-kotlin-remote-config/github-packages/publisher.gradle'

    ...
}

plugins {
    ... // Other plugins already configured
    id 'maven-publish'
}

...
```

Finally, to publish a package just execute the `publish` Gradle task

## Publishing a package with GitHub Actions

Configure the project as specified in the previous section and just import the Action configuration file found in 
`github-packages/workflow/github-packages-publish.yml`. Then, each time you create a release in your project, the
GitHub Action will be triggered, and a new package will be published.

Ensure you have updated the library version info with the proper version value, or the script will fail it a package
for the previous version already exists.

## Consuming a package from GitHub Packages

Add the next configuration to your project `build.gradle` file

```groovy
buildscript {
    apply from: 'https://raw.githubusercontent.com/rekursio/rest-kotlin-remote-config/github-packages/consumer.gradle'

    ...
}

...
```

Then just declare the dependencies in your module `build.gradle` files.