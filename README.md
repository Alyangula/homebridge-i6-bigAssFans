<span align="center">

# homebridge-bigassfans-i6

<!-- [![verified-by-homebridge](https://badgen.net/badge/homebridge/verified/purple)](https://github.com/homebridge/homebridge/wiki/Verified-Plugins) -->
<!-- [![homebridge-miot](https://badgen.net/npm/v/homebridge-bigassfans-i6?icon=npm)](https://www.npmjs.com/package/homebridge-bigassfans-i6)
[![mit-license](https://badgen.net/npm/license/lodash)](https://github.com/oogje/homebridge-bigassfans-i6/blob/master/LICENSE)
<!-- [![follow-me-on-twitter](https://badgen.net/twitter/follow/merdok_dev?icon=twitter)](https://twitter.com/merdok_dev) -->
<!-- [![join-discord](https://badgen.net/badge/icon/discord?icon=discord&label=homebridge-xiaomi-fan)](https://discord.gg/AFYUZbk) -->

</span>

`homebridge-bigassfans-i6 ` is a plugin for Homebridge which allows you to control a Big Ass Fans model i6.

This work in progress is my first plugin and first time I've used javascript, let alone Node.js or typescript.  This works 
with my LED equipped i6 fan.  I'm hoping it works for you.  I created the plugin by observing network traffic and for the 
most part guessing the format of the binary messages that were sent to and from the fan.  Of the appoximately 80 unique 
message types I've seen, I think I know what about half of them probably mean.

### Bugs
The network connection to the fan will reset occasionally.  I try to handle that gracefully but if it happens when you
issue a command (e.g., turn on the light) as oppposed to the periodic probe message, the command will be ignored.  Try again after two seconds.


### Features
* Turn fan and/or light on or off!
* Change speed, and direction (keep in mind Big Ass Fans frowns on reversing speed.)
* Change brightness level of LED lamp.
* See the fan's bluetooth remote's temperature and humidity sensors.

## Installation

If you are new to homebridge, please first read the homebridge [documentation](https://github.com/homebridge/homebridge#readme).
If you are running on a Raspberry, you will find a tutorial in the [homebridge wiki](https://github.com/homebridge/homebridge/wiki/Install-Homebridge-on-Raspbian).

Install homebridge:
```sh
sudo npm install -g homebridge
```

Install homebridge-bigassfans-i6:
```sh
sudo npm install -g homebridge-bigassfans-i6@beta
```

## Configuration

Add the `BigAssFans-i6` platform in `config.json` in your home directory inside `.homebridge`.

Add your fan(s) in the `fans` array.

Example configuration:

```js
{
  "platforms": [
    {
      "platform": "BigAssFans-i6",
            "fans": [
                {
                    "name": "Big Fan",
                    "mac": "b8:f0:09:ac:db:b6",
                    "ip": "192.168.7.150"
                }
            ]
    }
  ]
}
```


#### Platform configuration fields
- `platform` [required]
Should always be **"BigAssFans-i6"**.
- `fans` [required]
A list of your fans.
#### General configuration fields
- `name` [required]
Name of your fan.
- `ip` [required]
IP address of your fan.  Can be found in the Big Ass Fans app's Wi-Fi settings screen.
- `mac` [required]
MAC address of your fan.  Can be found in the Big Ass Fans app's Wi-Fi settings screen.
- `megaDebugLevel` [optional]
Determines volume of debug messages. (a number or "MAX")
- `whoosh` [optional]
Adds accessory switch for Whoosh Mode (true/false)
- `dimToWarm` [optional]
Adds accessory switch for Dim to Warm (true/false)

## Troubleshooting
If you have any issues with the plugin or fan services then you can run Homebridge in debug mode, which will provide some additional information. This might be useful for debugging issues.

Homebridge debug mode:
```sh
homebridge -D
```

For the mega debug log, add the following to your config.json:
```json
"deepDebugLog": <specify a number or the word MAX>
```
This will enable extra logging which might be helpful to debug all kind of issues.

## Special thanks
[homebridge-miot](https://github.com/merdok/homebridge-miot) - whose style served as a guide.

[homebridge-bigAssFans](https://github.com/sean9keenan/homebridge-bigAssFans) - where the Haiku message protocol gave me some insight.

[HAP-NodeJS](https://github.com/KhaosT/HAP-NodeJS) & [homebridge](https://github.com/nfarina/homebridge) - for making this possible.

[Big Ass Fans](https://www.bigassfans.com) - who is presuably hard at work on their Homekit implementation.