---
title: Global Automotives Cloud - API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php

toc_footers:
  - <a href='https://global.automotivescloud.com/my-account'>Sign Up for a Developer Key</a>
  - <a href='https://www.automotivescloud.com'>Documentation Powered by Automotives Cloud</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Global Automotives Cloud API! You can use our API to access Vehicle API endpoints, which can get information on vehicle based on registration/plate number in our database.

We have language bindings in Shell and PHP! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

If you have any question or feedback, you are feel free to contact [Automotives Cloud](https://global.automotivescloud.com).

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: Bearer API_TOKEN"
  -H "Accept: application/json"
```

```php
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

> Make sure to replace `API_TOKEN` with your API token.

Global Automotives Cloud uses API tokens to allow access to the API. You will get API TOKEN on [Global Automotives Cloud](https://global.automotivescloud.com/my-account/settings).

Global Automotives Cloud expects for the API Token and Accept type to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer API_TOKEN`
`Accept: application/json`

In addition, you must add

<aside class="notice">
You must replace <code>API_TOKEN</code> with your personal API Token.
</aside>
<aside class="notice">
You must add <code>Accept: application/json</code> in header.
</aside>

# Vehicle

## Get vehicle by registration/plate number

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "https://global.automotivescloud.com/api/v1/vehicle" \
  -H "Authorization: Bearer API_TOKEN"
  -H "Accept: application/json"
  -d "country_code={country_code}"
  -d "registration_no={registration_no}"
```
> You must replace `{country_code}` with two character country code and `{registration_no}` with your real registration/plate number.
> The above command returns JSON structured (Country wise vehicle data can be different) like this:

```json
{
    "data": {
        "general": {
            "Description": "RENAULT SCÉNIC III",
            "RegistrationYear": "2016",
            "CarMake": "RENAULT",
            "CarModel": "SCÉNIC III",
            "EngineSize": "5",
            "FuelType": "DIESEL",
            "MakeDescription": "RENAULT",
            "ModelDescription": "SCÉNIC III",
            "Immobiliser": "",
            "IndicativeValue": 0,
            "DriverSide": "",
            "BodyStyle": "MONOSPACE COMPACT",
            "RegistrationDate": "2016-06-24",
            "ImageUrl": "http://immatriculationapi.com/image.aspx/@UkVOQVVMVCBTQ8OJTklDIElJSQ==",
            "VIN": "VF1JZ890H55864144"
        },
        "others": {
            "FirstManufacturingYear": "2016",
            "Transmission": "",
            "FuelTypeCode": "D",
            "BodyVersionCode": "",
            "SafetyClassification": "",
            "VersionTrim": "1.5 dCi 1461cm3 110cv ",
            "VersionCode": "",
            "MakeCode": "RE",
            "ModelCode": "",
            "ProductCode": "",
            "BodyCode": "",
            "SeatNumber": "5",
            "FirstRegistrationDate": "24062016",
            "BatteryIssues": "",
            "ElectricCar": "",
            "Type": "",
            "TypeCode": "",
            "ValueAsNew": "",
            "RiskLevel": "",
            "ManufacturerProtection": "",
            "DynamicPower": "110",
            "VehicleSegmentCode": ""
        }
    }
}
```

This endpoint retrieves registration details of vehicle.

### HTTP Request

`GET https://global.automotivescloud.com/api/v1/vehicle/`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
registration_no |  | Charge will be taken on each success call. For free testing you have to use predefined registration number based on country. Please see [Free Registration Number](#free-registration-number)
country_code | fr | Please see [Available Countries](#available-countries)

<aside class="warning">You will be charged on each call of vehicle if you don't use free registration numbers.</aside>

# Available Countries

Right now we are supporting only one country. More are coming soon.  If you have any request please let me know.

### Countries List

Country Code | Description
--------- | -------
fr | Franch
it | Italy

# Free Registration Number

Following registration number is only for testing. We will not take charge if you use these numbers. Otherwise, you will be charged on each call.

### Registration/plate number
Country Code | Registration Number | Description
--------- | ------- | -----------
fr | Eg258ma |
it | BN071VN |

<aside class="warning">You will be charged on each call of vehicle if you don't use above registration numbers.</aside>
