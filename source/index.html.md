---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Bienvenidos a la documentacion oficial de Saive, aqui se encuentra a detalle los parametros requeridos para el correcto funcionamiento de las cloud functions bajo el endpoint
`https://us-central1-saive-70572.cloudfunctions.net/`

# Authentication

# Saive APP

## /register
```json
{
    "data":  {
        "id": "1",
        "name": "Luis", 
        "email": "luisxciv@gmail.com",
        "gender": "Male", 
        "country": "MX", 
        "state": "Queretato",
        "birthdate": 1570207276000, 
        "brand_carrier":"AT&T",
        "phone_model":"Iphone 6", 
        "phone_number": "4426682688",
        "platform":"iOS",
        "car_brand":"Toyota", 
        "car_model":"Prius",
        "car_year":2019,
        "insurance_company": "Mapfre", 
        "insurance_expiration": 1569937894000, 
        "reference_number": 293847,
        "push_token": "LY83H0AHEVX5J4VX99WB7",
        "saive_insurance": false
    }
}
```
Registra un usuario en la base de datos
### HTTP Request

`POST https://us-central1-saive-70572.cloudfunctions.net/register`

### Query Parameters

Parameter | Type | Description | Default
--------- | ------- | ----------- | -----
id | STR | El id del documento con el que se va a crear el registro en /mobile_user | None
name | STR | El nombre del usuario | None
email | STR | El e-mail del usuario | None
gender | STR | Genero del usuario: `Male`, `Female` | None
country | STR | Codigo de pais de residencia del usuario: `MX` | None
state | STR | Nombre del estado de residencia del usuario: `Queretato` | None
birthdate | INT | Unix timestamp en milisegundos con la fecha de nacimiento del usuario | None
brand_carrier | STR | Nombre de la compania carrier del tel del usuario | `Null`
phone_model | STR | Modelo del smartphone del usuario | None
phone_number | STR | Telefono del usuario | None
platform | STR | Sistema operativo del smartphone del usuario `iOS`, `Android` | None
car_brand | STR | Marca de automobil | None
car_model | STR | Modelo del automobil | None
car_year | INT | Ano de manufactura del automobil | None
insurance_company | STR | Nombre de la compania con la que el usuario esta asegurado | `Null`
insurance_expiration | INT | Fecha de expiracion del seguro del usuario | `Null`
reference_number | INT | Numero de referencia de seguro | `Null`
push_token | STR | Token de notificaciones firebase | None 
saive_insurance | BOOL | Especifica si el usuario esta asegurado con saive | `Null`

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

