## 0.0.4

* Replace usage of `$.evalJSON` and `$.toJSON` with ES5-compliant `JSON.parse` and `JSON.stringify` (Brian Moseley)
* Only pass protocols to WebSocket if they exist (t3chn0r)

## 0.0.3

* Add support for optional protocols parameter in WebSocket constructor (Valentin Kunz)

## 0.0.2

* Support multiple websocket connections from one html page by ensuring that
  each gets its own settings.
