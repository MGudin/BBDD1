# Resolucion


## PREGUNTAS

(?? es posible combinar condiciones en una sola seleccion)
(?? Como poner desigual? -> != o ! (=) )
(?? Elemetos repetidos de una relacion se juntan)
(??? ESTA BIEN HECHO EL RENOMBRE? 4-C)

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


### Ejercicio 4

Dados los siguientes esquemas


**CLIENTE** (id\_cliente, nombreCliente, puntaje, edad)


**AUTOMOVIL** (id\_automovil, marca, color)


**RESERVA** (id\_cliente, id_automovil, fecha)


Tener en cuenta que un cliente puede realizar diversas reservas


*a) Obtener los colores de los automóviles reservados por Juan.*

**Obtengo las reservas que hizo juan**


_AUTOS-JUAN_ **←**  **π**(idAutomovil) [ **σ**(nombreCliente='Juan') [ _RESERVA_ **|X|** _CLIENTE_ ] ]


**Obtengo los colores**


**π**(color) [ _AUTOS-JUAN_ **|X|** _AUTOMOVIL_ ]


**b) Obtener los nombres de los clientes que no han reservado un automóvil verde.**


**Obtengo los id de los autos que NO son verdes**


_AUTOS-NO-VERDE_ **←** [ **π**(idAutomovil) [ **σ**(color!='verde') _AUTOMOVIL_ ] ]


**Cruzo con la tabla de reserva para obtener las reservas de autos que no son verdes y saco los id de los clientes de dichas reservas**


_CLIENTES-NO-VERDE_ **←**  **π**(idCliente) [ _RESERVA_ **|X|** _AUTOS-NO-VERDE_ ]


**Finalmente cruzo los datos para obtener el nombre de los clientes**


**π**(nombre) [ _CLIENTE_ **|X|** _CLIENTES-NO-VERDE_ ]


*c) Obtener los nombres de los clientes que han reservado por lo menos dos automóviles.*


**Con el producto theta obtengo aquellas combinaciones con igual numero de cliente pero distinto automovil (osea clientes con mas de un auto reservado)**


_RESERVA1_ **←**  **ρ**(RESERVA) _RESERVA1_ 


_CLIENTE-2OMAS_ **←** [ **π**(RESERVA.idCliente) [ _RESERVA_ **|X|**(RESERVA.idCliente=RESERVA1.idCliente && RESERVA.idAutomovil!= RESERVA1.idAutomovil) _RESERVA1_ ] ]


**Finalmente cruzo con la tabla cliente y obtengo los nombres**


**π**(nombreCliente) [ _CLIENTE_ **|X|** _CLIENTE-2OMAS_ ]


**d) Obtener el id de aquel cliente con el puntaje más alto.**


**Similar al ejercicio anterior, hago un producto theta, pero con la condicion de que el puntaje de uno sea menor al del otro. De esta forma quedara fuera de la relacion aquel con puntaje mas alto. Pues su puntaje no sera menor que ninguno.**

_CLIENTE1_ **←**  **ρ**(CLIENTE) _CLIENTE2_ 



_CLIENTE-PUNTAJE-BAJO_ **←**  **π**(idCliente) [ _CLIENTE_ **|X|**(CLIENTE.puntaje < CLIENTE1.PUNTAJE) _CLIENTE1_ ]


**Ahora tenemos una tabla con los id de los clientes cuyo puntaje no es maximo. Con una simple resta obtenemos el id del cliente con maximo puntaje**


[ **π**(idCliente) _CLIENTE_ ] **–** _CLIENTE-PUNTAJE-BAJO_


### Ejercicio 5

Dados los siguientes esquemas

**ESTUDIANTE** ( #legajo, nombreCompleto, nacionalidad, añoDeIngreso, códigoDeCarrera )


**CARRERA** ( códigoDeCarrera, nombre )


**INSCRIPCIONAMATERIA** ( #legajo, códigoDeMateria )


**MATERIA** ( códigoDeMateria, nombre )


*a) Obtener el nombre de los estudiantes que ingresaron en 2009.*


**π**(nombreCompleto)  [ **σ**(anioDeIngreso=2009) _ESTUDIANTE_ ]


*b) Obtener el nombre de los estudiantes con nacionalidad “Argentina” que NO estén en la carrera con código “LI07”*



