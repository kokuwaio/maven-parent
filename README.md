# Maven Parent

## Goal

Provide a `pom.xml` with [intelligent defaults](https://en.wikipedia.org/wiki/Convention_over_configuration) for projects of Kokuwa project.
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
<inceptionYear>2020</inceptionYear>
<scm>
	<url>https://github.com/kokuwaio/{repository}</url>
	<connection>scm:git:https://github.com/kokuwaio/{repository}.git</connection>
	<developerConnection>scm:git:https://github.com/kokuwaio/{repository}.git</developerConnection>
	<tag>HEAD</tag>
</scm>
<issueManagement>
	<system>github</system>
	<url>https://github.com/kokuwaio/{repository}/issues</url>
</issueManagement>
```

## Profiles

**release** (match Sonatype [requirements](https://central.sonatype.org/pages/requirements.html)):

 * add source jar (no javadoc, no test-sources)
 * sign packages with gpg
 * test instrumentation with jacoco for recording test coverage
 * use [tidy-maven-plugin](http://www.mojohaus.org/tidy-maven-plugin/) to check pom structure
 * enforce correct java version (accepts all versions equal or above property **maven.compiler.source**)

## Version updates

Display dependency updates:
```
mvn versions:display-property-updates -U
```

Update dependencies:
```
mvn versions:update-properties -DgenerateBackupPoms=false
```

Or build site:
```
mvn site
firefox target/site/index.html
```