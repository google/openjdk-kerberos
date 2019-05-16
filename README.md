# OpenJDK Kerberos Implementation

A subset of OpenJDK containing an implementation of the Kerberos protocol, built for use on Android.

## NOTE
This is not an officially supported Google product.
It is provided as a way to help other Android developers build products that utilize Kerberos.

## About
The code in this package is an adaptation of the Kerberos implementation from [OpenJDK](https://openjdk.java.net/),
intended for use in Android applications.

## Building
A JAR file suitable for inclusion in Android apps can be built using
[Bazel](https://docs.bazel.build/versions/master/bazel-overview.html).

## Using
For the most part, the standard GSS-API can be used, particularly classes under `org.ietf.jgss`, as well as the `Krb5LoginModule`.

## Local changes
As the Android SDK includes some of the relevant source files, with some
modifications, a few changes have been made to get the code to cleanly
compile and work with an Android app.

### Namespace changes
Relevant classes under `javax.naming` and `javax.security` have been prefixed
with `krb`, so are now under `krb.javax.naming` and `krb.javax.security`.

### Ticket storage
Since the Android SDK does not properly implement a `SecurityManager`,
the `Subject` instance containing the ticket from a Kerberos authentication
cannot be obtained via the implementation of the GSS API.

To address that, a new method has been added to `sun.security.jgss.GSSUtil`,
`setGlobalSubject(Subject subject)`.

This method sets a `Subject` instance that will be used as the context for all GSS
calls.

The caller should take care to clear the global context by setting a `null` subject
after the GSS-related operations have been completed.

## Contributing
The [CONTRIBUTING.md](CONTRIBUTING.md) file contains instructions on how to
submit the Contributor License Agreement before sending any pull requests (PRs).
Of course, if you're new to the project, it's usually best to discuss any
proposals and reach consensus before sending your first PR.

## License
This package retains the OpenJDK original license, which is The GNU General
Public License (GPL) Version 2 with the Classpath Exception. See the
[LICENSE](LICENSE) file.
