# BuildingFeatures

A class representing the set of possible building characteristics.  All values default to None, indicating that the given characteristic is unknown for the represented residence. If a characteristic has the string value of \"None\" it indicates that the characteristic, like Air Conditioning or a Pool, is not present at the represented residence.  Attributes ----------     geometry_floor_area (float | None): The square footage of the residence.     geometry_stories (float | None): The number of stories in the residence..     bedrooms (float | None): The number of bedrooms contained in the residence.     bathrooms (float | None) : The number of bathrooms contained in the residence.     vintage (float | None): The year in which the residence was built.     geometry_attic_type (List[str] | None): The type of attic.     hvac_cooling_type (List[str] | None): The type of cooling system present in the residence.     hvac_heating_type (List[str] | None): The type of ductwork used for heating in the residence.     geometry_garage (List[str] | None): The size of the garage as measured in the number of cars         that can be placed within the garage.     misc_pool (List[str] | None): A string indicating the presence of a pool at the residence.     misc_hot_tub_spa (List[str] | None): The fuel type used to heat a hot tub if one is present         at the residence.     misc_well_pump (List[str] | None): The efficiency of a well pump if one is located at the residence.     misc_pool_heater (List[str] | None): The presence and fuel type of a pool heater.     geometry_wall_type (List[str] | None): The material of the exterior walls on the residence.     geometry_wall_exterior_finish (List[str] | None): The finish and color of exterior walls         on the residence.     roof_material (List[str] | None): The material of the roof on the residence.     geometry_building_type_acs (List[str] | None): The American Community Survey building type         of the residence.     geometry_building_number_units_sfa (float | None): The number of units in a single-family attached building.     geometry_building_number_units_mf (float | None): The number of units in a multifamily building.     heating_fuel (List[str] | None): The primary fuel used for heating the residence.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**geometry_floor_area** | **float** |  | [optional] 
**geometry_stories** | **float** |  | [optional] 
**bedrooms** | **float** |  | [optional] 
**bathrooms** | **float** |  | [optional] 
**vintage** | **float** |  | [optional] 
**geometry_attic_type** | **List[str]** |  | [optional] 
**hvac_cooling_type** | **List[str]** |  | [optional] 
**hvac_heating_type** | **List[str]** |  | [optional] 
**geometry_garage** | **List[str]** |  | [optional] 
**misc_pool** | **List[str]** |  | [optional] 
**misc_hot_tub_spa** | **List[str]** |  | [optional] 
**misc_well_pump** | **List[str]** |  | [optional] 
**misc_pool_heater** | **List[str]** |  | [optional] 
**geometry_wall_type** | **List[str]** |  | [optional] 
**geometry_wall_exterior_finish** | **List[str]** |  | [optional] 
**roof_material** | **List[str]** |  | [optional] 
**geometry_building_type_acs** | **List[str]** |  | [optional] 
**geometry_building_number_units_sfa** | **float** |  | [optional] 
**geometry_building_number_units_mf** | **float** |  | [optional] 
**heating_fuel** | **List[str]** |  | [optional] 

## Example

```python
from rewiringamerica_rem.models.building_features import BuildingFeatures

# TODO update the JSON string below
json = "{}"
# create an instance of BuildingFeatures from a JSON string
building_features_instance = BuildingFeatures.from_json(json)
# print the JSON string representation of the object
print(BuildingFeatures.to_json())

# convert the object into a dict
building_features_dict = building_features_instance.to_dict()
# create an instance of BuildingFeatures from a dict
building_features_from_dict = BuildingFeatures.from_dict(building_features_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


