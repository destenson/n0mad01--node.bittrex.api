Node Bittrex API
=========

Node Bittrex API is an asynchronous node.js library for the Bittrex API - https://bittrex.com/.
The Bittrex API data can be received either as a GET request or a Stream.

Documentation to the Bittrex API: https://bittrex.com/Home/Api

This Library was created by  [Adrian Soluch (@n0mad01)](https://github.com/n0mad01/) [soluch.us](http://soluch.us) and is licensed under the [MIT license](https://github.com/n0mad01/node.bittrex.api/blob/master/LICENSE).

Contributors
----
Thanks go to the people who have contributed code to this Library.

* [samuelhei](https://github.com/samuelhei) Special kudos - thanks to him all missing calls are complemented as also structural improvements have been made.
* [192-sean](https://github.com/192-sean)
* [caffeinewriter](https://github.com/caffeinewriter)
* [apense](https://github.com/apense)


Installation
----
install it most convenient via npm:
```sh
$ npm install node.bittrex.api
```

##### or

fetch the project via git:
```sh
$ git clone https://github.com/n0mad01/node.bittrex.api.git
```
then meet the package dependencies:
```sh
$ cd node-bittrex-api/
$ npm install
```

First steps
----

include node.bittrex.api.js into your project:
```javascript
var bittrex = require('./node.bittrex.api.js');
```

##### configure
```javascript
bittrex.options({
    'apikey' : API_KEY,
    'apisecret' : API_SECRET, 
    'stream' : true,
    'verbose' : true,
    'cleartext' : false 
});
```

By default the returned data is an object, in order to get clear text you have to add the option **cleartext** (streams will always return objects):
```javascript
'cleartext' : true
```

The baseUrl itself can also be set via options
```javascript
'baseUrl' : 'https://bittrex.com/api/v1'
```

Streams
--
To activate Streaming simply add to your options:
```javascript
'stream' : true
```

Streaming depends on the following npm packages:
- JSONStream https://www.npmjs.org/package/JSONStream
- event-stream https://www.npmjs.org/package/event-stream

Examples
--
After configuration you can use the object right away:
example #1
```javascript
bittrex.getmarketsummaries( function( data ) {
    for( var i in data.result ) {
        bittrex.getticker( { market : data.result[i].MarketName }, function( ticker ) {
            console.log( ticker );
        });
    }
});
```
example #2
```javascript
bittrex.getbalance({ currency : 'BTC' }, function( data ) {
    console.log( data );
});
```


Other
--

Other libraries utilized:
- request https://www.npmjs.org/package/request

For HmacSHA512 this package is using a part of Googles Crypto.js (the node crypt package could not provide any appropriate result).
- http://crypto-js.googlecode.com/svn/tags/3.1.2/build/rollups/hmac-sha512.js

Methods
----

Optional parameters may have to be looked up at https://bittrex.com/Home/Api.

> It may happen that some Bittrex API methods are missing, also they could have been forgotten in the documentation. In this case, if this strikes you, feel free to open a issue or send me a pull request.

> Also: the method **sendCustomRequest** enables completely custom requests, regardless the specific API methods.

##### sendCustomRequest 
- url           String
- callback      Function
- credentials   Boolean     optional    whether the credentials should be applied to the request/stream or not, default is set to false.

example #1
```javascript
var url = 'https://bittrex.com/api/v1.1/public/getticker?market=BTC-LTC';
bittrex.sendCustomRequest( uri, function( data ) {
    console.log( data );
});
```

example #2 (credentials applied to request/stream)
```javascript
bittrex.sendCustomRequest( 'https://bittrex.com/api/v1.1/account/getbalances?currency=BTC', function( data ) {
    console.log( data );
}, true );

will result in (the Header is being set too):
https://bittrex.com/api/v1.1/account/getbalances?currency=BTC&apikey=API_KEY&nonce=4456490600
```

##### getticker
```javascript
bittrex.getticker( { market : 'BTC-LTC' }, function( data ) {
    console.log( data );
});
```

##### getbalances
```javascript
bittrex.getbalances( function( data ) {
    console.log( data );
});
```

##### getmarkethistory
```javascript
bittrex.getmarkethistory({ market : 'BTC-LTC' }, function( data ) {
    console.log( data );
});
```

##### getmarketsummaries
```javascript
bittrex.getmarketsummaries( function( data ) {
    console.log( data );
});
```

##### getmarketsummary
```javascript
bittrex.getmarketsummary( { market : 'BTC-LTC'}, function( data ) {
    console.log( data );
});
```

##### getorderbook
```javascript
bittrex.getorderbook({ market : 'BTC-LTC', depth : 10, type : 'both' }, function( data ) {
    console.log( data );
});
```

##### getwithdrawalhistory
```javascript
bittrex.getwithdrawalhistory({ currency : 'BTC' }, function( data ) {
    console.log( data );
});
```

##### getdepositaddress
```javascript
bittrex.getdepositaddress({ currency : 'BTC' }, function( data ) {
    console.log( data );
});
```

##### getdeposithistory
```javascript
bittrex.getdeposithistory({ currency : 'BTC' }, function( data ) {
    console.log( data );
});
```

##### getbalance
```javascript
bittrex.getbalance({ currency : 'BTC' }, function( data ) {
    console.log( data );
});
```

##### withdraw
```javascript
bittrex.withdraw({ currency : 'BTC', quantity : '1.5112', address : 'THE_ADDRESS' }, function( data ) {
    console.log( data );
});
```

##### donations welcome! 
> BTC: 1N5T2VYACYKxK3UUDHhp7g69qtUmsDdAjZ

