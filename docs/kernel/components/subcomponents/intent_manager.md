---
icon: fontawesome/solid/diagram-predecessor
---

# Intent Manager
 
El subcomponente `Intent Manager` corresponde a la sección del kernel que se encarga de interceptar los eventos 
relacionados con los intents de la aplicación para realizar las acciones correspondientes. La finalidad de este es
facilitar al cliente la gestión de los intents de la aplicación. Se centra en gestionar la peticion de intents, 
centralizando la gestión de los mismos.

???+ note
    Por el momento, `Intent Manager` solo soporta `Intents` para iniciar Activities de la propia aplicacion.

## Inicio de actividades 

