# Apache HTTP Server Cloud Native Buildpack

## Integration

The Apache HTTPD CNB provides httpd as a dependency. Downstream buildpacks, like
[php-web](https://github.com/paketo-buildpacks/php-web) can require the httpd
dependency by generating a [Build Plan
TOML](https://github.com/buildpacks/spec/blob/master/buildpack.md#build-plan-toml)
file that looks like the following:

```toml
[[requires]]

  # The name of the Apache HTTPD dependency is "httpd". This value is considered
  # part of the public API for the buildpack and will not change without a plan
  # for deprecation.
  name = "httpd"

  # The version of the Apache HTTPD dependency is not required. In the case it
  # is not specified, the buildpack will provide the newest version, which can
  # be seen in the buildpack.toml file.
  # If you wish to request a specific version, the buildpack supports
  # specifying a semver constraint in the form of "2.*", "2.4.*", or even
  # "2.4.43".
  version = "2.4.43"

  # The Apache HTTPD buildpack supports some non-required metadata options.
  [requires.metadata]

    # Setting the launch flag to true will ensure that the Apache HTTPD
    # dependency is available on the $PATH for the running application. If you
    # are writing an application that needs to run Apache HTTPD at runtime, this
    # flag should be set to true.
    launch = true
```

## Usage

To package this buildpack for consumption:

```
$ ./scripts/package.sh
```

This builds the buildpack's Go source using `GOOS=linux` by default. You can supply another value as the first argument to `package.sh`.
