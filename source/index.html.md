---
title: Global Automotives Cloud - API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php

toc_footers:
  - <a href='https://global.automotivescloud.com/my-account'>Sign Up for a API Token</a>
  - <a href='mailto:global@automotivescloud.com'>global@automotivescloud.com</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Global Automotives Cloud API! You can use our API to access Vehicle API endpoints, which can get information on vehicle based on registration/plate number in our database.

We have language bindings in Shell and PHP! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

If you have any question or feedback, you are feel free to contact [Automotives Cloud](https://global.automotivescloud.com) or send e-mail to [global@automotivescloud.com](mailto:global@automotivescloud.com).

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
        // Available data should be here...
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
        "VIN": "VF1JZ890H55864144",
        "RegistrationDate": "2016-06-24",
        "RegistrationYear": "2016",
        "FirstRegistrationDate": "24062016",
        "FirstManufacturingYear": "2016",
        "Make": "RENAULT",
        "MakeCode": "RE",
        "MakeDescription": "RENAULT",
        "Model": "SCÉNIC III",
        "ModelCode": "",
        "ModelDescription": "SCÉNIC III",
        "Description": "RENAULT SCÉNIC III",
        "EngineSize": "5",
        "FuelType": "DIESEL",
        "FuelTypeCode": "D",
        "Immobiliser": "",
        "IndicativeValue": 0,
        "DriverSide": "",
        "BodyStyle": "MONOSPACE COMPACT",
        "BodyVersionCode": "",
        "BodyCode": "",
        "ImageUrl": "http://immatriculationapi.com/image.aspx/@UkVOQVVMVCBTQ8OJTklDIElJSQ==",
        "Transmission": "MECANIQUE",
        "Version": "1.5 dCi 1461cm3 110cv ",
        "SafetyClassification": "",
        "ProductCode": "",
        "SeatNumber": "5",
        "BatteryIssues": "",
        "ElectricVehicle": "",
        "ValueAsNew": "",
        "RiskLevel": "",
        "ManufacturerProtection": "",
        "DynamicPower": "110",
        "SegmentCode": "",
        "KtypeId": "5853",
        "EngineCC": "1461",
        "Co2": "105",
        "Cylinders": "4",
        "CNIT": "M10RENVP472E768",
        "Type": "VP",
        "TypeCode": "",
        "TypeAsEuropeanClassification": "Passenger Car",
        "TypeCodeAsEuropeanClassification": [
            "M1"
        ]
    }
}
```
> Registration details of France


Field | Type | Description
--------- | ------- | -------
VIN | string |
RegistrationDate | string |
RegistrationYear | string |
FirstRegistrationDate | string |
FirstManufacturingYear | string |
Make | string |
MakeCode | string |
MakeDescription | string |
Model | string |
ModelCode | string |
ModelDescription | string |
Description | string |
EngineSize | string |
FuelType | string |
FuelTypeCode | string |
Immobiliser | string |
IndicativeValue | string |
DriverSide | string |
BodyStyle | string |
BodyVersionCode | string |
BodyCode | string |
ImageUrl | string |
Transmission | string |
Version | string |
SafetyClassification | string |
ProductCode | string |
SeatNumber | string |
BatteryIssues | string |
ElectricVehicle | string |
ValueAsNew | string |
RiskLevel | string |
ManufacturerProtection | string |
DynamicPower | string |
SegmentCode | string |
KtypeId | string |
EngineCC | string |
Co2 | string |
Cylinders | string |
CNIT | string |
Type | string | As French Classification
TypeCode | string | As French Classification
TypeAsEuropeanClassification | string |
TypeCodeAsEuropeanClassification | array | Frech classification is mapped with European Calssification according to this this documentation https://www.carte-grise.org/docs/Liste-Genres-et-Energies_12-06-2009.pdf


## Italy

```json
{
    "data": {
        "VIN": "",
        "RegistrationYear": "2000",
        "Description": "Peugeot 206",
        "Make": "Peugeot",
        "MakeDescription": "Peugeot",
        "Model": "206",
        "ModelDescription": "206",
        "EngineSize": "14 cv (da 1119,2 a 1243,6 cc.)",
        "FuelType": "Benzina",
        "Immobiliser": "",
        "ImageUrl": "http://www.targa.co.it/image.aspx/@UGV1Z2VvdCAyMDY=",
        "NumberOfDoors": "",
        "Version": "206 1.1 3p. Xr (08-2000)",
        "ABS": "N",
        "AirBag": "S",
        "KType": "",
        "PowerCV": "",
        "PowerKW": "",
        "PowerFiscal": ""
    }
}
```
>Registration details of Italy

Field | Type | Description
--------- | ------- | -------
VIN | string |
RegistrationYear | string |
Description | string |
Make | string |
MakeDescription | string |
Model | string |
ModelDescription | string |
EngineSize | string |
FuelType | string |
Immobiliser | string |
ImageUrl | string |
NumberOfDoors | string |
Version | string |
ABS | string |
AirBag | string |
KType | string |
PowerCV | string |
PowerKW | string |
PowerFiscal | string |