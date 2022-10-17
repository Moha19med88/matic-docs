---
id: json-rpc-commands
title: Comandos de JSON RPC
description: "Lista de comandos de JSON RPC para Polygon Edge."
keywords:
  - docs
  - polygon
  - edge
  - json
  - rpc
  - commands
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import {useState} from 'react';

export const JsonRpcTerminal = (props) => {
 const [value, setValue] = useState("");
 const { method, params, network } = props;
 return (
<div>
<div>
{value ! = "" ? <pre className="json_rpc_terminal"></pre>{value} : null}
</div>
<div>
{value == "" ? (
 <button
className="json_rpc_terminal_button"
onClick={() => {
 fetch(network, {
 method: "POST",
 headers: {
 Accept: "application/json",
 "Content-Type": "application/json",
 },
 body: JSON.stringify({
 jsonrpc: "2.0",
 method: method,
 params: params,
 id: 1,
}),
 })
 .then((res) => res.json())
 .then((response) => {
 setValue(JSON.stringify(response));
 });
 }}
 >
 Ejecutar comando
</button>
 ) : (
 <button
className="json_rpc_terminal_button"
onClick={() => {
 setValue("");
 }}
 >
 Borrar terminal
</button>
 )}
</div>
</div>
);
 };

## eth {#eth}

### eth_chainId {#eth_chainid}

Regresa la identificación de la cadena que se está configurando actualmente, un valor utilizado en una firma de transacción con protección de repetición como se introdujo en EIP-155.

---

<h4><i>Parámetros:</i></h4>

* Ninguno

<h4><i>Devoluciones:</i></h4>

* <b> QUANTITY: </b>número entero grande de la identificación de cadena actual.

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_chainId","params":[],"id":1}'
````

<JsonRpcTerminal method="eth_chainId" params=[]{} network="https://rpc.poa.psdk.io:8545"/>

### eth_syncing {#eth_syncing}

Devuelve información acerca del estado de sincronización del nodo.

---

<h4><i>Parámetros:</i></h4>

* Ninguno

<h4><i>Devoluciones:</i></h4>

*<b> Boolean (FALSE)</b>: si el nodo no se sincroniza (significa que se ha sincronizado completamente)

*<b> Object: </b>un objeto con los datos del estado de sincronización si el nodo se está sincronizando.
  * <b>startingBlock: QUANTITY </b>El bloque en el cual comenzó la importación (solo se restablecerá después de que la sincronización alcance la cabecera).
  * <b>currentBlock: QUANTITY </b>El bloque actual, igual a eth_blockNumber.
  * <b>highestBlock: QUANTITY </b>El bloque más alto calculado.

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_syncing","params":[],"id":1}'
````

<JsonRpcTerminal method="eth_syncing" params=[]{} network="https://rpc.poa.psdk.io:8545"/>

### eth_getBlockByNumber {#eth_getblockbynumber}

Devuelve la información del bloque por número.

---

<h4><i>Parámetros:</i></h4>

* <b>QUANTITY|TAG: </b>número entero de un número de bloque o la “última” cadena.
* <b> Boolean: </b> Si es verdad, devuelve los objetos de la transacción completa, si es falso, solo los hashes de las transacciones.

<h4><i>Devoluciones:</i></h4>
Object: Un objeto de bloque o nulo si no se encontró un bloque.

