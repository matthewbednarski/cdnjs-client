
# Cdnjs-client

**Cdnjs-client** is a minimal substitute for [bower](http://bower.io/) in a [node](https://nodejs.org/en/) free environment. It depends on [bash](https://www.gnu.org/software/bash/), [jq](https://stedolan.github.io/jq/) and [curl](http://curl.haxx.se/).

Initially it was a client for [cdnjs](https://cdnjs.com/) but it can handle any `GET`'able, publicly-available resources. 

```sh
$ cdnjs-client --help
Usage: cdnjs-client [OPTIONS] [ARGS]:

    Options:
    --conf [CONFIG FILE]            use a custom config file

    -f, --find, find [ARGS]         perform query on api.cdnjs.com
        --search, search [ARGS]     same as "--search [ARGS]"

    -c, --clean, clean [ARGS]       clean configured relative-location
    -s, --sync, sync [ARGS]         syncronize to configured relative-locations
    -a, + [LIB[+VERSION]] [GROUP]   add library with optional version to optional
        --add, add                   group

    -v, --verbose, verbose          print debug/verbose output
        --debug, debug              same as "--verbose"
    -h, -?, --help, help            print usage
```

## Configuration example:

a file `.cdnjs` in the `pwd` or passed to the program through the `--conf [conf-file]` option.

```json
{
    "cloudflare": {
        "root": "https://cdnjs.cloudflare.com/ajax/libs",
        "relative-location": "src/test/webapp/motive/libs",
        "dependencies": {
            "font-awesome": {
                "version": "4.4.0",
                "files": [
                    "css/font-awesome.min.css",
                    "fonts/fontawesome-webfont.woff",
                    "fonts/fontawesome-webfont.woff2",
                    "fonts/fontawesome-webfont.eot",
                    "fonts/fontawesome-webfont.ttf"
                ]
            },
            "lodash.js": {
                "version": "3.10.1",
                "files": [
                    "lodash.min.js"
                ]
            },
            "moment.js": {
                "version": "2.10.3",
                "files": [
                    "moment.min.js",
                    "moment-with-locales.min.js"
                ]
            },
            "jquery": {
                "version": "2.1.4",
                "files": [
                    "jquery.min.js"
                ]
            },
            "angular.js": {
                "version": "1.3.18",
                "files": [
                    "angular.min.js"
                ]
            },
            "bootstrap-datepicker": {
                "version": "1.4.0",
                "files": [
                    "js/bootstrap-datepicker.min.js",
                    "css/bootstrap-datepicker.min.css"
                ]
            },
            "twitter-bootstrap": {
                "version": "3.3.5",
                "js": [
                    "js/bootstrap.min.js",
                    "js/bootstrap.js",
                    "css/bootstrap.min.css",
                    "css/bootstrap.css",
                    "fonts/glyphicons-halflings-regular.woff",
                    "fonts/glyphicons-halflings-regular.eot",
                    "fonts/glyphicons-halflings-regular.ttf",
                    "fonts/glyphicons-halflings-regular.woff2"
                ]
            }
        }
    },
    "gists": {
        "root": "https://gist.githubusercontent.com",
        "relative-location": "src/test/webapp/motive/libs",
        "dependencies": {
            "pouchdb-service": {
                "files": [{
                    "file": "pouchdb-service.js",
                    "url": "https://gist.githubusercontent.com/matthewbednarski/5dd19e501409c386fa92/raw/7e69b3f34fc715f2c8101694ee54f69bdac98c51/pouchdb-service.js",
                    "outpath": "custom"
                }]
            }
        }
    }
}
```
## Setup

`cdnjs-client` depends on `bash`, `jq`, `curl` and `mktemp`.  If those dependencies are met and and `cdnjs` is on your `$PATH` everything should be fine.


## Windows Setup

Since `cdnjs-client` is a `bash` script it will work in a bash environment such as [Git for Windows](https://git-for-windows.github.io/), however it requires `jq` and `mktemp` ( not found in `Git for Windows` pre version `1.9.5`).

### Download Jq

[Download the `jq` binary](https://stedolan.github.io/jq/download/) and rename it to `jq.exe`. Place it in a folder known to be on your `$PATH`, eg. if you are using `Git for Windows` version `2.6.1` you will have `%PROGRAMFILES%\Git\usr\bin` in which you can place the `jq.exe` binary.

### Download Cdnjs-client

Download the [latest version of cdnjs](https://raw.githubusercontent.com/matthewbednarski/cdnjs-client/master/cdnjs). Save it to a folder on you `$PATH` and make it executable.

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
$ if [ ! -d "~/bin" ]; then mkdir "~/bin"; fi
$ cd ~/bin
$ wget https://raw.githubusercontent.com/matthewbednarski/cdnjs-client/master/cdnjs
$ chmod +x cdnjs
$ wget https://github.com/stedolan/jq/releases/download/jq-1.5/jq-win64.exe
$ mv jq-win64.exe jq.exe
$ chmod +x jq.exe
$ ls -al
```

## Todo

 + add an `init` command
 + allow partial `clean`'s and `sync`'s by section key (ie `cdnjs` or `gists` )
