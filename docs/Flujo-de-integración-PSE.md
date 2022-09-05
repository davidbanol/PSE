# Flujo de integración PSE

A continuación se describen cada uno de los elementos y posibles situaciones que se deben tener presentes para que una transacción sea exitosa a través de su sitio mediante el medio de pago PSE.

**¿Cómo funciona la implementación?**

1. Se muestra como opción de pago PSE (Débitos a cuentas de ahorro y corriente en Colombia).

2. Una vez el usuario la selecciona, se presenta la lista de bancos y el tipo de banca a desplegar (personas o empresas). (Se debe cachear la lista de bancos localmente y su refrescamiento debe ser 1 vez por día).

3. En el momento que el cliente confirma la operación, se debe consumir el servicio para realizar la petición de la transacción.

4. Si la petición es exitosa se retorna la URL a la cual debe ser enviado el cliente para que realice la operación en el banco. En caso contrario se retorna el motivo de rechazo de la petición.

5. Almacenar los datos de la transacción retornados por el servicio (identificador de la transacción, autorización/cus, identificador sesión de Placetopay).

6. Redirigir el navegador a la URL retornada en caso de éxito.

7. Una vez la ejecución de la petición retorna a la URL especificada en el momento que se realizó la petición para crear la transacción **returnURL**, se debe preguntar a Placetopay por el estado de la transacción mediante el consumo al servicio de información.

8. Dependiendo de la respuesta del servicio, la transacción puede haber sido aprobada, rechazada o seguir pendiente de procesamiento.

9. Una vez culminado el proceso, se debe informar al usuario el estado de la transacción.

10. Si la transacción está pendiente, o si el cliente al abandonar el portal no ha regresado, se debe tener una sonda que pregunte por el estado de la transacción cada 15 minutos únicamente para transacciones con un periodo de ejecución mayor a 8 minutos.

### Despliegue de bancos disponibles

Una vez el cliente ha determinado que desea pagar con débito a una cuenta corriente o de ahorros, se deberá presentar la lista de los bancos que en el momento están disponibles para la ejecución de la transacción. Esta lista de bancos se obtiene mediante el consumo al método [getBankList](Métodos-de-interfaz-PSE.md#getBankList) el cual debe ser consumido una vez por día, lo que exige que se disponga de un mecanismo de caché que permita recuperar la lista de este si ya ha sido consumido el servicio en el día.

Adicional a darle a escoger al cliente con qué banco se va a realizar la transacción, el usuario también debe indicar qué tipo de interfaz del banco desea desplegar, es decir, si la de personas o la de empresas.

Si por algún motivo la lista de bancos no pudo ser obtenida, deberá mostrarse un mensaje “No se pudo obtener la lista de Entidades Financieras, por favor intente más tarde” y, nuevamente se consumiría el servicio de lista de bancos para intentar obtener dicha lista y almacenar el resultado en el caché.

Tenga en cuenta que en operaciones de Multicrédito se debe utilizar el código de servicio para multicrédito y que siempre deberá pasar todas las cuentas dependientes (entidad, servicio) para los créditos, así algunas de ellas vayan con valores en cero. Es requerido que la lista de créditos corresponda con todos los subcódigos dependientes.

### Confirmación y redirección al banco

Una vez se poseen los datos del pagador y/o comprador, así como la información de qué banco y qué tipo de interfaz debe mostrar el banco, se realiza entonces el consumo al servicio de [createTransaction](Métodos-de-interfaz-PSE.md#createTransaction) para obtener la URL en la cual deberá ser redirigidó el cliente y finalizar la transacción.

Debe tener en cuenta que en los datos solicitados para crear la transacción se requiere la dirección IP desde la cual el cliente está realizando la transacción, así como la información del agente de navegación usado. Si lo desea, también puede proveer datos adicionales con la transacción, los cuales le permitirán tener esta información disponible en la consola de consulta de transacciones de Placetopay.

Si la respuesta del servicio es SUCCESS, entonces deberá almacenar la información retornada en su base de datos, de vital importancia el **transactionId**, pues es con este identificador que podrá consultar el estado final de la transacción.

Tenga en cuenta que una respuesta SUCCESS en este punto sólo implica que la transacción ha sido aprovisionada por el banco y está en espera mientras que el cliente llegue a la interfaz del banco, se autentique y autorice la operación iniciada.

Al crear la transacción, esta puede fallar; algunos motivos incluyen montos por fuera del rango permitido, no disponibilidad del banco, problemas de configuración de la cuenta recaudadora, entre otros. Utilice la propiedad **responseReasonText** para obtener el mensaje de por qué falló la creación de la transacción. Algunos códigos no relacionados con el pagador pueden indicarle que genere una alerta sobre problemas con la disponibilidad del servicio, particularmente los relacionados con mala configuración.

Una vez ha almacenado la información en su base de datos y ha confirmado que es exitosa la petición, se redirigirá al cliente a la URL del banco. Tenga en cuenta que la redirección a la interfaz del banco no debe realizarse en un frame o cualquier otro mecanismo que oculte la URL en la cual el cliente ingresará sus datos de autenticación.

### Reingreso del cliente

Una vez el cliente ha finalizado la transacción en la interfaz del banco, el banco redirige al cliente a la URL especificada al crear la transacción **returnURL**, en este punto de entrada en su aplicativo, se deberá consumir el servicio [getTransactionInformation](Métodos-de-interfaz-PSE.md#getTransactionInformation) que le permitirá determinar el estado de la transacción. Solo si la transacción tiene como estado OK es porque la transacción fue autorizada, si por el contrario obtiene un estado PENDING es porque aún no se tiene respuesta final del banco en relación a la transacción.

Ya sea que el cliente retorne al punto de reingreso y que la transacción esté pendiente, o que haya abandonado la operación y se haya interrumpido el flujo normal, se deberá consumir el servicio [getTransactionInformation](Métodos-de-interfaz-PSE.md#getTransactionInformation) para todas las operaciones que en el momento que fue invocado el [createTransaction](Métodos-de-interfaz-PSE.md#createTransaction) llevan más de 15 minutos sin un estado final de operación.










