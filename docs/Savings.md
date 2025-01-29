# Savings

Represent the savings due to an upgrade.  Attributes ---------- fuel_results     A list of results, one for each fuel type. rates:     A list of rates used to compute the cost of fuel consumed. emissions_factors:     A list of factors used to compute the the emissions from various fuels.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**fuel_results** | [**Dict[str, FuelSavings]**](FuelSavings.md) |  | 
**rates** | **Dict[str, List[FuelRate]]** |  | 
**emissions_factors** | [**Dict[str, Quantity]**](Quantity.md) |  | 

## Example

```python
from rewiringamerica_rem.models.savings import Savings

# TODO update the JSON string below
json = "{}"
# create an instance of Savings from a JSON string
savings_instance = Savings.from_json(json)
# print the JSON string representation of the object
print(Savings.to_json())

# convert the object into a dict
savings_dict = savings_instance.to_dict()
# create an instance of Savings from a dict
savings_from_dict = Savings.from_dict(savings_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


