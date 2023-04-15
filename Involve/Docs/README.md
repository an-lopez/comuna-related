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


### ~~Nacionalidad~~

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

### OCR

### Paso 1: Selección de Archivo

1. Revisar que se envíe correctamente a los dos endpoints
	- `POST https://dev.micros.involverh.com.mx/files/extraccioncv/upload-files?typeFile=pdf`
	- `POST https://dev.micros.involverh.com.mx/files/upload/uploadFile?typeFile=URL_CV`

### Paso 2
1. Ajuste de endpoint para obtener `"extraccionCorrect":true` usando
`GET https://dev.micros.involverh.com.mx/candidate/candidate`
2. Ajuste de endpoint para resultados extracción
`GET https://dev.micros.involverh.com.mx/files/extraccioncv/result-extraccioncv`
3. Ajuste de endpoint para eliminar una experiencia laboral.

`OPTIONS https://dev.micros.involverh.com.mx/files/extraccioncv/experience?experienceTTId=2c9f906e875cc6f7018781d767040013`

Body Request

```json
[
  {
    "op": "replace",
    "path": "/statusExperience",
    "value": "DELETE"
  }
]
```

4. Botón validar experiencia laboral no se activa cuando se cargan los datos.


-
### Changelog

03/14/2023: 

- Actualización de Endpoint en ciudades. Actualización de modelos de ciudades impacta a las siguientes clases: `Paso8.java`, `Paso9.java`, `Paso10.java`, `InformacionPersonal.java`, `CityAdapter.java`
- Actualización OCR endpoint de subida y candidato para obtener cuándo está procesada la información del OCR.

# Análisis

La aplicación Involve RH carece de arquitectura, patrones de diseño, lineamientos de desarrollo de aplicaciones Android violando todos los principios y no permitiéndo un mantenimiento _fácil_ y reduciendo sus oportunidades de escalabilidad en gran manera. Tiene deuda técnica por todos lados, utiliza tecnología antigua comparado al tiempo de la fecha del último _commit_ visible en el proyecto. Existe poca o nula reutilización de código, en el código puedes ver esta misma sentencia al menos 11 veces, mismo nombre `verifyUser` sin tener sentido el nombre de la variable con la intención de la sentencia, sin agregar el `Disposable` a un `CompositeDisposable` permitiendo la ejecución de estas tareas asíncronas aún después de que la actividad no sea visible.

Si buscamos algo de principios SOLID dentro del código fallamos en todos, empezando por responsabilidad única: se puede revisar el archivo `FileUtils.java` en el cuál se puede apreciar cómo tiene distintas funcionalidades más allá de los archivos, teniendo dentro de sí `SharedPreferences`, sentencias relacionadas a lógica de negocio y código sin utilizar.

```kotlin
Observable<Response<CandidateInvolve>> verifyUser = ApiAdapterOB.getInvolveService().patchCandidate(auxLst, user.getToken());
```

El stack tecnológico actual:

- Java: No hay problema con el desarrollo en Java, puesto que Kotlin usa JVM para ejecutarse, sin embargo, Android es una plataforma Kotlin first, es decir, toda la documentación saldrá primero en Kotlin y después en Java, si es que se cree necesario.
- RxJava2
- Retrofit
- Gson
- [ButterKnife](https://github.com/JakeWharton/butterknife) (Deprecated)
- Librerías de 3eros para ciertas vistas.

> Attention: This tool is now deprecated. Please switch to view binding. Existing versions will continue to work, obviously, but only critical bug fixes for integration with AGP will be considered. Feature development and general bug fixes have stopped.

- Lombok (Incompatibilidad con IDE Android Studio): Esta tecnología esta fuertemente ligada a Java y no permite que otros desarrolladores que no utilizan esta herramienta puedan trabajar de forma fácil, levantar el entorno y encontrar una versión compatible puede demorar horas.

