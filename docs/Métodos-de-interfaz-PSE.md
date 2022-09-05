# Métodos de interfaz PSE

A continuación se describen cada una de los métodos de tipo petición respuesta expuestas por el Webservice, se muestran los parámetros de entrada a cada operación y vínculos a las estructuras de datos usadas.

### getBankList

Obtiene la lista de bancos disponibles para el establecimiento de comercio en el sistema PSE de ACH Colombia.

**PARÁMETROS**

| Nombre   |      Tipo     | Descripción |
|----------|-------------|------|
| auth |   [Autenticación](Autenticación.md#autenticación)| Datos de autenticación |


**Retorna:**


[Bank{ }](Estructura-de-datos-PSE.md#bank). Un arreglo con la lista de bancos habilitados.

<!-- theme: warning -->

>La respuesta de este servicio debe ser cacheada.


<!-- theme: primary -->
>El servicio debe ser consumido una vez por día.

#### getBankList ejemplo en PHP:
```php
function bancos(){

    $login = "loginp2p";
    $secretKey = 'secretp2p';
    $seed = date('c');
    $trankey = sha1($seed.$secretKey);
    $servicio = 'https://test.placetopay.com/soap/pse/v11/?wsdl'; //URL DEL SERVICIO

    //AUTENTICACIÓN
    $auth = array(
    'login' => $login,
    'tranKey' => $trankey,
    'seed' => $seed,
    );

    $arguments = array(
            'auth' => $auth,
            );
    $client = new nusoap_client($servicio, array('trace' => true)); // EN LUGAR DE SOAPCLIENT  SE UTILIZA NUSOAP_CLIENT

    // LAMADA AL MÉTODO GETBANKLIST DE PSE
    $resp = $client->call('getBankList', $arguments);
    $resp1 = $resp['getBankListResult']['item'];
    echo '<h5>Seleccione su banco </h5><br>
      <select name="banco" id="bank" class="form-control" onchange ="r();">';

    // SE RECORRE EL ARRAY PARA LISTAR BANCOS
    foreach ($resp1 as $key => $valor) {
    echo '<option value="'.$valor['bankCode'].'">'.$valor['bankName'].'</option>';
    }
    echo '</select>';
}
```

### createTransaction

Solicita la creación de una transacción. En los datos de la solicitud se específica quién es el pagador, el comprador y el despacho. Así mismo para cuál de los bancos habilitados se hace la petición y a que URL de retorno debe el banco redirigir al cuentahabiente.

**PARÁMETROS**

| Nombre   |      Tipo      |  Descripción |
|----------|:-------------:|------:|
| auth | [Autenticación](Autenticación.md#autenticación) | Datos de autenticación |
| transaction |[PSETransactionRequest](Estructura-de-datos-PSE.md#psetransactionrequest)  |   Datos de la solicitud |

**Retorna:**


 [PSETransactionResponse](Estructura-de-datos-PSE.md#psetransactionresponse). Respuesta de la creación de la transacción, tenga en cuenta que la URL del banco se entrega solo si la propiedad **returnCode** es SUCCESS.

#### createTransaction ejemplo en PHP:
```php
function RealizarPago(){

      $login = "loginp2p";
      $secretKey = 'secretp2p';
      $seed = date('c');
      $trankey = sha1($seed.$secretKey);

      //PAGO POR PSE
      if (isset($_POST['banco']) && $_POST['banco'] != '') {
      $banco = $_POST['banco'];
      $servicio = 'https://test.placetopay.com/soap/pse/v11/?wsdl'; //URL DEL SERVICIO

      $auth = array(
      'login' => $login,
      'tranKey' => $trankey,
      'seed' => $seed,
      );

      $payer = array(
              'documentType' => $_POST['tipdoc'],
              'document' => $_POST['cedula'],
              'firstName' => $_POST['nombre'],
              'lastName' => $_POST['apellido'],
              'emailAddress' => $_POST['correo'],
              'city' => $_POST['ciudad'],
              'province' => $_POST['pais'],
              'country' => 'Antioquia',
              'mobile' => $_POST['telefono'],
      );

      $transaction = array(
              'bankCode' => $banco,
              'bankInterface' => 0,
              'returnURL' => 'http://localhost/example.php',
              'reference' => $reference = time(),
              'description' => 'Pago',
              'language' => 'ES',
              'currency' => $_POST['moneda'],
              'totalAmount' => $_POST['total'],
              'taxAmount' => 0,
              'devolutionBase' => 0,
              'tipAmount' => 0,
              'payer' => $payer,
              'ipAddress' => '192.168.1.12',
      );

      $arguments = array(
              'auth' => $auth,
              'transaction' => $transaction,
      );
      $client = new nusoap_client($servicio, array('trace' => true));

      // SE CREA LA TRANSACCIÓN PARA PAGO POR PSE
      $resp = $client->call('createTransaction', $arguments);
      var_dump($resp);

      $_SESSION['transactionId'] = $resp['createTransactionResult']['transactionID'];

      //REDIRECCION AL PSE
      echo '<script>
      window.location = "'.$resp['createTransactionResult']['bankURL'].'";
      </script>';
}
```

### createTransactionMultiCredit

Solicita la creación de una transacción con dispersión de fondos. En los datos de la solicitud se especifica quién es el pagador, el comprador y el despacho. Así mismo para cuál de los bancos habilitados se hace la petición y a que URL de retorno debe el banco redirigir al cuentahabiente. Así como también se detalla cada uno de los créditos a aplicar para cada uno de los servicios asociados a la dispersión. **Tenga en cuenta que un servicio multicrédito tiene asociado unos servicios dependientes, por lo tanto siempre deberá cobrar a todos los servicios dependientes así el valor para uno de los créditos sea cero.**

**PARÁMETROS**

| Nombre   |      Tipo      |  Descripción |
|----------|:-------------:|------:|
| auth |  	[Autenticación](Autenticación.md#autenticación) | Datos de autenticación |
| transaction |  [PSETransactionMultiCreditRequest](Estructura-de-datos-PSE.md#psetransactionmulticreditrequest) |   Datos de la solicitud |

**Retorna:**

 [PSETransactionResponse](Estructura-de-datos-PSE.md#psetransactionresponse). Respuesta de la creación de la transacción, tenga en cuenta que la URL del banco se entrega solo si la propiedad returnCode es SUCCESS.

#### createTransactionMultiCredit ejemplo en PHP:
```php
function RealizarPagoMultiCredit(){

      $login = "loginp2p";
      $secretKey = 'secretp2p';
      $seed = date('c');
      $trankey = sha1($seed.$secretKey);

      //PAGO POR PSE
      if (isset($_POST['banco']) && $_POST['banco'] != '') {
      $banco = $_POST['banco'];
      $servicio = 'https://test.placetopay.com/soap/pse/v11/?wsdl'; //URL DEL SERVICIO

      $auth = array(
      'login' => $login,
      'tranKey' => $trankey,
      'seed' => $seed,
      );

      $payer = array(
              'documentType' => $_POST['tipdoc'],
              'document' => $_POST['cedula'],
              'firstName' => $_POST['nombre'],
              'lastName' => $_POST['apellido'],
              'emailAddress' => $_POST['correo'],
              'city' => $_POST['ciudad'],
              'province' => $_POST['pais'],
              'country' => 'Antioquia',
              'mobile' => $_POST['telefono'],
      );

      $credits = array(
            'item' => [array(
                  'entityCode'=> '90029922801',
                  'serviceCode'=> '77700101',
                  'amountValue'=> $_POST['totalitem1'],
                  'taxValue'=> 0,
                  'description'=> 'Payment split 1'
            ),array(
                  'entityCode'=> '90029922801',
                  'serviceCode'=> '77700102',
                  'amountValue'=> $_POST['totalitem2'],
                  'taxValue'=> 0,
                  'description'=> 'Payment split 2'
            ),array(
                  'entityCode'=> '90029922801',
                  'serviceCode'=> '77700103',
                  'amountValue'=> $_POST['totalitem3'],
                  'taxValue'=> 0,
                  'description'=> 'Payment split 3'
            )]
      );

//EL ARREGLO TIPO ITEM[] ES APARTIR DEL CUAL SE DAN LAS DISPERSIONES A LAS CUENTAS, EL ENTITYCODE ES EL NIT DEL COMERCIO SIN DIGITO DE VERIFICACIÓN, EL SERVICECODE REPRESENTA LAS CUENTAS HIJAS A LAS CUALES SE REALIZARÁ LA DISPERSIÓN. LOS TOTALES DEL ARREGLO TIPO ITEM[] DEBEN COINCIDIR CON TRANSACTION['TOTAL']. DE NO CUMPLIRSE LOS CRITERIOS ANTERIORES SE GENERARÁ ERROR.


      $transaction = array(
              'bankCode' => $banco,
              'bankInterface' => 0,
              'returnURL' => 'http://localhost/example.php',
              'reference' => $reference = time(),
              'description' => 'Pago',
              'language' => 'ES',
              'currency' => $_POST['moneda'],
              'totalAmount' => $_POST['total'],
              'taxAmount' => 0,
              'devolutionBase' => 0,
              'tipAmount' => 0,
              'payer' => $payer,
              'credits' => $credits,
              'ipAddress' => '192.168.1.12',
      );

      $arguments = array(
              'auth' => $auth,
              'transaction' => $transaction,
      );
      $client = new nusoap_client($servicio, array('trace' => true));

      // SE CREA LA TRANSACCIÓN PARA PAGO POR PSE
      $resp = $client->call('createTransactionMultiCredit', $arguments);
      var_dump($resp);

      $_SESSION['transactionId'] = $resp['createTransactionResult']['transactionID'];

      //REDIRECCION AL PSE
      echo '<script>
      window.location = "'.$resp['createTransactionResult']['bankURL'].'";
      </script>';
}
```
<!-- theme: warning -->
> [Ver posibles errores](Autenticación.md#posibles-errores-en-multicrédito)

### getTransactionInformation

Obtiene la información de una transacción, debe ser consultado para cualquier operación previamente creada con el método 	[createTransaction](Métodos-de-interfaz-PSE.md#createtransaction) o [createTransactionMultiCredit](Métodos-de-interfaz-PSE.md#createtransactionmulticredit) ya sea cuando regresa del banco o cuando al menos han transcurrido 8 minutos desde que el cliente fue redirigido a la interfaz del banco. Deberá consumirse en intervalos de al menos cada 15 minutos hasta que tenga un estado de transacción diferente a PENDING.

**PARÁMETROS**

| Nombre   |      Tipo      |  Descripción |
|----------|:-------------:|------:|
| auth |  	[Autenticación](Autenticación.md#autenticación) | Datos de autenticación |
| transactionID |    int  |   Identificador único de la transacción en Placetopay, equivale al retornado en la creación de la transacción. |

**Retorna:**

[TransactionInformation](Estructura-de-datos-PSE.md#transactioninformation). Información del estado de la transacción.

#### getTransactionInformation ejemplo en PHP:
```php
function información(){

      if (!isset($_SESSION)){
       session_start();
      }
        if (isset($_SESSION["transactionId"])) 
        {
        $id = $_SESSION["transactionId"]; //'1476515432' $_SESSION["transactionId"]

        $login = "loginp2p";
        $secretKey = 'secretp2p';
        $seed = date('c');
        $trankey = sha1($seed.$secretKey);
        $servicio="https://test.placetopay.com/soap/pse/v11/?wsdl"; //URL DEL SERVICIO

        $auth = array(
                'login' => $login,
                'tranKey' => $trankey,
                'seed' => $seed,
                );

        $arguments = array(
                      'auth' => $auth,
                      'transactionID'=>$id
                      );
        $client = new nusoap_client($servicio, array('trace' => true));

        $resp = $client->call('getTransactionInformation', $arguments);
        //var_dump($resp);
        foreach ($resp as $key => $valor) 
        {
                $reason = $valor["responseReasonText"];
                $reference = $valor["reference"];
                $estado  =  $valor["transactionState"];
        }
        echo 
        '<div class="card m-t-25 ">
                <div class="card-body">
                      <div class="row">
                              <div class="col-md-6">
                              <h4>Referencia :'.$reference.' </h4>

                              <h4>Estado :'.$estado.' </h4>

                              <h4>Razon :'.$reason.' </h4>
                              </div>
                      </div>
                </div>
        </div>';

        session_destroy();
        }

}
```
