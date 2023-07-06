# API_SIMEM

## Índice
1. [Descripción general](#section1)
2. [Posibles solicitudes para consumir la API](#section2)
3. [URL/Endpoints para consumir la API](#section3)
4. [Comentarios finales](#section4)

<a id='section1'></a>
## Descripción general

Con el propósito de brindar información pertinente para la utilización de la API se ha creado este repositorio en el cual se da explicación de como utilizarla con herramientas de consulta para obtener la información requerida. 
El objetivo de esta guía es que el usuario tenga la capacidad de consumir los servicios expuestos haciendo uso de la herramienta que prefiera para dicho fin. 


<a id='section2'></a>
## Posibles solicitudes para consumir la API

A continuación, se dará ejemplos de código en donde se demuestra como se puede realizar solicitudes a la API desde diferentes lenguajes:

**Python**
```python
import http.client/n 
conn = http.client.HTTPSConnection("func-simemfile-prb-01.azurewebsites.net")/n
payload = ''
headers = {}
conn.request("GET", "/api/Http_Get_ParquetData?fechaInicio=2023-01-16&fechaFin=2023-01-17&dataId=6E1BCC6B-2F1D-4E6B-976F-54CA056F9729&descargable=false", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))</code>
```

**Jquery**
```js
var settings = {
  "url": "https://func-simemfile-prb-01.azurewebsites.net/api/Http_Get_ParquetData?fechaInicio=2023-01-16&fechaFin=2023-01-17&dataId=6E1BCC6B-2F1D-4E6B-976F-54CA056F9729&descargable=false",
  "method": "GET",
  "timeout": 0,
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

**Ruby**
```ruby
require "uri"
require "net/http"

url = URI("https://func-simemfile-prb-01.azurewebsites.net/api/Http_Get_ParquetData?fechaInicio=2023-01-16&fechaFin=2023-01-17&dataId=6E1BCC6B-2F1D-4E6B-976F-54CA056F9729&descargable=false")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)
```


<a id='section3'></a>
## URL/Endpoints para consumir la API

Para realizar el consumo de los servicios se han creado diferentes *endpoints* los cuales se detallarán a continuación:

**URL** definada para ambiente de pruebas:
* https://func-simemfile-prb-01.azurewebsites.net/api/
  
**URL** definida para ambiende de producción: 
* 

**Endpoints**:

1. **DatosAbiertosPublico**
* **Método**: GET
* **Parámetros**:
```
Key: startdate
Value: 2023-01-16

Key: enddate
Value: 2023-01-17

Key: datasetId
Value: 6E1BCC6B-2F1D-4E6B-976F-54CA056F9729

(?startdate=2023-01-16&enddate=2023-01-17&datasetId=6E1BCC6B-2F1D-4E6B-976F-54CA056F9729)
```
* **Respuestas**:
* Status: 200 OK <br>
```json
[
  {
    "id": "0eaf4943-8401-4540-bf7b-2849f36fd62f",
    "nombreArchivo": "PRUEBA.parquet",
    "fechaCreacion": "2023-07-06T20:42:06.633268",
    "rutaContenedora": "SIMEM/ca4098d8-d5a3-4f52-80a8-11345335e1a9/2023/1/17/",
    "rutaAbsolutaDirectorioPadre": "SIMEM/Pruebas Fabian Dev/2023/1/17/PRUEBA_11.parquet",
    "tipo": null,
    "tipoContenido": "application/octet-stream",
    "tamanio": "17415",
    "qty": null,
    "fechaIndexado": "2023-01-17T00:00:00",
    "ruta": null,
    "rutaFechaExpiracion": "0001-01-01T00:00:00"    
  }
]
```
* Status: 400 Bad Request
```
{
  "message": "Error obteniendo info con los parametros proporcionados, Value cannot be null. (Parameter 's')"
}
```

2. **Http_Descargar_Archivo_ParquetAExcel**
* **Método**: POST
* **Body**:
```
{
  "archivoIds": ["1","2", ..."n"]
}
```
* **Respuestas**:
* Status: 200 OK <br>
_FileStreamResult_ <br>
( CodVariable;FechaInicio;CodigoDuracion;UnidadMedida;CodPlanta;Version;Valor
CCMdoSec;2022-12-30;P1D;kWh;CTG1;TX4;0
CCMdoSec;2022-12-30;P1D;kWh;GEC3;TX4;210853
CCMdoSec;2022-12-30;P1D;kWh;HMIN;TX4;16000
CCMdoSec;2022-12-30;P1D;kWh;MOY1;TX4;536763
CCMdoSec;2022-12-30;P1D;kWh;PES1;TX4;7032936
CCMdoSec;2022-12-30;P1D;kWh;SLVJ;TX4;205354
CCMdoSec;2022-12-30;P1D;kWh;TCBE;TX4;120600
CCMdoSec;2022-12-30;P1D;kWh;TCD2;TX4;1135289
CCMdoSec;2022-12-30;P1D;kWh;TCDT;TX4;3366036 )
* Status: 400 Bad Request
```
{
  "message": "Error al obtener el archivo o no existe (Parameter '1')"
}
```

3. **Http_Get_Files_ByDataId**
* **Método**: GET
* **Parámetros**:
```
Key: dataid
Value: 6E1BCC6B-2F1D-4E6B-976F-54CA056F9729

(?dataid=6E1BCC6B-2F1D-4E6B-976F-54CA056F9729)
```
* **Respuestas**:
* Status: 200 OK <br>
```json
[
  {
    "id": "0eaf4943-8401-4540-bf7b-2849f36fd62f",
    "nombreArchivo": "PRUEBA.parquet",
    "fechaCreacion": "2023-07-06T20:42:06.633268",
    "rutaContenedora": "SIMEM/ca4098d8-d5a3-4f52-80a8-11345335e1a9/2023/1/17/",
    "rutaAbsolutaDirectorioPadre": "SIMEM/Pruebas Fabian Dev/2023/1/17/PRUEBA_11.parquet",
    "tipo": null,
    "tipoContenido": "application/octet-stream",
    "tamanio": "17415",
    "qty": null,
    "fechaIndexado": "2023-01-17T00:00:00",
    "ruta": null,
    "rutaFechaExpiracion": "0001-01-01T00:00:00"
  },
  {
    "id": "a08af7c7-4261-48b9-bb15-6325f9ef3033",
    "nombreArchivo": "otroarchivopruebatest.parquet",
    "fechaCreacion": "2023-07-06T20:42:27.4137348",
    "rutaContenedora": "SIMEM/6e1bcc6b-2f1d-4e6b-976f-54ca056f9729/2022/2/22/",
    "rutaAbsolutaDirectorioPadre": "SIMEM/6e1bcc6b-2f1d-4e6b-976f-54ca056f9729/2022/2/22/otroarchivopruebatest_5.parquet",
    "tipo": null,
    "tipoContenido": "application/octet-stream",
    "tamanio": "462",
    "qty": null,
    "fechaIndexado": "2022-02-22T00:00:00",
    "ruta": "https://stsimemprb.blob.core.windows.net/simem/SIMEM/6e1bcc6b-2f1d-4e6b-976f-54ca056f9729/2022/2/22/otroarchivopruebatest_5.parquet?sv=2021-08-06&st=2023-07-06T20%3A42%3A27Z&se=2023-08-05T20%3A42%3A27Z&sr=c&sp=r&sig=mJDgLjJ%2BDu4Hm03N%2B4FlgVtIqFFKlFZ3aD8GkhUqAAE%3D",
    "rutaFechaExpiracion": "2023-08-05T20:42:27.3807854"
  }
]
```
* Status: 400 Bad Request
```
{
  "message": "Error obteniendo info con el id proporcionado"
}
```

4. **Http_Get_ParquetData_Json**
* **Método**: GET
* **Parámetros**:
```
Key: fechaInicio
Value: 2023-01-16

Key: fechaFin
Value: 2023-01-17

Key: dataId
Value: D808D43D-E3DA-493D-AAB5-015A818ADE10

(?fechaInicio=2023-01-16&fechaFin=2023-01-17&dataId=D808D43D-E3DA-493D-AAB5-015A818ADE10)
```
* **Respuestas**:
* Status: 200 OK <br>
```json
{
  "parameters": {
    "datasetId": "d808d4",
    "startDate": "1/16/2023",
    "endDate": "1/17/2023"
  },
  "success": true,
  "result": {
    "datasetId": "d808d4",
    "name": "InformacionAnillosdeSeguridadCxC",
    "metadata": {
        "description": "Contiene la Enería de Referencia para el Mercado Secundario por planta. Incluye también la Energía Firme del Cargo por Confiabilidad (ENFICC) y la Energía Disponible Adicional (EDA) por planta",
        "creationDate": "2023-06-04T17:29:21.87",
        "lastUpdate": "2023-06-21T01:48:20.857",
        "entity": "XM",
        "category": "Energía de Referencia para el Mercado Secundario",
        "periodicity": "Diaria",
        "private": false
      },
      "variables": [
         {
          "variableCode": "PrecioMarginalEscasez",
          "variableName": "Precio marginal de escasez",
          "measurementUnit": "COP/kWh",
          "description": "Precio marginal de escasez"
        },
        {
          "variableCode": "PrecioEscasezActivacion",
          "variableName": "Precio de escasez de activación",
          "measurementUnit": "COP/kWh",
          "description": "Precio de escasez de activación"
        },
      ],
      "columns": [
        {
          "nameColumn": "VCMS_EDA",
          "dataType": "flotante",
          "description": "Ventas en Contratos del Mercado Secundario de EDA"
        },
        {
          "nameColumn": "EDA_No_Comprometida",
          "dataType": "flotante",
          "description": "EDA no comprometida"
        },
        {
          "nameColumn": "CodPlanta",
          "dataType": "string",
          "description": "Código del recurso asignado por el ASIC"
        },
        {
          "nameColumn": "Fecha",
          "dataType": "fecha",
          "description": "Fecha de representación de la información"
        }
      ],
      "tags": [
        {
          "id": "8c2d44b2-7416-4337-9e90-b8659a69f36f",
          "name": "Cargo por Confiabilidad"
        },
        {
          "id": "f3e56e18-e6f5-4c09-8871-bd63fbc302e0",
          "name": "Energía de Referencia para el Mercado Secundario"
        }
      ]
  }
}
```
* Status: 400 Bad Request
```
{
  "message": "Valor no puede ser nulo"
}
```

5. **Http_GetParquetDataByFileId**
* **Método**: GET
* **Parámetros**:
```
Key: fileid
Value: 002245ca-3375-4ea3-b134-43ca2ddc2fa8

(?fileid=002245ca-3375-4ea3-b134-43ca2ddc2fa8)
```
* **Respuestas**:
* Status: 200 OK <br>
```json
[
  {
    "CodVariable": "CCMdoSec",
    "FechaInicio": "2022-12-30",
    "CodigoDuracion": "P1D",
    "UnidadMedida": "kWh",
    "CodPlanta": "CTG1",
    "Version": "TX4",
    "Valor": 0.0
  },
  {
    "CodVariable": "CCMdoSec",
    "FechaInicio": "2022-12-30",
    "CodigoDuracion": "P1D",
    "UnidadMedida": "kWh",
    "CodPlanta": "GEC3",
    "Version": "TX4",
    "Valor": 210853.0
  },
  {
    "CodVariable": "CCMdoSec",
    "FechaInicio": "2022-12-30",
    "CodigoDuracion": "P1D",
    "UnidadMedida": "kWh",
    "CodPlanta": "HMIN",
    "Version": "TX4",
    "Valor": 16000.0
  },
  {
    "CodVariable": "CCMdoSec",
    "FechaInicio": "2022-12-30",
    "CodigoDuracion": "P1D",
    "UnidadMedida": "kWh",
    "CodPlanta": "MOY1",
    "Version": "TX4",
    "Valor": 536763.0
  },
  {
    "CodVariable": "CCMdoSec",
    "FechaInicio": "2022-12-30",
    "CodigoDuracion": "P1D",
    "UnidadMedida": "kWh",
    "CodPlanta": "PES1",
    "Version": "TX4",
    "Valor": 7032936.0
  },
  {
    "CodVariable": "CCMdoSec",
    "FechaInicio": "2022-12-30",
    "CodigoDuracion": "P1D",
    "UnidadMedida": "kWh",
    "CodPlanta": "SLVJ",
    "Version": "TX4",
    "Valor": 205354.0
  }
]
```
* Status: 400 Bad Request
```
{
  "message": "Error al obtener el archivo o no existe (Parameter '6E1BCC6B-2F1D-4E6B-976F-54CA056F9729')"
}
```

6. **Http_Post_Save_Files_Indexed**
* **Método**: POST
* **Body**:
```
{
    "uid": "99686983-57A4-433B-BC5E-028ECD0845BA",
    "fecha": "2022-02-21",
    "hora": "30",
    "filasTotales": "10"
}
```
* **Respuestas**:
* Status: 200 OK <br>
_FileStreamResult_ <br>
( CodVariable;FechaInicio;CodigoDuracion;UnidadMedida;CodPlanta;Version;Valor
CCMdoSec;2022-12-30;P1D;kWh;CTG1;TX4;0
CCMdoSec;2022-12-30;P1D;kWh;GEC3;TX4;210853
CCMdoSec;2022-12-30;P1D;kWh;HMIN;TX4;16000
CCMdoSec;2022-12-30;P1D;kWh;MOY1;TX4;536763
CCMdoSec;2022-12-30;P1D;kWh;PES1;TX4;7032936
CCMdoSec;2022-12-30;P1D;kWh;SLVJ;TX4;205354
CCMdoSec;2022-12-30;P1D;kWh;TCBE;TX4;120600
CCMdoSec;2022-12-30;P1D;kWh;TCD2;TX4;1135289
CCMdoSec;2022-12-30;P1D;kWh;TCDT;TX4;3366036 )
* Status: 400 Bad Request
```
{
  "message": "Error al obtener el archivo o no existe"
}
```


<a id='section4'></a>
## Comentarios finales
Tener en cuenta que el formato de fecha que recibe la API es YYYY-MM-DD, también los UID ó Ids deben de existir previamente en la base de datos

