# api documentation for  [file-stream-rotator (v0.1.0)](https://github.com/holidayextras/file-stream-rotator#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-file-stream-rotator.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-file-stream-rotator) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-file-stream-rotator.svg)](https://travis-ci.org/npmdoc/node-npmdoc-file-stream-rotator)
#### Automated stream rotation

[![NPM](https://nodei.co/npm/file-stream-rotator.png?downloads=true)](https://www.npmjs.com/package/file-stream-rotator)

[![apidoc](https://npmdoc.github.io/node-npmdoc-file-stream-rotator/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-file-stream-rotator_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-file-stream-rotator/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-file-stream-rotator/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-file-stream-rotator/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Roger Castells"
    },
    "bugs": {
        "url": "https://github.com/holidayextras/file-stream-rotator/issues"
    },
    "dependencies": {
        "moment": "^2.11.2"
    },
    "description": "Automated stream rotation",
    "devDependencies": {},
    "directories": {},
    "dist": {
        "shasum": "28669790e0ca270fe6e8ad78b8654671dc90372b",
        "tarball": "https://registry.npmjs.org/file-stream-rotator/-/file-stream-rotator-0.1.0.tgz"
    },
    "gitHead": "de1276ffadf26e23c2d71b115303267fe4f40b3c",
    "homepage": "https://github.com/holidayextras/file-stream-rotator#readme",
    "keywords": [
        "stream",
        "express",
        "restify",
        "connect",
        "rotate",
        "file",
        "minute",
        "hourly",
        "daily",
        "logrotate"
    ],
    "license": "MIT",
    "main": "FileStreamRotator.js",
    "maintainers": [
        {
            "name": "danjenkins",
            "email": "dan.jenkins@holidayextras.com"
        },
        {
            "name": "viktort",
            "email": "viktor.trako@gmail.com"
        },
        {
            "name": "rogerc",
            "email": "rogerc@ataclick.net"
        },
        {
            "name": "joezo",
            "email": "joe.warren@holidayextras.com"
        },
        {
            "name": "pauly",
            "email": "pauly@clarkeology.com"
        },
        {
            "name": "rahulpatel",
            "email": "rahul.patel@holidayextras.com"
        },
        {
            "name": "michaelcarter",
            "email": "mike@mcarter.me"
        },
        {
            "name": "hxmarkterry",
            "email": "mark.terry@holidayextras.com"
        },
        {
            "name": "hxoliverrumbelow",
            "email": "oliver.rumbelow@holidayextras.com"
        },
        {
            "name": "shackpank",
            "email": "npm@olliebuck.com"
        },
        {
            "name": "holidayextras",
            "email": "ollie.buck@holidayextras.com"
        }
    ],
    "name": "file-stream-rotator",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/holidayextras/file-stream-rotator.git"
    },
    "scripts": {
        "test": "node test.js"
    },
    "version": "0.1.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module file-stream-rotator](#apidoc.module.file-stream-rotator)
1.  [function <span class="apidocSignatureSpan">file-stream-rotator.</span>getDate (format, date_format)](#apidoc.element.file-stream-rotator.getDate)
1.  [function <span class="apidocSignatureSpan">file-stream-rotator.</span>getFrequency (frequency)](#apidoc.element.file-stream-rotator.getFrequency)
1.  [function <span class="apidocSignatureSpan">file-stream-rotator.</span>getStream (options)](#apidoc.element.file-stream-rotator.getStream)
1.  [function <span class="apidocSignatureSpan">file-stream-rotator.</span>parseFileSize (size)](#apidoc.element.file-stream-rotator.parseFileSize)



# <a name="apidoc.module.file-stream-rotator"></a>[module file-stream-rotator](#apidoc.module.file-stream-rotator)

#### <a name="apidoc.element.file-stream-rotator.getDate"></a>[function <span class="apidocSignatureSpan">file-stream-rotator.</span>getDate (format, date_format)](#apidoc.element.file-stream-rotator.getDate)
- description and source-code
```javascript
getDate = function (format, date_format) {
    date_format = date_format || DATE_FORMAT;
    if (format && staticFrequency.indexOf(format.type) !== -1) {
        switch (format.type) {
            case 'm':
                var minute = Math.floor(moment().minutes() / format.digit) * format.digit;
                return moment().minutes(minute).format(date_format);
                break;
            case 'h':
                var hour = Math.floor(moment().hour() / format.digit) * format.digit;
                return moment().hour(hour).format(date_format);
                break;
            case 'daily':
            case 'custom':
            case 'test':
                return moment().format(date_format);
        }
    }
    return moment().format(date_format);
}
```
- example usage
```shell
...
    if(moment().format(dateFormat) != moment().add(2,"hours").format(dateFormat) || moment().format(dateFormat) == moment().add(
1,"day").format(dateFormat)){
        console.log("Changing type to custom as date format changes more often than once a day or not every day");
        frequencyMetaData.type = "custom";
    }
}

if (frequencyMetaData) {
    curDate = (options.frequency ? self.getDate(frequencyMetaData,dateFormat) : "");
}

var filename = options.filename;
var oldFile = null;
var logfile = filename + (curDate ? "." + curDate : "");
if(filename.match(/%DATE%/)){
    logfile = filename.replace(/%DATE%/g,(curDate?curDate:self.getDate(null,dateFormat)));
...
```

#### <a name="apidoc.element.file-stream-rotator.getFrequency"></a>[function <span class="apidocSignatureSpan">file-stream-rotator.</span>getFrequency (frequency)](#apidoc.element.file-stream-rotator.getFrequency)
- description and source-code
```javascript
getFrequency = function (frequency) {
    var _f = frequency.toLowerCase().match(/^(\d+)([m|h])$/)
    if(_f){
        return _checkNumAndType(_f[2], parseInt(_f[1]));
    }

    var dailyOrTest = _checkDailyAndTest(frequency);
    if (dailyOrTest) {
        return dailyOrTest;
    }

    return false;
}
```
- example usage
```shell
...

if (!options.filename) {
    console.error("No filename supplied. Defaulting to STDOUT");
    return process.stdout;
}

if (options.frequency) {
    frequencyMetaData = self.getFrequency(options.frequency);
}

var fileSize = null;
var fileCount = 0;
var curSize = 0;
if(options.size){
    fileSize = FileStreamRotator.parseFileSize(options.size);
...
```

#### <a name="apidoc.element.file-stream-rotator.getStream"></a>[function <span class="apidocSignatureSpan">file-stream-rotator.</span>getStream (options)](#apidoc.element.file-stream-rotator.getStream)
- description and source-code
```javascript
getStream = function (options) {
    var frequencyMetaData = null;
    var curDate = null;
    var self = this;

    if (!options.filename) {
        console.error("No filename supplied. Defaulting to STDOUT");
        return process.stdout;
    }

    if (options.frequency) {
        frequencyMetaData = self.getFrequency(options.frequency);
    }

    var fileSize = null;
    var fileCount = 0;
    var curSize = 0;
    if(options.size){
        fileSize = FileStreamRotator.parseFileSize(options.size);
    }

    var dateFormat = (options.date_format || DATE_FORMAT);
    if(frequencyMetaData && frequencyMetaData.type == "daily"){
        if(!options.date_format){
            dateFormat = "YYYY-MM-DD";
        }
        if(moment().format(dateFormat) != moment().add(2,"hours").format(dateFormat) || moment().format(dateFormat) == moment().
add(1,"day").format(dateFormat)){
            console.log("Changing type to custom as date format changes more often than once a day or not every day");
            frequencyMetaData.type = "custom";
        }
    }

    if (frequencyMetaData) {
        curDate = (options.frequency ? self.getDate(frequencyMetaData,dateFormat) : "");
    }

    var filename = options.filename;
    var oldFile = null;
    var logfile = filename + (curDate ? "." + curDate : "");
    if(filename.match(/%DATE%/)){
        logfile = filename.replace(/%DATE%/g,(curDate?curDate:self.getDate(null,dateFormat)));
    }
    var verbose = (options.verbose !== undefined ? options.verbose : true);
    if (verbose) {
        console.log("Logging to", logfile);
    }

    if(fileSize){
        var t_log = logfile;
        var f = null;
        while(f = fs.existsSync(t_log)){
            fileCount++;
            t_log = logfile + "." + fileCount;
        }
        logfile = t_log;
    }

    mkDirForFile(logfile);

    var rotateStream = fs.createWriteStream(logfile, {flags: 'a'});
    if (curDate && frequencyMetaData && (staticFrequency.indexOf(frequencyMetaData.type) > -1)) {
        if (verbose) {
            console.log("Rotating file", frequencyMetaData.type);
        }
        var stream = new EventEmitter();
        stream.end = function(){
            rotateStream.end.apply(rotateStream,arguments);
        };
        BubbleEvents(rotateStream,stream);

        stream.write = (function (str, encoding) {
            var newDate = this.getDate(frequencyMetaData,dateFormat);
            if (newDate != curDate || (fileSize && curSize > fileSize)) {
                var newLogfile = filename + (curDate ? "." + newDate : "");
                if(filename.match(/%DATE%/) && curDate){
                    newLogfile = filename.replace(/%DATE%/g,newDate);
                }

                if(fileSize && curSize > fileSize){
                    fileCount++;
                    newLogfile += "." + fileCount;
                }else{
                    // reset file count
                    fileCount = 0;
                }
                curSize = 0;

                if (verbose) {
                    console.log("Changing logs from %s to %s", logfile, newLogfile);
                }
                curDate = newDate;
                oldFile = logfile;
                logfile = newLogfile;
                rotateStream.destroy();

                mkDirForFile(logfile);

                rotateStream = fs.createWriteStream(newLogfile, {flags: 'a'});
                stream.emit('new',newLogfile);
                stream.emit('rotate',oldFile, newLogfile);
                BubbleEvents(rotateStream,stream);
            }
            rotateStream.write(str, encoding);
            curSize += str.length
        }).bind(this);
        process.nextTick(function(){
            stream.emit('new',logfile);
        })
        return stream;
    } else {
        if (verbose) {
            console.log("File won't be rotated", options.frequency, frequencyMetaData && frequencyMetaData.type);
        }
        process.nextTick(function(){
            rotateStream.emit('new',logfile);
        })
        return rotateStream;
    }
}
```
- example usage
```shell
...
 *   - 'filename'   Filename including full path used by the stream
 *   - 'frequency'  How often to rotate. At present only 'daily' and 'test' are available. 'test' rotates every minute.
 *                  If frequency is set to none of the above, a YYYYMMDD string will be added to the end of the filename.
 *   - 'verbose'    If set, it will log to STDOUT when it rotates files and name of log file. Default is TRUE.
 *
 * To use with Express / Connect, use as below.
 *
 * var rotatingLogStream = require('FileStreamRotator').getStream({filename:"/tmp/test.log", frequency:"daily", verbose: false})
 * app.use(express.logger({stream: rotatingLogStream, format: "default"}));
 *
 * @param {Object} options
 * @return {Object}
 * @api public
 */
var FileStreamRotator = {};
...
```

#### <a name="apidoc.element.file-stream-rotator.parseFileSize"></a>[function <span class="apidocSignatureSpan">file-stream-rotator.</span>parseFileSize (size)](#apidoc.element.file-stream-rotator.parseFileSize)
- description and source-code
```javascript
parseFileSize = function (size) {
    if(size && typeof size == "string"){
        var _s = size.toLowerCase().match(/^((?:0\.)?\d+)([k|m|g])$/);
        if(_s){
            switch(_s[2]){
                case 'k':
                    return _s[1]*1024
                case 'm':
                    return _s[1]*1024*1024
                case 'g':
                    return _s[1]*1024*1024*1024
            }
        }
    }
    return null;
}
```
- example usage
```shell
...
    frequencyMetaData = self.getFrequency(options.frequency);
}

var fileSize = null;
var fileCount = 0;
var curSize = 0;
if(options.size){
    fileSize = FileStreamRotator.parseFileSize(options.size);
}

var dateFormat = (options.date_format || DATE_FORMAT);
if(frequencyMetaData && frequencyMetaData.type == "daily"){
    if(!options.date_format){
        dateFormat = "YYYY-MM-DD";
    }
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
