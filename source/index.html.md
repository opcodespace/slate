---
title: Global Automotives Cloud - API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php

toc_footers:
  - <a href='https://global.automotivescloud.com/my-account'>Sign Up for a API Token</a>
  - <a href='mailto:support@automotivescloud.com'>support@automotivescloud.com</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Global Automotives Cloud API! You can use our API to access Vehicle API endpoints, which can get information on vehicle based on registration/plate number in our database.

We have language bindings in Shell and PHP! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

If you have any question or feedback, you are feel free to contact [Automotives Cloud](https://global.automotivescloud.com) or send e-mail to [support@automotivescloud.com](mailto:support@automotivescloud.com).

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: Bearer API_TOKEN"
  -H "Accept: application/json"
```

```php

```

> Make sure to replace `API_TOKEN` with your API token.

Global Automotives Cloud uses API tokens to allow access to the API. You will get API TOKEN on [Global Automotives Cloud](https://global.automotivescloud.com/my-account/settings).

Global Automotives Cloud expects for the API Token and Accept type to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer API_TOKEN`
`Accept: application/json`

<aside class="notice">
You must replace <code>API_TOKEN</code> with your personal API Token.
</aside>
<aside class="notice">
You must add <code>Accept: application/json</code> in header.
</aside>

# Vehicle

## Get vehicle by registration/plate number

```php
// You will get api token here https://global.automotivescloud.com/my-account/settings
$api_token = '<API TOKEN>';

$data = [
    'registration_no' => 'Eg258ma',
    'country_code' => 'fr'
];

$url  = "https://global.automotivescloud.com/api/v1/vehicle?" . http_build_query($data);

$ch = curl_init();
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer '. $api_token,
    'Accept: application/json'
    ]
);
//Get the response from cURL
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_URL, $url);
$result = json_decode(curl_exec($ch), true);
$httpcode = curl_getinfo($ch, CURLINFO_HTTP_CODE);
curl_close($ch);

if($httpcode != 200){
    // on Error
    echo $result['message'];
}
else{
    // On Success
    echo '<pre>'; print_r($result); echo '</pre>';
}
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
          // available data should be here
        },
        "others": {
          // available data should be here
        }
    }
}
```

This endpoint retrieves registration details of vehicle.

### HTTP Request

`GET https://global.automotivescloud.com/api/v1/vehicle`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
registration_no |  | Charge will be taken on each success call. For free testing you have to use predefined registration number based on country. Please see [Free Registration Number](#free-registration-number)
country_code | fr | Please see [Available Countries](#available-countries)

<aside class="warning">You will be charged on each call of vehicle if you don't use free registration numbers.</aside>

### Return

On success you will get details of vehicle as per country. Please see [available data based on country](##available-data-based-on-country). If you have error please see [errors section](#errors) for details.

# Available Countries

Right now we are supporting only two countries. More are coming soon.  If you have any request, please let us know.

### Countries List

Country Code | Description
--------- | -------
fr | France
it | Italy

# Free Registration Number

Following registration number is only for testing. We will not take charge if you use these numbers. Otherwise, you will be charged on each call.

### Registration/plate number
Country Code | Registration Number | Description
--------- | ------- | -----------
fr | Eg258ma |
it | BN071VN |

<aside class="warning">You will be charged on each call of vehicle if you don't use above registration numbers.</aside>

# Available Data Based on Country
## France
```json
{
    "data": {
        "general": {
            "Description": "RENAULT SCÉNIC III",
            "RegistrationYear": "2016",
            "VehicleMake": "RENAULT",
            "VehicleModel": "SCÉNIC III",
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
            "ElectricVehicle": "",
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
> Registration details of France


### General
Field | Description
--------- | -------
Description |
RegistrationYear |
VehicleMake |
VehicleModel |
EngineSize |
FuelType |
MakeDescription |
ModelDescription |
Immobiliser |
IndicativeValue |
DriverSide |
BodyStyle |
RegistrationDate |
ImageUrl |
VIN |


### Others
Field | Description
--------- | -------
FirstManufacturingYear |
Transmission |
FuelTypeCode |
BodyVersionCode |
SafetyClassification |
VersionTrim |
VersionCode |
MakeCode |
ModelCode |
ProductCode |
BodyCode |
SeatNumber |
FirstRegistrationDate |
BatteryIssues |
ElectricVehicle |
Type |
TypeCode |
ValueAsNew |
RiskLevel |
ManufacturerProtection |
DynamicPower |
VehicleSegmentCode |

## Italy

```json
{
    "data": {
        "general": {
            "Description": "Peugeot 206",
            "RegistrationYear": "2000",
            "VehicleMake": "Peugeot",
            "VehicleModel": "206",
            "EngineSize": "14 cv (da 1119,2 a 1243,6 cc.)",
            "FuelType": "Benzina",
            "MakeDescription": "Peugeot",
            "ModelDescription": "206",
            "Immobiliser": "",
            "VIN": "",
            "ImageUrl": "http://www.targa.co.it/image.aspx/@UGV1Z2VvdCAyMDY=",
            "NumberOfDoors": "",
            "Version": "206 1.1 3p. Xr (08-2000)",
            "ABS": "N",
            "AirBag": "S",
            "KType": "",
            "PowerCV": "",
            "PowerKW": "",
            "PowerFiscal": ""
        },
        "others": []
    }
}
```
>Registration details of Italy

### General
Field | Description
--------- | -------
Description |
RegistrationYear |
VehicleMake |
VehicleModel |
EngineSize |
FuelType |
MakeDescription |
ModelDescription |
Immobiliser |
ImageUrl |
VIN |
NumberOfDoors |
Version |
ABS |
AirBag |
KType |
PowerCV |
PowerKW |
PowerFiscal |