# Notas del curso de Mongo y Redis

### ¿Qué es NoSQL?

**NoSQL:** Es un conjunto de bases de datos que tienen un propósito especifico. Lo que significa que cada motor de base de datos soluciona un problema en específico. Por ejemplo: <br>

**MongoDB:** Resuelve un problema de escalabilidad. <br>
**Redis:** Nos resuelve el problema de guardar información con llave - valor. <br><br><br>


### Ventajas y desventajas de NoSQL:

#### Ventajas:

**Escalabilidad:** Es la forma en la que la base de datos se expande a la hora de almacenar información, las bases de datos NoSQL están diseñadas para escalar fácilmente de manera horizontal, generando beneficios como alta disponibilidad. <br>

**Esquemas de bases de datos flexibles:** Podrías guardar diferentes tipos de información bajo la misma tabla, diferentes registros con diferentes campos en la misma colección. <br>

**Velocidad:** Las bases de datos pueden ser muy rápidas con respecto a las bases de datos SQL, un error común es tratar de que una base de datos **NoSQL** funcione como una base de datos relacional, mientras uses el motor de bases de datos para su propósito inicial vas a obtener las mejores características del motor. <br>

#### Desventajas:

**No son transaccionales:** Las transacciones son consultas generalmente de escritura, donde si ocurre un error, se hace rollback a todo lo que se hizo en la base de datos. NoSQL no garantiza que eso suceda, es desventaja si tu aplicación requiere que la información se guarde completa y se requiere volver a estados anteriores. <br>

**No tiene joins:** Porque de hecho no tiene relaciones. Con MongoDB muchas personas tratan de simular relaciones con los índices pero en ese punto Mongo pierde sentido, si estás usando una base de datos NoSQL debes evitar usar joins. <br><br>


### Diferencias entre SQL y NoSQL:

> **SQL** es el lenguaje de programación que utilizan la mayoría de los sistemas, está basado en álgebra relacional. En una base de datos **NoSQL** no estamos obligados, incluso muchas veces el motor no implementa el lenguaje.

> Las bases de datos **NoSQL** están diseñadas para ser distribuidas desde el comienzo, las bases de datos relacionales no.

> **Sharding:** Con las bases de datos **NoSQL** puedo tener varios servidores y en cada servidor tener una parte de la base de datos, puedo distribuir la información y eso me facilita los procesos de recuperación y puedo escalar únicamente lo que necesito y no es necesario escalar todo el cluster. En las bases de datos relacionales es complejo el proceso de distribución.


### Comandos a tener en cuenta:

`mongo --help` Muestra el menú de ayuda. <br>
`show dbs` Muestra las bases de datos existentes en **MongoDB**. <br>
`use [name-db]` Permite usar una base de datos determinada. <br>
`db.<collection>.insert({JSON-Document})` Permite crear una colección (tabla en MySQL) e insertar datos en una base de datos. <br>
`show collections` Muestra las colecciones existentes. <br>
`db.createCollection('name-colletion')` Crea una colección de manera explicita. <br>
`load('name-file.js')` Permite cargar un archivo JavaScript a **MongoDB**. <br>


### Insertar Documentos:

`db.<collection>.insert({JSON-Document})` Permite agregar una o varias colecciones a una base de datos. <br>
`db.<collection>.insertOne({JSON-Document})` A diferencia del insert({JSON-Document}), este método solo inserta una colección. <br>
`db.<collection>.insertMany([{JSON-Document}, {Other-JSON-Document}, {...}])` Este método es similar a `insert({JSON-Document})`, sin embargo, este método fue incluido en la versión 3 de MongoDB por ende debe comenzar a usarse y evitar `insert({JSON-Document})` <br>

### Buscar documentos:

`db.<collection>.find()` Imprime los primeros 20 documentos que encuentre. <br>
`db.<collection>.findOne()` Imprime solo el primer documentos que encuentre. <br>


### Operaciones avanzadas con find() findOne():

`db.collection.find()` Imprime los primeros 20 documentos que encuentra. <br>
`.limit(n)` Imprime los primeros n documentos que encuentra. <br>
`.pretty()` Imprime los documentos de una forma más legible. <br>
`db.collection.find({"clave": "valor"}, {"clave": valor})` Imprime el documento que contenga la(s) clave(s) y el (o los) valor(es) especificado(s). Con `findOne({...})` se muestran los documentos de forma más legibles para la vista. <br>
`db.collection.find({"clave": {$gt: "valor"}})` Imprime los documentos mayores al valor de alguna clave en un documento. <br>
**$gt** Significa mayor que (>). <br>
**$lt** Significa menor que (<). <br>
**$gte** Significa mayor o igual a (>=). <br>
**$lte** Significa menor o igual a (<=). <br>


### Modificación de Documentos:

`db.<collection>.save({JSON-Document)}` Modifica un campo si se encuentra en una colección, si no se agrega. <br>
`db.<collection>.update({JSON-Document)}` Actualiza el documento por completo, es decir, elimina todos los campos y agrega los nuevos dejando así solo el **_id**. <br>
`db.<collection>.updateOne({filtro}, {"clave": "valor"})` Se actualizará el primer documento que coincida con el filtro. <br>
`db.<collection>.updateMany({filtro}, {"clave": "valor"})` Se actualizará todos los documentos que coincida con el filtro. <br>

