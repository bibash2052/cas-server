CAS Overlay Template [![Build Status](https://travis-ci.org/apereo/cas-overlay-template.svg?branch=master)](https://travis-ci.org/apereo/cas-overlay-template)
=======================

Generic CAS WAR overlay to exercise the latest versions of CAS. This overlay could be freely used as a starting template for local CAS war overlays.

# Versions

- CAS `6.4.x`
- JDK `11`

# Overview

To build the project, use:

```bash
# Use --refresh-dependencies to force-update SNAPSHOT versions
./gradlew[.bat] clean build
```

# Configuration

- The `etc` directory contains the configuration files and directories that need to be copied to `/etc/cas/config`.

```bash
./gradlew[.bat] copyCasConfiguration
```

- The specifics of the build are controlled using the `gradle.properties` file.

## Adding Modules

CAS modules may be specified under the `dependencies` block of the [Gradle build script](build.gradle):

```gradle
dependencies {
    implmentation "org.apereo.cas:cas-server-some-module:${project.casVersion}"
    ...
}
```

To collect the list of all project modules and dependencies:

```bash
./gradlew[.bat] allDependencies
```

You could also add modules and dependencies dynamically on the fly using the `casModules` project property. For example, to include support for OpenID Connect and Duo Security, you could invoke the build using `-PcasModules=oidc,duo` and have it auto-include modules that provide requested functionality. Needless, to say, you will need to know the module name beforehand.

### Clear Gradle Cache

If you need to, on Linux/Unix systems, you can delete all the existing artifacts (artifacts and metadata) Gradle has downloaded using:

```bash
# Only do this when absolutely necessary
rm -rf $HOME/.gradle/caches/
```

Same strategy applies to Windows too, provided you switch `$HOME` to its equivalent in the above command.

# Deployment

- Create a keystore file `thekeystore` under `/etc/cas`. Use the password `changeit` for both the keystore and the key/certificate entries. This can either be done using the JDK's `keytool` utility or via the following command:

```bash
./gradlew[.bat] createKeystore
```

- Ensure the keystore is loaded up with keys and certificates of the server.

On a successful deployment via the following methods, CAS will be available at:

* `https://cas.server.name:8443/cas`

## Executable WAR

Run the CAS web application as an executable WAR:

```bash
./gradlew[.bat] run
```

Debug the CAS web application as an executable WAR:

```bash
./gradlew[.bat] debug
```
##Connecting to database

To connect to database change the cas.properties file inside {project_root}/etc/cas/config location.

For this demo, PostgresSQL is used. Feel free to use any other database.

##CAS-CLIENT
Link to cas-client: https://github.com/bibash2052/cas-client