**π**(nombreCompleto) [ **σ**(nacionalidad='Argentina && codigoDeCarrera != 'LI07') _ESTUDIANTE_ ]



*c) Obtener el legajo de los estudiantes que se hayan anotado en TODAS las materias.*


_INSCRIPCIONAMATERIA_ **%** [ **π**(codigoDeMateria) _MATERIA_ ]


### Ejercicio 6


Dados los siguientes esquemas


**ALUMNO** (#alumno, nombre)


**CURSA** (#alumno, #curso)


**CURSO** (#curso, nombre_curso)


**PRACTICA** (#practica, #curso)


**ENTREGA** (#alumno, #practica, nota)


*a) Obtener #alumno y nombre de los alumnos que aprobaron con 7 o más todas las prácticas de los cursos que realizaron.*


### Ejercicio 7


Dados los siguientes esquemas


**PDA** (imei, marca, numeroSerie)


**JURISDICCIÓN** (idJurisdiccion, nombre)


**CONDUCTOR** (dniConductor, nombre, apellido, idJurisdiccion)


**TIPOINFRACCION** (codigo, descripcion, puntos, tipo)


**ACTAINFRACCION** (#acta, imei, fecha, dniConductor, idJurisdiccion)


**INFRACCIONACTA** (#acta, codigo)


*a) Obtener los códigos de los tipos de infracciones que no fueron utilizadas en las actas labradas de la jurisdicción “La Plata”*


**En primer lugar obtengo las actas que fueron labradas en la plata**


_INFRACCIONLP_ **←** _ACTAINFRACCION_ **|X|** [ **σ**(nombre='La Plata') _JURISDICCION_ ] 


**Ahora relacionamos las infracciones con sus codigos mediante INFRACCIONACTA y nos quedamos con dichos codigos. Tambien obtenemos todos los codigos **



_CODIGOSLP_ **←**  **π**(codigo) [ _INFRACCIONLP_ **|X|** _INFRACCIONACTA_ ]


_CODIGOS_ **←**  **π**(codigo) _INFRACCIONACTA_


**Aquellos codigos que no esten en CODIGOSLP son los buscados**


_CODIGOS_ **–** _CODIGOSLP_


*b) Obtener los #Actas en donde el conductor pertenezca a la misma jurisdicción del lugar del labrado del acta*


**Cruzamos CONDUCTOR con ACTAINFRACION para tener en la misma relacion el numero de acta junto con la jurisdiccion donde fue labrada y al jurisdiccion del conductor. Pero al hacer el producto natural tenemos el problema del campo idJurisdiccion que se llaman igual, por lo que entra dentro de la condicion de igualdad. Por esta razon primero debemos renombrar uno de los dos campos (en este caso el de conductor) para que la informacion no se pierda en la operacion**


_NUEVOCONDUCTOR_ **←**  **ρ**(dniConductor, nombre, apellido, idJurisdiccionConductor) _CONDUCTOR_


**π**(#acta)  **σ**(idJurisdiccion=idJusrisdiccionConductor) [ _ACTAINFRACCION_ **|X|** _NUEVOCONDUCTOR_ ]


*c) Obtener los imei de PDA que han labrado actas de tipo “Velocidad” sólo en la ciudad de “Mar del Plata”.*


**Como primer paso obtenemos el id de mar del plata para sacar aquellas actas de dicha jurisdiccion.  Tambien el codigo de infraccion de velocidad**




_IDVELOCIDAD_ **←**  **π**(codigo)  [ **σ**(descripcion='velocidad') _TIPOINFRACCION_ ]


_INFRACCIONMDQ_ **←**  _ACTAINFRACCION_ **|X|** [ **π**(idJurisdiccion) [**σ**(nombre='Mar del Plata') _JURISDICCION_ ] ]


**Ahora con las infracciones de mdq, cruzamos la informacion con el id de velocidad y obtenemos todas las infracciones de mdq de velocidad. De esta relacion nos quedamos con los imei**


**π**(imei) [ _INFRACCIONMQ_ **|X|** _IDVELOCIDAD_ ]