* <b> number: QUANTITY </b>el número de bloque.
* <b> hash: DATA, 32 Bytes </b>hash del bloque.
* <b> parentHash: DATA, 32 Bytes </b>hash del bloque parent.
* <b> nonce: DATA, 8 Bytes </b>hash de la prueba de trabajo generada.
* <b> sha3Uncles: DATA, 32 Bytes </b>SHA3 de los datos uncles en el bloque.
* <b> logsBloom: DATA, 256 Bytes </b>el filtro de bloom para los registros del bloque.
* <b> transactionsRoot: DATA, 32 Bytes </b>la raíz del trie de la transacción del bloque.
* <b>stateRoot: DATA, 32 Bytes </b>la raíz del trie de estado final del bloque.
* <b> receiptsRoot: DATA, 32 Bytes </b>la raíz del trie de recibos del bloque.
* <b> miner: DATA, 20 Bytes </b>la dirección del beneficiario que recibió las recompensas de minería.
* <b> difficulty: QUANTITY </b>número entero de la dificultad de este bloque.
* <b> totalDifficulty: QUANTITY </b>número entero de la dificultad total de la cadena hasta este bloque.
* <b> extraData: DATA </b>el campo “extra data” de este bloque.
* <b> size: QUANTITY </b>número entero del tamaño de este bloque en bytes.
* <b> gasLimit: QUANTITY </b>la cantidad de gas máxima que se permite en este bloque.
* <b> gasUsed: QUANTITY </b>el gas total utilizado para todas las transacciones de este bloque.
* <b> timestamp: QUANTITY </b>la marca de tiempo de Unix de cuando se cotejó el bloque.
* <b> transactions: Array </b>una matriz de objetos de transacciones o hashes de transacciones de 32 bytes que depende del último parámetro obtenido.
* <b> uncles: Array </b>una matriz de hashes uncle.

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest", true],"id":1}'
````

<JsonRpcTerminal method="eth_getBlockByNumber" params=[{"latest", tru]e} network="https://rpc.poa.psdk.io:8545"/>


### eth_getBlockByHash {#eth_getblockbyhash}

Devuelve información del bloque por hash.

---

<h4><i>Parámetros:</i></h4>

* <b> DATA , 32 Bytes </b>hash de un bloque.
* <b> Boolean: </b>Si es verdad, devuelve los objetos de la transacción completa, si es falso, solo los hashes de las transacciones.

<h4><i>Devoluciones:</i></h4>
<b> Object: </b>un objeto de bloque o nulo si no se encontró un bloque.

* <b> number: QUANTITY </b>el número de bloque.
* <b> hash: DATA, 32 Bytes </b>hash del bloque.
* <b> parentHash: DATA, 32 Bytes </b>hash del bloque parent.
* <b> nonce: DATA, 8 Bytes </b>hash de la prueba de trabajo generada.
* <b> sha3Uncles: DATA, 32 Bytes </b>SHA3 de los datos uncles en el bloque.
* <b> logsBloom: DATA, 256 Bytes </b>el filtro de bloom para los registros del bloque.
* <b> transactionsRoot: DATA, 32 Bytes </b>la raíz del trie de la transacción del bloque.
* <b>stateRoot: DATA, 32 Bytes </b>la raíz del trie de estado final del bloque.
* <b> receiptsRoot: DATA, 32 Bytes </b>la raíz del trie de recibos del bloque.
* <b> miner: DATA, 20 Bytes </b>la dirección del beneficiario que recibió las recompensas de minería.
* <b> difficulty: QUANTITY </b>número entero de la dificultad de este bloque.
* <b> totalDifficulty: QUANTITY </b>número entero de la dificultad total de la cadena hasta este bloque.
* <b> extraData: DATA </b>el campo “extra data” de este bloque.
* <b> size: QUANTITY </b>número entero del tamaño de este bloque en bytes.
* <b> gasLimit: QUANTITY </b>la cantidad de gas máxima que se permite en este bloque.
* <b> gasUsed: QUANTITY </b>el gas total utilizado para todas las transacciones de este bloque.
* <b> timestamp: QUANTITY </b>la marca de tiempo de Unix de cuando se cotejó el bloque.
* <b> transactions: Array </b>una matriz de objetos de transacciones o hashes de transacciones de 32 bytes que depende del último parámetro obtenido.
* <b> uncles: Array </b>una matriz de hashes uncle.

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBlockByHash","params":["0xdc0818cf78f21a8e70579cb46a43643f78291264dda342ae31049421c82d21ae",false],"id":1}'
````

### eth_blockNumber {#eth_blocknumber}

Devuelve el número del bloque más reciente.

---

<h4><i>Parámetros:</i></h4>

Ninguno

<h4><i>Devoluciones:</i></h4>

