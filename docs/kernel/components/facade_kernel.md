---
icon: material/guy-fawkes-mask
---

# Kernel Facade

El Kernel Facade es el componente que se encarga de gestionar las llamadas de los modulos
al kernel, y de gestionar las respuestas del kernel a los modulos. Basicamente es un
intermediario entre los modulos y el kernel, que se encarga de que la comunicacion entre
ambos sea correcta y lo mas sencilla posible de cara a los modulos y el usuario final.

## Funcionamiento

El funcionamiento del Kernel Facade es muy sencillo. Basicamente se encarga de gestionar
las llamadas de los modulos a los componentes del kernel y viceversa, de forma que los
modulos no tengan que preocuparse de saber como se comunican con el kernel. Para ello,
el Kernel Facade expone una serie de metodos que los modulos pueden utilizar para
comunicarse con los componentes internos, ya que la principal funcion del Kernel Facade es la de
abstraer a los modulos de la complejidad de la comunicacion con los componentes del kernel y 
evitar la necesidad de saber y depender de como funciona internamente el framework.

## Estructura


```mermaid
    flowchart TB
        subgraph p[" "]
            direction LR
            pa(Plugin 1) 
            pb(Plugin 2)
            pc(Plugin N)
        end
            
        subgraph f[" "]
            f1(Facade)
            subgraph sf["  "]
                sf1(Subfacade 1)
                sf2(Subfacade 2)
                sf3(Subfacade N)
            end
        end
        subgraph sc[" "]
            direction TB
            sc1(Subcomponent 1)
            sc2(Subcomponent 2)
            sc3(Subcomponent N)
        end
        
        p --> f
        f1 --> sf1
        f1 --> sf2
        f1 --> sf3
        sf1 --> sc1
        sf2 --> sc2
        sf3 --> sc3
        
```

!!! info   
    Se puede observar que el Kernel Facade esta compuesto por un conjunto de subfacade, los cuales
    se encargan de gestionar las llamadas a los componentes internos del kernel. Esta subdivision se debe
    a que el Kernel Facade es un componente muy complejo, por lo que se ha decidido dividirlo en
    subfacade para facilitar su comprension y mantenimiento.


[//]: # (todo seguir con la estructura del facade)