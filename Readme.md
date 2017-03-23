# node-counterparty
[![travis][travis-image]][travis-url]
[![npm][npm-image]][npm-url]
[![downloads][downloads-image]][downloads-url]
[![js-standard-style][standard-image]][standard-url]

[travis-image]: https://travis-ci.org/monaco-ex/node-counterparty.svg?branch=master
[travis-url]: https://travis-ci.org/monaco-ex/node-counterparty

[npm-image]: https://img.shields.io/npm/v/counterparty.svg?style=flat
[npm-url]: https://npmjs.org/package/counterparty

[downloads-image]: https://img.shields.io/npm/dm/counterparty.svg?style=flat
[downloads-url]: https://npmjs.org/package/counterparty

[standard-image]: https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat
[standard-url]: http://standardjs.com

node-counterparty is a simple wrapper for the Bitcoin client's JSON-RPC API.
(Based on [node-bitcoin](https://github.com/freewil/node-bitcoin))

If starting a new project, I highly encourage you to take a look at the more modern modules.

The API is equivalent to the API document [here](http://counterparty.io/docs/api/).
The methods are exposed as lower camelcase methods on the `bitcoin.Client`
object, or you may call the API directly using the `cmd` method.

## Install

`npm install counterparty`

## Examples

### Create client
```js
// all config options are optional
var client = new counterparty.Client({
  host: 'localhost',
  port: 8332,
  user: 'username',
  pass: 'password',
  timeout: 30000
});
```

### Get running info

```js
client.getRunningInfo('*', 6, function() {
  if (err) return console.log(err);
  console.log('Balance:', balance);
});
```

## SSL

It looks counterparty-server itself doesn't support SSL. But you can keep secure by SSL proxy.

If you're using this to connect to counterparty-server across a network it is highly
recommended to enable `ssl`, otherwise an attacker may intercept your RPC credentials
resulting in theft of your tokens.

When enabling `ssl` by setting the configuration option to `true`, the `sslStrict`
option (verifies the server certificate) will also be enabled by default. It is
highly recommended to specify the `sslCa` as well, even if your server has
a certificate signed by an actual CA, to ensure you are connecting
to your own server.

```js
var client = new counterparty.Client({
  host: 'localhost',
  port: 4000,
  user: 'username',
  pass: 'password',
  ssl: true,
  sslStrict: true,
  sslCa: fs.readFileSync(__dirname + '/myca.cert')
});
```
