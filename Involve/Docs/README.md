## Pasos a resolver

### Género
1. Descagar catálogo de `https://dev.micros.involverh.com.mx/management/catalog-sytem/by-type?type=gender&keySystem=MEX`

2. Actualizar módelo de respuesta.

```json
[
  {
    "op": "replace",
    "path": "/steepsOnboarding",
    "value": 3
  },
  {
    "op": "replace",
    "path": "/user/gender",
    "value": {
      "catalogSystemId": "4028e4a986843df50186845181950009",
      "name": "MUJER",
      "type": "gender",
      "status": true,
      "keySystem": "MEX"
    }
  }
]
```

### Estado Civil

1. Descagar catálogo de `https://dev.micros.involverh.com.mx/management/catalog-sytem/by-type?type=maritalStatus&keySystem=MEX`
2. Actualizar modelo de respuesta

```json
[
  {
    "op": "replace",
    "path": "/steepsOnboarding",
    "value": "4"
  },
  {
    "op": "replace",
    "path": "/maritalStatus",
    "value": {
      "catalogSystemId": "4028e4a986843df5018684517f820007",
      "name": "CASADO",
      "type": "maritalStatus",
      "status": true,
      "keySystem": "MEX"
    }
  }
]
```



### Nacionalidad

1. Descargar catálogo con AutoCompleteTextView `https://dev.micros.involverh.com.mx/management/catalog/nationality/`


### Dónde buscas trabajar

Los endpoints que cambiaron fueron los de Estado y Alcaldía. Anteriormente se descargaban todos los catálogos y se guardaban en base de datos. **Se cambiará a siempre solicitarlo del servicio en cada cambio.**

De igual manera se hizo un cambio de `AutoCompleteTextView` por `EditText` con Dropdown en `BottomSheetFragment` para homologar la vista con Web.

1. Descargar catálogo `https://dev.micros.involverh.com.mx/management/catalog/country`
2. En cada actualización del país cargar el estado y alcaldía
`https://dev.micros.involverh.com.mx/management/catalog/state?countryCode=MX`
`https://dev.micros.involverh.com.mx/management/catalog/city?countryCode=MX&stateCode=MX-AGU`
3. Actualizar payload

```json
[
  {
    "op": "replace",
    "path": "/steepsOnboarding",
    "value": "8"
  },
  {
    "op": "replace",
    "path": "/citySearch",
    "value": {
      "cityId": "2c9f936481969f0cccc996a00e090978",
      "name": "Doctor González",
      "stateCode": "MX-NLE",
      "countryCode": "MX",
      "latitude": 25.84081,
      "longitude": -99.83125,
      "state": {
        "stateId": "2c9f936481969f0bbbb996a00e090019",
        "name": "Nuevo León",
        "countryCode": "MX",
        "fipsCode": "19",
        "iso2": "MX-NLE",
        "latitude": 25.58333,
        "longitude": -99.75,
        "country": {
          "countryId": "2c9f936481969f0aaaa996a00e090001",
          "capital": "Mexico City",
          "currency": "MXN",
          "currencySymbol": "$",
          "iso2": "MX",
          "iso3": "MEX",
          "latitude": 19.4284,
          "longitude": -99.1276,
          "name": "Mexico",
          "nameNative": "México",
          "phoneCode": "52",
          "region": "Americas",
          "subregion": "Central America",
          "timezones": "[{\"zoneName\":\"America/Bahia_Banderas\",\"gmtOffset\":-21600,\"gmtOffsetName\":\"UTC-06:00\",\"abbreviation\":\"CST\",\"tzName\":\"Central Standard Time (North America\"},{\"zoneName\":\"America/Cancun\",\"gmtOffset\":-18000,\"gmtOffsetName\":\"UTC-05:00\",\"abbreviation\":\"EST\",\"tz",
          "tld": ".mx",
          "translations": "{\"br\":\"México\",\"pt\":\"México\",\"nl\":\"Mexico\",\"hr\":\"Meksiko\",\"fa\":\"?????\",\"de\":\"Mexiko\",\"es\":\"México\",\"fr\":\"Mexique\",\"ja\":\"????\",\"it\":\"Messico\"}",
          "flagCountry": "https://flagcdn.com/w20/mx.png"
        }
      }
    }
  }
]
```

### Vives actualmente ahí?

1. Actualizar payload 'No'

```json
[
  {
    "op": "replace",
    "path": "/residentJob",
    "value": false
  },
  {
    "op": "replace",
    "path": "/cityResidence",
    "value": null
  },
  {
    "op": "replace",
    "path": "/steepsOnboarding",
    "value": "9"
  }
]
```
2. Actualizar payload 'Sí'
Con información previa cargar el estado `https://dev.micros.involverh.com.mx/management/catalog/city?countryCode=MX&stateCode=MX-NLE`
3. Actualizar payload 

```json
[
  {
    "op": "replace",
    "path": "/residentJob",
    "value": true
  },
  {
    "op": "replace",
    "path": "/cityResidence",
    "value": {
      "cityId": "2c9f936481969f0cccc996a00e090970",
      "name": "Aramberri",
      "stateCode": "MX-NLE",
      "countryCode": "MX",
      "latitude": 24.22304,
      "longitude": -99.82752,
      "state": {
        "stateId": "2c9f936481969f0bbbb996a00e090019",
        "name": "Nuevo León",
        "countryCode": "MX",
        "fipsCode": "19",
        "iso2": "MX-NLE",
        "latitude": 25.58333,
        "longitude": -99.75,
        "country": {
          "countryId": "2c9f936481969f0aaaa996a00e090001",
          "capital": "Mexico City",
          "currency": "MXN",
          "currencySymbol": "$",
          "iso2": "MX",
          "iso3": "MEX",
          "latitude": 19.4284,
          "longitude": -99.1276,
          "name": "Mexico",
          "nameNative": "México",
          "phoneCode": "52",
          "region": "Americas",
          "subregion": "Central America",
          "timezones": "[{\"zoneName\":\"America/Bahia_Banderas\",\"gmtOffset\":-21600,\"gmtOffsetName\":\"UTC-06:00\",\"abbreviation\":\"CST\",\"tzName\":\"Central Standard Time (North America\"},{\"zoneName\":\"America/Cancun\",\"gmtOffset\":-18000,\"gmtOffsetName\":\"UTC-05:00\",\"abbreviation\":\"EST\",\"tz",
          "tld": ".mx",
          "translations": "{\"br\":\"México\",\"pt\":\"México\",\"nl\":\"Mexico\",\"hr\":\"Meksiko\",\"fa\":\"?????\",\"de\":\"Mexiko\",\"es\":\"México\",\"fr\":\"Mexique\",\"ja\":\"????\",\"it\":\"Messico\"}",
          "flagCountry": "https://flagcdn.com/w20/mx.png"
        }
      }
    }
  },
  {
    "op": "replace",
    "path": "/steepsOnboarding",
    "value": "10"
  }
]
```

### Cuánto quieres ganar?

1. Actualizar payload

```json
[
  {
    "op": "replace",
    "path": "/steepsOnboarding",
    "value": "11"
  },
  {
    "op": "replace",
    "path": "/desiredSalary",
    "value": "30000"
  }
]
```

----
### Dudas

1. ¿Cómo obtener el keySystem?
2. En los catálogos se envía un parámetro `status:true` ¿qué significa?
