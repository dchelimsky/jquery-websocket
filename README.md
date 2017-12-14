Send and receive the JSON object directly with Web Sockets API.

# Deprecated

This fork of http://code.google.com/p/jquery-websocket/ is no longer in development. Please
feel free to use it as/is or fork it if you wish to make changes.

# Usage

## Connection

    var ws = $.websocket("ws://127.0.0.1:8080/");

## Sending Message

    ws.send('hello');                          // sending message is '{type:'hello'}'.
    ws.send('say', {name:'foo', text:'baa'});  // sending message is '{type:'say', data:{name:'foo', text:'baa'}}'

## Event Handling

    var ws = $.websocket("ws://127.0.0.1:8080/", {
        open: function() { ... },
        close: function() { ... },
        events: {
            say: function(e) {
                alert(e.data.name); // 'foo'
                alert(e.data.text); // 'baa'
            }
        }
    });

# Example


    <!doctype html>
    <html>
      <head>
        <meta charset="UTF-8">
        <title>WebSocket Chat</title>
      </head>
      <body>
        <h1>WebSocket Chat</h1>
        <section id="content"></section>
        <input id="message" type="text"/>
        <script src="http://www.google.com/jsapi"></script>
        <script>google.load("jquery", "1.3")</script>
        <script src="https://raw.github.com/douglascrockford/JSON-js/master/json2.js"></script>
        <script src="https://raw.github.com/dchelimsky/jquery-websocket/v0.0.4/jquery.websocket.js"></script>
        <script>
          var ws = $.websocket("ws://127.0.0.1:8080/", {
              events: {
                  message: function(e) { $('#content').append(e.data + '<br>') }
              }
          });
          $('#message').change(function(){
              ws.send('message', this.value);
              this.value = '';
          });
        </script>
      </body>
    </html>

## Note on ECMA5cript 5 JSON API compatibility

Version 0.3 and below explicitly depended on the [jquery-json](https://code.google.com/p/jquery-json/) library to define the `$.evalJSON` and `$.toJSON` methods. This requirement has been replaced in subsequent versions by a dependency on the JSON parsing and serialization API defined in ECMAScript5 ([described thoroughly here](http://ejohn.org/blog/ecmascript-5-strict-mode-json-and-more/)).

When upgrading from 0.0.3, you must do one of the following:

1. Replace your usage of jquery-json with a library that defines `JSON.parse` and `JSON.stringify` for browsers that do not support them natively. json2.js from the [JSON-js](https://github.com/douglascrockford/JSON-js) library is a good choice.
2. Provide your own implementations of those methods or otherwise deal on your own with browsers that do not support them natively.

# License

The MIT License (MIT)

Copyright (c) 2010 by shootaroo (Shotaro Tsubouchi).

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
