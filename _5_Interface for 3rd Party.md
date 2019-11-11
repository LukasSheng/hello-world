
# 5. Interface for 3rd Party
## 5.1 UserManagement

To use any function of MoC middleware, 3rd party must have an account of MoC middleware. This account can contain all vehicles with MOC devices in its fleet, or only contains one client’s vehicles of 3rd party application. It is up to 3rd party how to manage its clients’ structure.

The application process is:

 - 3rd party application to apply an account with 5.1.1 Register function with its desired username (cannot be changed) and password (can be changed with 5.1.2 PasswardChange function). MoC admin needs to approve this account and confirm with 3rd party application by email.
 - 3rd party application needs to use the approved username and password in 5.1.3 AppIDSecret to apply the so-called AppID (cannot be changed) and AppSecret(can be reset with 5.1.4 AppSecretReset function). These two are the ID and passcode for MoC middleware services.

For this function, no AccessToken is needed.

### 5.1.1	Register 
> Example Request:
```json
{

"request_header":{

"timestamp":"1447644285294"

},

"request_body":{

"username":"mobilityoncloudvip",
"password":"123456aA934j)",
"email":"test@test.com",
"phone":"08618688860259"

}

}
```
>Example Response:

```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"apiuniqueid": "c7e45a48ace940c6abe5c037cd3b1cc5",
"rsptime": "5",
"resultcode": "00000",
"resultdesc": "Success"

}

}
```

### HTTP Request
`POST https://production.mobilityoncloud.com/moc-server/usermanagement/register`

***Description:*** To apply an account in the MoC middleware

<aside class="notice">
One IP can only register max 100 accounts per day, if more than 100, there will be no feedback from MoC middleware. Password has a certain requirement that must contain number letter and punctuation. MOC admin needs to approve this manually and afterward 3rd party application will receive a confirmation by email.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
username | 1 | String |
password| 1 | String |
phone | ? | String |
email | 1 | String |Relevant email will be sent to this email account (processing)

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success

## 5.1.2 PasswordChange
> Example Request
```json
{

"request_header":{

"timestamp":"1447644285294"

},

"request_body":{

"username":"mobilityoncloudvip",
"password":"123456aA934j)",
"passwordchange":"skfj3ue**fj3UU"

}

}
```
>Example Response
```json
{

"response_header": {

"rspcode": "0000",

"rspdesc": "Success"

},

"response_body": {

"apiuniqueid": "1b62b38733144e35a06b2a27acbc25e4",
"rsptime": "7",
"resultcode": "00000",
"resultdesc": "Success"

}

}
```

### HTTP Request
`POST https://production.mobilityoncloud.com/moc-server/usermanagement/passwordchange`

***Description:*** Change the password

<aside class="warning">
One IP can only send this command max 100 per day, if more than 100, there will be no feedback from MoC middleware. Password has a certain requirement that must contain number letter and punctuation. If the wrong password 3 times per day, the account will be blocked.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
username | 1 | String |
password | 1 | String |
passwordchange| 1 | String | The password to change

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success

### 5.1.3  AppIDSecret

> Example Request
```json
{

"request_header":{

"timestamp":"1447644285294"

},

"request_body":{

"username":"mobilityoncloudvip",
"password":"skfj3ue**fj3UU"

}

}
```
>Example Response
```json
{

"response_header": {

"rspcode": "0000",

"rspdesc": "Success"

},

"response_body": {

"apiuniqueid": "c5caf85bafeb4846ad7ssssss069ea29",
"appid": "MoC-143333983078",
"appsecret": "1JUaqtqddddNbxTH3uW5zq8ZxBvqnhjB",
"rsptime": "6",
"resultcode": "00000",
"resultdesc": "Success"

}

}
```

### HTTP Request
`POST https://production.mobilityoncloud.com/moc-server/usermanagement/appsecretreset`

***Description:*** Appsecret Reset

<aside class="warning">
One IP can only send this command max 100 per day, if more than 100, there will be no feedback from MoC middleware. Password has certain requirement that must contains number letter and punctuation. If wrong password 3 times per day, the account will be blocked.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
username | 1 | String |
password | 1 | String |

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
appid | -
appsecret | -

## 5.2 AuthDomain
As important security measurement, MOC only accepted APIcalls from a white list of authorized domains if

 - 3rd party application wants to apply AccessToken
 - 3rd party application wants to use GeneralToken for any command

3rd party application can add/delete/modify and retrieve AuthDomain with functions 5.2.1 to 5.2.4.

