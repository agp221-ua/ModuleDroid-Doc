---
icon: material/information-outline
---

# ModuleDroid Kernel

## Introduction

> :material-information: La documentacion del kernel de ModuleDroid esta pensada para aquellos
> que desean desarrollar modulos o plugins para el framework o quieren saber mas sobre el
> funcionamiento del mismo. No es necesario conocer el funcionamiento interno del kernel
> para utilizar el framework.

ModuleDroid esta basado en un sistema de modulos y plugins, de forma que cada modulo
es independiente del resto, y puede ser añadido o eliminado del sistema en cualquier momento.
Para ello, el sistema esta compuesto por un nucleo (kernel) que se encarga de gestionar
los modulos y plugins que se ejecutan en el sistema, asi como de gestionar los eventos
que se producen en él. 

Internamente, el kernel esta compuesto a su vez por un conjunto de componentes que se encargan
de gestionar los diferentes aspectos del sistema, de forma que si un modulo necesita interactuar
con un aspecto del sistema, lo hace a traves del kernel y este se encarga de gestionar la
interaccion con el componente correspondiente.

<br/>

```mermaid
flowchart TB
    subgraph k[KERNEL]
        direction TB
        f(Facade)
        subgraph c[INTERNAL BUS]
            c1(Internal Bus)
        end
        subgraph sc[SUBCOMPONENTS]
            sc1(Current Context Manager)
            sc2(Activity Lifecycle)
            sc3(Kernel Configurator)
        end
    end
    
    subgraph p[Plugins]
        direction LR
        pa(Plugin 1) 
        pb(Plugin 2)
        pc(Plugin N)
    end
    p --> f
    
    f <-.-> sc
    c <-.-> sc
    sc ---> System

```

[//]: # (todo añadir los nuevos componentes a los subcomponentes del kernel)


## Plugins
Los plugins son modulos que se ejecutan de forma independiente al kernel, de forma que
pueden ser añadidos o eliminados de la aplicacion en cualquier momento sin afectar al resto
de modulos. 

Para ello, los plugins se comunican con el kernel a traves del componente Facade, de 
forma que el plugin se absrae de la implementacion interna del kernel y solo se comunica
con el nucleo a traves de una interfaz.

## Kernel
El kernel es el nucleo del framework, por lo que es el encargado de gestionar los modulos o plugins
que se ejecutan en el sistema, asi como de gestionar los eventos que se producen en él.
Internamente, el kernel esta compuesto a su vez por un conjunto de componentes que se encargan de
gestionar los diferentes aspectos del sistema, de forma que si un modulo necesita interactuar
con un aspecto del sistema, lo hace a traves del kernel y este se encarga de gestionar la
interaccion con el componente correspondiente.

> :material-alert: El kernel es un componente que se ejecuta en el hilo principal de la aplicacion,
> por lo que no se debe ejecutar codigo bloqueante en él.
<!-- Separador -->
> :material-information: Acceder a algun aspecto del sistema sorteando el kernel puede provocar
> comportamientos inesperados en el sistema, por lo que se recomienda no hacerlo. Si se necesita acceder a algun aspecto del sistema no implementado en el kernel, se recomienda notificar al
> equipo de desarrollo para que baraje la posibilidad de añadirlo al kernel o otorgen alguna solucion
> alternativa.

## Componentes
Como se ha comentado anteriormente, el kernel esta compuesto por un conjunto de componentes
que se encargan de gestionar y facilitar el acceso los diferentes aspectos del sistema. 

A continuación detallamos los componentes que componen el kernel:

::cards:: cols=2

- title: Facade
  content: Gestor de llamadas a los subcomponentes desde los plugins
  url: ../components/facade_kernel/
  
- title: Internal Bus
  content: Gestor de la comunicacion entre los subcomponentes del kernel
  url: ../components/internal_bus/

::/cards::

---

::cards:: cols=2

- title: Activity Lifecycle
  content: Gestor de eventos suscritos a los ciclos de vida de las activities
  url: ../components/subcomponents/activity_lifecycle/

- title: Bluetooth Manager
  content: Gestor de eventos relacionados con el bluetooth
  url: ../components/subcomponents/bluetooth_manager/

- title: Current Context Manager
  content: Gestor de eventos y recursos relacionados con el contexto actual
  url: ../components/subcomponents/current_context_manager/

- title: Device Info Manager
  content: Gestor de eventos y recursos relacionados con la informacion del dispositivo
  url: ../components/subcomponents/device_info_manager/

- title: Intent Manager
  content: Gestor de eventos relacionados con los intents
  url: ../components/subcomponents/intent_manager/

- title: Kernel Configurator
  content: Gestor de eventos relacionados con la configuracion del kernel
  url: ../components/subcomponents/kernel_configurator/

- title: Localization Manager
  content: Gestor de eventos relacionados con la localization
  url: ../components/subcomponents/localization_manager/

- title: Notification Manager
  content: Gestor de eventos relacionados con las notificaciones
  url: ../components/subcomponents/notification_manager/

- title: Permission Manager
  content: Gestor de eventos relacionados con los permisos
  url: ../components/subcomponents/permission_manager/

- title: Preferences Manager
  content: Gestor de eventos relacionados con las preferencias
  url: ../components/subcomponents/preferences_manager/

- title: Sensor Manager
  content: Gestor de eventos relacionados con los sensores
  url: ../components/subcomponents/sensor_manager/

- title: Speech Manager
  content: Gestor de eventos relacionados con el reconocimiento de voz y lectura de texto
  url: ../components/subcomponents/speech_manager/

- title: Task Scheduler
  content: Gestor de eventos relacionados con la planificacion de tareas
  url: ../components/subcomponents/task_scheduler/

- title: Theme Manager
  content: Gestor de eventos relacionados con los temas
  url: ../components/subcomponents/theme_manager/

- title: Thread Manager
  content: Gestor de eventos relacionados con los hilos
  url: ../components/subcomponents/thread_manager/

::/cards::

[//]: # (todo añadir los componentes del kernel)
