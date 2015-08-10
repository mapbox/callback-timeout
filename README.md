callback-timeout
================

[![NPM version](https://badge.fury.io/js/callback-timeout.png)](http://badge.fury.io/js/callback-timeout)
[![Build Status](https://travis-ci.org/jasonpincin/callback-timeout.svg?branch=master)](https://travis-ci.org/jasonpincin/callback-timeout)
[![Coverage Status](https://coveralls.io/repos/jasonpincin/callback-timeout/badge.png?branch=master)](https://coveralls.io/r/jasonpincin/callback-timeout?branch=master)

Executes callback with single error argument if timeout is exceeded before it's called naturally

[![browser support](http://ci.testling.com/jasonpincin/callback-timeout.png)](http://ci.testling.com/jasonpincin/callback-timeout)

# example

``` js
var timeout = require('callback-timeout')

function doSomethingFast(cb) { setTimeout(cb, 100) }
function doSomethingSlow(cb) { setTimeout(cb, 2000) }

doSomethingFast(timeout(function doSomethingFastHandler (err) {
    if (err)
        console.log(err.message) // Will not happen
    else
        console.log('doSomethingFastHandler executed without error.') // Will happen
}, 1000))

doSomethingSlow(timeout(function doSomethingSlowHandler (err) {
    if (err)
        console.log(err.message) // Will happen
    else
        console.log('doSomethingSlowHandler executed without error.') // Will not happen
}, 1000))
```

# usage

``` js
var timeout = require('callback-timeout')
```

## timeout(callback [, ms, msg])

Returns a callback function that will execute after `ms` milliseconds with a single `Error` argument 
if not invoked by other means first. If the `ms` timeout argument is omitted, 0, or null, then the timeout 
is disabled and the original callback is returned. `msg` may be used to set a custom error message (on 
timeout), otherwise an appropriate one will be set for you.

# install

With [npm](https://npmjs.org) do:

```
npm install callback-timeout
```

# license

MIT
