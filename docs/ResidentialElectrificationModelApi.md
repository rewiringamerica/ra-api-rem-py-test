# rewiringamerica_rem.ResidentialElectrificationModelApi

All URIs are relative to *https://api.rewiringamerica.org*

Method | HTTP request | Description
------------- | ------------- | -------------
[**get_by_address**](ResidentialElectrificationModelApi.md#get_by_address) | **GET** /api/v1/rem/address | Get By Address
[**get_by_profile**](ResidentialElectrificationModelApi.md#get_by_profile) | **POST** /api/v1/rem/profile | Get By Profile
[**get_impl_version**](ResidentialElectrificationModelApi.md#get_impl_version) | **GET** /api/v1/rem/server_version | Get Impl Version


# **get_by_address**
> Savings get_by_address(upgrade, address, heating_fuel)

Get By Address

Predict a user's savings using the Residential Electrification Model.  This API makes predictions of the effects of an upgrade based on the address of the home being upgraded, and the current heating fuel.  Using the provided address, it first queries a large database of home properties that Rewiring America has assembled, which contains data such as home age, size, construction material, and much more. We don't know all of the properties needed to get a good estimate of energy consumption, so we perform a [Monte Carlo](https://en.wikipedia.org/wiki/Monte_Carlo_method) simulation over a sample homes chosen from a [conditional probability distribution](https://github.com/NREL/resstock/tree/develop/project_national/housing_characteristics) based the properties that we do know. We then estimate the energy consumption for each sample building by running inference using a Machine Learning based surrogate model, trained on [EnergyPlus](https://energyplus.net/) simulations.  The response JSON is a dictionary with three components: - `fuel_results`: This is a dictionary of the main results from the model, one for each heating fuel type,   which are:   - `electricity`   - `fuel_oil`   - `natural_gas`   - `propane`   - `total` (for the total of all the others). - `rates`: A summary of the rates used to calculate the cost in dollars of the fuels used. - `emissions_factors`: A summary of the local emissions factors used to calculate emissions.   These vary from region to region based on how electricity is generated and the nature of   other fuels.  Within the `fuel_results` subsection for each of the fuel types, there are three components:   - `baseline`: the usage of the fuel before the upgrade   - `upgrade`: the usage of the fuel after the upgrade   - `delta`: the change is usage of the fuel.  Inside those three, there are parallel structures with statistics for the `energy` used in the form the fuel, the `emissions` associated with the use of the fuel, and  the `cost` of the fuel. The electricity emissions factors are [long run marginal emissions rates assuming a 95% decarbonized grid by 2050](https://www.nrel.gov/analysis/cambium.html). The emissions and costs are computed with the help of the numbers returned in the `rates` and `emissions_factors` data mentioned above, where the costs the reflect the annual costs from volumetric charges and fixed charges. Note that the fixed charges are based on the presense of the given fuel in the baseline scenario, and not assumed to change in the upgrade scenario. All of the statistics are for a full typical weather year. The units for each of the statistics are also provided and are as appropriate for the fuel, emissions, or cost.  *A note on statistics*: For each value we provide statistics for, we provide a mean, a median, and the 20th and 80th percentile values over all the set of sample homes in the Monte Carlo simulation. It is important to note that the statistics are taken over the distribution of the values they represent. This means, for example, that the median in terms of electricity usage before the upgrade and the median in terms of electricity usage after the upgrade and the median in terms of change of electricity usage might not be the same, so adding the median change to the median usage before the upgrade might fail to produce the number reported as the median usage after the upgrade.  Note that because we are modeling whole home energy consumption over a set of building samples, and the building set contains homes with a variety of fuels for the non-heating appliances, you may see consumption of fuels other than the passed heating fuel, particularly for the mean.  ### Demonstrations  There are two sample Python notebooks that demonstrate the API in action.  - [REM Demo.ipynb](https://github.com/rewiringamerica/api_demos/blob/main/notebooks/REM%20Demo.ipynb) illustrates   basic API calls. - [All About REM   Statistics.ipynb](https://github.com/rewiringamerica/api_demos/blob/main/notebooks/All%20About%20REM%20Statistics.ipynb)   digs into details on the statistics that the API returns and how they relate to one another in various   circumstances.  If you would like to integrate the REM API into a web site, there is also an example.  - [HTML/JavaScript Demo](https://github.com/rewiringamerica/api_demos/tree/main/www)   illustrates how to call the API from JavaScript on a simple web page. It shows how the   API could be used to allow a web site visitor to enter their address and see how much   they could save by installing a heat pump.

### Example

* Bearer Authentication (auth):

```python
import rewiringamerica_rem
from rewiringamerica_rem.models.heating_fuel import HeatingFuel
from rewiringamerica_rem.models.savings import Savings
from rewiringamerica_rem.models.supported_upgrade import SupportedUpgrade
from rewiringamerica_rem.rest import ApiException
from pprint import pprint


# Configure Bearer authorization: auth
configuration = rewiringamerica_rem.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with rewiringamerica_rem.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = rewiringamerica_rem.ResidentialElectrificationModelApi(api_client)
    upgrade = rewiringamerica_rem.SupportedUpgrade() # SupportedUpgrade | The upgrade whose effects we want to analyze. Supported values are as follows: - `basic_enclosure`: A basic weatherization upgrade for the home   as described in measure package 1 (on page 4) of [this   document](https://oedi-data-lake.s3.amazonaws.com/nrel-pds-building-stock/end-use-load-profiles-for-us-building-stock/2022/EUSS_ResRound1_Technical_Documentation.pdf). - `min_eff_hp_elec_backup`: A relatively-low efficiency heat pump upgrade for the home’s HVAC   system as described in measure package 3 (on page 5) of [this   document](https://oedi-data-lake.s3.amazonaws.com/nrel-pds-building-stock/end-use-load-profiles-for-us-building-stock/2022/EUSS_ResRound1_Technical_Documentation.pdf). - `high_eff_hp_elec_backup`: A high efficiency heat pump upgrade for the home’s HVAC system as   described in measure package 4 (on page 6) of [this   document](https://oedi-data-lake.s3.amazonaws.com/nrel-pds-building-stock/end-use-load-profiles-for-us-building-stock/2022/EUSS_ResRound1_Technical_Documentation.pdf). - `whole_home_electric_max_eff_basic_enclosure`: A whole-home upgrade including a high   efficiency heat pump for the home’s HVAC system, basic weatherization, a heat pump water heater, a heat pump dryer,   and an induction stove as described in measure package 9 (on page 9) of [this   document](https://oedi-data-lake.s3.amazonaws.com/nrel-pds-building-stock/end-use-load-profiles-for-us-building-stock/2022/EUSS_ResRound1_Technical_Documentation.pdf). - `med_eff_hp_hers_sizing_no_setback`: A medium-efficiency heat pump upgrade for   the home's HVAC system. Rewiring America simulated this upgrade using the same tools NREL uses for ResStock. - `med_eff_hp_hers_sizing_no_setback_basic_enclosure`: A custom upgrade based on a   medium-efficiency heat pump and basic weatherization upgrade for the home. Rewiring America simulated this upgrade   using the same tools NREL uses for ResStock. 
    address = 'address_example' # str | The address of the home being upgraded.
    heating_fuel = rewiringamerica_rem.HeatingFuel() # HeatingFuel | The heating fuel used in the home before the upgrade. Supported values are as follows: - `electricity`: the home was heated with electric heating, such as   baseboard heating, an electric boiler, or an electric furnace. - `natural_gas`: The home was heated with a natural gas furnace. - `fuel_oil`: The home was heated with a fuel oil boiler or furnace. - `propane`:  The home was heated with a propane furnace. 

    try:
        # Get By Address
        api_response = api_instance.get_by_address(upgrade, address, heating_fuel)
        print("The response of ResidentialElectrificationModelApi->get_by_address:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling ResidentialElectrificationModelApi->get_by_address: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **upgrade** | [**SupportedUpgrade**](.md)| The upgrade whose effects we want to analyze. Supported values are as follows: - &#x60;basic_enclosure&#x60;: A basic weatherization upgrade for the home   as described in measure package 1 (on page 4) of [this   document](https://oedi-data-lake.s3.amazonaws.com/nrel-pds-building-stock/end-use-load-profiles-for-us-building-stock/2022/EUSS_ResRound1_Technical_Documentation.pdf). - &#x60;min_eff_hp_elec_backup&#x60;: A relatively-low efficiency heat pump upgrade for the home’s HVAC   system as described in measure package 3 (on page 5) of [this   document](https://oedi-data-lake.s3.amazonaws.com/nrel-pds-building-stock/end-use-load-profiles-for-us-building-stock/2022/EUSS_ResRound1_Technical_Documentation.pdf). - &#x60;high_eff_hp_elec_backup&#x60;: A high efficiency heat pump upgrade for the home’s HVAC system as   described in measure package 4 (on page 6) of [this   document](https://oedi-data-lake.s3.amazonaws.com/nrel-pds-building-stock/end-use-load-profiles-for-us-building-stock/2022/EUSS_ResRound1_Technical_Documentation.pdf). - &#x60;whole_home_electric_max_eff_basic_enclosure&#x60;: A whole-home upgrade including a high   efficiency heat pump for the home’s HVAC system, basic weatherization, a heat pump water heater, a heat pump dryer,   and an induction stove as described in measure package 9 (on page 9) of [this   document](https://oedi-data-lake.s3.amazonaws.com/nrel-pds-building-stock/end-use-load-profiles-for-us-building-stock/2022/EUSS_ResRound1_Technical_Documentation.pdf). - &#x60;med_eff_hp_hers_sizing_no_setback&#x60;: A medium-efficiency heat pump upgrade for   the home&#39;s HVAC system. Rewiring America simulated this upgrade using the same tools NREL uses for ResStock. - &#x60;med_eff_hp_hers_sizing_no_setback_basic_enclosure&#x60;: A custom upgrade based on a   medium-efficiency heat pump and basic weatherization upgrade for the home. Rewiring America simulated this upgrade   using the same tools NREL uses for ResStock.  | 
 **address** | **str**| The address of the home being upgraded. | 
 **heating_fuel** | [**HeatingFuel**](.md)| The heating fuel used in the home before the upgrade. Supported values are as follows: - &#x60;electricity&#x60;: the home was heated with electric heating, such as   baseboard heating, an electric boiler, or an electric furnace. - &#x60;natural_gas&#x60;: The home was heated with a natural gas furnace. - &#x60;fuel_oil&#x60;: The home was heated with a fuel oil boiler or furnace. - &#x60;propane&#x60;:  The home was heated with a propane furnace.  | 

### Return type

[**Savings**](Savings.md)

### Authorization

[auth](../README.md#auth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details

| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** | Successful Response |  -  |
**422** | Validation Error |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_by_profile**
> Savings get_by_profile(rem_profile_request)

Get By Profile

Predict a user's savings using Residential Electrification Model using a Building Profile and an Upgrade.  This implementation takes in a dictionary of required inputs for the request body.  Parameters ----------     rem_profile_req (RemProfileRequest): An object containing all of the necessary inputs for Dohyo:         Upgrade, County, PUMA, Climate Zone, ResStock weather file location, state abbreviation, and         building features.  Returns -------     Savings: JSON containing prediction output from Dohyo.

### Example

* Bearer Authentication (auth):

```python
import rewiringamerica_rem
from rewiringamerica_rem.models.rem_profile_request import RemProfileRequest
from rewiringamerica_rem.models.savings import Savings
from rewiringamerica_rem.rest import ApiException
from pprint import pprint


# Configure Bearer authorization: auth
configuration = rewiringamerica_rem.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with rewiringamerica_rem.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = rewiringamerica_rem.ResidentialElectrificationModelApi(api_client)
    rem_profile_request = rewiringamerica_rem.RemProfileRequest() # RemProfileRequest | 

    try:
        # Get By Profile
        api_response = api_instance.get_by_profile(rem_profile_request)
        print("The response of ResidentialElectrificationModelApi->get_by_profile:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling ResidentialElectrificationModelApi->get_by_profile: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **rem_profile_request** | [**RemProfileRequest**](RemProfileRequest.md)|  | 

### Return type

[**Savings**](Savings.md)

### Authorization

[auth](../README.md#auth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details

| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** | Successful Response |  -  |
**422** | Validation Error |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_impl_version**
> str get_impl_version()

Get Impl Version

Return the back end version of the code that is deployed.  This is not the version of the API, but rather of the code that implements it. This is mainly to track code deployments. The same API version is typically supported by a series of deployments each of which improves upon earlier ones in some way, such as fixing bugs or improving performance.

### Example

* Bearer Authentication (auth):

```python
import rewiringamerica_rem
from rewiringamerica_rem.rest import ApiException
from pprint import pprint


# Configure Bearer authorization: auth
configuration = rewiringamerica_rem.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with rewiringamerica_rem.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = rewiringamerica_rem.ResidentialElectrificationModelApi(api_client)

    try:
        # Get Impl Version
        api_response = api_instance.get_impl_version()
        print("The response of ResidentialElectrificationModelApi->get_impl_version:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling ResidentialElectrificationModelApi->get_impl_version: %s\n" % e)
```



### Parameters

This endpoint does not need any parameter.

### Return type

**str**

### Authorization

[auth](../README.md#auth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details

| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** | Successful Response |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

