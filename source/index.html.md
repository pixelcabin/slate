---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - xml

toc_footers:
  - <a href='onestopshop.online'>OneStopShop Homepage</a>
  - <a href='mailto:integrations@onestopshop.online'>integrations@onestopshop.online</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the OneStopShop integration API. You can use our API to send updates on various data types to our platform, as well as receive order data. Some example use-cases are integrating with an ERP, pre-existing online shop, product database, or order-intake tool.


<aside>
There are four possible integrations possible:

* Customers: automatically send your customers database to OneStopShop, so accounts can be easily created
* Products: automatically send your product data to OneStopShop, such as the SKU number, EAN code, picture(s) and order description
* Prices: automatically send the specific prices per product, per customers. OneStopShop is fully capable of offering different prices for the same SKU to different customers, if required
* Orders: automatically receive the orders in an XML format to easily import them in the existing order flow

On this page, the following is explained:

* Data structure: the fields and contents of fields per topic
* Integration types: the types of documents we accept (XML / CSV / ….) What do we currently order?
* Transfer method: the way the files can be send to, or received from, OneStopShop
</aside>


<aside class="notice">
These docs are currently in in draft status
</aside>

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Customers

## Create new customers

```xml
<customers>
  <customer>
    <first_name>John</first_name>
    <last_name>Kanters</last_name>
    <email>info@kantersrestaurant.nl</email>
    <company>Kanters Restaurant</company>
    <address_1>Steenweg 2</address_1>
    <city>Moerdijk</city>
    <zip>4781 PA</zip>
    <country>Netherlands</country>
    <country_code>NL</country_code>
    <phone>31168412310</phone>
    <account_number>SoldTo10174993</account_number>
    <price_groups>KANTERS</price_groups>
  </customer>
</customers>
```


Property | Type | Required | Description
--------- | --------- | ----------- | ---------
first_name | String | **true** | Customer's first name
last_name | String | **true** | Customer's last name
email | String | **true** | Contact email address
company | String | **true** | Company Name
address_1 | String | **true** | First line of address
city | String | **true** |
zip | String | **true** |
country | String | **true** |
country_code | String | **true** | [ISO_3166 (Alpha-2)](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) Country Code
phone | String | **true** |
account_number | String | **true** | The account number used by the Vendor to identify the customer
price_groups | String | false | A comma-separated list of price groups this customer is a member of


# Products

## Create new products

```xml
<products>
  <product>
    <sku>7550795</sku>
    <ean_code>312453629932739234</ean_code>
    <title>1Wine Rose</title>
    <pack_size>24X18.7Cl</pack_size>
    <brand>1Wine</brand>
    <description>Een rose wijn uit Frankrijk met een zoete afdronk</description>
    <vendor>AB InBev</vendor>
    <product_type>Wijn</product_type>
    <product_subgroup>rose-wijn</product_subgroup>
    <price>3440</price>
    <image_url>https://cdn.shopify.com/s/files/1/2113/6405/products/rose.jpg?v=1523438325</image_url>
    <portion_type>Piece</portion_type>
  </product>
</products>
```

Property | Type | Required | Description
--------- | --------- | ----------- | ---------
sku | String | **true** |
ean_code | Integer | **true** |
title | String | **true** |
pack_size | String | **true** |
brand | String | **true** |
description | String | false |
vendor | String | **true** |
product_type | String | **true** |
product_subgroup | String | **true** |
price | Integer | **true** |
image_url | String | **true** |
portion_type | String | false |

# Price Lists

## Create new price lists

```xml
<price_list>
  <product>
    <sku>7550795</sku>
    <price_group>
      <id>KANTERS</id>
      <price>2261</price>
    </price_group>
    <price_group>
      <id>SMITH</id>
      <price>2044</price>
    </price_group>
  </product>
  <prices>
    <sku>7550796</sku>
    <price_group>
      <id>KANTERS</id>
      <price>61</price>
    </price_group>
    <price_group>
      <id>SMITH</id>
      <price>106</price>
    </price_group>
  </prices>
</price_list>
```

# Orders

## Receive new order data

-----------------------------

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | **true** | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

