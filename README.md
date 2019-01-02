# mqtt-rx  [![npm](https://img.shields.io/npm/v/mqtt-rx.svg)](https://www.npmjs.com/package/mqtt-rx) [![Travis](https://img.shields.io/travis/sirockin/mqtt-rx.svg)](https://travis-ci.org/sirockin/mqtt-rx)

This library has been forked with the permission of the creator from v6.8.2 of  [ngx-mqtt](https://github.com/sclausen/ngx-mqtt). I've very grateful for this.

Like its parent it provides a [ReactiveX](http://reactivex.io/) wrapper around the [Mqtt.js](https://www.npmjs.com/package/mqtt) library, with an identical API but for server-side use so:
1. Without the Angular dependency
1. Directly importing the [Mqtt.js](https://www.npmjs.com/package/mqtt) library
1. Allowing use of all the transports provided by [Mqtt.js](https://www.npmjs.com/package/mqtt)

It uses observables and takes care of subscription handling and message routing.

To keep the codebase as similar as possible to its parent while removing the Angular dependency, I have copied the `EventEmitter` implementation from the Angular source.

Since I am still carrying out integration tests, it is not yet production-ready. I also haven't yet done a comprehensive audit so it's possible there are obsolete code and config files hanging around.

## Usage

```TypeScript
import { Subscription } from 'rxjs';

import {
  IMqttMessage,
  MqttService,
  IMqttServiceOptions
} from 'mqtt-rx';

export const MQTT_SERVICE_OPTIONS: IMqttServiceOptions = {
  hostname: 'localhost',
  port: 1883,
  path: '/mqtt'
};

export class ExampleComponent {
  private subscription: Subscription;
  public message: string;
  private _mqttService: MqttService;

  constructor() {
    this._mqttService = new MqttService(MQTT_SERVICE_OPTIONS);
    this.subscription = this._mqttService.observe('my/topic').subscribe((message: IMqttMessage) => {
      this.message = message.payload.toString();
    });
  }

  public unsafePublish(topic: string, message: string): void {
    this._mqttService.unsafePublish(topic, message, {qos: 1, retain: true});
  }

  public destroy() {
    this.subscription.unsubscribe();
    this._mqttService.disconnect();
  }
}
```