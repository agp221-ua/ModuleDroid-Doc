---
icon: material/nut
---

# Current Context Manager

El subcomponente `Current Context Manager` corresponde a la seccion del kernel que se encarga de gestionar los recursos
necesarios que dependen del contexto actual de la aplicacion. La finalidad de este subcomponente es la de permitir que
los otros subcomponentes y plugins de la aplicacion puedan acceder a los recursos que dependen del contexto actual de la
aplicacion sin depender directamente de la actividad o fragmento actual.

## Obtencion del contexto actual

Para obtener el contexto actual de la aplicacion, el subcomponente `Current Context Manager` hace uso de un metodo con
visibilidad restringida que permite obtener el contexto actual de la aplicacion personalizada ya mencionada en [`Activity Lifecycle`](../activity_lifecycle).
Este sistema ofrece al subcomponente el contexto actual de manera segura, para facilitar el acceso a los recursos que
dependen de este.

???+ tip
    Igualmente, se ofrece la posibilidad de desactivar la obtencion del contexto de forma automatica y sustituirlo por un
    sistema manual, el cual permite establecer el contexto actual (a nivel de microkernel, no de aplicacion) al cliente, para
    casos mas especificos en los que se requiera un control mas preciso del contexto. Se detalla más a fondo posteriormente
    en esta pagina.




[//]: # (todo introduccion del manejador de contexto)

[//]: # (todo seguir con la estructura del manejador de contexto)
