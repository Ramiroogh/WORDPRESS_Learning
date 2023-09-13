# Database Mysql-phpMyAdmin wp-login.php
En WordPress, cuando un usuario se registra en un sitio, el código que crea el usuario y lo guarda en la base de datos MySQL **generalmente se encuentra en el archivo wp-login.php y es manejado por funciones y ganchos específicos de WordPress**. Este proceso implica una serie de funciones y acciones que interactúan con la base de datos para agregar un nuevo usuario. Aquí hay un resumen simplificado de cómo funciona:

+ **Formulario de Registro**: El formulario de registro en WordPress se encuentra en la página predeterminada de registro, que generalmente es *wp-login.php?action=register*. Los usuarios completan este formulario con su información, como nombre de usuario, correo electrónico y contraseña.

+ **Validación y Sanitización**: WordPress valida y sanitiza los datos ingresados por el usuario para garantizar que sean seguros y cumplan con los requisitos. Esto incluye comprobar si el correo electrónico es único y si la contraseña cumple con los criterios de seguridad configurados.

+ **Creación del Usuario**: Una vez que los datos del usuario han pasado la validación, WordPress utiliza la función wp_create_user() para crear un nuevo usuario. Esta función toma el nombre de usuario, la contraseña y la dirección de correo electrónico como argumentos y agrega al usuario a la base de datos.

+ **Acciones y Ganchos**: Durante este proceso, WordPress dispara varios ganchos (hooks) que permiten a los desarrolladores personalizar la funcionalidad de registro. Uno de los ganchos clave es user_register, que se ejecuta después de que se ha creado el usuario. Puedes usar este gancho para realizar acciones adicionales después de que se ha registrado el usuario.

+ **Inicio de Sesión Automático**: Después de registrarse, WordPress inicia automáticamente la sesión del usuario y lo redirige a la página de inicio o a una página personalizada según la configuración del sitio.

El código específico de creación de usuario se encuentra en el núcleo de WordPress y no suele ser necesario modificarlo directamente para la mayoría de los sitios web. Sin embargo, si deseas personalizar el proceso de registro o agregar campos personalizados al formulario de registro, puedes hacerlo mediante plugins o funciones personalizadas utilizando los ganchos adecuados. Por ejemplo, puedes usar el gancho registration_errors para personalizar las validaciones o user_register para realizar acciones adicionales después de que se ha registrado el usuario.