* <b> QUANTITY </b>número entero del número de bloque actual en el que está el cliente.

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'
````

<JsonRpcTerminal method="eth_blockNumber" params=[]{} network="https://rpc.poa.psdk.io:8545"/>

### eth_gasPrice {#eth_gasprice}

Devuelve el precio actual de gas en wei.
 Si se estableció un precio de gas mínimo mediante la disposición del indicador `--price-limit`,
 esta terminal devolverá el valor que define este indicador como precio de gas mínimo.

---

<h4><i>Parámetros:</i></h4>

Ninguno

<h4><i>Devoluciones:</i></h4>

* <b> QUANTITY </b>número entero del precio de gas actual en wei.

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":1}'
````

<JsonRpcTerminal method="eth_gasPrice" params=[]{} network="https://rpc.poa.psdk.io:8545"/>

### eth_getBalance {#eth_getbalance}

Devuelve el saldo de la cuenta de la dirección determinada.

---

<h4><i>Parámetros:</i></h4>

* <b> DATA, 20 Bytes </b>dirección para verificar el saldo.
* <b> QUANTITY|TAG</b>: número entero de bloque o la cadena “última”.

<h4><i>Devoluciones:</i></h4>

* <b> QUANTITY: </b>número entero del saldo actual en wei.

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1", "latest"],"id":1}'
````

### eth_sendRawTransaction {#eth_sendrawtransaction}

Crea una nueva transacción de llamada de mensaje o la creación de un contrato para las transacciones firmadas.

---

<h4><i>Parámetros:</i></h4>

* <b> DATA </b>Datos de la transacción firmada.

<h4><i>Devoluciones:</i></h4>

* <b> DATA, 32 Bytes </b>el hash de la transacción o el hash cero si la transacción todavía no está disponible.

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_sendRawTransaction","params":["0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"],"id":1}'
````

### eth_getTransactionByHash {#eth_gettransactionbyhash}

Devuelve la información acerca de una transacción solicitada por el hash de la transacción.

---

<h4><i>Parámetros:</i></h4>

* <b> DATA, 32 Bytes: </b>hash de una transacción.

<h4><i>Devoluciones:</i></h4>
<b> Object: </b>un objeto de la transacción o nulo cuando no se encontró la transacción.

* <b>  blockHash: DATA, 32 Bytes: </b>hash del bloque donde se encontraba esta transacción.
* <b>  blockNumber: QUANTITY </b>número del bloque donde se encontraba esta transacción.
* <b>  from: DATA, 20 Bytes </b>dirección del remitente.
* <b>  gas: QUANTITY </b>gas provisto por el remitente.
* <b>  gasPrice: QUANTITY </b>precio del gas provisto por el remitente en wei.
* <b>  hash: DATA, 32 Bytes </b>hash de la transacción.
* <b>  input: DATA </b>los datos enviados junto con la transacción.
* <b>  nonce: QUANTITY </b>la cantidad de transacciones realizadas por el remitente antes de esta.
* <b>  to: DATA, 20 Bytes </b>dirección del receptor, nulo cuando se trata de una transacción de creación de un contrato.
* <b>  transactionIndex: QUANTITY </b>número entero de la posición del índice de transacciones del bloque.
* <b>  value: QUANTITY </b>valor transferido en wei.
* <b>  v: QUANTITY </b>identificación de recuperación de ECDSA
* <b>  r: DATA, 32 Bytes </b>firma r de ECDSA
* <b>  s: DATA, 32 Bytes </b>firma s de ECDSA

<h4><i>Ejemplo:</i></h4>


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getTransactionByHash","params":["0x88df016429689c079f3b2f6ad39fa052532c56795b733da78a91ebe6a713944b"],"id":1}'
````

### eth_getTransactionReceipt {#eth_gettransactionreceipt}

Devuelve el recibo de una transacción por hash de transacción.

Ten en cuenta que el recibo no está disponible para las transacciones pendientes.

---

<h4><i>Parámetros:</i></h4>

* <b> DATA, 32 Bytes: </b>hash de una transacción.

