
# Cdnjs Client

**cdnjs** is a minimalist substitute for [bower](http://bower.io/) in a [node](https://nodejs.org/en/) free environment. It depends on [bash](https://www.gnu.org/software/bash/), [jq](https://stedolan.github.io/jq/) and [curl](http://curl.haxx.se/).

Initially it was a client for [cdnjs](https://cdnjs.com/) but it can handle any `GET`'able, publicly-available resources. 

## Commands

### Usage

To print the script's usage:

```sh
$ cdnjs --help
```
Which gives the following output:

```sh
$ cdnjs --help
Usage: cdnjs [OPTIONS] [ARGS]:

    Options:
    --init, init                     initialize a config file
    --conf [CONFIG FILE]             use a custom config file
    --list, list   [/to/exclude]     prints a list of link and script tags
    --index, index [/to/exclude]     same as "--list"
    --html, html   [/to/exclude]     same as "--list"

    --nodev, nodev                   excludes non '.min.*' files; a flag for \"--list\"
    --dev, dev                       excludes '.min.*' files; a flag for \"--list\"

    -f, --find, find [ARGS]          perform query on api.cdnjs.com
        --search, search [ARGS]      same as "--search [ARGS]"
    -c, --clean, clean [ARGS]        clean configured relative-location
    -s, --sync, sync [ARGS]          syncronize to configured relative-locations
        --update, update [ARGS]      same as "--sync [ARGS]"
    -a, + [LIB[+VERSION]] [GROUP]    add library with optional version to optional
        --add, add                    group

    -v, --verbose, verbose           print debug/verbose output
        --debug, debug               same as "--verbose"
        --nocolor, nocolor           don't echo in color, useful for logging stdout/stderr
    -h, -?, --help, help             print usage
```


### Init

To initialize a cdnjs configuration file at the default location `$(pwd)/.cdnjs`:

```sh
$ cdnjs init
```

To specify another location to initialize:

```sh
$ cdnjs --conf .another-cdnjs.conf init
```

To initialize a non-default configuration file in another directory: 

```sh
$ cdnjs --conf ~/dir/to/create/.cdnjs init
```
NB. if the `path` of the file doesn't exist the script will attempt to create it.


### Search/Find

Requires a parameter `"search string"`.

To search for libraries containing `jquery`:

```sh
$ cdnjs search jquery
```

### Add

This command requires a parameter `library` with an optional suffix `+version`.

To add the latest version of `jquery` to your configuration:

```sh
$ cdnjs add jquery
```
To add a specific version of `jquery` to your configuration use the syntax `library[+version]`

```sh
$ cdnjs add jquery+1.9.0
```

### Clean

To clean all the paths indicated by the configuration's `relative-location`:

```sh
$ cdnjs clean
```

### Sync/Update

To download the resources indicated by the current configuration:

```sh
$ cdnjs sync 
```
NB. the resources will be downloaded to a *tmp* directory and then moved to the configuration's `relative-location`'s.


## Flags

There are a few *flags* for modifying output or functionality.

Some are *general* and can be used with any command, such as `--conf`, `--debug` or `--nocolor`.

Others can be used only with *specific* commands, such as the `list` command's `--dev` and `--nodev` flags.

### Conf

Any command that requires the use of a configuration file can use the *flag* `--conf` to indicate an alternate file.

The commands which require a configuration file are `--init`, `--add`, `--clean` and `--sync`.

The default configuration file, if `--conf` is not specified, is `.cdnjs` in the current working directory.

To initialize a non-default configuration file in the current working directory:

```sh
$ cdnjs --conf .another-cdnjs.conf init
```

To add `jquery` version `2.1.4` to a non-default configuration:

```sh
$ cdnjs --conf .another-cdnjs.conf --add jquery+2.1.4
```

### Debug/Verbose

To output `debug` messages add the `-v` flag to any command:

```sh
$ cdnjs sync -v
# or
$ cdnjs clean --verbose
# or
$ cdnjs clean --debug
# or
$ cdnjs clean verbose
# or
$ cdnjs clean debug
```

### No Color

To not output *color* escape codes add the `nocolor` flag.  This is helpful when you want to log `stdout/stderr` to file.

```sh
$cdnjs sync nocolor
```


### Dev

A flag for the `--list` command, it excludes any `min.js` or `min.css` from its output.

```sh
$ cdnjs list --dev
```

### No-Dev

A flag for the `--list` command, it excludes any library not ending in `min.js` or `min.css` from its output.

```sh
$ cdnjs list --nodev
# or
$ cdnjs list nodev
```


## Configuration example:

An example configuration file is found in this repository at [example/.cdnjs](https://raw.githubusercontent.com/matthewbednarski/cdnjs-client/master/example/.cdnjs).

A file `.cdnjs` in the `pwd` or passed to the program through the `--conf [conf-file]` option.

## Setup

`cdnjs` depends on `bash`, `jq`, `curl` and `mktemp`.  If those dependencies are met and and `cdnjs` is on your `$PATH` everything should be fine.


## Windows Setup

Since `cdnjs` is a `bash` script it will work in a bash environment such as [Git for Windows](https://git-for-windows.github.io/), however it requires `jq` and `mktemp` ( not found in `Git for Windows` pre version `1.9.5`).

### Download Jq

[Download the `jq` binary](https://stedolan.github.io/jq/download/) and rename it to `jq.exe`. Place it in a folder known to be on your `$PATH`, eg. if you are using `Git for Windows` version `2.6.1` you will have `%PROGRAMFILES%\Git\usr\bin` in which you can place the `jq.exe` binary.

### Download cdnjs

Download the [latest version of cdnjs](https://raw.githubusercontent.com/matthewbednarski/cdnjs/master/cdnjs). Save it to a folder on you `$PATH` and make it executable.

### Windows Setup Example Steps:

1. Edit `.bashrc`:

```sh
...
if [ -d "~/bin" ]; then
  export PATH=$PATH:~/bin
fi
...
```

2. Then perform the following commands:

```sh
if [ ! -d "~/bin" ]; then mkdir "~/bin"; fi
cd ~/bin
wget https://raw.githubusercontent.com/matthewbednarski/cdnjs/master/cdnjs
chmod +x cdnjs
wget https://github.com/stedolan/jq/releases/download/jq-1.5/jq-win64.exe
mv jq-win64.exe jq.exe
chmod +x jq.exe
ls -al
```

## Todo

 + allow partial `clean`'s and `sync`'s by section key (ie `cdnjs` or `gists` )
