# ncp - Asynchronous recursive file & directory copying

Think `cp -r`, but pure node, and asynchronous.  `ncp` can be used both as a CLI tool and programmatically.

## Command Line usage

Usage is simple: `ncp [source] [dest] [--limit=concurrency limit] [--filter=filter]`

The 'filter' is a Regular Expression - matched files will be copied.

The 'concurrency limit' is an integer that represents how many pending file system requests `ncp` has at a time.

If there are no errors, `ncp` will output `done.` when complete.  If there are errors, the error messages will be logged to `stdout` and to `./ncp-debug.log`, and the copy operation will attempt to continue.

## Programmatic usage

Programmatic usage of `ncp` is just as simple.  The only argument to the completion callback is a possible error.  

```javascript
var ncp = require('ncp').ncp;

ncp.limit = 16;

ncp(source, destination, function (err) {
 if (err) {
   return console.error(err);
 }
 console.log('done!');
});
```

You can also call ncp like `ncp(source, destination, options, callback)`. 
`options` should be a dictionary. Currently, such options are available:

  * `options.filter` - a `RegExp` instance, against which each file name is
  tested to determine whether to copy it or not, or a function taking single
  parameter: copied file name, returning `true` or `false`, determining
  whether to copy file or not.

Please open an issue if any bugs arise.  As always, I accept (working) pull requests, and refunds are available at `/dev/null`.