<h4><i>Devoluciones:</i></h4>
<b> Object </b>un objeto de recibo de la transacción o inválido cuando no se encontró recibo.

* <b> transactionHash : DATA, 32 Bytes </b>hash de la transacción.
* <b> transactionIndex: QUANTITY </b>número entero de la posición del índice de transacciones del bloque.
* <b> blockHash: DATA, 32 Bytes:</b> hash del bloque donde se encontraba esta transacción.
* <b> blockNumber: QUANTITY </b>número del bloque donde se encontraba esta transacción.
* <b> from: DATA, 20 Bytes </b>dirección del remitente.
* <b> to: DATA, 20 Bytes </b>dirección del receptor, nulo cuando se trata de una transacción de creación de un contrato.
* <b> cumulativeGasUsed : QUANTITY</b> la cantidad total de gas utilizado cuando esta transacción se ejecutó en el bloque.
* <b> gasUsed : QUANTITY </b>la cantidad de gas utilizado por esta sola transacción específica.
* <b> contractAddress : DATA, 20 Bytes </b>la dirección del contrato creado, si la transacción fue la creación de un contrato, de lo contrario es nulo.
* <b> logs: Array </b>matriz de objetos de registro, que esta transacción generó.
* <b> logsBloom: DATA, 256 Bytes </b>filtro de bloom para que los clientes ligeros puedan recuperar rápidamente registros relacionados.

También puede devolver lo siguiente:

* <b> root  : DATA 32 bytes </b>stateroot posterior a la transacción (prebizantina)
* <b>status: QUANTITY </b>1 (éxito) o 0 (falla)

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getTransactionReceipt","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id":1}'
````

### eth_getTransactionCount {#eth_gettransactioncount}

Devuelve la cantidad de transacciones enviadas desde una dirección.

---

<h4><i>Parámetros:</i></h4>

* <b>  DATA, 20 Bytes </b>dirección.
* <b>  QUANTITY|TAG:</b> número entero de bloque o la cadena “última”.

<h4><i>Devoluciones:</i></h4>

* <b>  QUANTITY </b>número entero de la cantidad de transacciones enviadas desde esta dirección.

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getTransactionCount","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1","latest"],"id":1}'
````

### eth_getBlockTransactionCountByNumber {#eth_getblocktransactioncountbynumber}

Devuelve la cantidad de transacciones en un bloque que coincide con el número de bloque determinado.

---

<h4><i>Parámetros:</i></h4>

* <b>  QUANTITY|TAG</b>: número entero de un número de bloque o la “última” cadena.

<h4><i>Devoluciones:</i></h4>

* <b>  QUANTITY </b>número entero de la cantidad de transacciones de este bloque.

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBlockTransactionCountByNumber","params":["latest"],"id":1}'
````

<JsonRpcTerminal method="eth_getBlockTransactionCountByNumber" params=[]{} network="https://rpc.poa.psdk.io:8545"/>

### eth_getLogs {#eth_getlogs}

Devuelve una matriz de todos los registros que coinciden con un objeto de filtro determinado.

---

<h4><i>Parámetros:</i></h4>
<b> Object </b>Las opciones de filtro:

* <b> fromBlock: QUANTITY|TAG </b>(opcional, por defecto: "último") número entero de bloque o "último" para el último bloque minado.
* <b> toBlock: QUANTITY|TAG </b>(opcional, por defecto: "último") número entero de bloque o "último" para el último bloque minado.
* <b> address: DATA|Array, 20 Bytes </b>(opcional) dirección del contrato o una lista de direcciones a partir de la cual se deben originar los registros.
* <b> topics: Array of DATA </b>(opcional) matriz de temas de DATOS de 32 bytes. Los temas dependen del orden. Cada tema también puede ser una matriz de DATOS con opciones "o".
* <b> blockhash: DATA, 32 Bytes </b>(opcional, futuro) con el agregado de EIP-234, blockHash será una nueva opción de filtro que limita los registros devueltos a un solo bloque con el hash blockHash de 32 bytes. Usar blockHash es equivalente a fromBlock = toBlock = el número de bloque con hash blockHash. Si blockHash está presente en los criterios de filtro, entonces no se permite fromBlock ni toBlock.

