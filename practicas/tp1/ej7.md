# Operativos Viales
Un operativo vial se realiza en una jurisdicción determinada con un
grupo de agentes. Estos agentes utilizan dispositivos móviles (PDA)
para labrar actas.

Los agentes detienen a los conductores de forma aleatoria y realizan
un control de documentación. En caso de constatar alguna infracción,
el agente labra un acta con una PDA tomando los siguientes datos:

- El conjunto de infracciones cometidas (por ejemplo: licencia vencida
  y seguro impago)
- El vehículo del conductor.
- El agente que realizó el acta.
- La jurisdicción del lugar del labrado del acta.
- La PDA utilizada para realizar el acta.
- En caso de ser necesario, un testigo.
- Foto y firma del infractor.

El número de acta es generado por la
PDA y es único, de la PDA se conoce: el imei (valor único de
identificación), número de serie, marca y modelo.

De las infracciones se conoce el código de infracción (que es único),
artículo, descripción, UF (Las Unidades Fijas son valores numéricos
que equivalen al menor precio de venta al público de un litro de nafta
especial) y puntos a descontar (scoring). No todas las infracciones
asociadas al acta deben aplicar el scoring para descontar puntos en la
licencia, para esto se debe registrar qué infracciones asociadas al
acta aplican scoring y cuáles no.

Además, se debe asociar al acta el precio actual del litro de nafta
especial, que junto a las UFs de cada infracción se utilizan para
calcular el monto total de la misma. Este monto se debe registrar.

Del vehículo se registra el dominio (patente), marca, modelo, tipo de
vehículo, año de patentamiento y su conductor (si bien el vehículo
puede tener más de un propietario, solo se registra el que conduce el
vehículo).

El conductor posee una única licencia y al igual que el agente los
datos que se registran son: nombre, apellido, dirección, sexo, número
de documento, tipo de documento y la jurisdicción a la que pertenecen.

Para el agente se registra además el cargo y el número de legajo.

De la licencia se desea registrar: el número, la/s clase/es de
licencia, fecha de vencimiento, grupo/factor sanguíneo.  El testigo es
una persona que no puede ser ni el agente ni el conductor. Del testigo
se conoce el dni, nombre, apellido, domicilio y teléfono.
