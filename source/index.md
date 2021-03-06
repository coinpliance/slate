---
title: API Reference

language_tabs:
  - shell
  - node


includes:

search: true
---

# Introduction

Welcome to the Coinpliance API!


# Merchants

## Create new Merchant

```shell
curl -H "Content-type: application/json" --data-binary @$1 -u <companyname>api:(apiKey) -XPUT https://<companyname>:8501/<companyname>/api/merchants/<companyname>db:(id)

```

> The above command returns JSON structured like this:

```json
{
  "moatId":"<companyname>db:150932"
}
```

This endpoint creates a new merchant in CP mapped to BP. 

### https Post

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
curl -H "Content-type: application/json" --data-binary @$1 -u <companyname>api:(apiKey) -XPUT https://coinpliance.us/<companyname>/api/merchants/<companyname>db:$2

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



##Get Recent Merchants 


```shell 
curl -k -H "Content-type: application/json" -u <companyname>api:(apiKey) -XGET https://coinpliance.us/<companyname>/api/merchants

```

> ---------------- Returns------------------

```json
[
	{
		"moat_id": "<companyname>:102103",
		"merchantGovTaxID": "123456789",
		"moatAppStatus": "approved",
		"approvedTier": "2", 
		"requiredTier": "1",
		"website": "www.example.com",
		"suspended": false
	},

	{
		"moat_id": "<companyname>:102103",
		"merchantGovTaxID": "123456789",
		"moatAppStatus": "approved",
		"approvedTier": "2", 
		"requiredTier": "1",
		"website": "www.example.com",
		"suspended": false
	}
]

```


```node

```

### GET Request

`GET https://coinpliance.us/<companyname>/api/merchants`


Returns all the merchants who have been updated via the coinpliance UI within the last 30 minutes.

###Return Values 

Name | Description | optional
---- | ----------- | --------
moat_id | companyname + : + coinpliance ID. Is the reference to the merchant in coinpliance. | no 
merchantGovTaxID | the Tax ID for the merchant if it has been submitted otherwise null. | yes
moatAppStatus | the processing status of the merchant. | no
approvedTier | the tier at which the merchant is cleard to process at. | no
requiredTier | the tier the merchant must be at to process funds. | no 
website | the merchants website | yes
suspended | True if merchant is suspended. False otherwise | no


## Get Specific

Returns details for the specific merchant.


```shell

curl -k -H "Content-type: application/json" -u <companyname>api:(apiKey) -XGET https://coinpliance.us/<companyname>/api/merchants/<companyname>:<coinplianceID>
```

> ---------------- Returns------------------

```json
	{
		"moat_id": "<companyname>:<cpID>",
		"merchantGovTaxID": "123456789",
		"moatAppStatus": "approved",
		"approvedTier": "2", 
		"requiredTier": "1",
		"website": "www.example.com",
		"suspended": false
	}
```

```node

```

Returns values are in the same format as get recent. 


### GET Request

`GET https://coinpliance.us/<companyname>/api/merchants/<companyname>:<coinplianceID>`




