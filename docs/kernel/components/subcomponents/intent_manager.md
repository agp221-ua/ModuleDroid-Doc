---
icon: fontawesome/solid/diagram-predecessor
---

# Intent Manager

El subcomponente `Intent Manager` corresponde a la sección del kernel que se encarga de interceptar los eventos 
relacionados con los intents de la aplicación para realizar las acciones correspondientes. La finalidad de este es
facilitar al cliente la gestión de los intents de la aplicación. Se centra en gestionar la peticion de intents, 
centralizando la gestión de los mismos y facilitando la peticion de intents externos del sistema, como puede ser
la apertura de la camara para realizar una foto.

## Petición de intents

El subcomponente expone una serie de métodos que permiten realizar peticiones de intents de manera sencilla.


[//]: # (todo: mas ideas o tal vez ejemplos de uso de este subcomponente)