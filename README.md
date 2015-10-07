
# Cdnjs-client

Initially it was a client for [cdnjs](https://cdnjs.com/) but it can handle any `GET`'able, publicly-available resource.

## Configuration example:

```json
{
    "cloudflare": {
        "root": "https://cdnjs.cloudflare.com/ajax/libs",
        "relative-location": "src/test/webapp/motive/libs",
        "dependencies": {
            "font-awesome": {
                "version": "4.4.0",
                "css": [
                    "font-awesome.min.css"
                ],
                "fonts": [
                    "fontawesome-webfont.woff",
                    "fontawesome-webfont.woff2",
                    "fontawesome-webfont.eot",
                    "fontawesome-webfont.ttf"
                ]
            },
            "lodash.js": {
                "version": "3.10.1",
                "create-js-dir": false,
                "js": [
                    "lodash.min.js"
                ]
            },
            "moment.js": {
                "version": "2.10.3",
                "create-js-dir": false,
                "js": [
                    "moment.min.js",
                    "moment-with-locales.min.js"
                ]
            },
            "jquery": {
                "version": "2.1.4",
                "create-js-dir": false,
                "js": [
                    "jquery.min.js"
                ]
            },
            "angular.js": {
                "version": "1.3.18",
                "create-js-dir": false,
                "js": [
                    "angular.min.js"
                ]
            },
            "bootstrap-datepicker": {
                "version": "1.4.0",
                "js": [
                    "bootstrap-datepicker.min.js"
                ],
                "css": [
                    "bootstrap-datepicker.min.css"
                ]
            },
            "twitter-bootstrap": {
                "version": "3.3.5",
                "js": [
                    "bootstrap.min.js",
                    "bootstrap.js"
                ],
                "css": [
                    "bootstrap.min.css",
                    "bootstrap.css"
                ],
                "fonts": [
                    "glyphicons-halflings-regular.woff",
                    "glyphicons-halflings-regular.eot",
                    "glyphicons-halflings-regular.ttf",
                    "glyphicons-halflings-regular.woff2"
                ]
            }
        }
    },
    "gists": {
        "root": "https://gist.githubusercontent.com",
        "relative-location": "src/test/webapp/motive/libs",
        "dependencies": {
            "notmasteryet": {
                "url": "https://gist.githubusercontent.com/notmasteryet/1057924/raw/d97b4e2e67918e6a8c778ff11d551f7f6a057ca1/hacks.js",
                "version": "1057924/raw/d97b4e2e67918e6a8c778ff11d551f7f6a057ca1",
                "create-js-dir": false,
                "js": [{
                    "file": "myD.js",
                    "url": "https://gist.githubusercontent.com/matthewbednarski/fadc78a75c3bb1c01d6b/raw/2d2bd13c3acc176f0590efd8739805981074d02c/datepicker-directive.js",
                    "outpath": "directive/test"
                }, {
                    "file": "hacks2.js",
                    "url": "https://sdafvlsjdflgist.githubusercontent.com/notmasteryet/1057924/raw/d97b4e2e67918e6a8c778ff11d551f7f6a057ca1/hacks.js",
                    "outpath": "tsdfasdjh"
                }]
            }
        }
    }
}
```
