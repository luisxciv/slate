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
### Response


<aside class="success">
Status:`ok` — msg: `Se creo el usuario con exito`
</aside>

<aside class="warning">
Status:`error` — msg: `Este mail ya esta registrado`
</aside>

## /score
```json
{
    "data":  {
        "id": "1",
        "report_date": "2019-30-09 12:00:00",
        "latitude": "20.598324",
        "longitude": "-100.390755",
        "time": 1,
        "speed": 100, 
        "distance": 2,
        "acceleration": 30,
        "trip_id": "ZPD93"
    }
}
```
Guarda datos de manejo en tiempo real

Campos de control: 
 `last_latitude`
 `last_longitude`
 `last_score_date`

 Estadisticas generales del usuario generales del usuario:
 
 `speed_counter`
 `avg_speed`
 `speed_total`
 `acceleration_counter`
 `avg_acceleration`
 `acceleration_total`
 `distance_counter`
 `distance_total`
 `daily_distance`
 `avg_distance`
 `daily_time`
 `time_total`

 Estadisticas de viaje, contorlados por los prefijos  `last_trip_*`

### HTTP Request

`POST https://us-central1-saive-70572.cloudfunctions.net/changeInsurance`

### Query Parameters

Parameter | Type | Description | Default
--------- | ------- | ----------- | -----
id | STR | El id del documento en /mobile_user | None
report_date | STR | La fecha en la que se levanto la info | None
latitude | STR | latitud | None
longitude | STR | longitud | None 
time | INT | El tiempo de manejo | None 
speed | INT | La velocidad de manejo | None 
distance | INT | La distancia manejda | None 
acceleration | INT | La aceleracion del vehiculo | None 
trip_id | STR | El id del viaje (debe ser unico) | None


### Response

<aside class="success">
Status:`ok` — msg: `New score for user`
</aside>


<aside class="warning">
Status:`error` — msg: `La velocidaad de manejo sobrepasa los limites, se imitio el score.`
</aside>

## /changeUsername
```json
{
    "data":  {
        "id": "1",
        "username": "Luisxciv" 
    }
}
```
Cambia el username 
### HTTP Request

`POST https://us-central1-saive-70572.cloudfunctions.net/changeUsername`

### Query Parameters

Parameter | Type | Description | Default
--------- | ------- | ----------- | -----
id | STR | El id del documento en /mobile_user | None
username | STR | Username | None

### Response


<aside class="success">
Status:`ok` — msg: `Se cambio el nombre del usuario`
</aside>

<aside class="warning">
Status:`error` — msg: `Tu usuario tiene mas de 9 caracteres o tiene caracteres especiales.`
</aside>


## /usernameExists
```json
{
    "data":  {
        "id": "1",
        "username": "Luisxciv" 
    }
}
```
Cambia el username 
### HTTP Request

`POST https://us-central1-saive-70572.cloudfunctions.net/usernameExists`

### Query Parameters

Parameter | Type | Description | Default
--------- | ------- | ----------- | -----
id | STR | El id del documento en /mobile_user | None
username | STR | Username | None

### Response


<aside class="success">
Status:`ok` — msg: `Nombre de usuario disponible`
</aside>

<aside class="success">
Status:`ok` — msg: `Nombre de usuario no esta disponible`
</aside>

<aside class="warning">
Status:`error` — msg: `Tu usuario tiene mas de 9 caracteres o tiene caracteres especiales.`
</aside>


## /changeInsurance
```json
{
    "data":  {
        "id": "1",
        "insurance_company": "Chubb",
        "insurance_expiration": "2019-10-01",
        "saive_insurance": false,
        "reference_number": 299345

    }
}
```
Cambia el username 
### HTTP Request

`POST https://us-central1-saive-70572.cloudfunctions.net/changeInsurance`

### Query Parameters

Parameter | Type | Description | Default
--------- | ------- | ----------- | -----
id | STR | El id del documento en /mobile_user | None
insurance_company | STR | Compania de seguros | None
insurance_expiration | STR | Fecha de expiracion del seguro `YYYY-MM-DD` | None
saive_insurance | BOOL |Si el usuario esta asegurado con saive | `Null`
reference_number | INT | Numero de referencia de seguro | None



### Response

<aside class="success">
Status:`ok` — msg: `e actualizaron los datos del seguro`
</aside>


