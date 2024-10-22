---
icon: material/wrench-cog
---

# Kernel Configurator
 
The `KernelConfigurator` is a subcomponent responsible for configuring the microkernel and its components in the application.
All the configurations are done by this subcomponent. It prepares all the configurations preset in each component
and also registers all the plugins, initializes them and sets the pertinent configurations. That is the first component
initialized, and it allows to realize certain actions before and after the initialization of the microkernel.

[//]: # (todo: determinar las interfaces que debe implementar cada subcomponente y los plugins, puesto que debe de conocer)

[//]: # (todo: todas ellas ya que las configura siguiendo cierto orden de prioridad o dependencias.)

[//]: # (todo [opcional]: tal vez emplear un fichero de configuracion o algo)