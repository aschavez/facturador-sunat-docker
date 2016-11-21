# Qué es el `Facturador Sunat`?

Es un sistema de facturación electrónica gratuito, disponible para su descarga desde el [Portal de SUNAT](http://cpe.sunat.gob.pe/facturador-empresas), dirigido principalmente a medianos y pequeños contribuyentes que cuentan con sistemas computarizados y tienen un alto volumen de facturación.

Características:

* Convierte la información del contribuyente a formato XML de manera automática.
* No se requiere conexión a internet para la emisión, sólo para el envío a la SUNAT.
* Realiza las validaciones establecidas por SUNAT.
* Firma digitalmente el comprobante.
* Genera un archivo PDF del comprobante en caso requiera entregar una representación impresa.
* Envía automática o manualmente, el comprobante a SUNAT (mediante un temporizador en el caso de la opción automática).
* SUNAT almacena, archiva y conserva la factura electrónica y la nota electrónica vinculada a aquella que se emita a través de este sistema.

Desde este sistema pueden emitirse:

* Facturas,
* Boletas de venta,
* Notas de crédito y
* Notas de débito.

[Más información](http://cpe.sunat.gob.pe/facturador-empresas).

# Cómo usar esta imagen

## Quick start
```
docker run --name facturador-sunat -p 8090:8090 aschavez/facturador-sunat
```


## Exponiendo los directorios principales
```
docker run --name facturador-sunat -v /data:/data0/facturador/DATA -p 8090:8090 aschavez/facturador-sunat
```

Los directorios principales son los siguientes:

|Directorio|Contenido|
|----------|---------|
|/data0/facturador/ALMCERT|Directorio que contiene la base de datos de certificados para firmar comprobantes de pago|
|/data0/facturador/CERT|Directorio de transito, que permite copiar el certificado para ser registrado en la BD de certificados: `ALMCERT`|
|/data0/facturador/DATA|Directorio donde debe copiarse los comprobantes de pago en formato TXT, JSON ó XML.|
|/data0/facturador/ENVIO|Directorio donde se encuentran los comprobantes de pago enviados hacia SUNAT, los cuales se encuentran comprimidos en un formato zip por cada archivo.|
|/data0/facturador/FIRMA|Directorio donde se encuentran los archivos XML, firmados por el facturador y pendientes de enviar a SUNAT.|
|/data0/facturador/FORM|Directorio en el cual se encuentran los fuentes para confección de los reportes de impresión de boletas, facturas, notas de crédito y notas de débito.|
|/data0/facturador/ORIDAT|Origen de datos de los reportes de impresión del directorio `FORM`|
|/data0/facturador/PARSE|Archivos XML que fueron validados, en esquema y según validaciones de contenido.|
|/data0/facturador/REPO|Archivo que contiene los PDF generados por el facturador.|
|/data0/facturador/RPTA|Directorio donde se encuentran los archivos de respuesta de la SUNAT. Sólo se guardan CDR OK.|
|/data0/facturador/TEMP|Directorio temporales del facturador, aquí se encuentran los archivos xml sin validar, cuando vienen de un formato json o plano.|
|/data0/facturador/VALI|Formatos de Plantillas para generar los pdf y xml|

## Ejecutando en modo deamon
```
docker run --name facturador-sunat -d -p 8090:8090 aschavez/facturador-sunat
```

## Mediante `docker-compose.yml`
```
app:
  build: aschavez/facturador-sunat
  ports:
  - 8090:8090
```
> *PD*: A considerar, luego de ejecutar el `docker run`, para que se muestre el aplicativo tomara unos cuantos segundos.
