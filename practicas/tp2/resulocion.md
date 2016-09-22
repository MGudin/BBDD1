# Resolucion


## Notacion

· Proyección π


· Producto Theta |X|θ


· Selección σ 


· Intersección ∩ 


· Producto Cartesiano X


· Renombre ρ


· Unión U


· Diferencia o Resta –


· Producto Natural |X|


· División %


· Asignación ←


### Ejercicio 1

1. Dados los siguientes esquemas:


**DUEÑO**(id\_dueño, nombre, teléfono, dirección, dni)


**CHOFER**(id\_chofer, nombre, teléfono, dirección, fecha\_licencia\_desde, fecha\_licencia\_hasta, dni)


**AUTO**(patente, id\_dueño, id\_chofer, marca, modelo, año)


**VIAJE**(patente, hora\_desde, hora\_hasta, origen, destino, tarifa, metraje)


*a) Listar el dni, nombre y teléfono de todos los dueños que NO son choferes*



_DUENIO\_PROY_ **←**  **π** (dni, nombre, telefono) _DUEÑO_


_CHOFER\_PROY_ **←**  **π** (dni, nombre, telefono) _CHOFER_


_DUENIO\_PROY_ **–** _CHOFER\_PROY_


*b) Listar la patente y el id_chofer de todos los autos a cuyos choferes les caduca la licencia el 01/01/2017*


_CHOFER-LIC-CADUCA_ **←**  **π** (id\_chofer) [ **σ**(fecha\_licencia\_hasta=01/01/2017) _CHOFER_ ]


_CHOFER-AUTO_ **←**  **π**(patente, id\_chofer) _AUTO_


_CHOFER-AUTO_ **|X|** _CHOFER-LIC-CADUCA_


---


### Ejercicio 2

2. Dados los siguientes esquemas


**ALUMNO**(#alumno, nombre\_alumno, edad, provincia, beca)


**MATRICULA**(#alumno, #asignatura, grupo)


**ASIGNATURA** (#asignatura, nombre\_asignatura, grupo, año)


**PROFESOR** (#profesor, #asignatura, nombre_prefesor, grupo)


*a) Listar el nombre de los alumnos matriculados en todas las asignaturas de segundo año*


**Primero obtengo todas las asignaturas de 2do anio**


_2DO-ANIO_ **←**  **π**(#asignatura) [ **σ**(anio=2) _ASIGNATURA_ ]


**Obtengo aquellos numeros de alumno que estan matriculados en todas las asignatuas de 2do anio**


_#ALUMNOS-MATRICULADOS_ **←**  **π**(#alumno) [ _MATRICULA_ **%** _2D0-ANIO_ ]


**Por ultimo, teniendo todos los numeros de alumno matriculados en TODAS las materias de 2do anio, obtengo el nombre**



**π**(nombre\_alumno) [ _ALUMNO_ **|X|** _#ALUMNO-MATRICULADOS_ ]



*b) Listar el #alumno de los alumnos que no estén matriculados en BBDD*


**Obtengo la matricula de BBDD**


_#ALUMNOS-BBDD_ **←**  **π**(#alumno) [_MATRICULA_ **|X|** [**π**(#asignatura) [ **σ**(nombre\_asignatura=BBDD) _ASIGNATURA_ ]]]


**Saco el nro de alumno de ALUMNO y obtengo aquellos que NO estan en BBDD**


**π**(#alumno) _ALUMNO_  **–** _#ALUMNOS-BBDD_


---


### Ejercicio 3


3. Dados los siguientes esquemas


**TIPOMUEBLE** (id\_tipomueble,descripción)


**FABRICANTE** (id\_fabricante,nombrefabricante,cuit)


**TIPOMADERA** (id\_tipomadera,nombremadera)


**AMBIENTE** (id\_ambiente,descripcionambiente)


**MUEBLE** (id\_mueble, id\_tipomueble, id\_fabricante, id\_tipomadera, precio, dimensiones, descripcion)


**MUEBLEAMBIENTE** (id\_mueble,id_ambiente)


*a) Obtener los nombres de los fabricante que fabrican muebles en todos los tipos de Madera*

**Obtengo el los muebles segun su tipo de madera  y sus fabricantes**


_MUEBLEFABRICANTE_ **←** **π**(id\_fabricante, id\_tipomadera) _MUEBLE_


**Saco los id de los fabricantes que estan relacionados con todas las maderas**


_FABRICANTEMADERA_ **←** _MUEBLEFABRICANTE_ **%** [**π**(id\_tipomadera) _TIPOMADERA_] 


**Finalmente con los id de fabricante, obtengo los nombres**


**π**(nombrefabricante) _FABRICANTE_ **|X|** _FABRICANTEMADERA_







b) Obtener los nombres de los fabricantes que sólo fabrican muebles en Pino
c) Obtener los nombres de los fabricantes que fabrican muebles para todos los ambientes
d) Obtener los nombres de los fabricantes que sólo fabrican muebles para oficina
e) Obtener los nombres de los fabricantes que sólo fabrican muebles para baño y cocina.
f) Obtener los nombres de los fabricantes que producen muebles de cedro y roble.
g) Obtener los nombres de los fabricantes que producen muebles de melamina o MDF

