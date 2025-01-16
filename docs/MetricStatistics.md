# MetricStatistics

Represents a statistic associated with a particular fuel and type of impact.  Attributes ----------     mean: Mean.     median: Median.     percentile_20: 20th percentile.     percentile_80: 80th percentile.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**mean** | [**Quantity**](Quantity.md) |  | 
**median** | [**Quantity**](Quantity.md) |  | 
**percentile_20** | [**Quantity**](Quantity.md) |  | 
**percentile_80** | [**Quantity**](Quantity.md) |  | 

## Example

```python
from rewiringamerica_rem.models.metric_statistics import MetricStatistics

# TODO update the JSON string below
json = "{}"
# create an instance of MetricStatistics from a JSON string
metric_statistics_instance = MetricStatistics.from_json(json)
# print the JSON string representation of the object
print(MetricStatistics.to_json())

# convert the object into a dict
metric_statistics_dict = metric_statistics_instance.to_dict()
# create an instance of MetricStatistics from a dict
metric_statistics_from_dict = MetricStatistics.from_dict(metric_statistics_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