<h4><i>Devoluciones:</i></h4>

* <b> QUANTITY</b> número entero de la cantidad de transacciones enviadas desde esta dirección.

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getLogs","params":[{"topics": ["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b"]}],"id":1}'
````


### eth_getCode {#eth_getcode}

Devuelve el código de una dirección determinada.

---

<h4><i>Parámetros:</i></h4>

* <b>  DATA, 20 Bytes </b>dirección
* <b>  QUANTITY|TAG:</b> número entero de bloque o la cadena “última”.

<h4><i>Devoluciones:</i></h4>

* <b>  DATA </b>el código de la dirección determinada.

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getCode","params":["0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b", "0x2"],"id":1}'
````

### eth_call {#eth_call}

Ejecuta una llamada de mensaje nuevo de inmediato sin crear una transacción en la cadena de bloques.

---

<h4><i>Parámetros:</i></h4>
<b> Object </b>el objeto de llamada de la transacción.

* <b>  from: DATA, 20 Bytes </b>(opcional) la dirección desde la cual se envía la transacción.
* <b>  to: DATA, 20 Bytes </b>la dirección a la cual se dirige la transacción.
* <b>  gas: QUANTITY </b>(opcional) número entero del gas provisto para la ejecución de la transacción. eth_call no consume nada de gas, pero es posible que se necesite este parámetro en algunas ejecuciones.
* <b>  gasPrice: QUANTITY </b>(opcional) número entero del gasPrice utilizado para cada gas pagado
* <b>  value: QUANTITY </b> (opcional) número entero del valor enviado con esta transacción
* <b>  data: DATA </b> (opcional) hash de la firma del método y los parámetros codificados. Si deseas conocer los detalles, consulta el contrato ABI de Ethereum en la documentación de Solidity.
* <b>  QUANTITY|TAG </b>número entero de bloque o "última" cadena, consulta los parámetros del bloque por defecto.

<h4><i>Devoluciones:</i></h4>

* <b>  DATA </b>el valor devuelto del contrato ejecutado.

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_call","params":[{see above}],"id":1}'
````

### eth_getStorageAt {#eth_getstorageat}

Devuelve el valor de una posición de almacenamiento en una dirección determinada.

---

<h4><i>Parámetros:</i></h4>

* <b>  DATA, 20 Bytes </b>dirección del almacenamiento.
* <b>  QUANTITY </b>número entero de la posición en el almacenamiento.
* <b>  QUANTITY|TAG:</b> número entero de bloque o la cadena “última”.

<h4><i>Devoluciones:</i></h4>

* <b>  DATA </b>el valor de esta posición de almacenamiento.

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getStorageAt","params":["0x295a70b2de5e3953354a6a8344e616ed314d7251", "0x0", "latest"],"id":1}'
````

### eth_estimateGas {#eth_estimategas}

Genera y devuelve un cálculo de cuánto gas se necesita para finalizar la transacción. La transacción no se agregará a la cadena de bloques. Ten en cuenta que el cálculo puede ser significativamente mayor a la cantidad de gas que se utilice realmente en la transacción por diversos motivos, entre los que se incluyen la mecánica EVM y el rendimiento de los nodos.

---

<h4><i>Parámetros:</i></h4>

Prevé que todas las propiedades sean opcionales.

<b> Object </b>el objeto de la llamada de la transacción.

* <b>  from: DATA, 20 Bytes </b>la dirección de la cual se envía la transacción.
* <b>  to: DATA, 20 Bytes </b>la dirección a la cual se dirige la transacción.
* <b>  gas: QUANTITY</b> número entero del gas provisto para la ejecución de la transacción. eth_call no consume nada de gas, pero es posible que se necesite este parámetro en algunas ejecuciones.
* <b>  gasPrice: QUANTITY </b>número entero del gasPrice utilizado por cada gas pagado.
* <b>  value: QUANTITY </b>número entero del valor enviado con esta transacción.
* <b>  data: DATA </b>hash de la firma del método y los parámetros codificados. Si deseas conocer los detalles, consulta el contrato ABI de Ethereum en la documentación de Solidity.
* <b>  QUANTITY|TAG </b>número entero de bloque o "última" cadena, consulta los parámetros del bloque por defecto.

