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

1- Dados los siguientes esquemas:


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



2) Dados los siguientes esquemas


**ALUMNO**(#alumno, nombre\_alumno, edad, provincia, beca)


**MATRICULA**(#alumno, #asignatura, grupo)


**ASIGNATURA** (#asignatura, nombre\_asignatura, grupo, año)


**PROFESOR** (#profesor, #asignatura, nombre_prefesor, grupo)


*a) Listar el nombre de los alumnos matriculados en todas las asignaturas de segundo año*


*Primero obtengo todas las asignaturas de 2do anio*


_2DO-ANIO_ **←**  **π**(#asignatura) [ **σ**(anio=2) _ASIGNATURA_ ]


*Obtengo aquellos numeros de alumno que estan matriculados en todas las asignatuas de 2do anio*


_#ALUMNOS-MATRICULADOS_ **←**  **π**(#alumno) [ _MATRICULA_ **%** _2D0-ANIO_ ]


*Por ultimo, teniendo todos los numeros de alumno matriculados en TODAS las materias de 2do anio, obtengo el nombre*



**π**(nombre\_alumno) [ _ALUMNO_ **|X|** _#ALUMNO-MATRICULADOS_ ]



b) Listar el #alumno de los alumnos que no estén matriculados en BBDD
