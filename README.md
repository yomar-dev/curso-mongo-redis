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


### Enlaces de interes:

[Coin Market Cap](https://coinmarketcap.com/) <br>
[Descargar MongoDB](https://www.mongodb.com/download-center#community) <br>
[Instalar MongoDB en Windows](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/) <br>
[Instalar MongoDB en Mac](https://treehouse.github.io/installation-guides/mac/mongo-mac.html) <br>
[Guia de MongoDB](https://joaquinaraujo.github.io/mongodb-redis/) <br>