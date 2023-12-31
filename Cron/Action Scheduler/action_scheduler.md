# Action Scheduler - Job Queue for WordPress
[Action Scheduler](https://actionscheduler.org/) es una **Biblioteca de programación de tareas en segundo plano para WordPress**. Permite a los desarrolladores programar y ejecutar tareas en segundo plano de manera eficiente y confiable.

Action Scheduler es una cola de trabajos escalable y rastreable para procesar en segundo plano grandes conjuntos de acciones en WordPress. Está especialmente diseñado para distribuirse en complementos de WordPress.

---
### Action-scheduler y el Segundo Plano
En WordPress, las tareas en segundo plano se utilizan para ejecutar funcionalidades que requieren tiempo adicional o recursos del servidor, como enviar correos electrónicos, procesar imágenes, realizar actualizaciones de bases de datos, entre otros. Estas tareas se ejecutan en segundo plano sin afectar la experiencia del usuario en el sitio web.

Action Scheduler se relaciona con la ejecución de funcionalidades en segundo plano en WordPress porque proporciona una forma estructurada y confiable de programar y ejecutar estas tareas. Permite a los desarrolladores definir acciones que deben ejecutarse en un momento específico o en intervalos regulares. Además, Action Scheduler maneja la administración de tareas, la planificación y la ejecución en segundo plano, lo que garantiza que las tareas se realicen de manera eficiente y sin interrupciones en el rendimiento del sitio web.

+ Action Scheduler funciona activando un gancho de acción para que se ejecute en algún momento en el futuro. Cada enlace se puede programar con datos únicos, para permitir que las devoluciones de llamada realicen operaciones con esos datos. El gancho también se puede programar para que se ejecute en una o más ocasiones.

Piense en ello como una extensión a do_action()la que se le añade la capacidad de retrasar y repetir un gancho.

---
### Procesamiento en segundo plano probado en batalla
Cada mes, Action Scheduler procesa millones de pagos de suscripciones , webhooks para WooCommerce , así como correos electrónicos y otros eventos para una variedad de otros complementos.

Se ha visto en sitios activos que procesan colas de más de 50 000 trabajos y realizan operaciones que requieren un uso intensivo de recursos, como procesar pagos y crear pedidos, a un ritmo sostenido de más de 10 000 por hora sin afectar negativamente las operaciones normales del sitio.

Todo esto ocurre en infraestructura y sitios de WordPress fuera del control del autor del complemento.

Si su complemento necesita procesamiento en segundo plano, especialmente de grandes conjuntos de tareas, Action Scheduler puede ayudarlo.

---
### ¿Porque aveces se utiliza el archivo action-scheduler.php con su ruta en un plugin?
el propósito de incluir el archivo "action-scheduler.php" desde un directorio específico dentro de un plugin de WordPress está relacionado con la integración de funcionalidades adicionales en un plugin mediante una biblioteca externa. Esto suele hacerse para extender las capacidades del plugin y garantizar una mayor funcionalidad y compatibilidad.

En el contexto que proporcionaste, donde se incluye "action-scheduler.php" desde el directorio "/vendor/woocommerce/action-scheduler/", es probable que el plugin esté integrando la biblioteca "Action Scheduler" en su funcionalidad. Esta biblioteca se utiliza comúnmente en plugins de WooCommerce y otros complementos relacionados con el comercio electrónico en WordPress.

El propósito de esto puede incluir:

+ **Extensión de Funcionalidad**: La biblioteca "Action Scheduler" proporciona funcionalidades relacionadas con la programación de tareas y la ejecución de acciones en momentos específicos. Al incluir esta biblioteca, el plugin puede aprovechar estas capacidades para programar tareas, acciones o eventos en su propia lógica.

+ **Mejora de la Compatibilidad**: Al integrar una biblioteca bien mantenida y ampliamente utilizada como "Action Scheduler," el plugin puede mejorar su compatibilidad con otros plugins y temas de WordPress, especialmente si estos también hacen uso de la misma biblioteca.

+ **Mantenimiento Simplificado**: Al externalizar ciertas funcionalidades en una biblioteca, el mantenimiento y la actualización de esas funcionalidades se vuelven más sencillos. En lugar de reinventar la rueda, el plugin puede confiar en una biblioteca probada y mantenerla actualizada según sea necesario.

+ **Efectividad y Eficiencia**: Utilizar bibliotecas existentes y bien diseñadas puede ahorrar tiempo y recursos de desarrollo, ya que no es necesario crear desde cero funcionalidades que ya están disponibles en la biblioteca.

+ **Buena Práctica**: La inclusión de bibliotecas externas siguiendo las mejores prácticas es una forma sólida de desarrollar plugins de WordPress. Esto permite que los desarrolladores se enfoquen en las características específicas del plugin sin preocuparse por los detalles de implementación de funcionalidades comunes.

En resumen, incluir "action-scheduler.php" desde un directorio específico en un plugin de WordPress es una estrategia que se utiliza para aprovechar funcionalidades existentes y mejorar la funcionalidad y compatibilidad del plugin. Esto es común en el desarrollo de plugins de WordPress, especialmente en casos en los que se necesita una funcionalidad más avanzada o específica que ya está disponible en bibliotecas externas de confianza.

---
### Ejemplo sencillo
+ ejemplo sencillo de un plugin de WordPress que utiliza el Cron de WordPress para programar una tarea periódica que guarda un mensaje en un archivo de registro. Este es un ejemplo básico para ilustrar cómo funciona el Cron en WordPress.

1. Crea una carpeta para tu plugin: En el directorio wp-content/plugins/, crea una nueva carpeta para tu plugin. Por ejemplo, puedes llamarla "cron-example."

2. Crea el archivo principal del plugin: Dentro de la carpeta "cron-example," crea un archivo PHP para el plugin. Por ejemplo, "cron-example.php."

3. Agrega el código del plugin:

``` php
<?php
/**
 * Plugin Name: Cron Example
 * Description: Un plugin de ejemplo que utiliza el Cron de WordPress.
 */

// Función para ejecutar la tarea programada
function my_custom_task() {
    // Registro de un mensaje en un archivo de registro (reemplace la ruta según sea necesario)
    $log_file = dirname(__FILE__) . '/cron-log.txt';
    file_put_contents($log_file, "Tarea programada ejecutada el " . date('Y-m-d H:i:s') . "\n", FILE_APPEND);
}

// Programar la tarea cuando se active el plugin
register_activation_hook(__FILE__, function() {
    if (!wp_next_scheduled('my_custom_task')) {
        wp_schedule_event(time(), 'daily', 'my_custom_task');
    }
});

// Desprogramar la tarea cuando se desactive el plugin
register_deactivation_hook(__FILE__, function() {
    wp_clear_scheduled_hook('my_custom_task');
});

// Agregar una acción para ejecutar la tarea programada
add_action('my_custom_task', 'my_custom_task');
```
Este plugin realiza las siguientes acciones:

+ Define un nombre y descripción para el plugin.
+ Crea una función **my_custom_task** que se ejecutará cuando se active el Cron programado. En este caso, registra un mensaje con la fecha y hora en un archivo de registro.
+ Utiliza **register_activation_hook** para programar la tarea cuando se active el plugin.
+ En este ejemplo, se programa para ejecutarse diariamente.
+ Utiliza **register_deactivation_hook** para desprogramar la tarea cuando se desactive el plugin.
+ Agrega una acción para que la función **my_custom_task** se ejecute cuando se dispare el evento my_custom_task.
+ Después de crear este plugin, actívalo desde el panel de administración de WordPress. A partir de ese momento, el Cron de WordPress ejecutará la tarea programada una vez al día, registrando mensajes en el archivo "cron-log.txt" dentro del directorio del plugin.

Recuerda ajustar la frecuencia y el comportamiento de la tarea programada según tus necesidades específicas. Este es solo un ejemplo simple para demostrar el uso del Cron de WordPress en un plugin.