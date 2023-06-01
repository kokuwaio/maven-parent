# Maven Parent

[![License](https://img.shields.io/github/license/kokuwaio/maven-parent.svg?label=License)](https://github.com/kokuwaio/maven-parent/blob/main/LICENSE)
[![Maven Central](https://img.shields.io/maven-central/v/io.kokuwa.maven/maven-parent.svg?label=Maven%20Central)](https://central.sonatype.com/namespace/io.kokuwa.maven)
[![CI](https://img.shields.io/github/actions/workflow/status/kokuwaio/maven-parent/ci.yaml?branch=main&label=CI)](https://github.com/kokuwaio/maven-parent/actions/workflows/ci.yaml?query=branch%3Amain)

## Goal

Provide a `pom.xml` with [intelligent defaults](https://en.wikipedia.org/wiki/Convention_over_configuration) for projects of Kokuwa.io project.
The default maven configuration is still based on [Java 5](https://maven.apache.org/plugins/maven-compiler-plugin/compile-mojo.html#source) and platform dependent builds.

## KeyFacts

* java 11 (lts version)
* [junit jupiter](http://junit.org/junit5/docs/current/user-guide/) (junit 4 is [still supported](http://junit.org/junit5/docs/current/user-guide/#running-tests-junit-platform-runner) for legacy projects)
* Sonatype distribution repositories enabled
* fixed versions for common plugins (org.apache.maven.plugins & org.codehaus.mojo)
* default configurations, e.g. java 11, junit 5 provider
* configured maven reports and site

## Usage

Just add the following code to your `pom.xml` and insert the version:

```xml
<parent>
 <groupId>io.kokuwa</groupId>
 <artifactId>maven-parent</artifactId>
 <version>${version}</version>
 <relativePath />
</parent>
```

For deployment and release build add the following lines to your `pom.xml` and replace the variables with your values:

```xml
<url>https://github.com/kokuwaio/{repository}</url>
<scm>
 <url>https://github.com/kokuwaio/{repository}</url>
 <connection>scm:git:https://github.com/kokuwaio/{repository}.git</connection>
 <developerConnection>scm:git:https://github.com/kokuwaio/{repository}.git</developerConnection>
 <tag>HEAD</tag>
</scm>
```

## Profiles

**check** (enabled by default):

* use [tidy-maven-plugin](http://www.mojohaus.org/tidy-maven-plugin/) to check pom structure
* enforce correct java version (accepts all versions equal or above property **maven.compiler.source**)
* enforce checkstyle rules

**site**: (enabled if env.CI is present)

* test instrumentation with jacoco for recording test coverage
* configures site deployment to [github.com/kokuwaio/maven-sites](https://github.com/kokuwaio/maven-sites)

**deploy**: (enabled if env.CI is present)

* add source jar
* add javadoc jar
* use [flatten-maven-plugin](http://www.mojohaus.org/tidy-maven-plugin/) to simplify pom

**deploy** with **release** (match Sonatype [requirements](https://central.sonatype.org/pages/requirements.html)):

* add source jar
* add javadoc jar
* use [flatten-maven-plugin](http://www.mojohaus.org/tidy-maven-plugin/) to simplify pom
* sign packages with gpg
* deploy to [oss.sonatype.org](https://oss.sonatype.org)
