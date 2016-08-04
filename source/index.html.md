---
title: Convoy API Documentation

language_tabs:
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: false
---

# Introduction

Welcome to the Convoy API.  You can use our API to access various endpoints that'll help you create, update and track your inventory.

Currently there are no language bindings but using the API should be straightforward! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```python
import requests

response = requests.get("https://api.getconvoy.com/",
    headers={'Authorization': 'API_KEY'})
```

> Make sure to replace `API_KEY` with your API key.

Convoy uses API keys to allow access to the API. You can register a new Convoy API key at our [developer portal](http://getconvoy.com/developers).

Convoy expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: API_KEY`

<aside class="notice">
You must replace <code>API_KEY</code> with your personal API key.
</aside>


# Manufacturers

## Get all Manufacturers

```python
import requests

response = requests.get("https://api.getconvoy.com/manufacturers",
    headers={'Authorization': 'API_KEY'})
```

> The above command returns JSON structured like this:

```json
[
  {
    "manufacturer_id": 1,
    "name": "Apple"
  },
  {
    "manufacturer_id": 2,
    "name": "Google"
  }
]
```

This endpoint retrieves all manufacturers.

### HTTP Request

`GET https://api.getconvoy.com/manufacturers`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | If set, will retrieve a specific page of items.
limit | 25 | The number of items per page to return.


## Get a Specific Manufacturer

```python
import requests

response = requests.get("https://api.getconvoy.com/manufacturers/2",
    headers={'Authorization': 'API_KEY'})
```

> The above command returns JSON structured like this:

```json
{
  "manufacturer_id": 2,
  "name": "Google"
}
```

This endpoint retrieves a specific manufacturer.

### HTTP Request

`GET https://api.getconvoy.com/manufacturers/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the manufacturer to retrieve


## Create a Manufacturer

```python
import requests

response = requests.post("https://api.getconvoy.com/manufacturers",
    data={'manufacturer_id': 3, 'name': 'Amazon'},
    headers={'Authorization': 'API_KEY'})
```

> The above command returns JSON structured like this:

```json
{
    "manufacturer_id": 3,
    "name": "Amazon"
}
```

This endpoint creates a manufacturer

### HTTP Request
`POST https://api.getconvoy.com/manufacturers`

### POST Parameters

Parameter | Description
--------- | -----------
manufacturer_id | The id of the manufacturer stored in your database. If none is provided, Convoy will generate a random string.
name | The name of the manufacturer



# Products

## Get All Products

```python
import requests

response = requests.get("https://api.getconvoy.com/products",
    headers={'Authorization': 'API_KEY'})
```

> The above command returns JSON structured like this:

```json
[
    {
        "sku": "sku1234",
        "barcode": "P4d119947-271f-4c59-95e9-dea70b84b6d1",
        "name": "iPhone 5s",
        "manufacturer": {
            "manufacturer_id": 1,
            "name": "Apple"
        }
    },
    {
        "sku": "sku2345",
        "barcode": "P104ec297-f258-4160-a6ff-567a125937b0",
        "name": "iPad Mini",
        "manufacturer": {
            "manufacturer_id": 1,
            "name": "Apple"
        }
    }
]
```

This endpoint retrieves a list of current products

### HTTP Request
`GET https://api.getconvoy.com/products`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | If set, will retrieve a specific set of products
count | 25 | The number of products per page to return.  Cannot exceed 50.
manufacturer_id | None | If set, will only return products related to the specified manufacturer


## Get a Product

```python
import requests

response = requests.get("https://api.getconvoy.com/products/sku/sku1234",
    headers={'Authorization': 'API_KEY'})
```

> The above command returns JSON structured like this:

```json
{
    "sku": "sku1234",
    "barcode": "P4d119947-271f-4c59-95e9-dea70b84b6d1",
    "name": "iPhone 5s",
    "manufacturer": {
        "manufacturer_id": 1,
        "name": "Apple"
    }
}
```

This endpoint retrieves a product by its SKU/Identifier

### HTTP Request
`GET https://api.getconvoy.com/products/sku/<sku>`

### URL Parameters

Parameter | Description
--------- | -----------
sku | The SKU of the product you want to retrieve


## Get a Product

```python
import requests

response = requests.get(
    "https://api.getconvoy.com/products/barcode/P4d119947-271f-4c59-95e9-dea70b84b6d1",
    headers={'Authorization': 'API_KEY'})
```

> The above command returns JSON structured like this:

```json
{
    "sku": "sku1234",
    "barcode": "P4d119947-271f-4c59-95e9-dea70b84b6d1",
    "name": "iPhone 5s",
    "manufacturer": {
        "manufacturer_id": 1,
        "name": "Apple"
    }
}
```

This endpoint retrieves a product by its barcode.

### HTTP Request
`GET https://api.getconvoy.com/products/barcode/<barcode>`

### URL Parameters

Parameter | Description
--------- | -----------
barcode | The barcode of the product you want to retrieve.


## Create a Product

```python
import requests

data = {
    "name": "Nexus S",
    "sku": "sku3456",
    "manufacturer_id": 2
}
response = requests.post("https://api.getconvoy.com/products",
    data=data,
    headers={'Authorization': 'API_KEY'})
```

> The above command returns JSON structured like this:

```json
{
    "sku": "sku3456",
    "name": "Nexus S",
    "barcode": "P39dcc365-f09f-4e1a-991c-990094806025",
    "manufacturer": {
        "manufacturer_id": 2,
        "name": "Google"
    }
}
```

This endpoint creates a product.

### HTTP Request
`POST https://api.getconvoy.com/products`

### POST Parameters

Parameter | Description
--------- | -----------
name | The name of the product.
sku | The SKU associated with the product line.
manufacturer_id | The manufacturer of this product.


# Inventory

## Get All Inventory Items

```python
import requests

response = requests.get("https://api.getconvoy.com/inventory",
    headers={'Authorization': 'API_KEY'})
```

> The above command returns JSON structured like this:

```json
[
    {
        "state": "INVENTORIED",
        "barcode": "I954d3fae-885e-4e46-b9fb-5de959acd7b5",
        "date_created": 1470287770,
        "date_modified": 1470287770,
        "product": {
            "sku": "sku1234",
            "name": "iPhone 5s",
            "manufacturer": {
                "manufacturer_id": 1,
                "name": "Apple"
            }
        }
    },
    {
        "state": "PACKED",
        "barcode": "I3b8c1c7e-9301-4ca2-89c8-b389bb2bdd6e",
        "date_created": 1470201567,
        "date_modified": 1470203927,
        "product": {
            "sku": "sku2345",
            "name": "iPad Mini",
            "manufacturer": {
                "manufacturer_id": 1,
                "name": "Apple"
            }
        }
    }
]
```

This endpoint retrieves all inventory items in most recently created order

### HTTP Request
`GET https://api.getconvoy.com/inventory`

### QUERY PARAMETERS

Parameter | Default | Description
--------- | ------- | -----------
state | None | Only inventory items in this state will be returned
sku | None | Only inventory items of this product type will be returned
page | 1 | If set, will return a specific page of products
count | 25 | The number of inventory items to return per page. Cannot be over 50.


## Get an Inventory Item

```python
import requests

response = requests.get("https://api.getconvoy.com/inventory/<barcode>",
    headers={'Authorization': 'API_KEY'})
```

> The above command returns JSON structured like this:

```json
{
    "state": "INVENTORIED",
    "barcode": "I954d3fae-885e-4e46-b9fb-5de959acd7b5",
    "date_created": 1470287770,
    "date_modified": 1470287770,
    "product": {
        "sku": "sku1234",
        "name": "iPhone 5s",
        "manufacturer": {
            "manufacturer_id": 1,
            "name": "Apple"
        }
    }
}
```

This endpoint retrieves an inventory item by barcode

### HTTP Request
`GET https://api.getconvoy.com/inventory/<barcode>`

### URL Parameters

Parameter | Description
--------- | -----------
barcode | Barcode associated with the inventory item.


## Create an Inventory Item

```python
import requests

data = {
    'sku': 'sku1234',
    'quantity': 20
}
response = requests.get("https://api.getconvoy.com/inventory",
    data=data,
    headers={'Authorization': 'API_KEY'})
```

> The above command returns JSON structured like this:

```json
[
    {
        "state": "INVENTORIED",
        "barcode": "Ic3568f2c-a9e7-4f2e-b735-a351506c2897",
        "date_created": 1470289468,
        "date_modified": 1470289468,
        "product": {
            "sku": "sku1234",
            "name": "iPhone 5s",
            "manufacturer": {
                "manufacturer_id": 1,
                "name": "Apple"
            }
        }
    },
    ...
]
```

This endpoint creates `quantity` number of items in inventory of `sku` product type.

### HTTP Request
`POST https://api.getconvoy.com/inventory`

### POST Parameters

Parameter | Description
--------- | -----------
sku | The product sku which you want to add to inventory
quantity | The number of items to add to the inventory


## Update an Inventory Item

```python
import requests

data = {'state': 'PACKED'}
response = requests.put(
    "https://api.getconvoy.com/inventory/I954d3fae-885e-4e46-b9fb-5de959acd7b5",
    data=data,
    headers={'Authorization': 'API_KEY'})
```

> The above command returns JSON structured like this:

```json
[
    {
        "state": "PACKED",
        "barcode": "I954d3fae-885e-4e46-b9fb-5de959acd7b5",
        "date_created": 1470287770,
        "date_modified": 1470287770,
        "product": {
            "sku": "sku1234",
            "name": "iPhone 5s",
            "manufacturer": {
                "manufacturer_id": 1,
                "name": "Apple"
            }
        }
    }
]
```

This endpoint updates an inventory item specified by the `barcode`

### HTTP Request
`PUT https://api.getconvoy.com/inventory/<barcode>`

### URL Parameters

Parameter | Description
--------- | -----------
barcode | The barcode associated with a specific inventory item

### PUT Parameters

Parameter | Description
--------- | -----------
state | The state of the inventory item.
