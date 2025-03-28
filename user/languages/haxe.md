---
title: Build a Haxe Project
layout: en

---


This guide covers build environment and configuration topics specific to
[Haxe](http://haxe.org/) projects. Please make sure to read our
[Onboarding](/user/onboarding/) and
[General Build configuration](/user/customizing-the-build/) guides first.

### Community-Supported Warning

Travis CI support for Haxe is contributed by the community and may be removed
or altered at any time. If you run into any problems, please report them in the
[Travis CI issue tracker](https://github.com/travis-ci/travis-ci/issues/new?labels=haxe)
and cc [@andyli](https://github.com/andyli), [@waneck](https://github.com/waneck), and [@Simn](https://github.com/Simn).

## Test against Haxe versions

Haxe workers on Travis CI download and install the binary of Haxe.
To select one or more versions, use the `haxe:`
key in your `.travis.yml` file, for example:

```yaml
language: haxe
haxe:
  - "3.2.1"
  - stable      # the latest stable release defined in https://haxe.org/download/list/
  - development # the latest build of the development branch in http://build.haxe.org/
```
{: data-file=".travis.yml"}

## Default Haxe Version

If you leave the `haxe:` key out of your `.travis.yml`, Travis CI will use `stable`, which is
the latest stable release defined in the [haxe.org download list](https://haxe.org/download/list/).

## Default Neko Version

By default, [Neko](http://nekovm.org/) 2.3.0 will also be downloaded and installed.
Use the `neko:` key in your `.travis.yml` file to specify a different Neko version,
for example:

```yaml
language: haxe
neko: "2.0.0"
```
{: data-file=".travis.yml"}

However, unlike `haxe:`, you can provide only one value (not an array) to `neko:`.

## Test Configuration

If your project makes use of the standard hxml files for building, you can specify
the list of hxml files using the `hxml:` key, for example:

```yaml
language: haxe
hxml:
  - build.hxml
```
{: data-file=".travis.yml"}

In the *install* phase, the worker will run `yes | haxelib install $hxml` for
each of the provided values. Similarly, in the *script* (test) phase,
the worker will run `haxe $hxml` for each of the provided values.

You can replace the default *install* and *script* behavior by using the
`install:` and `script:` keys, respectively, as described
in the [general build configuration](/user/customizing-the-build/) guide.

## Build Matrix

For Haxe projects, `env:` and `haxe:` can be given as arrays
to construct a build matrix.

## Environment Variable

The versions of Haxe and Neko a job is using are available as:

```
TRAVIS_HAXE_VERSION
TRAVIS_NEKO_VERSION
```

## Build Config Reference

You can find more information on the build config format for [Haxe](https://config.travis-ci.com/ref/language/haxe) in our [Travis CI Build Config Reference](https://config.travis-ci.com/).
