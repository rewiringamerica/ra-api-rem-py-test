# BuildingProfile

A class representing the known geographic features and building characteristics for a given residence.  Attributes ----------     county (str): The county where a residence is located (in GISJOIN format).     puma (str): The Public Use Microdata Area (PUMA) where a residence is located (in GISJOIN format).     ashrae_iecc_climate_zone_2004 (str): The IECC Climate Zone where a residence is located.     weather_file_city (str): The location of the ResStock Weather File used for the area where the residence         is located.     state (str): The 2 letter postal code of the state where the residence is located.     building_features(BuildingFeatures): The building characteristics found for the residence. See BuildingFeatures         documentation for full details about possible characteristics and their meanings.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**county** | **str** |  | 
**puma** | **str** |  | 
**ashrae_iecc_climate_zone_2004** | **str** |  | 
**weather_file_city** | **str** |  | 
**state** | **str** |  | 
**building_features** | [**BuildingFeatures**](BuildingFeatures.md) |  | [optional] 

## Example

```python
from rewiringamerica_rem.models.building_profile import BuildingProfile

# TODO update the JSON string below
json = "{}"
# create an instance of BuildingProfile from a JSON string
building_profile_instance = BuildingProfile.from_json(json)
# print the JSON string representation of the object
print(BuildingProfile.to_json())

# convert the object into a dict
building_profile_dict = building_profile_instance.to_dict()
# create an instance of BuildingProfile from a dict
building_profile_from_dict = BuildingProfile.from_dict(building_profile_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