<aside class="notice">
Command with DeviceToken can be accepted if it is sent not from the authorized domains, e.g. can be sent directly from the smartphone.
</aside>

### 5.2.1 DomainAdd

> Example Request
```json
{

"request_header":{

"timestamp":"1447644285294"

},

"request_body":{

"username":"mobilityoncloudvip",
"password":"skfj3ue**fj3UU",
"authdomain":"www.xxx.com"

}

}
```
>Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"uuid": "e0e6a53d1a0e4821828ad97c0f1e6a6c",
"apiuniqueid": "264cb594f3944550a54086cb3a9bc297",
"rsptime": "125",
"resultcode": "00000",
"resultdesc": "Success"  

}

}
```

### HTTP Request

`POST https://production.mobilityoncloud.com/moc-server/usermanagement/add`

***Description:*** To add authorised domains

<aside class="notice">
Max to add 3 authorised domains. If set as *.*, all servers linked to this domain are accepted
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
username | 1 | String |
password | 1 | String |
authdomain | 1 | String

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
uuid| The added domain uuid

### 5.2.2 DomainDel

> Example Request
```json
{

"request_header":{

"timestamp":"1447644285294"

},

"request_body":{

"username":"mobilityoncloudvip",
"password":"skfj3ue**fj3UU",
"uuid":"a9ae47878a22409385d5bd38473ac851"

}

}
```
>Example Response
```json
"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"rsptime": "26",
"apiuniqueid": "be2274cb5c5e486ab5d3bac01145105d",
"uuid": "a9ae47878a22409385d5bd38473ac851",
"resultcode": "00000",
"resultdesc": "Success" 
 
}

}
```

### HTTP Request

`POST https://production.mobilityoncloud.com/moc-server/usermanagement/del`

***Description:*** To delete the authorized domains

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
username | 1 | String |
password | 1 | String |
uuid| 1 | String| the uuid of the domains

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
uuid| The deleted domain uuid

### 5.2.3  DomainModify
> Example Request
```json
{

"request_header":{

"timestamp":"1447644285294"

},

"request_body":{

"username":"mobilityoncloudvip",
"password":"skfj3ue**fj3UU",
"uuid":"a9ae47878a22409385d5bd38473ac851",
"authdomain":"www.bbb.com"

}

}
```

>Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"rsptime": "26",
"apiuniqueid": "be2274cb5c5e486ab5d3bac01145105d",
"uuid": "a9ae47878a22409385d5bd38473ac851",
"resultcode": "00000",
"resultdesc": "Success"  

}

}
```

### HTTP Request

`POST https://production.mobilityoncloud.com/moc-server/usermanagement/modify`

***Description:*** To modify the authorized domains

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
username | 1 | String 
password | 1 | String 
uuid| 1 | String| the uuid of the domains
authdomain | 1 | String 

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
uuid| The modified domain uuid

### 5.2.4  DomainRetrieve
> Example Request
```json
{

"request_header":{

"timestamp":"1447644285294"

},

"request_body":{

"username":"mobilityoncloudvip",
"password":"skfj3ue**fj3UU"

}

}
```
>Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"resultlist": [

{

"createTime": "2016-11-04 10:20:51",
"domainName": "www.ccccc.com",
"uuid": "6f807a73517f44f091b4830710412728"

},

],

"apiuniqueid": "49a865c5edb444a0b75a94792828629e",
"rsptime": "23",
"resultcode": "00000",
"resultdesc": "Success"

}

}
```

### HTTP Request

`POST https://production.mobilityoncloud.com/moc-server/usermanagement/retrieve`

***Description:*** To retrieve the authorized domains

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
username | 1 | String 
password | 1 | String 

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
resultlist| Includes “createTime”, "domainName" and "uuid" per saved value

## 5.3 Authentication

###  5.3.1 GeneralToken

#### 5.3.1.1 Get
> Example Request
```json
{

"request_header":{

"timestamp":"1447644285294"

},

"request_body":{

"appid":"MoC-103501988119",
"appsecret":"AlJAf26siLbIzj10RaJzgva35zKisqbx"

}

}
```

>Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"rsptime": "26",
"apiuniqueid": "be2274cb5c5e486ab5d3bac01145105d",
"resultcode": "00000",
"resultdesc": "Success",
"generaltoken": "492C2EC983DA6A5B712D540B39CA91C5AD25510DE32A11778EBF19653DDFCC0BB1600CF05A57EFD3"

}

}
```
### HTTP Request

`POST https://production.mobilityoncloud.com/moc-server/token/generaltokenget`

