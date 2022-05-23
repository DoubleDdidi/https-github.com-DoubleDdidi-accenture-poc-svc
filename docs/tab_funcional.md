 

**Contenido del token**



 En el proceso de login, el API GW incluye el siguiente parámetro en el payload del token con el siguiente formato: 

 "customPayload": { 
 "userTokenId": "{userInfo.userId}", 
 "tokenClientId": "{userInfo.clientId}", 
 "userBK": "TRON2000" (valor fijo) 
 }, 



 Los valores de las variables **userInfo.userId** y **userInfo.clientId** se obtiene de la respuesta enviada por el backend.



 Cuando se invoca a algunas del APIs a las que autoriza con el token generado, el API GW enviará los siguientes parámetros de cabecera:
* userBK con valor {customPayload.userBK}
* tokenClientId con valor {customPayload.tokenClientId}




**Login process graphically:**

 



 

 

**Example of the login process:**

 

*   1. **Normal login process. **All services include a "login" resource, which is accessed with basic security to obtain the token. The call would be similar to this one (only the relevant fields for explanation are included):

 

**POST ****[https://apisb.mapfre.com/srv/api/GestionarConsolidacionPropuestasSV/propuestas/login](https://apisb.mapfre.com/srv/api/GestionarConsolidacionPropuestasSV/propuestas/login)** HTTP/1.1

Content-Type: application/json

**Authorization: ****Basic**** YWRtLXNvYTphZG0tc29h (You can use APP-ACTPNEO-MRE / g5D3qdXvSP)**

** **

This call will return a token along with its expiration, which should be used in successive calls to business operations, and a refresh token, which we will use to reorder a token once it has expired:

 

{

 "token": "ecevScDuJniLMFHo4xuhsAP63OtGTCEsLre3POO7_D9Ipac30Xt0Ecbg7XohM4JdYF0iieX8R21fJSIwovY25Q",

 "exp": 1531909741,

 **"refreshToken": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.ew0KICAic3ViIjogImFkbS1zb2EiLA0KICAiYXVkIjogImJpYmxpb2dyYXBoaWVzIiwNCiAgImV4cCI6IDE1MzE5MDk3NDENCn0.WYOhwtvK92IcPPg3GaiOH4vAUPl6J166yrrRRDOev8rHqolPFT4V03T0pADyjnDWaetf-SqOBQN2s623qCYWSw"**

}

 

*   1. **Other resources. To call any resource, use the token collected in the initial call, including the header "Authorization" with the value "Bearer TokendevueltoPorLogin", this way:**

GET: [https://apisb.mapfre.com/srv/api/GestionarConsolidacionPropuestasSV/test](https://apisb.mapfre.com/srv/api/GestionarConsolidacionPropuestasSV/test)

**Authorization**: apisb ecevScDuJniLMFHo4xuhsAP63OtGTCEsLre3POO7_D9Ipac30Xt0Ecbg7XohM4JdYF0iieX8R21fJSIwovY25Q

 

*   1. **Refreshment of the token. **The token expires after 15 minutes of use, if before or after a refresh token is used, it will obtain a new token, which will last another 15 minutes. The call is exactly the same as in step 1, except that in this case, the Authorization header contains the refresh token, preceded by the Bearer tag:

** **

**POST **[**https://10.229.132.141:8443/srv/bibliographies/login**](https://10.229.132.141:8443/srv/bibliographies/login) HTTP/1.1

Content-Type: application/json

A**uthorization: ****Bearer ****eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.ew0KICAic3ViIjogImFkbS1zb2EiLA0KICAiYXVkIjogImJpYmxpb2dyYXBoaWVzIiwNCiAgImV4cCI6IDE1MzE5MDk3NDENCn0.WYOhwtvK92IcPPg3GaiOH4vAUPl6J166yrrRRDOev8rHqolPFT4V03T0pADyjnDWaetf-SqOBQN2s623qCYWSw**

 

It is observed that here, the token has changed, but the refresh token, which remains the same, is not returned. After one hour, the refresh token expires, and the only way to renew credentials is to return to point 1. 

{

 "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.ew0KICAic3ViIjogImFkbS1zb2EiLA0KICAiYXVkIjogImJpYmxpb2dyYXBoaWVzIiwNCiAgImV4cCI6IDE1MzE5MDk4NzANCn0.u4Deb8qb4Exb9s5CjjldJVAQyrfipJeMVlEI2_VE_U2lATi0ir-1kvEU1-YZVoDpOQfuw6xK6JpcQnIyi2UEaw",

 "exp": 1531909870

}