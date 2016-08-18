# Sistema de venta de inmuebles.

Se desea diseñar una base de datos sobre la informacion de las ventas
realizadas por un sistema de inmobiliarias, el cual esta formado por
diversas inmobiliarias. De cada una de ellas, se conoce el nombre,
direccion, telefono y conjunton de empleados que trabaja para la
misma (un empleado trabaja para una unica inmobiliaria).


De los empleados de cada inmobiliaria, se registra el DNI, el nombre,
el apellido, la fecha de ingreso y la fecha de nacimiento.


De cada inmueble se conoce su direccion, cantidad de habitaciones,
tipo (casa, departamento, oficina, etc) y comodidades que brinda
(pileta. patio, lavadero, etc).


Cada inmueble se ofrece, por una inmobiliadia durante un determinado
periodo de tiempo, es decir se conoce el rango de fechas entre el cual
ese inmueble es ofrecido por la misma. El mismo inmueble puede estar
ofrecido por mas de una inmobiliaria simultaneamente, sin embargo, en
caso de concretarse la venta, solamente una de ellas la realizara. De
cada inmueble ofrecido por una inmobiliaria se conoce la forma en que
esta lo cataloga (por ejemplo: estado bueno, regular o a demoler).
Tener presente, que en caso de un ofrecimiento del inmueble por mas de
una inmobiliaria simultaneamente, cada una puede catalogarlo de una
manera diferente.


Cada vez que un inmueble se ofrece para la venta, se registran los
dueños actuales. Puede haber mas de un dueño por inmueble y los dueños
pueden ser personas fisicas o juridicas. Ademas, para cada
ofrecimiento del inmueble, los dueños pueden variar.


Cada inmobiliaria fija para cada inmueble en cada periodo, el precio
de tasacion del mismo y el tipo de moneda en el cual se va a realizar
la venta. Estos valores pueden variar para cada periodo de tiempo. 


De todas las personas se conoce un identificador que le asigna el
sistema de inmobiliarias, un nombre y un telefono. De las personas
fisicas, se registra ademas el DNI y el numero de CUIL. Mientra que de
las personas juridicas se guarda la fecha de constitucion y un numero
de CUIT.


La venta del inmueble es realizada por una inmobiliaria en particular
en un periodo de tiempo. De cada venta se debe registrar el precio
real de la venta, el/los compradores y el empleado de la inmobiliaria
que realizo la venta del mismo.

