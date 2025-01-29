# Quantity

A class to represent a quantity, which is a value with units.  Attributes ----------     value (float): The numerical value.     units (str): The units.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**value** | **float** |  | [optional] [default to 0.0]
**units** | **str** |  | 

## Example

```python
from rewiringamerica_rem.models.quantity import Quantity

# TODO update the JSON string below
json = "{}"
# create an instance of Quantity from a JSON string
quantity_instance = Quantity.from_json(json)
# print the JSON string representation of the object
print(Quantity.to_json())

# convert the object into a dict
quantity_dict = quantity_instance.to_dict()
# create an instance of Quantity from a dict
quantity_from_dict = Quantity.from_dict(quantity_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


