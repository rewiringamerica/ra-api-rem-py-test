# ImpactMetric

Represents a collection of impacts associated with a fuel.  Attributes ---------- energy     Energy statistics emissions     Emissions statistics cost     Cost statistics

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**energy** | [**MetricStatistics**](MetricStatistics.md) |  | 
**emissions** | [**MetricStatistics**](MetricStatistics.md) |  | 
**cost** | [**MetricStatistics**](MetricStatistics.md) |  | 

## Example

```python
from rewiringamerica_rem.models.impact_metric import ImpactMetric

# TODO update the JSON string below
json = "{}"
# create an instance of ImpactMetric from a JSON string
impact_metric_instance = ImpactMetric.from_json(json)
# print the JSON string representation of the object
print(ImpactMetric.to_json())

# convert the object into a dict
impact_metric_dict = impact_metric_instance.to_dict()
# create an instance of ImpactMetric from a dict
impact_metric_from_dict = ImpactMetric.from_dict(impact_metric_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