***Description:*** To obtain the GeneralToken

<aside class="warning">
One IP can only send this command max 1000. If over 1000 or wrong AppID/AppSecret more than 10 times, the IP will be blocked. Max valid time 12 hour.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
appid| 1 | String 
appsecret| 1 | String 

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
generaltoken|

#### 5.3.1.2 Refresh

> Example Request
```json
{

"request_header":{
"timestamp":"1447644285294"

},

"request_body":{

"appid":"MoC-103501988119",
"appsecret":"AlJAf26siLbIzj10RaJzgva35zKisqbx"

}

}
```

>Example Response
```json
{

"response_header": {
"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"rsptime": "26",
"apiuniqueid": "be2274cb5c5e486ab5d3bac01145105d",
"resultcode": "00000",
"resultdesc": "Success",  
"generaltoken": "97EDB0BFB2F67892D1609BAEA8BB145869ABC296602669F4516122EB33C09CFEE31AF10CB443DAA3"

}

}
```
### HTTP Request

`POST https://production.mobilityoncloud.com/moc-server/token/generaltokenrefresh`

***Description:*** To refresh GeneralToken and get new one

<aside class="warning">
One IP can only send this command max 1000. If over 1000 or wrong AppID/AppSecret more than 10 times, the IP will be blocked. Max valid time 12 hour.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
appid| 1 | String 
appsecret| 1 | String 

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
generaltoken|

###  5.3.2 DeviceToken

#### 5.3.2.1 Get

> Example Request
```json

{

"request_header":{

"timestamp":"1447644285294"

},

"request_body":{

"appid":"MoC-103501988119",
"appsecret":"AlJAf26siLbIzj10RaJzgva35zKisqbx",
"deviceuuid":"14b91cbf1e8b4c188f9ebe42ec0d3897"

}

}
```

>Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"rsptime": "26",
"apiuniqueid": "be2274cb5c5e486ab5d3bac01145105d",
"resultcode": "00000",
"resultdesc": "Success",
"devicetoken": "62B62310B36A2F19B1CF828E4D85E3D4EBDA5C827822A2531E79DECEB3F6AC5C4F20A4C6371526663542C8303FED52213AFC63029BAF28709C462FB810A2C407B24C150701E59CCB8DDD8FA627D3D440"

}

}
```

### HTTP Request

`POST https://production.mobilityoncloud.com/moc-server/token/devicetokenget`

***Description:*** To obtain the DevideToken which can control a device with specific device UUID

<aside class="warning">
If one IP has reached 10 wrong AppID and AppSecret, this IP will be blocked. Device Token is always valid unless use refresh one or invalid all command.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
appid| 1 | String 
appsecret| 1 | String 
deviceuuid | 1|String|This device uuid is given when adding the device in 5.5.1.

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
devicetoken|

#### 5.3.2.2 RefreshOne

> Example Request
```json

{

"request_header":{

"timestamp":"1447644285294"

},

"request_body":{

"appid":"MoC-103501988119",
"appsecret":"AlJAf26siLbIzj10RaJzgva35zKisqbx",
"deviceuuid":"14b91cbf1e8b4c188f9ebe42ec0d3897"

}

}
```

>Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"rsptime": "26",
"apiuniqueid": "be2274cb5c5e486ab5d3bac01145105d",
"resultcode": "00000",
"resultdesc": "Success",
"devicetoken": "62B62310B36A2F19B1CF828E4D85E3D4EBDA5C827822A2531E79DECEB3F6AC5CA1130249422172BDA24AD113400B4FB9F757E923E2200AFF60CA3C1ED6197992F853EA12643F9AFA2D43955AD4291CB3"

}

}
```

`POST https://production.mobilityoncloud.com/moc-server/token/devicetokenrefreshone`

***Description:*** Refresh DeviceToken for a specific UUID device, afterward previous DeviceToken will expire and new one will be given

<aside class="warning">
If one IP has reached 10 wrong AppID and AppSecret, this IP will be blocked.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
appid| 1 | String 
appsecret| 1 | String 
deviceuuid | 1|String|This device uuid is given when adding the device in 5.5.1.

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
devicetoken|


## 5.4 SystemConfig
3rd party application can make settings for whole system which will be applied to all devices under this account. If only make setting for one specific device, please refer to 5.6 Device Setting.