<h4><i>Devoluciones:</i></h4>

* <b>  QUANTITY </b>la cantidad de gas utilizado.

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_estimateGas","params":[{see above}],"id":1}'
````

### eth_newFilter {#eth_newfilter}

Crea un objeto de filtro, basado en las opciones de filtro.
 Para obtener todos los registros que coincidan con el filtro específico, llama eth_getFilterLogs.
 Para comprobar si el estado cambió, llama eth_getFilterChanges.

---

<h4><i>Parámetros:</i></h4>
<b> Object </b>Las opciones de filtro:

* <b>  fromBlock: QUANTITY|TAG</b> (opcional, por defecto: "último") número entero de bloque o "último" para el último bloque minado.
* <b>  toBlock: QUANTITY|TAG </b>(opcional, por defecto: "último") número entero de bloque o "último" para el último bloque minado.
* <b>  address: DATA|Array, 20 Bytes </b>(opcional) dirección del contrato o una lista de direcciones a partir de la cual se deben originar los registros.
* <b>  topics: Array of DATA </b>(opcional) matriz de temas de DATOS de 32 bytes. Los temas dependen del orden. Cada tema también puede ser una matriz de DATOS con opciones "o".

<h4><i>Devoluciones:</i></h4>

* <b> QUANTITY </b> una identificación de filtro.

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_newFilter","params":[{"topics":["0x12341234"]}],"id":1}'
````

### eth_newBlockFilter {#eth_newblockfilter}

Crea un filtro en el nodo para recibir una notificación cuando un bloque nuevo llega.
 Para comprobar si el estado cambió, llama eth_getFilterChanges.

---

<h4><i>Parámetros:</i></h4>

Ninguno

<h4><i>Devoluciones:</i></h4>

1. QUANTITY: una identificación de filtro.

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_newBlockFilter","params":[],"id":1}'
````

<JsonRpcTerminal method="eth_newBlockFilter" params=[]{} network="https://rpc.poa.psdk.io:8545"/>

### eth_getFilterLogs {#eth_getfilterlogs}
Devuelve una matriz de todos los registros que coincidan en el filtro con la identificación determinada.

:::caution eth_getLogs vs. eth_getFilterLogs

Estos 2 métodos devolverán los mismos resultados para las mismas opciones de filtros:
1. eth_getLogs con [opciones] de params
2. eth_newFilter con [opciones] de params, devuelve un [filterId], luego llama eth_getFilterLogs con [filterId]

:::

<h4><i>Parámetros:</i></h4>

* <b>  QUANTITY</b>: la identificación de filtro.

<h4><i>Devoluciones:</i></h4>
<b> Array: </b>una matriz de objetos de registro o una matriz vacía.

* Para filtros creados con registros eth_newFilter existen objetos con los siguientes params:
    * <b> removed: TAG </b> verdadero cuando el registro se eliminó debido a una reorganización de la cadena; falso si es un registro válido.
    * <b> logIndex: QUANTITY </b>número entero de la posición de índice del registro en el bloque, es nulo cuando existe un registro pendiente.
    * <b> transactionIndex: QUANTITY </b>número entero del registro del cual se creó la posición del índice de las transacciones; es nulo cuando existe un registro pendiente.
    * <b> transactionHash: DATA, 32 Bytes </b>hash de las transacciones de las cuales se creó este registro; es nulo cuando existe un registro pendiente.
    * <b> blockHash: DATA, 32 Bytes </b>hash del bloque donde se encontraba este registro; nulo cuando existe un registro pendiente.
    * <b> blockNumber: QUANTITY </b>el número de bloque donde se encontraba este registro; nulo cuando existe un registro pendiente.
    * <b> address: DATA, 20 Bytes </b>dirección desde la cual se originó este registro.
    * <b> data: DATA </b>contiene uno o más argumentos no indexados de 32 Bytes del registro.
    * <b> topics: Array of DATA </b>matriz de 0 a 4 DATOS de 32 Bytes de argumentos del registro indexado. (En Solidity: el primer tema es el hash de la firma del evento (p. ej., Deposit(address,bytes32,uint256)), excepto que hayas declarado el evento con el especificador anónimo.)

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getFilterLogs","params":["0x16"],"id":1}'
````


