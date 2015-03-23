---
title: API Reference

language_tabs:
  - shell
  - node

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:

search: true
---

# Introduction

Welcome to the Coinpliance API!


# Merchants

## Create new Merchant

```shell
curl -H "Content-type: application/json" --data-binary @$1 -u <companyname>api:(apiKey) -XPUT http://<companyname>:8501/<companyname>/api/merchants/<companyname>db:(id)

```

> The above command returns JSON structured like this:

```json
{
  "moatId":"<companyname>db:150932"
}
```

This endpoint creates a new merchant in CP mapped to BP. 

### HTTP Post

`POST https://coinpliance.us/<companyname>/merchants`

### Post elements

Parameter |  Description
--------- |  -----------
merchant | merchant object 
users | array of users associatied with that merchant

### Merchant Object

Parameter | Description
--------- |  -----------
name | Merchant Name (business)
owners | array contaning owners for that merchant account {name, eid}
address | address object 
contactPhone | phone number
website | url 
industry | obvious 
isNonprofit | true/false
usTaxID | ein if supplied
appliedTier | tier the merchant whishes to go to
approvedTier | current Tier of the merchant (should be set to -1)
suspended | true/false

## Request Tier Upgrade

```shell
curl -H "Content-type: application/json" --data-binary @$1 -u <companyname>api:aee65f98-4947-4f29-a1e5-461c6fa002ba -XPUT http://coinpliance.us/<companyname>/api/merchants/<companyname>db:$2

```


> ---------------- Returns------------------

```json
{
  "reasonCode": code,
  "upgradeLink": "Some upgrade https link"
}
```

This endpoint sends a tier upgrade request to Coinpliance. 

### PUT Request

`PUT https://coinpliance.us/<companyname>/merchants/<ID>`

### Body Params

Parameter | Description
--------- | -----------
appliedTier | the tier the merchant <ID> would like to go to

### Reason Codes

Code | Description 
---- | -----------
1010 | Holy crap something blew up. Abort
1011 | No docs required for this upgrade
1012 | Docs already submitted for this possible upgrade 
1013 | Invalid request to upgrade to a lower tier 
1009 | Success 

