---
icon: material/chip
---

# Kernel Core

## Introduction

Core es el componente principal del kernel, ya que es el que se encarga de 
gestionar, almacenar y ejecutar ciertas partes del framework, las cuales son necesarias para
el correcto funcionamiento del mismo, como puede ser el caso del sistema de inicio.  
En este componente se almacenan todos aquellos datos que necesitan ser accedidos desde
cualquier parte del framework, tanto por subcomponentes como por modulos (a traves de estos),
en otras palabras, aquellos datos que son globales al framework y por lo tanto no pueden ser
almacenados en un componente especifico.

[//]: # (todo seguir con la estructura del core)