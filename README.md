# quickrepo

[![Build Status](https://travis-ci.com/albertodonato/quickrepo.svg?branch=master)](https://travis-ci.com/albertodonato/quickrepo)

This script provides a quick way to build a Debian repository from a set of
`.deb` or `.changes` files.

The resulting repository tree can be served via HTTP and added as a APT source.


## Get the script

`quickrepo` consists of a single script, which can be downloaded with

```bash
    curl -o quickrepo https://raw.githubusercontent.com/albertodonato/quickrepo/master/quickrepo
    chmod +x quickrepo
```


## Build a repository

The basic way to build a repository for a set of `.deb` is just to run

```bash
    ./quickrepo *.deb
```

This will create the `repo/` directory in the current path, import specified
files, and export necessary release indexes.  Repository architectures and
series match those of the machine the script is run on by default.

It is also possible to pass `.changes` files from a package build, which will
automatically import all files listed in the manifest.

The resulting repository is signed through GPG. You need to have at least one
private GPG key available in your `gpg` configuration.  If more than one key is
available, the desired one can be specified with the `-g GPGKEY` option.


## Usage

Available configuration options are as follows:

```
Usage: quickrepo [options] <files...>

 -a ARCHES     space-separated list of repository arches (default: "source amd64")
 -c CODENAME   value for the repository "Codename" (default: "focal")
 -d REPODIR    create the repository under REPODIR (default: "repo")
 -g GPGKEY     fingerprint of GPG key to use to sign the repository
               (default: default key from GPG config)
 -h            print this help
 -o ORIGIN     value for the repository "Origin" (default: "quickrepo")
 -v            verbose operations
```
