Comandos Multichat
==========

Servidor y Cliente de Sala de Chat en Java

Cliente -> Servidor (Automaticos)
------------------------------------
```java
/**
  * Primer mensaje enviado del cliente al servidor para identificarse. Contiene el nombre de usuario a utilizar.
  */
NICK <nombre> \n

/**
  * Envia un mensaje heartbeat al servidor para indicar que sigue ahi. Envia tambien la hora actual del cliente en milisegundos para calcular el ping.
  */
BEAT <hora en ms> \n

/**
  * Envia una peticion para recibir el listado de usuarios de la sala en la que se encuentra el usuario.
  */
LIST \n

/**
  * Envia una peticion de desconexion del usuario (se invoca automaticamente al cerrar la ventana del chat o al escribir EXIT en el chat).
  */
EXIT \n
```

Cliente -> Servidor (Basicos)
--------------------------------
```java
/**
  * Envia una peticion de informacion sobre el usuario con el nombre especificado.
  */
/WHOIS <nombre> \n

/**
  * Envia un mensaje privado a un usuario que este en la misma sala que el usuario emisor.
  */
/P <nombre> <mensaje> \n

/**
  * Envia una peticion para cambiar el nombre de usuario al indicado.
  */
/NICK <nombre> \n

/**
  * Envia una peticion para crear una nueva sala. El parametro contraseña es opcional, si no se indica ninguna contraseña cualquier usuario 
  * podra entrar a la sala, en caso de indicarse la sala requerira contraseña para poder entrar.
  */
/C <nombre sala> [contraseña] \n

/**
  * Envia una peticion para acceder a una sala existente. El parametro contraseña es opcional, si no se indica se tratara de acceder a la 
  * sala como si no tuviese contraseña.
  */
/J <nombre sala> [contraseña] \n

/**
  * Envia una peticion de listado de todas las salas disponibles en el servidor, asi como la cantidad de usuarios en cada una de ellas y 
  * si estan o no protegidas con contraseña.
  */
/LIST \n

/**
  * Genera un numero aleatorio entre el 1 y el 6 y muestra el resultado a todos los usuarios de la sala.
  */
/DADO \n
```

Cliente -> Servidor (SuperUsuario)
-------------------------------------
```java
/**
  * Envia una peticion de permisos de superusuario, indicando la contraseña para poder acceder a ellos. Los permisos de superusuario son 
  * necesarios para ejecutar todos los comandos descritos a continuacion.
  */
/SUDO <contraseña>

/**
  * Elimina una sala del servidor, moviendo a todos los usuarios que haya en ella a la sala Principal.
  */
/D <nombre sala> \n

/**
  * Expulsa a un usuario del chat desconectandolo del servidor. El usuario puede volver a acceder de nuevo.
  */
/KICK <nombre> \n

/**
  * Banea a un usuario de una sala, no pudiendo entrar hasta que el servidor sea reiniciado o se le quite el baneo al usuario. El baneo 
  * es tanto por IP como por nombre de usuario. Si se le banea de la sala principal, el usuario, no podra entrar al chat. Si se le banea 
  * de cualquier otra sala podra acceder al resto del chat, pero no a las salas donde ha sido baneado.
  */
/BAN <nombre> \n

/**
  * Quita el baneo del usuario especificado. El superusuario debe estar en la misma sala de la cual se quiere quitar el baneo al usuario.
  */
/UNBAN <nombre> \n
```

Servidor -> Cliente
----------------------
```java
/**
  * Mensaje de desconexion. Envia un error al cliente que provoca que este se desconecte. La descripcion se muestra en el cliente indicando 
  * el motivo de la desconexion.
  */
400 <descripcion> \n

/**
  * Mensaje de error. Envia un error al cliente pero no lo desconecta. Este es un mensaje informativo para el cliente cuando este realiza 
  * alguna operacion incorrecta, no permitida o desconocida.
  */
500 <descripcion> \n

/**
  * Mensaje de confirmacion. Significa que la ultima operacion realizada por el cliente se ha completado satisfactoriamente. Normalmente el 
  * cliente no hace nada al recibir este mensaje.
  */
200 OK \n

/**
  * Envia al cliente el nombre de la sala en la que se encuentra actualmente. Normalmente este mensaje es enviado cuando el usuario cambia de 
  * sala o se conecta al chat.
  */
SALA <nombre> \n

/**
  * Envia el listado de usuarios en la sala en la que se encuentra el cliente.
  */
LIST <usuario 1> <usuario 2> … <usuario n> \n
```