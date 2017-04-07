# api documentation for  [smtp-protocol (v2.4.7)](https://github.com/substack/node-smtp-protocol#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-smtp-protocol.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-smtp-protocol) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-smtp-protocol.svg)](https://travis-ci.org/npmdoc/node-npmdoc-smtp-protocol)
#### implements the smtp protocol for clients and servers

[![NPM](https://nodei.co/npm/smtp-protocol.png?downloads=true)](https://www.npmjs.com/package/smtp-protocol)

[![apidoc](https://npmdoc.github.io/node-npmdoc-smtp-protocol/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-smtp-protocol_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-smtp-protocol/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-smtp-protocol/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-smtp-protocol/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "James Halliday",
        "email": "mail@substack.net",
        "url": "http://substack.net"
    },
    "bugs": {
        "url": "https://github.com/substack/node-smtp-protocol/issues"
    },
    "dependencies": {
        "shallow-copy": "~0.0.1",
        "stream-combiner": "~0.0.2",
        "through": "^2.3.4",
        "through2": "^1.0.0"
    },
    "description": "implements the smtp protocol for clients and servers",
    "devDependencies": {
        "chunky": "~0.0.0",
        "concat-stream": "~1.2.0",
        "seq": "0.3.x",
        "split": "~0.2.10",
        "tap": "~0.4.4"
    },
    "directories": {
        "lib": ".",
        "example": "example",
        "test": "test"
    },
    "dist": {
        "shasum": "9900005e3d77f0c8338ab01de62b25bd3adfda83",
        "tarball": "https://registry.npmjs.org/smtp-protocol/-/smtp-protocol-2.4.7.tgz"
    },
    "gitHead": "7fb45429c96245a501555d9b269f4a8a4097f785",
    "homepage": "https://github.com/substack/node-smtp-protocol#readme",
    "keywords": [
        "email",
        "mail",
        "smtp",
        "client",
        "server"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "substack",
            "email": "mail@substack.net"
        }
    ],
    "name": "smtp-protocol",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/substack/node-smtp-protocol.git"
    },
    "scripts": {
        "test": "tap test/*.js"
    },
    "version": "2.4.7"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module smtp-protocol](#apidoc.module.smtp-protocol)
1.  [function <span class="apidocSignatureSpan">smtp-protocol.</span>connect ()](#apidoc.element.smtp-protocol.connect)
1.  [function <span class="apidocSignatureSpan">smtp-protocol.</span>createServer (opts, cb)](#apidoc.element.smtp-protocol.createServer)
1.  object <span class="apidocSignatureSpan">smtp-protocol.</span>dot
1.  object <span class="apidocSignatureSpan">smtp-protocol.</span>parse_data
1.  object <span class="apidocSignatureSpan">smtp-protocol.</span>protocol

#### [module smtp-protocol.dot](#apidoc.module.smtp-protocol.dot)
1.  [function <span class="apidocSignatureSpan">smtp-protocol.</span>dot (source)](#apidoc.element.smtp-protocol.dot.dot)
1.  [function <span class="apidocSignatureSpan">smtp-protocol.dot.</span>undot (target)](#apidoc.element.smtp-protocol.dot.undot)

#### [module smtp-protocol.parse_data](#apidoc.module.smtp-protocol.parse_data)
1.  [function <span class="apidocSignatureSpan">smtp-protocol.parse_data.</span>getBytes (n, target)](#apidoc.element.smtp-protocol.parse_data.getBytes)
1.  [function <span class="apidocSignatureSpan">smtp-protocol.parse_data.</span>getCommand (cb)](#apidoc.element.smtp-protocol.parse_data.getCommand)
1.  [function <span class="apidocSignatureSpan">smtp-protocol.parse_data.</span>getLine (cb)](#apidoc.element.smtp-protocol.parse_data.getLine)
1.  [function <span class="apidocSignatureSpan">smtp-protocol.parse_data.</span>getUntil (terminal, target)](#apidoc.element.smtp-protocol.parse_data.getUntil)
1.  [function <span class="apidocSignatureSpan">smtp-protocol.parse_data.</span>parseData (cb)](#apidoc.element.smtp-protocol.parse_data.parseData)
1.  [function <span class="apidocSignatureSpan">smtp-protocol.parse_data.</span>parseLines (cb)](#apidoc.element.smtp-protocol.parse_data.parseLines)

#### [module smtp-protocol.protocol](#apidoc.module.smtp-protocol.protocol)
1.  [function <span class="apidocSignatureSpan">smtp-protocol.protocol.</span>client (opts, stream)](#apidoc.element.smtp-protocol.protocol.client)
1.  [function <span class="apidocSignatureSpan">smtp-protocol.protocol.</span>server (stream)](#apidoc.element.smtp-protocol.protocol.server)



# <a name="apidoc.module.smtp-protocol"></a>[module smtp-protocol](#apidoc.module.smtp-protocol)

#### <a name="apidoc.element.smtp-protocol.connect"></a>[function <span class="apidocSignatureSpan">smtp-protocol.</span>connect ()](#apidoc.element.smtp-protocol.connect)
- description and source-code
```javascript
connect = function () {
    var args = [].slice.call(arguments).reduce(function (acc, arg) {
        acc[typeof arg] = arg;
        return acc;
    }, {});

    var stream;
    var cb = args.function;
    var options = args.object || {};

    var tlsOpts = options.tls;
    options.port = args.number || 25;
    options.host = args.string || 'localhost';

    if (args.string && args.string.match(/^[.\/]/)) {
        // unix socket
        stream = net.createConnection(args.string);
    }
    else if (tlsOpts) {
        stream = tls.connect(options.port, options.host, tlsOpts, function () {
            var pending = stream.listeners('secure').length;
            var allOk = true;
            if (pending === 0 && !stream.authorized
            && tlsOpts.rejectUnauthorized !== false) {
                allOk = false;
            }
            if (pending === 0) return done()

            var ack = {
                accept : function (ok) {
                    allOk = allOk && (ok !== false);
                    if (--pending === 0) done();
                },
                reject : function () {
                    allOk = false;
                    if (--pending === 0) done();
                }
            };
            stream.emit('secure', ack);

            function done () {
                if (!allOk) {
                    stream.end();
                    stream.emit('error', new Error(stream.authorizationError));
                }
                else cb(proto.server(stream));
            }
        });
    }
    else if (options.stream) {
        cb(proto.server(options.stream));
    }
    else {
        stream = net.connect(options);
        stream.on('connect', function () {
            cb(proto.server(stream));
        });
    }

    return stream;
}
```
- example usage
```shell
...
    //write(503, 'Bad sequence: already using TLS.');
    return next();
}
clienttls = true;

var tserver = tls.createServer(opts);
tserver.listen(0, '127.0.0.1', function () {
    var s = net.connect(tserver.address().port, '127.0.0.1');
    s.on('error', function (err) { stream.end() });
    s.pipe(stream).pipe(s);
    write(220, 'Ready to start TLS.');
});

var index = 0;
tserver.on('secureConnection', function (sec) {
...
```

#### <a name="apidoc.element.smtp-protocol.createServer"></a>[function <span class="apidocSignatureSpan">smtp-protocol.</span>createServer (opts, cb)](#apidoc.element.smtp-protocol.createServer)
- description and source-code
```javascript
createServer = function (opts, cb) {
    if (typeof opts === 'string') {
        opts = { domain: opts };
    }
    if (typeof opts === 'function') {
        cb = opts;
        opts = {};;
    }
    if (!opts) opts = {};
    var istls = Boolean(opts.tls);
    var tnet = istls ? tls : net;

    return tnet.createServer(opts, function (stream) {
        var req = proto.client(opts, stream);
        var clienttls = istls;

        req.on('error', function () {});
        stream.on('error', function (err) {});

        req.on('_tlsNext', function (write, next) {
            if (clienttls) {
                write(220, 'Already using TLS?');
                //write(503, 'Bad sequence: already using TLS.');
                return next();
            }
            clienttls = true;

            var tserver = tls.createServer(opts);
            tserver.listen(0, '127.0.0.1', function () {
                var s = net.connect(tserver.address().port, '127.0.0.1');
                s.on('error', function (err) { stream.end() });
                s.pipe(stream).pipe(s);
                write(220, 'Ready to start TLS.');
            });

            var index = 0;
            tserver.on('secureConnection', function (sec) {
                if (index ++ > 0) return sec.end();
                req._swapStream(sec);
                req.emit('tls', sec);
            });
            stream.on('close', function () {
                tserver.close();
            });
        });
        cb(req);
    });
}
```
- example usage
```shell
...
    cb = opts;
    opts = {};;
}
if (!opts) opts = {};
var istls = Boolean(opts.tls);
var tnet = istls ? tls : net;

return tnet.createServer(opts, function (stream) {
    var req = proto.client(opts, stream);
    var clienttls = istls;

    req.on('error', function () {});
    stream.on('error', function (err) {});

    req.on('_tlsNext', function (write, next) {
...
```



# <a name="apidoc.module.smtp-protocol.dot"></a>[module smtp-protocol.dot](#apidoc.module.smtp-protocol.dot)

#### <a name="apidoc.element.smtp-protocol.dot.dot"></a>[function <span class="apidocSignatureSpan">smtp-protocol.</span>dot (source)](#apidoc.element.smtp-protocol.dot.dot)
- description and source-code
```javascript
dot = function (source) {
    var first = true;
    var dot = through(function (buf) {
        var data = buf.toString();
        var s = first
            ? data.replace(/(^|\n)\./g, '$1..')
            : data.replace(/\n\./g, '\n..')
        ;
        first = data.charCodeAt(data.length - 1) === 10;
        this.queue(s);
    });
    source.pipe(dot);
    return dot;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.smtp-protocol.dot.undot"></a>[function <span class="apidocSignatureSpan">smtp-protocol.dot.</span>undot (target)](#apidoc.element.smtp-protocol.dot.undot)
- description and source-code
```javascript
undot = function (target) {
    var first = true;
    var dot = through(function (data) {
        var s = first
            ? data.replace(/(^|\n)\.\./g, '$1.')
            : data.replace(/\n\.\./g, '\n.')
        ;
        first = data.charCodeAt(data.length - 1) === 10;
        this.queue(s);
    });
    return combine(dot, target);
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.smtp-protocol.parse_data"></a>[module smtp-protocol.parse_data](#apidoc.module.smtp-protocol.parse_data)

#### <a name="apidoc.element.smtp-protocol.parse_data.getBytes"></a>[function <span class="apidocSignatureSpan">smtp-protocol.parse_data.</span>getBytes (n, target)](#apidoc.element.smtp-protocol.parse_data.getBytes)
- description and source-code
```javascript
getBytes = function (n, target) {
    this.bytes = n;
    this.target = target;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.smtp-protocol.parse_data.getCommand"></a>[function <span class="apidocSignatureSpan">smtp-protocol.parse_data.</span>getCommand (cb)](#apidoc.element.smtp-protocol.parse_data.getCommand)
- description and source-code
```javascript
getCommand = function (cb) {
    this.getLine(function (line) {
        var m = line.match(/^(\S+)(?:\s+(.*))?$/);
        if (!m) cb('syntax error')
        else {
            var cmd = parse(m[1].toLowerCase(), m[2]);
            if (cmd instanceof Error) cb(cmd)
            else cb(null, cmd)
        }
    });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.smtp-protocol.parse_data.getLine"></a>[function <span class="apidocSignatureSpan">smtp-protocol.parse_data.</span>getLine (cb)](#apidoc.element.smtp-protocol.parse_data.getLine)
- description and source-code
```javascript
getLine = function (cb) {
    this.queue.push(cb);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.smtp-protocol.parse_data.getUntil"></a>[function <span class="apidocSignatureSpan">smtp-protocol.parse_data.</span>getUntil (terminal, target)](#apidoc.element.smtp-protocol.parse_data.getUntil)
- description and source-code
```javascript
function getUntil(terminal, target) {
    var self = this;
    self.getLine(function getLine (line) {
        if (line === terminal) target.end()
        else {
            target.write(line + '\r\n');
            self.getLine(getLine);
        }
    });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.smtp-protocol.parse_data.parseData"></a>[function <span class="apidocSignatureSpan">smtp-protocol.parse_data.</span>parseData (cb)](#apidoc.element.smtp-protocol.parse_data.parseData)
- description and source-code
```javascript
parseData = function (cb) {
    var self = this;
    var bufs = [];

    self.stream.on('data', function ondata (buf, offset) {
        if (offset === undefined) offset = 0;

        if (self.bytes) {
            var ix = Math.min(buf.length, offset + self.bytes);
            var chunk = buf.slice(offset, ix);
            self.target.write(chunk);

            self.bytes -= chunk.length;
            if (self.bytes === 0) {
                if (buf.length > offset + chunk.length) {
                    ondata(buf, offset + chunk.length);
                }
                self.target.end();
            }
        }
        else {
            for (var i = offset; i < buf.length; i++) {
                if (buf[i] === 10) {
                    if (i > offset) bufs.push(buf.slice(offset, i));
                    cb(Buffer.concat(bufs).toString('utf8').replace(/\r$/, ''));
                    bufs = [];
                    if (buf.length > i + 1) ondata(buf, i + 1);
                    return;
                }
            }
            if (offset < buf.length) {
                bufs.push(buf.slice(offset, buf.length));
            }
        }
    });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.smtp-protocol.parse_data.parseLines"></a>[function <span class="apidocSignatureSpan">smtp-protocol.parse_data.</span>parseLines (cb)](#apidoc.element.smtp-protocol.parse_data.parseLines)
- description and source-code
```javascript
parseLines = function (cb) {
    var self = this;
    var continuation = null;

    self.parseData(function (line) {
        var m = line.match(/^(\d+)(?:([- ])(.+))?$/);
        var code = m && parseInt(m[1], 10);

        if (!m) {
            cb(new Error('syntax error parsing: ' + line));
        }
        else if (continuation) {
            if (code !== continuation.code) {
                cb(new Error('inconsistent code in line continuation'));
            }
            else {
                continuation.lines.push(m[3]);
                if (m[2] !== '-') {
                    cb(null, continuation.code, continuation.lines);
                    continuation = null;
                }
            }
        }
        else if (m[2] === '-') {
            continuation = { code : code, lines : [ m[3] ] };
        }
        else if (m[3] === undefined) {
            cb(null, code, []);
        }
        else cb(null, code, [ m[3] ]);
    });
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.smtp-protocol.protocol"></a>[module smtp-protocol.protocol](#apidoc.module.smtp-protocol.protocol)

#### <a name="apidoc.element.smtp-protocol.protocol.client"></a>[function <span class="apidocSignatureSpan">smtp-protocol.protocol.</span>client (opts, stream)](#apidoc.element.smtp-protocol.protocol.client)
- description and source-code
```javascript
client = function (opts, stream) {
    if (stream === undefined) {
        stream = opts;
        opts = {};
    }
    if (!opts) opts = {};

    var p = parser(stream);
    var write = writer(stream);
    write(220, opts.domain || os.hostname());

    function createAck (cb, okCode, raw) {
        return {
            accept : function (code, msg) {
                write(code, msg || "OK", okCode || 250);
                if (cb) cb();
                if (!raw) next();
            },
            reject : function (code, msg) {
                write(code, msg, 500);
                next();
            }
        };
    }

    function emit (name, x) {
        var fn = arguments[arguments.length - 1];
        var ack = arguments[arguments.length - 1] = createAck(fn);
        if (req.listeners(name).length === 0) {
            if (name === 'greeting' && x.greeting === 'ehlo') {
                ack.accept(250, [ x.hostname || remoteIp, 'STARTTLS' ]);
            }
            else if (name === 'greeting') {
                ack.accept(250, x.hostname);
            }
            else ack.accept();
        }
        req.emit.apply(req, arguments);
    }

    var req = new EventEmitter;
    req._swapStream = function (s) {
        write = writer(s);
        p = parser(s);
        stream = s;
        s.on('error', req.emit.bind(req, 'error'));
        next();
    };

    stream.on('error', req.emit.bind(req, 'error'));
    req.socket = stream;
    var remoteIp = stream.remoteAddress || 'unknown';

    var next = (function next () {
        p.getCommand(function (err, cmd) {
            if (err) {
                if (err.code) write(err.code, err.message || err.toString())
                else write(501, err.message || err.toString())
                return next();
            }
            var prevented = false;
            req.emit('command', cmd, {
                preventDefault: function () { prevented = true },
                write: write,
                next: next
            });
            if (prevented) return;

            if (cmd.name === 'quit') {
                write(221, 'Bye!');
                req.emit('quit');
                stream.end();
            }
            else if (cmd.name === 'rset') {
                write(250);
                req.to = undefined;
                req.from = undefined;
                req.emit('rset');
                next();
            }
            else if (!req.greeting) {
                if (cmd.name === 'greeting') {
                    emit('greeting', cmd, function () {
                        req.greeting = cmd.greeting;
                        req.hostname = cmd.hostname;
                    });
                }
                else {
                    write(503, 'Bad sequence: HELO, EHLO, or LHLO expected.');
                    next();
                }
            }
            else if (cmd.name === 'mail') {
                emit('from', cmd.from, function () {
                    req.fromExt = cmd.ext;
                    req.from = cmd.from;
                });
            }
            else if (cmd.name === 'rcpt') {
                emit('to', cmd.to, function () {
                    if (req.toExt == undefined) {
                        req.toExt = [];
                    }
                    req.toExt.push(cmd.ext);
                    if (req.to == undefined) {
                        req.to = [];
                    }
                    req.to.push(cmd.to);

                });
            }
            else if (cmd.name === 'data') {
                if (!req.from) {
                    write(503, 'Bad sequence: MAIL expected');
                    next();
                }
                else if (!req.to) {
                    write(503, 'Bad sequence: RCPT expected');
                    next();
                }
                else {
                    var target = makeTarget(write, next, emit);
                    var messageAck = createAck(function () {
                        p.getUntil('.', undot(target)); ...
```
- example usage
```shell
...
    opts = {};;
}
if (!opts) opts = {};
var istls = Boolean(opts.tls);
var tnet = istls ? tls : net;

return tnet.createServer(opts, function (stream) {
    var req = proto.client(opts, stream);
    var clienttls = istls;

    req.on('error', function () {});
    stream.on('error', function (err) {});

    req.on('_tlsNext', function (write, next) {
        if (clienttls) {
...
```

#### <a name="apidoc.element.smtp-protocol.protocol.server"></a>[function <span class="apidocSignatureSpan">smtp-protocol.protocol.</span>server (stream)](#apidoc.element.smtp-protocol.protocol.server)
- description and source-code
```javascript
server = function (stream) {
    return new Client(stream);
}
```
- example usage
```shell
...
        stream.emit('secure', ack);

        function done () {
            if (!allOk) {
                stream.end();
                stream.emit('error', new Error(stream.authorizationError));
            }
            else cb(proto.server(stream));
        }
    });
}
else if (options.stream) {
    cb(proto.server(options.stream));
}
else {
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