### 5.4.1 SystemConfig/callbackset
> Example Request
```json

{

"request_header":{

"timestamp":"1447644285294",
"accesstoken":"7D374F73B0B5BFE07D527C40D46041460DA8958689306ECAA3B0612065A9488B74CDD2C49B7F748F"

},

"request_body":{

"deviceuuid":"2dcc5cdcddb3449d98ad5c8sssb0c0f",

"propertyname":"centrallockimmobilizer",

"callback":"http://192.168.1.139:8080/moc-server/notify_url"

}

}
```

>Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"rsptime": "26",
"apiuniqueid": "be2274cb5c5e486ab5d3bac01145105d",
"resultcode": "00000",
"resultdesc": "Success"

}

}
```
3rd party application can choose to configure which information from device actions needs to be sent to 3rd party application server. And the configuration can be made based on the 3 following factors:

- which device to be configured

- which info needed to be sent to 3rd party server

- to which url link

All 3 different factors can be independent. Example: device 1’s unlock action needs to be sent to www.s1.com/lockand device 2’s ignition info needs to be sent to www.s2.com/ignition

All information (property names) which can be configured is listed in appendix, which are marked as activepush. 3rd party should use POST method to receive such callback.

Call back example:
https://120.24.153.90/ssmcar/callBack?timestamp=1447644285294&deviceuuid=fe50811a64ee4e08a487ea59440f4e39&propertyname=heartbeat&propertyvalue={"gpscurlocation":"00341f8100a620860500000000130b","ignitionstatus":"yes","fuellevel":"ffff","mileage":"ffffffff","vehecartotalvoltage":"ffff","vehecartotalcurrent":"ffff","vehspeed":"00cd","batterylevel":"048a","devbatvoltage":"0212","mobilenetwork_rssi":"10"}

`POST https://production.mobilityoncloud.com/moc-server/systemconfig/callbackset`

***Description:*** To make changes on system setting.

<aside class="warning">
If one IP reaches 10 times wrong AccessToken, this IP will be blocked.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
accesstoken| 1 | String 
deviceuuid| 1 | String |The device which need to be configured
propertyname|1| String | The info need to be feedback to 3rd party Application
callback|1|String| The callback url


### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success

### 5.4.2 SystemConfig/callbackget
> Example Request
```json

{

"request_header":{

"timestamp":"1447644285294",
"accesstoken":"BF595BEE57FABC7C0C283FAD028F5396EBEE83B81B9AF55F7AB50D6421AA6E941CEB9B4422651B38"

},

"request_body":{

"deviceuuid":"602ab3fa45494sfd18109db979dc604e4",
"propertyname":"centrallockimmobilizer"

}
```

> Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"apiuniqueid": "df0c795dbdd240439a35ced3ff58854f",
"deviceuuid": "602ab3fa454941a18109db979dc604e4",
"propertyname": "centrallockimmobilizer",
"callback": "http://192.168.33.129:8080/moc-server/notify_url",
"rsptime": "478",
"resultcode": "00000",
"resultdesc": "Success"

}

}
```
`POST https://production.mobilityoncloud.com/moc-server/systemconfig/callbackget`

***Description:*** To retrieve the current system setting

<aside class="warning">
If one IP reaches 10 times wrong AccessToken, this IP will be blocked.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
accesstoken| 1 | String 
deviceuuid| 1 | String |The device which need to be checked
propertyname|1| String | The info which need to be checked


### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
deviceuuid|
propertyname|
callback|The url has been set


## 5.4 DeviceManagement

3rd party application can only manage devices within its own device list. With this function, 3rd party application can add/change devices list.

### 5.5.1 DeviceAdd

> Example Request
```json

{

"request_header":{

"timestamp":"1450460624420",
"accesstoken":"BF595BEE57FABC7C0C283FAD028F5396EBEE83B81B9AF55F7AB50D6421AA6E941CEB9B4422651B38"

},
"request_body":{

"deviceserialno":"2016060100001",
"platevin":"008618688860259"

}

}
```

> Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

}

"response_body": {

"rsptime": "26",
"apiuniqueid": "be2274cb5c5e486ab5d3bac01145105d",
"deviceuuid": "14b91cbf1e8b4c188f9ebe42ec0d3897",
"resultcode": "00000",
"resultdesc": "Success"

}

}
```

`POST https://production.mobilityoncloud.com/moc-server/devicemanagement/add`

***Description:*** To add device to the device list of this account

<aside class="warning">
If one IP reaches 10 times wrong AccessToken, this IP will be blocked. All info needed below will be given when order device from MoC. Users cannot change Sim card before aligning with MoC.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
accesstoken| 1 | String 
deviceserialno| 1 | String |
platevin|1| String | The vehicle plate number or VIN number. This is the remark of vehicle will be used to identify the vehicle.


### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
deviceuuid|

### 5.5.2 Active

> Example Request
```json

{

"request_header":{

"timestamp":"1450460624420",
"accesstoken":"BF595BEE57FABC7C0C283FAD028F5396EBEE83B81B9AF55F7AB50D6421AA6E941CEB9B4422651B38"

},
"request_body":{

"deviceuuid":"10fa31ef4c14473e8369b0ecd85178d6",
"activation":"yes"

}

}
```

> Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

}

"response_body": {

"apiuniqueid": "e6254d648072491f95206baea4e6f11c",
"rsptime": "35",
"resultcode": "00000",
"resultdesc": "Success"

}

}
```

If a device is added to the account at the first time, the default status of the device is deactivated. The device needs to be activated before use. Besides, if a device is not intended to be use temporarily, it can be deactivated. Activation and deactivation will start immediately after the command.

`POST https://production.mobilityoncloud.com/moc-server/devicemanagement/active`

***Description:*** To activate or deactivate a device

<aside class="warning">
If one IP reaches 10 times wrong AccessToken, this IP will be blocked.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
accesstoken| 1 | String 
deviceuuid| 1 | String |
activation|1| String | 'yes' or 'no'

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success

### 5.5.3 DeviceModify

> Example Request
```json

{

"request_header":{

"timestamp":"1450460624420",
"accesstoken":"97EDB0BFB2F67892D1609BAEA8BB1458 69ABC296602669F4516122EB33C09CFEE31AF10CB443DAA3"

},

"request_body":{

"deviceuuid":"7423dbef9e82430daf171bd39693bbad",
"car":"BMW i3"

}

}
```

> Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"rsptime": "26",
"apiuniqueid": "be2274cb5c5e486ab5d3bac01145105d",
"deviceuuid": "7423dbef9e82430daf171bd39693bbad",
"resultcode": "00000",
"resultdesc": "Success"  }

}
```

`POST https://production.mobilityoncloud.com/moc-server/devicemanagement/modify`

***Description:*** To change device info from the device list of this account

<aside class="warning">
If one IP reaches 10 times wrong AccessToken, this IP will be blocked.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
accesstoken| 1 | String 
deviceuuid| 1 | String |
deviceserialno|1| String | 
platevin|?| String |
devicesmsimsi|?|String |
devicesmsno|?| String |
car|?| String |
ownership|?| String |
plate|?| String |
vin |?| String |
remark|?| String |


### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
deviceuuid |

### 5.5.4 DeviceRetrieve
#### 5.5.4.1

> Example Request
```json

{

"request_header":{

"timestamp":"1450460624420",
"accesstoken":"97EDB0BFB2F67892D1609BAEA8BB1458  69ABC296602669F4516122EB33C09CFEE31AF10CB443DAA3"

},

"request_body":{

"deviceuuid":"14b91cbf1e8b4c188f9ebe42ec0d3897"

}

}
```

> Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"deviceuuid": "14b91cbf1e8b4c188f9ebe42ec0d3897",
"deviceserialno": "863789025630000",
"devicebtblemac": "000e0b1462a6",
"devicebtsppmac": "000e0e1462a6",
"devicesmsno": "882360001690000",
"devicesmsimsi": "234507098230000",
"apiuniqueid": "5c55d6b1f7d047cd8c787b06de71f411",
"rsptime": "29",
"platevin": " Test",
"car": "McLaren P1",
"plate": "Test",
"vin": "",
"ownership": "",
"activation": "yes",
"statusmodifytime": "2018-03-04 12:12:23",
"remark": "for pilot",
"resultcode": "00000",
"resultdesc": "Success"  }

}
```

`POST https://production.mobilityoncloud.com/moc-server/devicemanagement/retrieveone`

***Description:*** To retrieve data of one specific device according to uuid

<aside class="warning">
If one IP reaches 10 times wrong AccessToken, this IP will be blocked.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
accesstoken| 1 | String 
deviceuuid| 1 | String |

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
deviceuuid |
deviceserialno | Device series number
devicebtblemac | Device BLE address
devicebtsppmac | Device SPP address
devicesmsno | Device sim card number
devicesmsimsi | Device sim card IMSI number
platevin | The plate or vin, which was defined by 3rd party app
car | Car model
plate | Vheicle plate number
vin | Vehicle VIN number
ownership | Onwership of the vehicle
activation | Activation status of the device
statusmodifytime | Last activation or deactivation time
remark | 

