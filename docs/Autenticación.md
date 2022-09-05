# Autenticación

### Endpoints
<!-- theme: warning -->
> Producción: 
> * WSDL: https://api.placetopay.com/soap/pse/v11/?wsdl
> * Servicio:  https://api.placetopay.com/soap/pse/v11/
>
> Pruebas:
> * WSDL: https://test.placetopay.com/soap/pse/v11/?wsdl
> * Servicio: https://test.placetopay.com/soap/pse/v11

La autenticación a los servicios web debe ser enviada sobre la estructura auth, compuesto como se muestra a continuación:

| Nombre   |      Tipo      |  Descripción |
|----------|-------------|------|
| login |  string | Identificador del sitio. |
| tranKey |    string   |   Llave transaccional, para el consumo del API: **SHA-1(seed + trankey).** |
|  seed    | string | Fecha actual, la cual se genera en formato [**ISO 8601**](https://www.iso.org/iso-8601-date-and-time-format.html). El sistema verificará que la petición no haya expirado, por ello es fundamental una sincronización.|
|additional|[Attribute](Estructura-de-datos-PSE.md#attribute)|Datos adicionales a la estructura de autenticación.|

> El login y el trankey son suministrados por Placetopay.

> El Hash es el que se remite como tranKey en la estructura de autenticación.

> La estructura de autenticación debe de ser enviada en cada petición realizada al servicio.


**Ejemplo de autenticación con la estructura auth:**
```xml
  <auth xmlns="">
      <login>[string]</login>
      <tranKey>[string]</tranKey>
      <seed>[dateTime]</seed>
      <!-- Optional -->
      <additional>
          <!-- Optional -->
          <item>
              <name>[string]</name>
              <value>[string]</value>
          </item>
      </additional>
  </auth>
```
<!-- theme: warning -->

> ### Posibles Errores en Multicrédito:
> | Descripción |  Causa |
> |----------   |:------:|
> |El valor total y el IVA no corresponde a la sumatoria de los créditos.|<li> La sumatoria de los totales y IVA dados en el arreglo tipo **item[]** no coinciden con el total de la transacción dado en **transaction['totalAmount']** y **transaction['taxAmount']**. <br><li> No se está cobrando a todos los servicios dependientes, incluso así el valor para uno de los créditos sea cero.|
> |La matriz de créditos no corresponde a la esperada para el servicio principal, por favor comuníquese con la empresa. | Este error se puede presentar por diversos factores entre los cuales pueden estar los siguiente motivos: <br><li>Faltan o sobran códigos hijos para participar en el proceso de dispersión.<br><li>Códigos hijos o padre no afiliados en ACH para dispersión.<br><li>Se está enviando el entityCode con separador.<br><li>Se están enviando códigos padres para el proceso de dispersión.<br><li> Uno o algunos de los entityCode enviados para el proceso de dispersión no pertenece al respectivo NIT de la cuenta hija.<br><li>Se está formando mal la estructura definida para el arreglo tipo **item[]** dada para el proceso de dispersión en **credits{}**.<br><li>Falta configuración del medio de pago en Placetopay.|





1/

