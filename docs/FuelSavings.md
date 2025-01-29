# FuelSavings

A class to represent savings data for a particular fuel.  Attributes ----------     baseline (FuelMetrics): The data if no upgrade is passed into the surrogate model.     upgrade (FuelMetrics): The data if an upgrade is passed into the surrogate model.     delta (FuelMetrics): The deltas if an upgrade is passed into the surrogate model.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**baseline** | [**ImpactMetric**](ImpactMetric.md) |  | 
**upgrade** | [**ImpactMetric**](ImpactMetric.md) |  | 
**delta** | [**ImpactMetric**](ImpactMetric.md) |  | 

## Example

```python
from rewiringamerica_rem.models.fuel_savings import FuelSavings

# TODO update the JSON string below
json = "{}"
# create an instance of FuelSavings from a JSON string
fuel_savings_instance = FuelSavings.from_json(json)
# print the JSON string representation of the object
print(FuelSavings.to_json())

# convert the object into a dict
fuel_savings_dict = fuel_savings_instance.to_dict()
# create an instance of FuelSavings from a dict
fuel_savings_from_dict = FuelSavings.from_dict(fuel_savings_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


