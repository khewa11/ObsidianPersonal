---
tags:
  - Proyecto_Personal
  - Planteamiento
date: 2026-10-06
---



>[!abstract]
>La idea es crear una solución para el problema de gestíon de inventario de barriles para la cervecería, perdida de en la trazabilidad de la cantidad de barriles y su fechas de manipulación.



### To Do List
- [ ] Levantamiento de requerimientos. --> ¿Que hay que controlar? ¿Que datos guardar? 
- [ ] Indagación en la arquitectura.
- [ ] Elección de tecnologías.
- [ ] Modelación de arquitectura
- [ ] Prototipado 1

### Requerimientos Funcionales

1. El sistema debe ser capaz de gestion minimo 3 bodegas a la vez (C1, C2, Evento)
2. Trackear todos lo barriles asociados a una sola bodega (Bodega = Atributo del barril)
3. Se debe alertar el usuario cuando un Barril está por vencer su fecha de manipulacion (Modificable por el usuario)
4. el sistema debe permitir modificar los atributos de un Barril, para ser agregado.
### Requerimientos No Funcionales

1. El sistema debe estar disponible 24/7.
2. Debe ser compatible con multiples plataformas. (Telegram com front)
3. Responder a mas de una peticion al mismo tiempo.(Cola de prioridad).
4. Facil de modificar el modelo de datos ante cambios del cliente.
5. Privado, solo los usuarios autorizados deben tener acceso a el.

### Estudio Tecnico 

- #### FrontEnd:
	- Para reducir el tiempo adaptabilidad de un usuario, se optó por eliminar dicha barrera de entrada, por lo que para un MVP demostrable usaremos un bot de Telegram, app de mensajería similar a WhatsApp que nos permite usar su API sin costo adicional para bots de pocas peticiones.
- #### BackEnd:
	- Con el fin de reducir el tiempo de desarrollo y su complejidad, se decidió que usaremos un arquitectura monolitica, evitando los microservicios, usaremos patrones de diseños que separen la logica del servidor, la comunicacion vía APIRest con el Bot. De esta forma logramos que si un futurio se debe escalar, sea mucho mas facil llegar a un microservicio.
- #### Base de Datos:
	- Dada la poca variedad de datos que se manejaran usar una base de datos relacional sería añadir una capa de complejidad innesesaria, Por lo que se optó por una base datos no relacional, basada en archivos JSON.
- ### Despliegue
	- Pendiente de analisis.

