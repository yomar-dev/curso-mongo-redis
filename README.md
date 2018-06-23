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

**No tiene joins:** Porque de hecho no tiene relaciones. Con MongoDB muchas personas tratan de simular relaciones con los índices pero en ese punto Mongo pierde sentido, si estás usando una base de datos NoSQL debes evitar usar joins. <br>