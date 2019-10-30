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

# Cloud Functions

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
        "distractionEvents": 4, 
			  "hard_acceleration_counter": 1,
			  "hard_deacceleration_counter": 4, 
			  "hard_cornering_counter": 2,
			  "hard_acceleration_value": 3.2, 
			  "hard_deacceleration_value": 4.0,
			  "hard_cornering_value": 2.2
    }
}
```

Guarda una coleccion de datos de manejo, cada request debe ser manejado como un viaje individual del usuario

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
acceleration | INT | La aceleracion del vehiculo | 0
distraction_events | INT | Contador de distracciones | 0
hard_acceleration_counter | INT | Contador de aceleraciones fuertes | 0
hard_acceleration_value | FLOAT | Promedio de score de aceleraciones fuertes | 0 
hard_deacceleration_counter | INT | Contador de desaceleraciones fuertes | 0
hard_deacceleration_value | FLOAT | Promedio de score de desaceleraciones fueres | 0 
hard_cornering_counter | INT | Contador de eventos de cornering | 0
hard_cornering_value | FLOAT | Promedio de score de eventos de cornering | 0 


### Actualiza en /mobile_user
### Campos de control: 
Parameter | Type | Description 
--------- | ------- | ----------- 
 `last_latitude` | FLOAT | Ultima posicion X en plano
 `last_longitude` | FLOAT | Ultima posicion Y en plano 
 `last_score_date` | STR | Ultima fecha de score (ultimo report_date enviado)

 
### Contadores
Parameter | Type | Description 
--------- | ------- | ----------- 
 `speed_counter` | INT | Conteo de registros donde la velocidad respeta los limites saive
 `acceleration_counter` | INT | Conteo de registros donde existio
 `distance_counter` | INT | Conteo de registros donde se registro una distancia
 `hard_acceleration_counter` | INT | Conteo de registros donde exisitio una aceleracion brusca 
 `hard_deacceeleration_counter` | INT | Conteo de registros donde exisitio desaceleracion brusca
 `hard_cornering_counter` | INT | Conteo de registros donde exisitio cornering brusco
 
 <aside class="notice">
Los campos de conteo y totales son utilizados en mayor parte para promediar las velocidades, tiempos, distancias y variables de manejo del usuario
</aside>

 
### Totales 
Parameter | Type | Description 
--------- | ------- | ----------- 
 `speed_total` | INT | Suma de las velocidades
 `time_total` | INT | Suma de los tiempos
 `acceleration_total` | INT | Suma de las aceleraciones
 `distance_total` | INT | Suma de las distancias
 `hard_acceleration_total` | INT | Suma de scores de aceleraciones bruscas
 `hard_deacceleration_total` | INT | Suma de scores de desaceleraciones bruscas
 `hard_cornering_total` | INT | Suma de scores de cornering brusco 
 `trips_total` | INT | Suma de total de trips
` distractions_total` | INT | Suma total de distracciones de manejo

### Promedios
 Parameter | Type | Description 
--------- | ------- | ----------- 
 `avg_speed` | FlOAT | Velocidad promedio general del usuario
 `avg_acceleration` | FLOAT | Acceleracion promedio del usuario
 `avg_distance` | FLOAT | Distancia promedio del usuario por minuto
 `avg_hard_acceleration` | FLOAT | Score promedio de aceleracion brusca
 `avg_hard_deacceleration` | FLOAT | Score promedio de desaceleracion brusca 
 `avg_hard_cornering` | FLOAT | Score promedio de cornering
 `avg_trip_distractions` | INT | Numero de distracciones promedio por viaje 
 `avg_trip_distance` | FLOAT | Numero de km promedio por viaje
 
### Daily Stats
 Parameter | Type | Description 
--------- | ------- | ----------- 
 `daily_time` | INT | Tiempo de manejo del dia
 `daily_distance` | FLOAT | Distancia recorrida en el dia

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
Actualiza los datos del usuario de la aseguradora 
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

<aside class="warning">
Status:`error` — msg: `Hubo un error al actualizar los datos.`
</aside>

## /addCar
```json
{
    "data":  {
        "id": "1",
         "car_brand": "Toyota", 
        "car_model": "Camry",
        "car_year": 2019,
        "car_version": "First"

    }
}
```
Actualiza los datos del vehiculo
### HTTP Request

`POST https://us-central1-saive-70572.cloudfunctions.net/addCar`

### Query Parameters

Parameter | Type | Description | Default
--------- | ------- | ----------- | -----
id | STR | El id del documento en /mobile_user | None
car_brand | STR | Marca del automobil | None
car_model | STR | Modelo del automibil | None
car_year | INT | Año de emision del automobil | None
car_version | STR | Version del automibil | None

### Response

<aside class="success">
Status:`ok` — msg: `Se actualizaron los datos del vehiculo`
</aside>
<aside class="warning">
Status:`error` — msg: `Hubo un error al actualizar los datos.`
</aside>

## /insuranceLead
```json
{
    "data":  {
        "id": "1",
         "phone": "4426682688", 
        "postal_code": 76190,
        "special": true

    }
}
```
Genera un lead de cotizacion (A definir triggers)
### HTTP Request

`POST https://us-central1-saive-70572.cloudfunctions.net/insuranceLead`

### Query Parameters

Parameter | Type | Description | Default
--------- | ------- | ----------- | -----
id | STR | El id del documento en /mobile_user | None
phone | STR | Telefono | None
postal_code | INT | Codigo Postal | None
special | BOOL | Si es taxista o servicio tipo uber | None

### Response

<aside class="success">
Status:`ok` — msg: `Se genero un nuevo lead con exito`
</aside>
<aside class="warning">
Status:`error` — msg: `Hubo un error al actualizar los datos.`
</aside>