### eth_getFilterChanges {#eth_getfilterchanges}

Método de sondeo para un filtro, que devuelve una matriz de registros que se produjeron desde el último sondeo.

---

<h4><i>Parámetros:</i></h4>

* <b>  QUANTITY</b>: la identificación de filtro.

<h4><i>Devoluciones:</i></h4>
<b> Array: </b>una matriz de objetos de registro o una matriz vacía si nada cambió desde el último sondeo.

* Para filtros creados con eth_newBlockFilter, la devolución son hashes de bloque (DATA, 32 Bytes), p. ej. ["0x3454645634534..."].
* Para filtros creados con registros eth_newFilter existen objetos con los siguientes params:
    * <b> removed: TAG </b> verdadero cuando el registro se eliminó debido a una reorganización de la cadena; falso si es un registro válido.
    * <b> logIndex: QUANTITY </b>número entero de la posición de índice del registro en el bloque, es nulo cuando existe un registro pendiente.
    * <b> transactionIndex: QUANTITY </b>número entero del registro del cual se creó la posición del índice de las transacciones; es nulo cuando existe un registro pendiente.
    * <b> transactionHash: DATA, 32 Bytes </b>hash de las transacciones de las cuales se creó este registro; es nulo cuando existe un registro pendiente.
    * <b> blockHash: DATA, 32 Bytes </b>hash del bloque donde se encontraba este registro; nulo cuando existe un registro pendiente.
    * <b> blockNumber: QUANTITY </b>el número de bloque donde se encontraba este registro; nulo cuando existe un registro pendiente.
    * <b> address: DATA, 20 Bytes </b>dirección desde la cual se originó este registro.
    * <b> data: DATA </b>contiene uno o más argumentos no indexados de 32 Bytes del registro.
    * <b> topics: Array of DATA </b>matriz de 0 a 4 DATOS de 32 Bytes de argumentos del registro indexado. (En Solidity: el primer tema es el hash de la firma del evento (p. ej., Deposit(address,bytes32,uint256)), excepto que hayas declarado el evento con el especificador anónimo.)

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getFilterChanges","params":["0x16"],"id":1}'
````

### eth_uninstallFilter {#eth_uninstallfilter}

Desinstala un filtro con una identificación determinada; siempre se debe llamar cuando ya no se necesita inspección.
 Además, se agota el tiempo de los filtros cuando no se los solicita mediante eth_getFilterChanges por determinado tiempo.

---

<h4><i>Parámetros:</i></h4>

* <b> QUANTITY:</b> la identificación de filtro.

<h4><i>Devoluciones:</i></h4>

* <b> Boolean: </b>es verdadero si el filtro se desinstaló correctamente, de lo contrario es falso.

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_uninstallFilter","params":["0xb"],"id":1}'
````

### eth_unsubscribe {#eth_unsubscribe}

Las suscripciones se cancelan con una llamada RPC regular con eth_unsubscribe como método y la identificación de suscripción como primer parámetro. Devuelve un bool que indica si la suscripción se canceló correctamente.

---

<h4><i>Parámetros:</i></h4>

* <b> SUBSCRIPTION ID </b>

<h4><i>Devoluciones:</i></h4>

* <b>UNSUBSCRIBED FLAG:</b> verdadero si la suscripción se canceló correctamente.

<h4><i>Ejemplo:</i></h4>

````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_unsubscribe","params":["0x9cef478923ff08bf67fde6c64013158d"],"id":1}'
````

## net {#net}

### net_version {#net_version}

Devuelve la identificación de red actual.

