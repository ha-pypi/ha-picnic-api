# HA-Picnic-API


Forked from version made by [Mike Brink](https://github.com/MikeBrink/python-picnic-api)

Unofficial Python wrapper for the [Picnic](https://picnic.app/nl/) API. While not all API methods have been implemented yet, you'll find most of what you need to build a working application are available. 

This library is not affiliated with Picnic and retrieves data from the endpoints of the mobile application. Use at your own risk.

## Getting started

The easiest way to install is directly from pip::

```
pip install ha-picnic-api
```


## Usage

I'll go over a few common operations here you'll most likely use in applications. 
To login:

```python
from ha_picnic_api import PicnicAPI

picnic = PicnicAPI(username='username', password='password', country_code="NL")
```

The country_code parameter defaults to NL, but you have to change it if you live in a different country than the Netherlands (Germany: DE, Belgium: BE).
You can also store your credentials by setting the store value to true, this will store your credentials and country_code in /config/app.yaml. 

## Searching for a product

```python
>>> picnic.search('coffee')
[{'type': 'CATEGORY', 'id': 'coffee', 'links': [{'type': 'SEARCH', 'href': 'https://storefront-prod.nl.picnicinternational.com/api/15/search?search_term=coffee'}], 'name': 'coffee', 'items': [{'type': 'SINGLE_ARTICLE', 'id': '10511523', 'decorators': [{'type': 'UNIT_QUANTITY', 'unit_quantity_text': '500 gram'}], 'name': 'Lavazza espresso koffiebonen', 'display_price': 599, 'price': 599, 'image_id': 'd3fb2888fc41514bc06dfd6b52f8622cc222d017d2651501f227a537915fcc4f', 'max_count': 50, 'unit_quantity': '500 gram', 'unit_quantity_sub': '€11.98/kg', 'tags': []}, ... 
```

## Check cart

```python
>>> picnic.get_cart()
{'type': 'ORDER', 'id': 'shopping_cart', 'items': [], 'delivery_slots': [...
```

## Manipulating your cart

All of these methods will return the shopping cart.

```python
# adding 2 'Lavazza espresso koffiebonen' to cart
picnic.add_product('10511523', count=2)

# removing 1 'Lavazza espresso koffiebonen' from cart
picnic.remove_product('10511523')

# clearing the cart
picnic.clear_cart()
```

## See upcoming deliveries

```python
>>> picnic.get_current_deliveries()
[]
```

See available delivery slots
----------------------------
```python
>>> picnic.get_delivery_slots()
```