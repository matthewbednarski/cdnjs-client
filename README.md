
# Cdnjs-client

**Cdnjs-client** is a minimal substitute for [Bower](http://bower.io/) in a [node](https://nodejs.org/en/) free environment. It depends on [bash](https://www.gnu.org/software/bash/), [jq](https://stedolan.github.io/jq/) and [curl](http://curl.haxx.se/).

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
