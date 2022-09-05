# Estructura de datos PSE

Las estructuras de datos utilizadas por los métodos del servicio web se describen a continuación:

#### Attribute
Estructura para almacenar información extendida.
<!--
type: tab
title: ATRIBUTOS
-->

| Nombre   |      Tipo      |  Descripción |
|----------|-------------|------|
| name |  string (30) | Código para referenciar el atributo |
| value |    string (128)   |   Valor que asume el atributo |

<!--
type: tab
title: XML
-->

```xml
<additional>
    <item>
        <name>[string]</name>
        <value>[string]</value>
    </item>
</additional>
```
<!-- type: tab-end -->

#### Persona
Estructura para reflejar la información de una persona involucrada en una transacción.
<!--
type: tab
title: ATRIBUTOS
-->

| Nombre   |      Tipo      |  Descripción |
|----------|-------------|------|
| document |string (12)| Número de identificación de la persona. |
| documentType | string (3) | Tipo de documento de identificación de la persona.|
| firstName | string (60) | Nombres |
| lastName | string (60) | Apellidos|
| company | string (60) | Nombre de la compañía en la cual labora o representa. |
| emailAddress | string (80) |Correo electrónico|
| address | string (100) |Dirección postal completa.  |
| city | string (50)| Nombre de la ciudad coincidente con la dirección. |
| province | string (50)| Nombre de la provincia o departamento coincidente con la dirección.|
| country |  string (2) |	Código internacional del país que aplica a la dirección física acorde a [**ISO 3166-1**](https://es.wikipedia.org/wiki/ISO_3166-1), (mayúscula sostenida).|
| phone | string (30) | Número de telefonía fija. |
| mobile | string (30) | Número de telefonía móvil o celular.|
| postalCode | string (10) |   |


<!--
type: tab
title: XML
-->

```xml
<payer>
  <documentType>[string]</documentType>
  <document>[string]</document>
  <firstName>[string]</firstName>
  <lastName>[string]</lastName>
  <company>[string]</company>
  <emailAddress>[string]</emailAddress>
  <address>[string]</address>
  <city>[string]</city>
  <province>[string]</province>
  <country>[string]</country>
  <phone>[string]</phone>
  <mobile>[string]</mobile>
  <postalCode>[string]</postalCode>
</payer>
<buyer>
  <documentType>[string]</documentType>
  <document>[string]</document>
  <firstName>[string]</firstName>
  <lastName>[string]</lastName>
  <company>[string]</company>
  <emailAddress>[string]</emailAddress>
  <address>[string]</address>
  <city>[string]</city>
  <province>[string]</province>
  <country>[string]</country>
  <phone>[string]</phone>
  <mobile>[string]</mobile>
  <postalCode>[string]</postalCode>
</buyer>
<shipping>
  <documentType>[string]</documentType>
  <document>[string]</document>
  <firstName>[string]</firstName>
  <lastName>[string]</lastName>
  <company>[string]</company>
  <emailAddress>[string]</emailAddress>
  <address>[string]</address>
  <city>[string]</city>
  <province>[string]</province>
  <country>[string]</country>
  <phone>[string]</phone>
  <mobile>[string]</mobile>
  <postalCode>[string]</postalCode>
</shipping>
```
<!-- type: tab-end -->

#### Bank
Estructura para reflejar la información de una entidad bancaria.
<!--
type: tab
title: ATRIBUTOS
-->

| Nombre   |      Tipo      |  Descripción |
|----------|-------------|------|
| bankCode | string (4) | Código de la entidad financiera.|
| bankName | string (60) | Nombre de la entidad financiera. |

<!--
type: tab
title: XML
-->

```xml
<getBankListResult>
  <item>
      <bankCode>0</bankCode>
      <bankName>A continuación seleccione su banco</bankName>
  </item>
  <item>
      <bankCode>1552</bankCode>
      <bankName>BAN.CO</bankName>
  </item>
  <item>
      <bankCode>1059</bankCode>
      <bankName>BANCAMIA</bankName>
  </item>
  <item>
      <bankCode>1040</bankCode>
      <bankName>BANCO AGRARIO</bankName>
  </item>
  <item>
      <bankCode>1081</bankCode>
      <bankName>BANCO AGRARIO DESARROLLO</bankName>
  </item>
  <item>
      <bankCode>1080</bankCode>
      <bankName>BANCO AGRARIO QA DEFECTOS</bankName>
  </item>
  <item>
      <bankCode>10322</bankCode>
      <bankName>BANCO CAJA SOCIAL</bankName>
  </item>
  <item>
      <bankCode>1032</bankCode>
      <bankName>BANCO CAJA SOCIAL DESARROLLO</bankName>
  </item>
  <item>
      <bankCode>1052</bankCode>
      <bankName>BANCO COMERCIAL AVVILLAS S.A.</bankName>
  </item>
  <item>
      <bankCode>1061</bankCode>
      <bankName>BANCO COOMEVA S.A. - BANCOOMEVA</bankName>
  </item>
  <item>
      <bankCode>1066</bankCode>
      <bankName>BANCO COOPERATIVO COOPCENTRAL</bankName>
  </item>
  <item>
      <bankCode>1058</bankCode>
      <bankName>BANCO CREDIFINANCIERA</bankName>
  </item>
  <item>
      <bankCode>1051</bankCode>
      <bankName>BANCO DAVIVIENDA</bankName>
  </item>
  <item>
      <bankCode>10512</bankCode>
      <bankName>BANCO DAVIVIENDA Desarrollo</bankName>
  </item>
  <item>
      <bankCode>1039</bankCode>
      <bankName>BANCO DE BOGOTA</bankName>
  </item>
  <item>
      <bankCode>1001</bankCode>
      <bankName>BANCO DE BOGOTA DESARROLLO 2013</bankName>
  </item>
  <item>
      <bankCode>1023</bankCode>
      <bankName>BANCO DE OCCIDENTE</bankName>
  </item>
  <item>
      <bankCode>1062</bankCode>
      <bankName>BANCO FALABELLA</bankName>
  </item>
  <item>
      <bankCode>1010</bankCode>
      <bankName>BANCO GNB COLOMBIA (ANTES HSBC)</bankName>
  </item>
  <item>
      <bankCode>1012</bankCode>
      <bankName>BANCO GNB SUDAMERIS</bankName>
  </item>
  <item>
      <bankCode>1060</bankCode>
      <bankName>BANCO PICHINCHA S.A.</bankName>
  </item>
  <item>
      <bankCode>1002</bankCode>
      <bankName>BANCO POPULAR</bankName>
  </item>
  <item>
      <bankCode>1203</bankCode>
      <bankName>BANCO PRODUCTOS POR SEPARADO</bankName>
  </item>
  <item>
      <bankCode>1101</bankCode>
      <bankName>Banco PSE</bankName>
  </item>
  <item>
      <bankCode>1065</bankCode>
      <bankName>BANCO SANTANDER COLOMBIA</bankName>
  </item>
  <item>
      <bankCode>1069</bankCode>
      <bankName>BANCO SERFINANZA</bankName>
  </item>
  <item>
      <bankCode>1035</bankCode>
      <bankName>BANCO TEQUENDAMA</bankName>
  </item>
  <item>
      <bankCode>1004</bankCode>
      <bankName>Banco union Colombia Credito</bankName>
  </item>
  <item>
      <bankCode>1022</bankCode>
      <bankName>BANCO UNION COLOMBIANO</bankName>
  </item>
  <item>
      <bankCode>1005</bankCode>
      <bankName>BANCO UNION COLOMBIANO FD2</bankName>
  </item>
  <item>
      <bankCode>1055</bankCode>
      <bankName>Banco Web Service ACH WSE 3.0</bankName>
  </item>
  <item>
      <bankCode>10072</bankCode>
      <bankName>BANCOLOMBIA DATAPOWER</bankName>
  </item>
  <item>
      <bankCode>10071</bankCode>
      <bankName>BANCOLOMBIA DESARROLLO</bankName>
  </item>
  <item>
      <bankCode>1007</bankCode>
      <bankName>BANCOLOMBIA QA</bankName>
  </item>
  <item>
      <bankCode>1077</bankCode>
      <bankName>BANKA</bankName>
  </item>
  <item>
      <bankCode>1013</bankCode>
      <bankName>BBVA COLOMBIA S.A.</bankName>
  </item>
  <item>
      <bankCode>1513</bankCode>
      <bankName>BBVA DESARROLLO</bankName>
  </item>
  <item>
      <bankCode>1009</bankCode>
      <bankName>CITIBANK COLOMBIA S.A.</bankName>
  </item>
  <item>
      <bankCode>1370</bankCode>
      <bankName>COLTEFINANCIERA</bankName>
  </item>
  <item>
      <bankCode>1292</bankCode>
      <bankName>CONFIAR COOPERATIVA FINANCIERA</bankName>
  </item>
  <item>
      <bankCode>1289</bankCode>
      <bankName>COOPERATIVA FINANCIERA COTRAFA</bankName>
  </item>
  <item>
      <bankCode>1283</bankCode>
      <bankName>COOPERATIVA FINANCIERA DE ANTIOQUIA</bankName>
  </item>
  <item>
      <bankCode>1558</bankCode>
      <bankName>CREDIFIANCIERA</bankName>
  </item>
  <item>
      <bankCode>1551</bankCode>
      <bankName>DAVIPLATA</bankName>
  </item>
  <item>
      <bankCode>1006</bankCode>
      <bankName>ITAU</bankName>
  </item>
  <item>
      <bankCode>1508</bankCode>
      <bankName>NEQUI CERTIFICACION</bankName>
  </item>
  <item>
      <bankCode>9988</bankCode>
      <bankName>prueba restriccion</bankName>
  </item>
  <item>
      <bankCode>121212</bankCode>
      <bankName>Prueba Steve</bankName>
  </item>
  <item>
      <bankCode>1151</bankCode>
      <bankName>RAPPIPAY</bankName>
  </item>
  <item>
      <bankCode>1019</bankCode>
      <bankName>SCOTIABANK COLPATRIA DESARROLLO</bankName>
  </item>
  <item>
      <bankCode>1078</bankCode>
      <bankName>SCOTIABANK COLPATRIA UAT</bankName>
  </item>
  <item>
      <bankCode>1305</bankCode>
      <bankName>SEIVY – GM FINANCIAL</bankName>
  </item>
</getBankListResult>
```
<!-- type: tab-end -->

#### CreditConcept
Estructura que representa el concepto del crédito a favor de un tercero.
<!--
type: tab
title: ATRIBUTOS
-->

| Nombre   |      Tipo      |  Descripción |
|----------|-------------|------|
| entityCode | string (12)| Código de la entidad del tercero para dispersión. |
| serviceCode | string (12) | Código del servicio del tercero. |
| amountValue | double | Valor total a recaudar a favor de la entidad. |
| taxValue | double | Discriminación del impuesto aplicado a favor de la entidad. |
| description | string (60) | Descripción del concepto cobrado.|

<!--
type: tab
title: XML
-->

```xml
<credits>
    <item>
        <entityCode>[string]</entityCode>
        <serviceCode>[string]</serviceCode>
        <amountValue>[decimal]</amountValue>
        <taxValue>[decimal]</taxValue>
        <description>[string]</description>
    </item>
</credits>
```
<!-- type: tab-end -->

#### PSETransactionRequest
Estructura que representa una solicitud de transacción con débitos a cuenta PSE.
<!--
type: tab
title: ATRIBUTOS
-->

| Nombre   |      Tipo      |  Descripción |
|----------|-------------|------|
| bankCode | string (4) | Código de la entidad financiera con la cual se va a realizar la transacción. |
| bankInterface | string (1) | Tipo de interfaz del banco a desplegar <br>**0 = PERSONAS <br> 1 = EMPRESAS** |
| returnURL | string (255) | URL de retorno especificada para la entidad financiera. |
| reference | string (32) | Referencia única de pago. |
| description | string (255) |Descripción del pago.|
|language |string (2) |Idioma esperado para las transacciones acorde a [**ISO 639-1**](https://es.wikipedia.org/wiki/ISO_639-1), (mayúscula sostenida). |
|currency |string (3) |Moneda a usar para el recaudo acorde a [**ISO 4217** ](https://es.wikipedia.org/wiki/ISO_4217), (mayúscula sostenida).  |
|totalAmount |double |Valor total a recaudar. |
|taxAmount |double |Discriminación del impuesto aplicado. |
|devolutionBase |double |Base de devolución para el impuesto. |
|tipAmount |double | Propina u otros valores exentos de impuesto (tasa aeroportuaria) y que deben agregarse al valor total a pagar.|
|payer |[Person](Estructura-de-datos-PSE.md#persona) |Información del pagador.|
|buyer |[Person](Estructura-de-datos-PSE.md#persona) |Información del comprador. |
|shipping|[Person](Estructura-de-datos-PSE.md#persona) |Información del receptor. |
|ipAddress |string (15) | Dirección IP desde la cual se realiza la transacción, (se obtiene del pagador).|
|userAgent |string (255) | Agente de navegación utilizado por el pagador.|
|additionalData |[Attribute](Estructura-de-datos-PSE.md#attribute)| Datos adicionales para ser almacenados con la transacción.|

<!--
type: tab
title: XML
-->

```xml
<transaction xmlns="">
  <bankCode>[string]</bankCode>
  <bankInterface>[string]</bankInterface>
  <returnURL>[string]</returnURL>
  <reference>[string]</reference>
  <description>[string]</description>
  <language>[string]</language>
  <currency>[string]</currency>
  <totalAmount>[decimal]</totalAmount>
  <taxAmount>[decimal]</taxAmount>
  <devolutionBase>[decimal]</devolutionBase>
  <tipAmount>[decimal]</tipAmount>
  <payer>
      <documentType>[string]</documentType>
      <document>[string]</document>
      <firstName>[string]</firstName>
      <lastName>[string]</lastName>
      <company>[string]</company>
      <emailAddress>[string]</emailAddress>
      <address>[string]</address>
      <city>[string]</city>
      <province>[string]</province>
      <country>[string]</country>
      <phone>[string]</phone>
      <mobile>[string]</mobile>
      <postalCode>[string]</postalCode>
  </payer>
  <buyer>
      <documentType>[string]</documentType>
      <document>[string]</document>
      <firstName>[string]</firstName>
      <lastName>[string]</lastName>
      <company>[string]</company>
      <emailAddress>[string]</emailAddress>
      <address>[string]</address>
      <city>[string]</city>
      <province>[string]</province>
      <country>[string]</country>
      <phone>[string]</phone>
      <mobile>[string]</mobile>
      <postalCode>[string]</postalCode>
  </buyer>
  <shipping>
      <documentType>[string]</documentType>
      <document>[string]</document>
      <firstName>[string]</firstName>
      <lastName>[string]</lastName>
      <company>[string]</company>
      <emailAddress>[string]</emailAddress>
      <address>[string]</address>
      <city>[string]</city>
      <province>[string]</province>
      <country>[string]</country>
      <phone>[string]</phone>
      <mobile>[string]</mobile>
      <postalCode>[string]</postalCode>
  </shipping>
  <ipAddress>[string]</ipAddress>
  <userAgent>[string]</userAgent>
  <additionalData/>
</transaction>
```
<!-- type: tab-end -->

#### PSETransactionMultiCreditRequest
Estructura que representa una solicitud de transacción con dispersión en débitos a cuenta PSE.
<!--
type: tab
title: ATRIBUTOS
-->

| Nombre   |      Tipo      |  Descripción |
|----------|-------------|------|
| bankCode | string (4) | Código de la entidad financiera con la cual se va a realizar la transacción. |
| bankInterface | string (1) | Tipo de interfaz del banco a desplegar <br>**0 = PERSONAS <br> 1 = EMPRESAS** |
| returnURL | string (255) | URL de retorno especificada para la entidad financiera. |
| reference | string (32) | Referencia única de pago. |
| description | string (255) |Descripción del pago.|
|language |string (2) |Idioma esperado para las transacciones acorde a [**ISO 639-1**](https://es.wikipedia.org/wiki/ISO_639-1), (mayúscula sostenida). |
|currency |string (3) |Moneda a usar para el recaudo acorde a [**ISO 4217** ](https://es.wikipedia.org/wiki/ISO_4217), (mayúscula sostenida).  |
|totalAmount |double |Valor total a recaudar. |
|taxAmount |double |Discriminación del impuesto aplicado. |
|devolutionBase |double |Base de devolución para el impuesto. |
|tipAmount |double | Propina u otros valores exentos de impuesto (tasa aeroportuaria) y que deben agregarse al valor total a pagar.|
|payer |[Person](Estructura-de-datos-PSE.md#persona) |Información del pagador.|
|buyer |[Person](Estructura-de-datos-PSE.md#persona) |Información del comprador. |
|shipping|[Person](Estructura-de-datos-PSE.md#persona) |Información del receptor. |
|ipAddress |string (15) | Dirección IP desde la cual se realiza la transacción, (se obtiene del pagador).|
|userAgent |string (255) | Agente de navegación utilizado por el pagador.|
|additionalData |[Attribute](Estructura-de-datos-PSE.md#attribute)| Datos adicionales para ser almacenados con la transacción.|
|credits|  [CreditConcept](Estructura-de-datos-PSE.md#creditconcept)| Representa el concepto del crédito a favor de un tercero.

<!--
type: tab
title: XML
-->

```xml
<transaction xmlns="">
  <reference>[string]</reference>
  <description>[string?]</description>
  <language>[string]</language>
  <currency>[string]</currency>
  <totalAmount>[decimal]</totalAmount>
  <taxAmount>[decimal]</taxAmount>
  <devolutionBase>[decimal]</devolutionBase>
  <tipAmount>[decimal]</tipAmount>
  <payer>
      <documentType>[string]</documentType>
      <document>[string]</document>
      <firstName>[string]</firstName>
      <lastName>[string]</lastName>
      <company>[string]</company>
      <emailAddress>[string]</emailAddress>
      <address>[string]</address>
      <city>[string]</city>
      <province>[string]</province>
      <country>[string]</country>
      <phone>[string]</phone>
      <mobile>[string]</mobile>
      <postalCode>[string]</postalCode>
  </payer>
  <buyer>
      <documentType>[string]</documentType>
      <document>[string]</document>
      <firstName>[string]</firstName>
      <lastName>[string]</lastName>
      <company>[string]</company>
      <emailAddress>[string]</emailAddress>
      <address>[string]</address>
      <city>[string]</city>
      <province>[string]</province>
      <country>[string]</country>
      <phone>[string]</phone>
      <mobile>[string]</mobile>
      <postalCode>[string]</postalCode>
  </buyer>
  <shipping>
      <documentType>[string]</documentType>
      <document>[string]</document>
      <firstName>[string]</firstName>
      <lastName>[string]</lastName>
      <company>[string]</company>
      <emailAddress>[string]</emailAddress>
      <address>[string]</address>
      <city>[string]</city>
      <province>[string]</province>
      <country>[string]</country>
      <phone>[string]</phone>
      <mobile>[string]</mobile>
      <postalCode>[string]</postalCode>
  </shipping>
  <ipAddress>[string]</ipAddress>
  <userAgent>[string]</userAgent>
  <additionalData/>
  <credits>
      <!-- Optional -->
      <item>
          <entityCode>[string]</entityCode>
          <serviceCode>[string]</serviceCode>
          <amountValue>[decimal]</amountValue>
          <taxValue>[decimal]</taxValue>
          <description>[string]</description>
      </item>
      <item>
          <entityCode>[string]</entityCode>
          <serviceCode>[string]</serviceCode>
          <amountValue>[decimal]</amountValue>
          <taxValue>[decimal]</taxValue>
          <description>[string]</description>
      </item>
  </credits>
  <bankCode>[string]</bankCode>
  <bankInterface>[string]</bankInterface>
  <returnURL>[string]</returnURL>
</transaction>
```
<!-- type: tab-end -->

#### PSETransactionResponse
Estructura con la información de respuesta para la creación de una transacción.
<!--
type: tab
title: ATRIBUTOS
-->

| Nombre   |      Tipo      |  Descripción |
|----------|----------------|--------------|
|transactionID |int|Identificador único de la transacción en Placetopay.|
|sessionID |string (32)|Identificador único de la sesión en Placetopay.|
|returnCode|string (30)|Código de respuesta de la transacción, puede tomar uno de los siguientes valores:<br>SUCCESS<br>FAIL_ENTITYNOTEXISTSORDISABLED<br>FAIL_BANKNOTEXISTSORDISABLED<br>FAIL_SERVICENOTEXISTS<br>FAIL_INVALIDAMOUNT<br>FAIL_INVALIDSOLICITDATE<br>FAIL_BANKUNREACHEABLE<br>FAIL_NOTCONFIRMEDBYBANK<br>FAIL_CANNOTGETCURRENTCYCLE<br>FAIL_ACCESSDENIED<br>FAIL_TIMEOUT<br>FAIL_DESCRIPTIONNOTFOUND<br>FAIL_EXCEEDEDLIMIT<br>FAIL_TRANSACTIONNOTALLOWED<br>FAIL_RISK<br>FAIL_NOHOST<br>FAIL_NOTALLOWEDBYTIME<br>FAIL_ERRORINCREDITS|
|trazabilityCode|string (40)|Código único de seguimiento para la operación dado por la red ACH|
|transactionCycle|int|Ciclo de compensación de la red|
|bankCurrency|string (3)|Moneda aceptada por el banco acorde a [**ISO 4217** ](https://es.wikipedia.org/wiki/ISO_4217).|
|bankFactor|float|Factor de conversión de la moneda.|
|bankURL|string (255) |	URL a la cual remitir la solicitud para iniciar la interfaz del banco, sólo disponible cuando **returnCode = SUCCESS**.|
|responseCode|int|Estado de la operación en Placetopay: <br> 0 = FAILED<br> 1 = APPROVED<br> 2 = DECLINED<br> 3 = PENDING|
|responseReasonCode|string (3)|Código interno de respuesta de la operación en Placetopay.|
|responseReasonText|string (255)|Mensaje asociado con el código de respuesta de la operación en Placetopay.|


<!--
type: tab
title: XML
-->

```xml
<ns1:createTransactionResponse>
    <createTransactionResult>
        <responseCode>3</responseCode>
        <responseReasonCode>?-</responseReasonCode>
        <responseReasonText>Transacción pendiente. Por favor verificar si el débito fue realizado en el Banco.</responseReasonText>
        <returnCode>SUCCESS</returnCode>
        <bankURL>https://registro.desarrollo.pse.com.co/PSEUserRegister/StartTransaction.aspx?enc=tnPcJHMKlSnmRpHM8fAbu71MTlLI9lbRu4P8W1Bt4FtOkV9nfNhknJdjsoAipWpR</bankURL>
        <trazabilityCode>2150228</trazabilityCode>
        <transactionCycle>1</transactionCycle>
        <transactionID>1509187577</transactionID>
        <sessionID>ae5da562836e756a9e49637296689870</sessionID>
        <bankCurrency>COP</bankCurrency>
        <bankFactor>1</bankFactor>
    </createTransactionResult>
</ns1:createTransactionResponse>
```
<!-- type: tab-end -->

#### TransactionInformation
Estructura con la respuesta a una solicitud de información de transacción.
<!--
type: tab
title: ATRIBUTOS
-->

| Nombre   |      Tipo      |  Descripción |
|----------|----------------|--------------|
|transactionID|int|Identificador único de la transacción en Placetopay.|
|sessionID|string (32) |Identificador único de la sesión en Placetopay.|
|reference|string (32)|Referencia única de pago.|
|requestDate|string|	Fecha de solicitud o creación de la transacción acorde a [**ISO 8601** ](https://www.iso.org/iso-8601-date-and-time-format.html).|
|bankProcessDate|string|	Fecha de procesamiento de la transacción acorde a [**ISO 8601** ](https://www.iso.org/iso-8601-date-and-time-format.html).|
|onTest|boolean|Indicador de si la transacción está o no en modo de pruebas.|
|returnCode|string (30)|Código de respuesta de la transacción, puede tomar uno de los siguientes valores:<br>SUCCESS<br>FAIL_INVALIDTRAZABILITYCODE<br>FAIL_ACCESSDENIED<br>FAIL_INVALIDSTATE<br>FAIL_INVALIDBANKPROCESSINGDATE<br>FAIL_INVALIDAUTHORIZEDAMOUNT<br>FAIL_INCONSISTENTDATA<br>FAIL_TIMEOUT<br>FAIL_INVALIDVATVALUE<br>FAIL_INVALIDTICKETID<br>FAIL_INVALIDSOLICITEDATE<br>FAIL_INVALIDAUTHORIZATIONID<br>FAIL_TRANSACTIONNOTALLOWED<br>FAIL_ERRORINCREDITS<br>FAIL_EXCEEDEDLIMIT|
|trazabilityCode|string (40)|Código único de seguimiento para la operación dado por la red ACH.|
|transactionCycle|int|Ciclo de compensación de la red.|
|transactionState|string (20)|Información del estado de la transacción:<br> OK<br>NOT_AUTHORIZED<br> PENDING<br> FAILED|
|responseCode|int|Estado de la operación en Placetopay.|
|responseReasonCode|string (3)|Código interno de respuesta de la operación en Placetopay.|
|responseReasonText|string (255)	| 	Mensaje asociado con el código de respuesta de la operación en Placetopay.|


<!--
type: tab
title: XML
-->

```xml
<ns1:getTransactionInformationResponse>
    <getTransactionInformationResult>
        <transactionID>1509191891</transactionID>
        <sessionID>4d5d68be1ff25d6d083e0a0ce0866d23</sessionID>
        <reference>1618927907</reference>
        <requestDate>2021-04-20T09:11:39-05:00</requestDate>
        <bankProcessDate>2021-04-20T09:11:39-05:00</bankProcessDate>
        <onTest>true</onTest>
        <returnCode>SUCCESS</returnCode>
        <trazabilityCode>2150308</trazabilityCode>
        <transactionCycle>-1</transactionCycle>
        <transactionState>PENDING</transactionState>
        <responseCode>3</responseCode>
        <responseReasonCode>?-</responseReasonCode>
        <responseReasonText>Transacción pendiente. Por favor verificar si el débito fue realizado en el Banco.</responseReasonText>
    </getTransactionInformationResult>
</ns1:getTransactionInformationResponse>
```
<!-- type: tab-end -->





















