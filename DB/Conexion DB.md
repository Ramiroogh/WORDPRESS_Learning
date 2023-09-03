### Interactuar con la base de datos de WordPress a través de mi plugin
Es fundamental interactuar con la base de datos de WordPress de manera segura para evitar problemas de seguridad. Para realizar consultas de manera segura, debes utilizar las funciones proporcionadas por WordPress para sanitizar y escapar los datos. Aquí tienes un ejemplo de cómo hacerlo:
``` php
global $wpdb;

$nombre_usuario = "usuario123";
$contrasena = "contraseña123";

$consulta = $wpdb->prepare(
    "SELECT * FROM {$wpdb->prefix}users WHERE user_login = %s AND user_pass = %s",
    $nombre_usuario,
    $contrasena
);

$resultado = $wpdb->get_results($consulta);

if ($resultado) {
    // Hacer algo con los datos obtenidos
} else {
    // Usuario no encontrado
}
```
+ En este ejemplo, $wpdb->prepare() se encarga de sanear y escapar los valores antes de ser utilizados en la consulta SQL, lo que ayuda a prevenir ataques de inyección de SQL.