# rxjs-mqtt  [![npm](https://img.shields.io/npm/v/rxjs-mqtt.svg)](https://www.npmjs.com/package/rxjs-mqtt) 

This library has been forked with the permission of the creator from v6.8.2 of  [ngx-mqtt](https://github.com/sclausen/ngx-mqtt). I've very grateful for this.

Like its parent it provides a [ReactiveX](http://reactivex.io/) wrapper around the [Mqtt.js](https://www.npmjs.com/package/mqtt) library, with an identical API but for server-side use so:
1. Without the Angular dependency
1. Directly importing the [Mqtt.js](https://www.npmjs.com/package/mqtt) library
1. Allowing use of all the transports provided by [Mqtt.js](https://www.npmjs.com/package/mqtt)

It uses observables and takes care of subscription handling and message routing.

To keep the codebase as similar as possible to its parent while removing the Angular dependency, I have copied the `EventEmitter` implementation from the Angular source.

Since I am still carrying out integration tests, it is not yet production-ready. I also haven't yet done a comprehensive audit so it's possible there are obsolete code and config files hanging around.
