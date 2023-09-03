# $wpdb
La variable $wpdb es una variable global en WordPress que representa una instancia de la clase wpdb definida en el *archivo /wp-includes/wp-db.php*. $wpdb es una parte integral del sistema de bases de datos de WordPress y se utiliza para **realizar consultas y manipular datos** en la base de datos de WordPress.

+ La variable $wpdb es específica de WordPress y no es una función o característica nativa de PHP en sí misma . WordPress utiliza esta variable para proporcionar una interfaz conveniente y segura para trabajar con la base de datos.

Como es una variable global en WordPress , puedes acceder a ella desde cualquier parte de tu código en WordPress una vez que se haya inicializado. Sin embargo, es importante tener en cuenta que la variable $wpdb solo estará disponible en un entorno de WordPress y *no se puede utilizar fuera de un proyecto de WordPress*.
## Ejemplo - Consulta
Supongamos que queremos realizar una consulta a la base de datos de WordPress para obtener los nombres de todos los usuarios registrados. Podríamos hacerlo de la siguiente manera:
``` php
// Acceder a la variable global $wpdb
global $wpdb;

// Realizar la consulta a la base de datos
$users = $wpdb->get_results("SELECT display_name FROM $wpdb->users");

// Recorrer los resultados y mostrar los nombres de los usuarios
foreach ($users as $user) {
    echo $user->display_name . "<br>";
}
```
En este ejemplo, primero accedemos a la variable global $wpdb utilizando la palabra clave global. Luego, utilizamos el método get_results() de $wpdb para ejecutar la consulta SQL y obtener los resultados.

Después, recorremos los resultados utilizando un bucle foreach y mostramos los nombres de los usuarios utilizando la propiedad display_name de cada objeto de usuario devuelto por la consulta.

+ Este es solo un ejemplo básico para ilustrar cómo se puede utilizar la variable $wpdb en WordPress para interactuar con la base de datos. En la práctica, existen muchas más operaciones y métodos disponibles en $wpdb que permiten realizar consultas más complejas y manipular los datos de la base de datos de WordPress de diferentes maneras.