---

<h4><i>Parámetros:</i></h4>

Ninguno

<h4><i>Devoluciones:</i></h4>

* <b> String: </b>la identificación de la red actual.

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_version","params":[],"id":83}'
````

<JsonRpcTerminal method="net_version" params=[]{} network="https://rpc.poa.psdk.io:8545"/>

### net_listening {#net_listening}

Devuelve “verdadero” si un cliente está escuchando activamente las conexiones de red.

---

<h4><i>Parámetros:</i></h4>

Ninguno

<h4><i>Devoluciones:</i></h4>

* <b> Boolean: </b>verdadero si está escuchando, de lo contrario es falso.

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":83}'
````

<JsonRpcTerminal method="net_listening" params=[]{} network="https://rpc.poa.psdk.io:8545"/>

### net_peerCount {#net_peercount}

Devuelve la cantidad de pares actualmente conectados al cliente.

---

<h4><i>Parámetros:</i></h4>

Ninguno

<h4><i>Devoluciones:</i></h4>

* <b> QUANTITY: </b>número entero de la cantidad de pares conectados.

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}'
````

<JsonRpcTerminal method="net_peerCount" params=[]{} network="https://rpc.poa.psdk.io:8545"/>

## web3 {#web3}

### web3_clientVersion {#web3_clientversion}

Devuelve la versión actual del cliente.

---

<h4><i>Parámetros:</i></h4>

Ninguno

<h4><i>Devoluciones:</i></h4>

* <b>  String: </b>la versión actual del cliente.

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":1}'
````

<JsonRpcTerminal method="web3_clientVersion" params=[]{} network="https://rpc.poa.psdk.io:8545"/>

### web3_sha3 {#web3_sha3}

Devuelve Keccak-256 (no SHA3-256 estandarizado) de los datos determinados.

---

<h4><i>Parámetros:</i></h4>

* <b> DATA: </b>los datos para convertir en un hash SHA3

<h4><i>Devoluciones:</i></h4>

* <b>DATA:</b> el resultado SHA3 de una cadena determinada.

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"web3_sha3","params":["0x68656c6c6f20776f726c64"],"id":1}'
````

<JsonRpcTerminal method="web3_sha3" params=[{"0x68656c6c6f20776f726c64]"} network="https://rpc.poa.psdk.io:8545"/>

## TxPool {#txpool}

### txpool_content {#txpool_content}

Devuelve una lista con los detalles exactos de todas las transacciones actualmente pendientes para que se incluyan en el/los siguiente/s bloque/s, como también las que se están programado para la ejecución futura solamente.

---

<h4><i>Parámetros:</i></h4>

Ninguno


<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"txpool_content","params":[],"id":1}'
````

<JsonRpcTerminal method="txpool_content" params=[]{} network="https://rpc.poa.psdk.io:8545"/>

### txpool_inspect {#txpool_inspect}

Devuelve una lista con un resumen textual de todas las transacciones actualmente pendientes para la inclusión en el/los siguiente/s bloque/s, como también las que se están programando para la ejecución futura solamente. Este es un método específicamente diseñado para los desarrolladores para que puedan ver rápidamente las transacciones en el grupo y que detecten cualquier posible problema.

---

<h4><i>Parámetros:</i></h4>

Ninguno


<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"txpool_inspect","params":[],"id":1}'
````

<JsonRpcTerminal method="txpool_inspect" params=[]{} network="https://rpc.poa.psdk.io:8545"/>

### txpool_status {#txpool_status}

Devuelve la cantidad de transacciones actualmente pendientes para la inclusión en el/los siguiente/s bloque/s, como también las que se están programando para la ejecución futura solamente.

---

<h4><i>Parámetros:</i></h4>

Ninguno

<h4><i>Ejemplo:</i></h4>

Ejecuta el comando y observa los resultados en directo desde nuestra red de prueba.


````bash
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"txpool_status","params":[],"id":1}'
````

<JsonRpcTerminal method="txpool_status" params=[]{} network="https://rpc.poa.psdk.io:8545"/>