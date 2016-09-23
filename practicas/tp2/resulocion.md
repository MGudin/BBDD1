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


---

### Ejercicio 1

Dados los siguientes esquemas:


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

Dados los siguientes esquemas


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


Dados los siguientes esquemas


**TIPOMUEBLE** (id\_tipomueble,descripción)


**FABRICANTE** (id\_fabricante,nombrefabricante,cuit)


**TIPOMADERA** (id\_tipomadera,nombremadera)


**AMBIENTE** (id\_ambiente,descripcionambiente)


**MUEBLE** (id\_mueble, id\_tipomueble, id\_fabricante, id\_tipomadera, precio, dimensiones, descripcion)


**MUEBLEAMBIENTE** (id\_mueble,id_ambiente)


*a) Obtener los nombres de los fabricante que fabrican muebles en todos los tipos de Madera*

**Obtengo el los muebles segun su tipo de madera  y sus fabricantes**


_MUEBLEFABRICANTE_ **←**  **π** (id\_fabricante, id\_tipomadera) _MUEBLE_


**Saco los id de los fabricantes que estan relacionados con todas las maderas**


_FABRICANTEMADERA_ **←** _MUEBLEFABRICANTE_ **%** [**π**(id\_tipomadera) _TIPOMADERA_] 


**Finalmente con los id de fabricante, obtengo los nombres**


**π**(nombrefabricante) _FABRICANTE_ **|X|** _FABRICANTEMADERA_


*b) Obtener los nombres de los fabricantes que sólo fabrican muebles en Pino (mal aplicado el producto theta*


**primero obtengo el id de aquellos que fabricaron pino**


_FABRICOPINO_ **←**  **π** (id\_fabricante) [ _MUEBLEFABRICANTE_ **|X|**(TIPOMADERA.nombremadera=pino) _TIPOMADERA_ ]


**luego obtengo el id de los fabricantes sacando las de  pino**


_NOFABRICOPINO_ **←**  **π**(id\_fabricante) [ _MUEBLEFABRICANTE_ **|X|**(TIPOMADERA.nombremadera!=pino) _TIPOMADERA_ ]


**Finalmente aquellos que fabricaron pino y NO se encuentran en las de no pino fabricaron solo muebles de pino.
De alli saco el nombre mediante el id**


**π**(nombrefabricante) [ _FABRICANTE_ **|X|** [ _FABRICOPINO_ **–** _NOFABRICOPINO_ ] ]


*c) Obtener los nombres de los fabricantes que fabrican muebles para todos los ambientes*


**Obtengo el listado de muebles con id de ambiente e id de fabricante**

_FABRICANTEAMBIENTE_ **←**  **π** (id\_fabricante, id\_ambiente) [ _MUEBLE_ **|X|** _MUEBLEAMBIENTE_ ]


**Obtengo el listado de id de ambientes**


**π**(id\_ambiente) _AMBIENTE_

**Obtengo aquellos fabricantes que estan relacionados con TODOS los ambientes**

_FABRICANTEAMBIENTE_ **%** [ **π**(id\_ambiente) _AMBIENTE_ ]


*d) Obtener los nombres de los fabricantes que sólo fabrican muebles para oficina*


**Obtengo la id de aquellos fabricantes que fabricaron algun mueble para oficina**

_FABRICO-OFICINA_ **←**  **π**(id\_fabricante) [ **σ**(AMBIENTE.descripcion=oficina) [ _FABRICANTEABMIENTE_ **|X|** _AMBIENTE_ ] ]


**De manera similar obtengo aquellos que NO fabricaron muebles de oficina**

_NO-FABRICO-OFICINA_ **←**  **π**(id\_fabricante) [ **σ**(AMBIENTE.descripcion!=oficina) [ _FABRICANTEABMIENTE_ **|X|** _AMBIENTE_ ] ]


**Por ultimo... aquellos que se encuentren en el primero y no se encuentren en el segundo, habran fabricado solo muebles de oficina**


_FABRICO-OFICINA_ **–** _NO-FABRICO-OFICINA_


*e) Obtener los nombres de los fabricantes que sólo fabrican muebles para baño y cocina.*


**En forma similar al ejercicio anterior. Primero obtengo los fabricantes que manufacturaron tanto muebles de cocina como de banio**

_ID-BANIO-Y-COCINA_ **←**  **π**(id\_ambiente) [ **σ**(descripcion=banio || descripcion=cocina) _AMBIENTE_ ]


_FABRICO-BANIO-Y-COCINA_ **←** [ _FABRICANTEAMBIENTE_ **%** _ID-BANIO-Y-COCINA_ ]


**Ahora obtenemos aquellos que no fabricaron muebles de banio ni de cocina**


_ID-OTROS_ **←**  **π**(id\_ambiente) [ **σ**(descripcion!=banio && descripcion!=cocina) _AMBIENTE_ ]


_FABRICO-OTROS_ **←**  **π**(id\_fabricante) [ _FABRICANTEAMBIENTE_ **|X|** _ID-OTROS_ ]


**Finalmente, nos interesan aquellos que fabricaron muebles de banio y cocina, y no se encuentran en la relacion de haber fabricado otros muebles**


_FABRICO-BANIO-Y-COCINA_ **–** _FABRICO-OTROS_


*f) Obtener los nombres de los fabricantes que producen muebles de cedro y roble.*


**primero obtenemos los ids correspondientes a al cedro y al roble**

_ID-CEDRO-Y-ROBLE_ **←**  **π**(id\_madera) [ **σ**(nombremadera=cedro || nombremadera=roble) _TIPOMADERA_ ]


**Recordando la relacion del ej a, obtenemos aquellas tuplas que estan relacionadas con ambos ids simultaneamente. Entonces como resultado tenemos aquellos id de fabricantes que al menos construyeron un mueble de cedro y uno de roble (no necesariamente solo estos dos)**


**π**(nombrefabricante)  [ _FABRICANTE_ **|X|** [ _MUEBLEFABRICANTE_ **%** _ID-CEDRO-Y-ROBLE_ ] ]


*g) Obtener los nombres de los fabricantes que producen muebles de melamina o MDF*


**Primero obtengo los fabricantes de muebles de melamina**
**Para ello genero una tabla intermedia con toda la informacion**

_MUEBLE-EXTENDIDA_ **←** [ _MUEBLE_ **|X|** _TIPOMADERA_ ] **|X|** _FABRICANTE_


_FABRICANTE-MELAMINA_ **←**  **π**(nombrefabricante) [ **σ**(nombremadera=melamina) _MUEBLE-EXTENDIDA_ ]


_FABRICANTE-MDF_ **←**  **π**(nombrefabricante) [ **σ**(nombremadera=MDF) _MUEBLE-EXTENDIDA_ ]


**Por ultimo... agregamos las tuplas de una y otra tabla en una unica relacion**


_FABRICANTE-MELAMINA_ **U** _FABRICANTE-MDF_


