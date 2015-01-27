---
layout: default
title: home
---

### Use cases

* Make a commercial version of your
application.
* Make a demo/evaluation/trial version of
your app without sources.
* Make some kind of self-extracting
archive or installer.
* No need to install node, npm.
* No need to download hundreds of files via
`npm install` to deploy your application.
Deploy it as a single independent file.
* Put your assets inside the executable
to make it even more portable.
* Test your app against new node version
without installing it.

### Install

```
npm install -g enclose
```

### The box

As input you specify the entry file of your
project `/path/project.js`. As output you
get a standalone executable `/path/project`.
Briefly "the box". When it is run, it does
the same as `node /path/project.js`.

### Command line

Command line call `project a b c` is similar
to `node project.js a b c`. But you can also
pass some node- and v8-specific parameters.
See docs.

### Dependencies

The compiler parses your sources, detects calls
to `require`, traverses the dependencies of
your project and includes them into the box.
You don't need to list them manually.

### Assets

If your project has assets (html templates,
css, etc), for example to serve via http,
you can bundle them into the box. Just
list them as a [glob](https://github.com/isaacs/node-glob#glob)
in the configuration file.

### Compilation? Srsly?

Both Yes and No.

Yes. Because JavaScript code is transformed
into native code at compile-time using
[V8 internal compiler](https://github.com/v8/v8-git-mirror/blob/master/src/compiler.cc).
Hence, your sources are simply not required
to execute the box, and they are excluded.

No. Optimized native code is generated
using information, collected at run-time.
Without that run-time info EncloseJS
can generate only "unoptimized" code,
that runs about 2x slower, than
optimized one.

Also, io.js code is put inside the box
(along with your code) to support all
JavaScript dynamic features for your
application at run-time. This increases
output file size.

So, this is not that static compilation
we used to know. But nevertheless you
get fully functional binary without
sources. Also, performance and file size
overhead are vectors of future work.

### Code protection?

The code protection is as strong as possible
when the sources are compiled to native code.
Hackers will deal with
[that push-mov stuff](https://github.com/v8/v8-git-mirror/blob/master/src/x87/full-codegen-x87.cc#L1110).
No need to obfuscate, no need to encrypt,
no "hidden" decryption keys. Stacktraces
show nothing (in case you wish to `require`
untrusted on-disk code). Also

```
myfunc.toString()
function myfunc() { [native code] }
```

### Fast

It takes seconds to make an executable.
You dont need to build io.js/node.js
from sources in order to make the box.
EncloseJS is shipped with precompiled
parts, ready for bundling.

### Both io.js and node.js

You can choose what runtime to wrap your
project in - io.js 1.0.x or node.js
0.11.x. Both branches are supported.

### Vanilla io.js

EncloseJS project does not aim to add
new features to io.js, to avoid undesirable
issues. Let's keep it vanilla.

### Unlimited code

You are not limited by the size of project.
...TODO...

### Platforms

EncloseJS supports Linux and Windows.
Mac OS is on the way.
