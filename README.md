node-ogone-directlink
=====================

A thin wrapper around the HTTPS DirectLink API of the ogone payment services with validation functionality.

This library is based on the request and xml2js libraries.

Installation
============

```
npm install ogone-directlink
```

Running the Tests
=================

```
npm test
```

Howto Use
=========

First of all read the Ogone DirectLink documentation and then continue reading.

```
var Ogone = require('ogone-directlink');

// Creates a ogone object in test mode. Change the last parameter to switch in prod mode.
var ogone = new Ogone('mypsid', 'myuserid', 'mypswd', 'test' /* 'prod' */);
```

Create your first order request:

```
var order = ogone.createOrderRequest();
order.orderid = '123;
order.amount = 1.50; // Amount is automatically multiplied by 100
order.brand = 'VISA';
order.ed = '09/12';
order.cvc = '123';
order.cardno = '4111111111111111';

// Create a request with the operation 'SAL'
// Use order.res(...) for an request with operation 'RES'
// Use order.rfd(...) for an request with operation 'RFD'
order.sal(function(err, result) {
    console.log(err || result);
});
```

Create an order with SHA-SIGN:

```
var order = ogone.createOrderRequest('sha1', 'myshapassword');
```

Create your first maintenance request:

```
var maintenance = ogone.createMaintenanceRequest();
maintenance.payid = 'abc';
maintenance.amount = 1.50;

// Create a request with the operation 'REN'
// Use maintenance.del(...) for an request with operation 'DEL'
// Use maintenance.des(...) for an request with operation 'DES'
// Use maintenance.sal(...) for an request with operation 'SAL'
// Use maintenance.sas(...) for an request with operation 'SAS'
// Use maintenance.rfd(...) for an request with operation 'RFD'
// Use maintenance.rfs(...) for an request with operation 'RFS'
maintenance.ren(function(err, result) {
    console.log(err || result);
});
```

Create your first query request:

```
varquery = ogone.createQueryRequest();
query.payid = 'abc';
query.status(function(err, result) {
    console.log(err || result);
});
```

**Note:** All parameters in the ogone documentation are available in camelcase notation.

Contribution and Issues
=======================

This API is used in production, but when you found bugs or want new features open and ticket or send me a pull request.

Lisence
=======

MIT