---
icon: material/sync
---

# Activity Lifecycle

El subcomponente `Activity Lifecycle` corresponde a la seccion del kernel que se encarga de interceptar los eventos del
ciclo de vida de las actividades de la aplicacion para realizar las acciones correspondientes. La finalidad de este es
la de permitir que los otros subcomponentes y plugins de la aplicacion puedan reaccionar a los eventos del ciclo de vida
de las activities para realizar diversas acciones.

???+ example "Ejemplo"
    Pongamos como ejemplo el caso de un plugin que se encarga de la navegacion entre pantallas de la aplicacion. 
    Este plugin necesita saber cuando se crea una nueva activity para poder pasar los datos pertinentes a la nueva
    pantalla. Para ello podría suscribirse al evento `onCreate` del ciclo de vida de las activities y realizar las
    acciones correspondientes cuando este evento se produzca.

???+ info
    Por el momento, el subcomponente `Activity Lifecycle` no es capaz de interceptar los eventos del ciclo de vida de
    fragmentos de manera oficial.

## Suscripcion a eventos

Como ya se ha comentado, el subcomponente `Activity Lifecycle` hace uso de un sistema de suscripcion a los eventos del
ciclo de vida de las activities. Para ello, `Activity Lifecycle` expone una serie de metodos que permiten suscribirse a
los eventos del ciclo de vida de las activities.

Para conseguir esto, el subcomponente `Activity Lifecycle` intercepta los eventos haciendo uso de una Application personalizada
que se encarga de registrar un `ActivityLifecycleCallbacks` en el `Application.ActivityLifecycleCallbacks` de la aplicacion.
De esta manera, cuando se produzca un evento del ciclo de vida de una activity, antes de que se ejecute el metodo
correspondiente de la activity, se ejecutaran todas las suscripciones a dicho evento que cumplan las restricciones 
pertinentes (explicadas mas abajo).

???+ warning "Alerta"
    Este componente hace uso de una `Application` personalizada. Si por algun motivo se necesita hacer uso de una
    Application propia, se debera tener en cuenta que el subcomponente `Activity Lifecycle` puede no funcionar
    correctamente. Para reducir las posibles incompatibilidades, deberá extender de la `Application` del subcomponente
    `Activity Lifecycle` y llamar al metodo `super` en el metodo `onCreate`. 

[//]: # (todo explicar con ejemplos el codigo para suscribirse)

[//]: # (tal vez dar la opcion de no especificar una activity para que por defecto tome todas las activities)
[//]: # (y si no, que tome que solo pasara con las que extiendan cierta clase y/o tengan cierta id)

## Eventos disponibles

`Activity Lifecycle` expone una serie de eventos que se corresponden con los eventos del ciclo de vida de las activities
de Android. Estos eventos son los siguientes:

### `onCreate`
### `onStart`
### `onResume`
### `onPause`
### `onStop`
### `onDestroy`
### `onRestart`
### `onActivitySaveInstanceState`





[//]: # (todo ampliar introduccion del activity lifecycle)

[//]: # (todo seguir con la estructura del activity lifecycle)