### Eliminar Documentos:

`db.<collection>.deleteOne({"filter")}` Elimina el primer documento encontrado según el filtro. <br>
`db.<collection>.deleteMany({"filter")}` Elimina todos los documentos encontrados según el filtro. <br>
`db.<collection>.remove({"filter")}` Elimina un campo según el filtro, es decir, si coincide uno o muchos documentos con el filtro serán eliminados de la base de datos. <br>
`db.<collection>.drop()` Elimina todos los documentos de una colección. <br>


### Instalar Redis en Mac:

1 - `brew update`
2 - `brew install redis`

**Ejecutar el servidor de Redis:** `redis-server`

> **Nota:** El puerto por defecto de Redis es *6379*.


### Insertar y leer datos en Redis:

Para insertar un primer valor en Redis se debe usar `SET` con dos parámetros, el primero la clave y el segundo el valor, ejemplo: <br>
`SET clave valor` <br><br>

Para información se bebe usar `GET` pasándo un parámetro que sería la clave, ejemplo: <br>
`GET clave` <br><br>


### Eliminar registros en Redis:

Para eliminar registro en Redis hay que utilizar el comando `DEL`, este comando recibe uno o más parámetros de tipo llave, puedo borrar N cantidad de claves al tiempo con el siguiente comando. <br>
`DEL clave` <br> <br>


### Limitación de Redis:

`DEL` no permite eliminar en lote, la solución para eliminar en lote desde la consola de **Redis** es utilizando **EVAL**. <br>

`EVAL "return redis.call('del', unpack(redis.call('keys', ARGV[1])))" 0 pattern*` <br>

Lo importante de ese snippet de código es la última parte `pattern*` ahí indicamos que todas las llaves que comiencen con
**pattern** serán eliminadas. <br>

Ese código es muy útil para eliminar por ejemplo cache de todos los usuarios si tienes un patrón como `cache:user:<user_id>`, si deseas eliminar todos los registros debes ejecutar el código de arriba con `cache:user:*` al final.


### SetEx, cómo guardar un registro que tenga una fecha de vencimiento:

**SETEX:** En Redis se puede guardar información con un tiempo de vencimiento, esto es útil cuando se crea una aplicación que necesite guardar información y modificarla o crearla luego de cierta cantidad de minutos. <br>

Por ejemplo, una aplicación del tiempo podría guardar el histórico en base de datos del tiempo de una ciudad y guardar el tiempo actual en una llave de Redis, el clima por lo general no cambia tan rápido en segundos por lo tanto esa llave con el tiempo actual podría tener un tiempo de vencimiento de 30 minutos, luego de 30 minutos no existirá y en ese momento se puede crear de nuevo otra llave con el mismo nombre que guarde el nuevo estado del clima. <br>

Para realizar esta funcionalidad Redis provee una función llamada **SETEX** la cual es muy similar a la función **SET** para guardar una llave con su valor. <br>

Aplicando la función **SETEX** en el ejemplo del clima, supongamos que la temperatura en centígrados para la ciudad de México es de 18°, podemos guardar esa información en una llave llamada `current-degrees-mexico-city`. <br>

Desde la consola de Redis ejecutamos: <br>
`redis> SETEX current-degrees-mexico-city 1800 "18°"`<br>

De esta manera Redis guardará una llave con el nombre de `current-degrees-mexico-city` con una duración de 1800 segundos o 30 minutos y que contendrá el valor "18°". <br>

Luego de 30 minutos la llave automáticamente se eliminará. Es recomendable que al leer la llave desde cualquier lenguaje de programación se verifique que contenga un valor ya que Redis no genera un error si la llave no existe solo devuelve un valor vacío. <br><br><br>


### Cómo eliminar una BD o todas las BD:

Al usar Redis muchas veces se necesita limpiar toda la base de datos sobre todo si le indicamos a Redis que guarde mucha información en memoria, para realizar esta acción tenemos dos alternativas: **FLUSHDB** y **FLUSHALL**.

**FLUSHDB:** Elimina la base de datos que se encuentra seleccionada. Por defecto Redis al iniciar la consola selecciona la base de datos número 0. Es recomendable asegurarse que se encuentra en la base de datos que desea eliminar ejecutando el comando SELECT antes de **FLUSH**. <br><br>

**FLUSHALL:** A diferencia de **FLUSHDB**, **FLUSHALL** elimina **toda la información de todas las bases de datos**, no importa en que base de datos te encuentres, al ejecutar **FLUSHALL** se elimina todo. <br>
Se recomienda evitar esta función a menos que sea dispensable la información que se encuentre registrada en la base de datos. <br><br>





### Enlaces de interes:

[Coin Market Cap](https://coinmarketcap.com/) <br>
[Descargar MongoDB](https://www.mongodb.com/download-center#community) <br>
[Instalar MongoDB en Windows](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/) <br>
[Instalar MongoDB en Mac](https://treehouse.github.io/installation-guides/mac/mongo-mac.html) <br>
[Guia de MongoDB](https://joaquinaraujo.github.io/mongodb-redis/) <br>