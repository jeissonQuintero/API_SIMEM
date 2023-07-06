# API_SIMEM

## Índice
1. [Descripción general](#section1)
2. [Posibles solicitudes para consumir la API](#section2)
3. [URL/Endpoints para consumir la API](#section3)
4. [Comentarios finales](#section6)
5. [Elementos necesarios para utilizar el servicio desde cualquier cliente](#section7)

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

1. **Http_Descargar_Archivo_ParquetAExcel**
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

2. **Http_Get_Files_ByDataId**
* **Método**: GET
* **Parámetros**:
```
Key: dataid
Value: 6E1BCC6B-2F1D-4E6B-976F-54CA056F9729
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