#### 5.5.4.2 Retrieveonesn

> Example Request
```json

{

"request_header":{

"timestamp":"1450460624420",
"accesstoken":"97EDB0BFB2F67892D1609BAEA8BB1458  69ABC296602669F4516122EB33C09CFEE31AF10CB443DAA3"

},

"request_body":{

"deviceserialno":"863789025630000"

}

}
```

> Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"deviceuuid": "14b91cbf1e8b4c188f9ebe42ec0d3897",
"deviceserialno": "863789025630000",
"devicebtblemac": "000e0b1462a6",
"devicebtsppmac": "000e0e1462a6",
"devicesmsno": "882360001690000",
"devicesmsimsi": "234507098230000",
"apiuniqueid": "5c55d6b1f7d047cd8c787b06de71f411",
"rsptime": "29",
"platevin": " Test",
"car": "McLaren P1",
"plate": "Test",
"vin": "",
"ownership": "",
"activation": "yes",
"statusmodifytime": "2018-03-04 12:12:23",
"remark": "for pilot",
"resultcode": "00000",
"resultdesc": "Success"  }

}
```

`POST https://production.mobilityoncloud.com/moc-server/devicemanagement/retrieveonesn`

***Description:*** To retrieve data of one specific device according to serial number

<aside class="warning">
If one IP reaches 10 times wrong AccessToken, this IP will be blocked.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
accesstoken| 1 | String 
deviceuuid| 1 | String |

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
deviceuuid |
deviceserialno | Device series number
devicebtblemac | Device BLE address
devicebtsppmac | Device SPP address
devicesmsno | Device sim card number
devicesmsimsi | Device sim card IMSI number
platevin | The plate or vin, which was defined by 3rd party app
car | Car model
plate | Vheicle plate number
vin | Vehicle VIN number
ownership | Onwership of the vehicle
activation | Activation status of the device
statusmodifytime | Last activation or deactivation time
remark | 

#### 5.5.4.3 Retrieveall

> Example Request
```json

{

"request_header":{

"timestamp":"1450460624420",
"accesstoken":"97EDB0BFB2F67892D1609BAEA8BB145869ABC296602669F4516122EB33C09CFEE31AF10CB443DAA3"

},

"request_body":{

}

}
```

> Example Response
```json
{

"response_header": {

"rspcode": "0000",
"rspdesc": "Success"

},

"response_body": {

"resultlist": [

{

"activation": "yes",
"car": "",
"devicebtblemac": "000e0b149520",
"devicebtsppmac": "000e0e149520",
"deviceserialno": "863789025632534",
"devicesmsimsi": "",
"deviceuuid": "a87ff814dfc24870bbe16aae6050b500",
"ownership": "",
"plate": "",
"platevin": "immo_issue",
"remark": "",
"vin": ""

},

{

"activation": "yes",
"car": "",
"devicebtblemac": "000e0b0cceca",
"devicebtsppmac": "000e0e0cceca",
"deviceserialno": "863789025623533",
"devicesmsimsi": "",
"devicesmsno": "7777546320354564",
"deviceuuid": "6243bb70b7114db4b4b6ad188542705d",
"ownership": "",
"plate": "",
"platevin": "",
"remark": "",
"vin": ""

}

],

"apiuniqueid": "aa3ed42da9f84220832d97120789bc82",
"rsptime": "22",
"totalcounts": "2",
"resultcode": "00000",
"resultdesc": "Success"

}

}
```

`POST https://production.mobilityoncloud.com/moc-server/devicemanagement/retrieveall`

***Description:*** To retieve all the device uuid under this account

<aside class="warning">
If one IP reaches 10 times wrong AccessToken, this IP will be blocked.
</aside>

### Request Body
Name| constraint  | Type | Description
-- |--|--|--
accesstoken| 1 | String 
page| ? | String | Offset value, it can return max 20 records. When it has more than 20 records, 3rd party application must use offset value to retireve all records in multiple patches.

### Response Body
Name | Description
-- |--
apiuniqueid | The unique ID for this API call
rsptime| Response time in millisecond
resultdesc| Success or not
resultcode| 00000 means success
Resultlist | Includes "activation", "car", "devicebtblemac", "devicebtsppmac", "devicesmsno", "devicesmsimsi", "devserialno", "deviceuuid", "platevin", "ownership", "plate", "remark", "statusmodifytime", "vin"
totalcounts | 




