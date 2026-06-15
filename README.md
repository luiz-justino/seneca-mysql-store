![Seneca](http://senecajs.org/files/assets/seneca-logo.png)

> A [Seneca.js](http://senecajs.org) Data Storage Plugin

# seneca-mysql-store

[![npm version][npm-badge]][npm-url]
[![Build Status][travis-badge]][travis-url]
[![Coverage Status][coverage-badge]][coverage-url]
[![Dependency Status][david-badge]][david-url]
[![Coveralls][BadgeCoveralls]][Coveralls]
[![Gitter][gitter-badge]][gitter-url]

| ![Voxgig](https://www.voxgig.com/res/img/vgt01r.png) | This open source module is sponsored and supported by [Voxgig](https://www.voxgig.com). |
|---|---|

A storage engine that uses [mySql][] to persist data. It may also be used as an example on how to
implement a storage plugin for Seneca using an underlying relational store.

If you're using this module, and need help, you can:

- Post a [github issue][],
- Tweet to [@senecajs][],
- Ask on the [Gitter][gitter-url].

If you are new to Seneca in general, please take a look at [senecajs.org][].

### Seneca compatibility
Supports Seneca versions **1.x** - **3.x**

### Supported functionality
All Seneca data store supported functionality is implemented in [seneca-store-test](https://github.com/senecajs/seneca-store-test) as a test suite.

## Install

To install, simply use npm. Remember you will need to install [Seneca.js][] separately.

```sh
npm install seneca
npm install seneca-mysql-store
```

## Quick Example

```js
var seneca = require('seneca')()
seneca.use('mysql-store', {
  name: 'senecatest',
  host: 'localhost',
  user: 'senecatest',
  password: 'senecatest',
  port: 3306
})

seneca.ready(function () {
  var apple = seneca.make$('fruit')
  apple.name  = 'Pink Lady'
  apple.price = 0.99
  apple.save$(function (err, apple) {
    console.log("apple.id = " + apple.id)
  })
})
```

## More Examples

### Seneca Entity API

You don't use this module directly. It provides an underlying data storage engine for the Seneca entity API:

```js
var entity = seneca.make$('typename')
entity.someproperty = "something"
entity.anotherproperty = 100

entity.save$(function (err, entity) { ... })
entity.load$({id: ...}, function (err, entity) { ... })
entity.list$({property: ...}, function (err, entity) { ... })
entity.remove$({id: ...}, function (err, entity) { ... })
```

### Native Driver

As with all seneca stores, you can access the native driver, in this case, the `mysql`
`connectionPool` object:

```js
entity.native$(function (err, connectionPool) {
  // use connectionPool
})
```

## Motivation

This plugin provides MySQL storage for the Seneca microservices framework.
It supports the standard Seneca query format via [seneca-standard-query][standard-query]
and can be extended with [seneca-store-query][store-query].

### Query Support

The standard Seneca query format is supported. See [seneca-standard-query][standard-query] for details.

### Extended Query Support

Use [seneca-store-query][store-query] to extend query capabilities.

## Support

If you have any questions:

- Post a [github issue][]
- Tweet to [@senecajs][]
- Ask on the [Gitter][gitter-url]

## API

See the [seneca-store-test](https://github.com/senecajs/seneca-store-test) suite for the full
store functionality specifications.

## Contributing

The [Senecajs org][senecajs-org] encourages open participation. If you feel you can help in any
way, be it with documentation, examples, extra testing, or new features please get in touch.

### Running tests with Docker

Build the MySQL Docker image:

```sh
npm run build
```

Start the MySQL container:

```sh
npm run start
```

Stop the MySQL container:

```sh
npm run stop
```

Run the tests:

```sh
npm run test
```

#### Testing for Mac users

Run `docker-machine env default` and copy the docker host address (e.g. `192.168.99.100`).
Insert it into `test/dbconfig.example.js` as the `host` value.

## Background

This plugin was created to provide MySQL storage for the Seneca microservices framework.
It is part of the [Voxgig](https://www.voxgig.com) open source initiative.

## License

Copyright (c) 2012-2016, Mircea Alexandru and other contributors.
Licensed under [MIT][].

[npm-badge]: https://img.shields.io/npm/v/seneca-mysql-store.svg
[npm-url]: https://npmjs.com/package/seneca-mysql-store
[travis-badge]: https://travis-ci.org/senecajs/seneca-mysql-store.svg
[travis-url]: https://travis-ci.org/senecajs/seneca-mysql-store
[coverage-badge]: https://coveralls.io/repos/senecajs/seneca-mysql-store/badge.svg?branch=master&service=github
[coverage-url]: https://coveralls.io/github/senecajs/seneca-mysql-store?branch=master
[david-badge]: https://david-dm.org/senecajs/seneca-mysql-store.svg
[david-url]: https://david-dm.org/senecajs/seneca-mysql-store
[gitter-badge]: https://badges.gitter.im/Join%20Chat.svg
[gitter-url]: https://gitter.im/senecajs/seneca
[mySql]: https://www.mysql.com/
[MIT]: ./LICENSE
[senecajs-org]: https://github.com/senecajs/
[Seneca.js]: https://www.npmjs.com/package/seneca
[senecajs.org]: http://senecajs.org/
[github issue]: https://github.com/senecajs/seneca-mysql-store/issues
[@senecajs]: http://twitter.com/senecajs
[Coveralls]: https://coveralls.io/github/senecajs/seneca-mysql-store?branch=master
[BadgeCoveralls]: https://coveralls.io/repos/github/senecajs/seneca-mysql-store/badge.svg?branch=master
[standard-query]: https://github.com/senecajs/seneca-standard-query
[store-query]: https://github.com/senecajs/seneca-store-query
