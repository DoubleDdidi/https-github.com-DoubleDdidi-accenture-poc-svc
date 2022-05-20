Description:
Operación que permite la consulta de localidades con talleres para una provincia.
Operation type:
*Request-response* El endpoint recibe un mensaje, y envia un mensaje correlacionado.
Input:
consultarLocalidades (soap:body, use = literal)
* consultarLocalidades type *consultarLocalidades*
Estructura con los parámetros de entrada de la operacion de consultarLocalidades.
  * MSEConsultarLocalidades ( Optional ) type *prLocalidadesTallerExecutorIn*
Estructura que contiene la entrada a la operación de consulta de localidades.
    * codProvincia type *string*
Código de la provincia por el que realizar el filtrado de cadenas luneras. Valores posibles tabla paramétrica 001.
Output:
consultarLocalidadesResponse (soap:body, use = literal)
* consultarLocalidadesResponse type *consultarLocalidadesResponse*
Estructura con los parámetros de salida de la operacion de consultarLocalidadesResponse.
  * MSSConsultarLocalidades ( Optional ) type *prLocalidadesTallerExecutorOut*
Estructura que contiene la salida de la operacion de consulta de localidades.
    * codRetorno type *int*
Código de retorno del servicio. (Obligatorio). Valores posibles: 1 --> OK.
    * descRetorno type *string*
Descripción de retorno del servicio. (Obligatorio).
    * localidades ( Optional ) type *localidades*
Lista de localidades de la salida del servicio.
      * localidad ( Optional - [0..999] ) type *orTllLocalidadSrt*
Estructura que contiene la información de una localidad.
        * codLocalidad ( Optional ) type *int*
Código de la localidad.
        * nomLocalidad ( Optional ) type *string*
Nombre de la localidad.
        * codPostalLocalidad ( Optional ) type *string*
Código postal de la localidad.
        * codProvincia ( Optional ) type *int*
Código de la provincia a la que pertenece la localidad. Valores posibles tabla paramétrica 001.
        * nomProvincia ( Optional ) type *string*
Nombre de la provincia a la que pertenece la localidad.
        * codPais ( Optional ) type *string*
Código del país al que pertenece la localidad. Valores posibles tabla paramétrica 004.
        * nomPais ( Optional ) type *string*
Nombre del país al que pertenece la localidad.
Fault:
SrtGaiaSoaException (soap:body, use = literal)
* gaiaSoaExceptionInfo type *gaiaSoaExceptionInfo*

  * application ( Optional ) type *string*
Nombre de la aplicacion que genero el error.
  * code ( Optional ) type *string*
El código del error.
  * component ( Optional ) type *string*
Componente que recibe el error y que lo propagara.
  * context ( Optional ) type *string*
Contexto en el que se produce el error.
  * errors ( nillable - Optional - [0..25] ) type *errorDetail*
Lista de información extra del error.
    * code ( Optional ) type *string*
El código del error.
    * component ( Optional ) type *string*
Componente que recibe el error y que lo propagara.
    * info ( nillable - Optional - [0..25] ) type *errorInfoEntry*
Lista de información custom sobre el error.
      * key ( Optional ) type *string*
La clave identificativa de la información personalizada.
      * value ( Optional ) type *string*
El valor de la información personalizada.
    * message ( Optional ) type *string*
El mensaje del detalle del error.
    * rootCause ( Optional ) type *string*
La causa raiz del error.
  * exception ( Optional ) type *string*
Detalle de la excepción.
  * message ( Optional ) type *string*
Mensaje descriptivo del error.
  * stackTrace ( nillable - Optional - [0..100] ) type *stackTrace*
Lista de trazas que ha generado la excepción.
    * declaringClass ( Optional ) type *string*
La clase sobre la que has saltado la excepción.
    * fileName ( Optional ) type *string*
El nombre del fichero sobre el que ha saltado la excepción.
    * lineNumber ( Optional ) type *int*
El número de linea en el que ha saltado la excepción.
    * methodName ( Optional ) type *string*
El nombre del metodo que ha lanzado la excepción.
  * timeStamp ( Optional ) type *dateTime*
La fecha de la excepcion en formato timestamp.
  * type ( Optional ) type *errorType*
El tipo del error.
    * errorType type *string*
