# TaxJar Sales Tax API for Node

Official Node client for Sales Tax API v2. For the REST documentation, please visit [http://developers.taxjar.com/api](http://developers.taxjar.com/api).

## Requirements

- Node 0.10.0 and later.

## Installation

```
npm install taxjar
```

## Authentication

```javascript
var taxjar = require('taxjar')(__env.TAXJAR_API_KEY);
```

## Usage

### List all tax categories

```javascript
taxjar.categories().then(function(res) {
  res.categories; // Array of categories
});
```

### List tax rates for a location (by zip/postal code)

```javascript
taxjar.ratesForLocation(90002).then(function(res) {
  res.rate; // Rate object
});
```

### Calculate sales tax for an order

```javascript
taxjar.taxForOrder({
  'from_country': 'US',
  'from_zip': '07001',
  'from_state': 'NJ',
  'to_country': 'US',
  'to_zip': '07446',
  'to_state': 'NJ',
  'amount': 16.50,
  'shipping': 1.5
}).then(function(res) {
  res.tax; // Tax object
  res.tax.amount_to_collect; // Amount to collect
});
```

### List order transactions

```javascript
taxjar.listOrders({
  from_transaction_date: '2015/05/01',
  to_transaction_date: '2015/05/31'
}).then(function(res) {
  res.orders; // Orders object
});
```

### Show order transaction

```javascript
taxjar.showOrder('123').then(function(res) {
  res.order; // Order object
});
```

### Create order transaction

```javascript
taxjar.createOrder({
  'transaction_id': '123',
  'transaction_date': '2015/05/14',
  'to_country': 'US',
  'to_zip': '90002',
  'to_state': 'CA',
  'to_city': 'Los Angeles',
  'to_street': '123 Palm Grove Ln',
  'amount': 17.45,
  'shipping': 1.5,
  'sales_tax': 0.95,
  'line_items': [
    {
      'quantity': 1,
      'product_identifier': '12-34243-9',
      'description': 'Fuzzy Widget',
      'unit_price': 15.0,
      'sales_tax': 0.95
    }
  ]
}).then(function(res) {
  res.order; // Order object
});
```

### Update order transaction

```javascript
taxjar.updateOrder({
  'transaction_id': '123',
  'amount': 17.45,
  'shipping': 1.5,
  'line_items': [
    {
      'quantity': 1,
      'product_identifier': '12-34243-0',
      'description': 'Heavy Widget',
      'unit_price': 15.0,
      'discount': 0.0,
      'sales_tax': 0.95
    }
  ]
}).then(function(res) {
  res.order; // Order object
});
```

### List refund transactions

```javascript
taxjar.listRefunds({
  from_transaction_date: '2015/05/01',
  to_transaction_date: '2015/05/31'
}).then(function(res) {
  res.refunds; // Refunds object
});
```

### Show refund transaction

```javascript
taxjar.showRefund('321').then(function(res) {
  res.refund; // Refund object
});
```

### Create refund transaction

```javascript
taxjar.createRefund({
  'transaction_id': '123',
  'transaction_date': '2015/05/14',
  'transaction_reference_id': '123',
  'to_country': 'US',
  'to_zip': '90002',
  'to_state': 'CA',
  'to_city': 'Los Angeles',
  'to_street': '123 Palm Grove Ln',
  'amount': 17.45,
  'shipping': 1.5,
  'sales_tax': 0.95,
  'line_items': [
    {
      'quantity': 1,
      'product_identifier': '12-34243-9',
      'description': 'Fuzzy Widget',
      'unit_price': 15.0,
      'sales_tax': 0.95
    }
  ]
}).then(function(res) {
  res.refund; // Refund object
});
```

### Update refund transaction

```javascript
taxjar.updateRefund({
  'transaction_id': '123',
  'amount': 17.95,
  'shipping': 2.0,
  'line_items': [
    {
      'quantity': 1,
      'product_identifier': '12-34243-0',
      'description': 'Heavy Widget',
      'unit_price': 15.0,
      'sales_tax': 0.95
    }
  ]
}).then(function(res) {
  res.refund; // Refund object
});
```