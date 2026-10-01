# Supermercado La Guadaíra

## Miembros del grupo

1. López Molina, Eva
2. Cerezo Berruezo, María
3. Martiín Luna, Fernando
4. Delgado Gómez, Samuel

## 1. Introducción al problema

### 1.1 Descripción general

Supermercado La Guadaíra es un establecimiento de alimentación local. Actualmente, la gestión del inventario físico se realiza a papel y manualmente a ordenador en hojas de cálculo básicas, lo que provoca descuadres entre el stock real y el registrado, pérdida económica por productos caducados que no se detectan a tiempo y falta de agilidad en la reposición.

El objetivo del proyecto es diseñar un sistema de información centrado en la gestión del inventario que permita registrar entradas y salidas, manejar los distintos productos y facilitar la reposición y compra.

Alcance: Gestión de inventario físico, pedidos a proveedores, recepción de mercancía, ventas en caja y ajustes de mermas. No se incluye integración con tienda online.

### 1.2 Actores del sistema

- Internos (usuarios y roles):
    - Empleado: registra compras a proveedores, ventas en caja, y ajustes de inventario (mermas/caducidad).
- Externos:
    - Proveedor: suministra la mercancía (frescos, envasados, limpieza).
    - Cliente: realiza las compras en el establecimiento.

### 1.3 Localizaciones

Tienda física con mostrados y estanterías, y un pequeño almacén en el mismo local.

## 2. Glosario de términos

<img width="562" height="482" alt="image" src="https://github.com/user-attachments/assets/710c0675-f68c-4ee8-bf12-c55cdcdb2c49" />

## 3. Objetivos (Requisitos generales)

- RG1 — Control de inventario y caducidades: Como empleado, quiero mantener actualizada la cantidad disponible de cada producto y saber si son perecederos, para evitar roturas de stock y controlar las mermas.
- RG2 — Registro de operaciones: Como empleado, quiero registrar compras, ventas y ajustes, para tener la trazabilidad exacta de la mercancía.
- RG3 — Detección y gestión de alertas: Como empleado, quiero recibir listados de stock bajo, para planificar los pedidos a los proveedores.
- RG4 — Control de usuarios: Como empleado, quiero gestionar la información de todos los empleados y proveedores.

## 4. Catálogo de requisitos

### 4.1. Requisitos funcionales

#### R.F.01. Gestión de catálogo de productos

Como empleado del supermercado
quiero registrar el alta, baja y modificación de productos indicando si son perecederos y su tipo de venta (unidad o granel).
para mantener el catálogo del supermercado actualizado.

**Prueba de aceptación**
- Se comprueba que el nuevo producto queda registrado con su código de barras, nombre, precio, categoría, stock mínimo, stock actual, indicador de perecedero y tipo de venta.
- Se verifica que el sistema no permite modificar el código de barras de un producto una vez dado de alta.

#### R.F.02. Registro de compras y entradas de mercancía

Como empleado del supermercado
quiero registrar compras a proveedores, sus líneas de compra y que al confirmar el albarán el sistema sume automáticamente las unidades o kilos al stock actual
para aumentar el inventario disponible al recibir mercancía en el almacén.

**Prueba de aceptación**
- Se comprueba que al confirmar una línea de compra, el `stockActual` del producto se incrementa exactamente en la cantidad o peso recibido.
- Se verifica que la compra queda asociada a un empleado registrado y a un proveedor válido con su fecha y hora.

#### R.F.03. Paso por caja y registro de ventas

Como empleado del supermercado
quiero registrar ventas y líneas de venta introduciendo las unidades o el peso en kilos, y que al confirmar la operación el sistema descuente automáticamente dicha cantidad del stock actual
para reflejar las salidas reales de mercancía en el momento del cobro.

**Prueba de aceptación**
- Se comprueba que al confirmar la venta, el `stockActual` de cada artículo incluido en el ticket disminuye en la cantidad o peso vendido.
- Se verifica que el sistema permite introducir decimales si el producto es de tipo "Granel" y exige números enteros si es de tipo "Unidad".

#### R.F.04. Registro de mermas y ajustes de inventario

Como empleado del supermercado
quiero registrar ajustes de inventario (productos caducados, envases rotos, frescos deteriorados o descuadres de recuento) indicando el motivo y la cantidad
para descontar las pérdidas y cuadrar el inventario físico con el registrado en el sistema.

**Prueba de aceptación**
- Se comprueba que el ajuste queda registrado con su fecha, tipo de merma, motivo, empleado responsable, producto y cantidad.
- Se verifica que el `stockActual` del producto se actualiza automáticamente tras registrar la merma o el recuento.

#### R.F.05. Listado de productos con stock bajo

Como empleado del supermercado
quiero generar automáticamente un listado de productos cuya cantidad o peso actual sea menor o igual que su stock mínimo
para detectar roturas de stock y planificar a tiempo los pedidos a los proveedores locales.

**Prueba de aceptación**
- Se comprueba que el listado muestra únicamente aquellos productos donde `stockActual` es menor o igual a `stockMinimo`.
- Se verifica que al reponer un producto mediante una compra y superar el umbral mínimo, dicho producto desaparece del listado de alertas.

#### R.F.06. Consulta de ventas y compras con filtros

Como empleado del supermercado
quiero consultar el historial de ventas de cada cliente y las compras realizadas a cada proveedor filtrando por fecha o empleado
para revisar las operaciones realizadas y detectar posibles errores o irregularidades en caja.

**Prueba de aceptación**
- Se comprueba que al filtrar por un cliente concreto se listan únicamente sus tickets de compra con su fecha, hora, importe y cajero.
- Se verifica que al filtrar por un proveedor se muestran todos los albaranes de entrada asociados a dicho distribuidor.

#### R.F.07. Consulta de importe de ventas y cálculo de beneficio

Como empleado del supermercado
quiero consultar el importe total de cada venta y calcular el beneficio unitario de cada producto (diferencia entre precio de venta y coste de compra)
para llevar un control financiero preciso y analizar la rentabilidad del negocio.

**Prueba de aceptación**
- Se comprueba que el importe total de una venta coincide con la suma de `cantidad * precioUnitario` de todas sus líneas de venta.
- Se verifica que el beneficio unitario mostrado equivale a la diferencia entre el precio de venta actual y el precio unitario de compra al proveedor.
- Se debe aplicar la regla de negocio R.N.09.

#### R.F.08. Clasificación y búsqueda de productos

Como empleado del supermercado
quiero consultar cada producto filtrando por su nombre, categoría y si es perecedero o no
para saber en todo momento de qué variedad disponemos en tienda y priorizar la salida de productos frescos.

**Prueba de aceptación**
- Se comprueba que al filtrar por una categoría (ej. Lácteos, Frutería, Limpieza) solo se devuelven productos pertenecientes a ella.
- Se verifica que el filtro de productos perecederos muestra exclusivamente aquellos artículos con el atributo `esPerecedero` activo.

#### R.F.09. Generación de facturas y tickets con desglose de IVA

Como empleado del supermercado
quiero obtener el desglose final de una venta con el precio base imponible y el precio total con el IVA incluido
para entregar el ticket detallado e informar al cliente del importe total que debe abonar.

**Prueba de aceptación**
- Se comprueba que el sistema calcula y muestra por separado la base imponible, el porcentaje de IVA aplicado y el total final del ticket.
- Se verifica que los importes mostrados están redondeados correctamente a dos decimales.

#### R.F.10. Actualización de precio de productos

Como empleado del supermercado
quiero actualizar el precio de venta unitario de un producto por un nuevo valor dado
para mantener actualizados los precios del catálogo frente a variaciones del mercado.

**Prueba de aceptación**
- Se comprueba que el nuevo precio queda guardado en la ficha del producto y se aplica a las ventas posteriores sin alterar el precio histórico de ventas pasadas.
- Se debe aplicar la regla de negocio R.N.05.
- Se debe aplicar la regla de negocio R.N.09.

#### R.F.11. Gestión y control de usuarios

Como empleado del supermercado
quiero dar de alta y gestionar la información de empleados, clientes y proveedores
para mantener controlados los accesos al sistema y los actores vinculados a las operaciones de la tienda.

**Prueba de aceptación**
- Se comprueba que el usuario se registra con sus datos personales y el rol asignado correctamente.

---

#### 4.1.1. Requisitos de información

##### RG1-RI-01 — Información de artículos

Como empleado del supermercado,
quiero que el sistema almacene por producto:
- código de barras (o referencia interna)
- nombre
- precio
- categoría
- stockMínimo
- stockActual
- esPerecedero (booleano)
- tipoVenta (Unidad o Granel)
para poder identificar, clasificar y controlar el stock y la caducidad de cada artículo.

##### RG2-RI-02 — Movimientos de inventario (Mermas y ajustes)

Como empleado del supermercado,
quiero registrar cada movimiento de ajuste con:
- fecha
- tipo de movimiento (Merma por caducidad, merma por rotura, deterioro de frescos o ajuste por recuento)
- cantidad (aceptando decimales para productos al peso)
- motivo
- empleado que registra el movimiento
- producto
para tener historial de pérdidas y auditoría del inventario físico.

##### RG2-RI-03 — Ventas y líneas de venta

Como empleado del supermercado,
quiero que el sistema guarde las ventas con:
- fecha y hora
- empleado que realiza la venta
- cliente al que se le realiza la venta
y las líneas de venta con:
- producto vendido
- cantidad o peso vendido
- precio unitario
para actualizar el stock en tiempo real y vincular tickets o devoluciones.

##### RG2-RI-04 — Compras

Como empleado del supermercado,
quiero que el sistema guarde las compras con:
- fecha y hora
- empleado que realiza la recepción de la compra
- proveedor al que se le realiza la compra
y las líneas de compra con:
- producto comprado
- cantidad o peso comprado
- precio unitario de coste
para llevar el control de las entradas de mercancía y los costes de aprovisionamiento.

##### RG4-RI-05 — Usuarios

Como empleado del supermercado,
quiero que el sistema almacene información sobre cada persona vinculada a la tienda:
- nombre
- apellidos
- fecha de nacimiento
- teléfono
- email
- contraseña
- salario (en el caso de que sea un empleado)
- tipo de usuario
para controlar quién puede acceder al sistema y gestionar sus datos.

##### RG4-RI-06 — Clientes

Como empleado del supermercado,
quiero distinguir a los clientes como el tipo específico de persona que realiza compras en el establecimiento,
para poder registrar las ventas asociadas a ellos y gestionar correctamente su historial de tickets.

##### RG4-RI-07 — Empleados

Como empleado del supermercado,
quiero identificar a los empleados como las personas que realizan operaciones internas (ventas en caja, compras a proveedores y ajustes de mermas),
para controlar qué trabajador ejecuta cada acción y garantizar la trazabilidad de los movimientos.

##### RG4-RI-08 — Proveedores

Como empleado del supermercado,
quiero reconocer a los proveedores como las entidades externas que suministran productos de alimentación y limpieza,
para poder registrar las compras, asociarlas a un distribuidor concreto y mantener el control del inventario.

---

#### 4.1.2. Reglas de negocio

##### R.N.01. Incompatibilidad de roles

Una persona registrada en el sistema puede ser empleado, cliente o proveedor, pero no puede tener asignados los roles de empleado y proveedor simultáneamente para evitar conflictos de intereses.
- **Casos positivos:** Se registra un nuevo usuario con un único rol (ej. empleado) y el sistema acepta la operación.
- **Casos negativos:** Se intenta registrar un usuario asignándole a la vez los roles de proveedor y empleado, y el sistema rechaza la operación.

##### R.N.02. Salario solo si es empleado

Si una persona registrada no tiene el rol de empleado, no puede tener asignado un salario, diferenciando así entre trabajadores internos y actores externos (clientes o proveedores).
- **Casos positivos:** A un nuevo empleado se le asigna un salario mensual y el sistema lo registra correctamente.
- **Casos negativos:** Se intenta asignar un salario a un cliente o a un proveedor y el sistema impide la operación.

##### R.N.03. Caracteres de la contraseña de usuario

La contraseña establecida para cualquier usuario del sistema no puede tener una longitud superior a 10 caracteres.
- **Casos positivos:** Un usuario establece su contraseña con 8 caracteres y el sistema lo permite.
- **Casos negativos:** Un usuario intenta crear una contraseña con 11 caracteres y el sistema rechaza la operación.

##### R.N.04. Código de barras de al menos 6 caracteres e inmutable

El código de barras o referencia interna de cada producto debe tener al menos 6 caracteres y no se puede modificar una vez creado el artículo para evitar confusiones de identificación y trazabilidad.
- **Casos positivos:** El sistema acepta y fija permanentemente el código de barras de un producto compuesto por 8 caracteres en el momento de su creación.
- **Casos negativos:** Se intenta registrar un producto con un código de 5 caracteres o menos, o se intenta modificar el código de un producto ya existente, y el sistema rechaza la acción.

##### R.N.05. Precio unitario de producto mayor que 0

El precio unitario de un producto (tanto de venta al público como de compra a proveedor) debe ser estrictamente mayor que 0.
- **Casos positivos:** Se registra un producto con un precio unitario de 1.50 euros y el sistema acepta la operación.
- **Casos negativos:** Se intenta registrar un producto con un precio igual a 0 o negativo y el sistema rechaza la operación.

##### R.N.06. Cantidad en un movimiento de inventario mayor que 0

La cantidad o peso introducido al registrar una merma o ajuste de inventario debe ser estrictamente mayor que 0 para evitar movimientos vacíos o incoherentes.
- **Casos positivos:** Se registra un ajuste de merma por caducidad con una cantidad de 10 unidades (o 2.5 kilos) y el sistema permite la operación.
- **Casos negativos:** Se intenta realizar un ajuste de inventario con una cantidad igual a 0 o negativa y el sistema no lo permite.

##### R.N.07. Control de venta a granel frente a unidades y límite de cantidad

En cada línea de venta, la cantidad comprada de un mismo producto debe ser mayor que 0 y no puede superar las 100 unidades o kilos (para evitar compras masivas destinadas a reventa). Además, solo se permiten cantidades decimales si el producto tiene `tipoVenta` igual a "Granel", exigiendo valores enteros si es de tipo "Unidad".
- **Casos positivos:** El sistema valida una venta de 1.25 kilos de un producto a granel (ej. manzanas) o de 4 unidades exactas de un producto por unidad (ej. leche) habiendo stock suficiente.
- **Casos negativos:** Se intenta vender 1.5 unidades de un producto de tipo "Unidad", o se intentan vender 120 unidades de un mismo artículo, y el sistema rechaza automáticamente la operación.

##### R.N.08. Evitar salidas de productos sin stock disponible

No se permite confirmar una venta ni registrar una merma de salida si la cantidad o peso solicitado supera el `stockActual` disponible de ese producto.
- **Casos positivos:** El sistema valida una venta de 10 unidades de un producto cuyo stock actual es de 50 unidades.
- **Casos negativos:** La venta de 60 unidades de un producto se rechaza automáticamente porque excede su stock actual de 50 unidades.

##### R.N.09. Evitar pérdidas económicas

Los productos deben venderse al público a un precio unitario mayor que el precio al que se compraron al proveedor para garantizar el margen comercial y evitar pérdidas económicas.
- **Casos positivos:** Un producto se compra al proveedor por 2.00 euros la unidad y se vende en el supermercado por 2.60 euros.
- **Casos negativos:** El sistema bloquea la operación si el empleado intenta establecer un precio de venta de 1.80 euros para un producto que se ha comprado al proveedor por 2.00 euros.

##### R.N.10. Solo empleados registran operaciones internas

Las ventas, compras a proveedores y ajustes de mermas solo pueden ser registrados por un usuario que posea el rol de empleado para evitar modificaciones de actores externos en el sistema.
- **Casos positivos:** Un empleado crea una venta o registra una merma y el sistema guarda la operación correctamente.
- **Casos negativos:** Un proveedor o un cliente intenta registrar una venta o un ajuste de inventario y el sistema deniega la operación.

##### R.N.11. Ventas exclusivas a clientes

Una venta en caja solo se le puede asociar a una persona que tenga asignado el rol de cliente.
- **Casos positivos:** Un cliente realiza una compra en el supermercado y el sistema registra la venta a su nombre correctamente.
- **Casos negativos:** El sistema impide que se asigne una venta a una persona registrada únicamente con el rol de proveedor.

##### R.N.12. Contratación solo a mayores de 16 años

Ningún empleado puede ser contratado ni dado de alta como trabajador en el sistema si su edad es menor a 16 años en la fecha de registro, cumpliendo así con los requisitos legales laborales.
- **Casos positivos:** Se inserta un nuevo registro de un empleado con una edad mayor o igual a 16 años y el sistema lo registra correctamente.
- **Casos negativos:** Se intenta registrar un nuevo empleado con una edad menor a 16 años y el sistema rechaza la acción mostrando un mensaje de error.

---

### 4.2. Mapa de historias de usuario (opcional)

| Actividad (Épica) | Gestión de Catálogo (RG1) | Movimientos de Stock (RG2) | Alertas y Consultas (RG3) | Gestión de Usuarios (RG4) |
| :--- | :--- | :--- | :--- | :--- |
| **Release 1 (MVP)** | R.F.01. Gestión de catálogo<br>RG1-RI-01. Info artículos | R.F.02. Registro compras<br>R.F.03. Paso por caja (Ventas)<br>RG2-RI-03 / RG2-RI-04 | R.F.05. Listado stock bajo | R.F.11. Gestión de usuarios<br>RG4-RI-05 a RG4-RI-08 |
| **Release 2** | R.F.10. Actualizar precios<br>R.F.08. Clasificación y filtros | R.F.04. Registro de mermas<br>RG2-RI-02. Movimientos | R.F.06. Consulta y filtros<br>R.F.09. Desglose IVA tickets | R.N.F.01. Control de acceso |
| **Release 3** | | | R.F.07. Cálculo de beneficio y rentabilidad | |

---

### 4.3. Requisitos no funcionales (opcional)

**R.N.F. 01. Control de acceso y seguridad**
Como empleado del supermercado
quiero que el acceso al sistema se realice mediante usuario (email) y contraseña
para garantizar que solo los empleados con permisos puedan dar de alta productos, cobrar en caja o registrar mermas.


-- fin entregable 1 --


## 5. Modelo conceptual

### 5.1. Diagramas de clases UML

- con restricciones.

### 5.2. Escenarios de prueba

- con descripción textual y diagrama de objetos UML.

## 6. Matrices de trazabilidad

- Matriz de trazabilidad entre los elementos del modelo conceptual y los requisitos.

|       | EntidadX   | AsociaciónX  | RestricciónX  | Entidad2 ...   | 
|:------|:-----------|:-----------|:-----------|:-----------|
| RI-1  | X          | X          | X          | X          |
| RI-2  |            | X          |            | X          |
| RF-1  |            | X          |            | X          |
| RF-2  | X          |            | X          | X          |
| RN-1  |            | X          |            |            |
| RN-2  | X          | X          | X          |            |
| ...   |            |            |            |            |

-- fin entregable 2 --

## 7. Modelo relacional en 3FN

- Relaciones obtenidas al aplicar la transformación del modelo conceptual.

### 7.1.  Justificación de la estrategia de transformación de jerarquías

- si se identificaron jerarquías en el MC.


### 8. Matriz de trazabilidad MC/SQL (opcional):

- Restricciones sobre el MC / Elementos del modelo tecnológico (SQL) (Triggers, checks, etc.)
- Incluir Reglas de negocio — Constraints/Triggers en las matrices de trazabilidad para el entregable 3

|       | EntidadX   | AsociaciónX  | RestricciónX  | Entidad2 ...   | 
|:-------|:-------|:-------|:-------|:-------|
| TABLA-1 |        |        |        |        |
| TABLA-2 |        |        |        |        |
| TABLA-3 |        |        |        |        |
| TABLA-4 |        |        |        |        |
| TRIG-1 |        |        |        |        |
| TRIG-2 | X      | X      |        | X      |
| TRIG-3 |        | X      |        | X      |
| TRIG-4 |        |        | X      |        |
| CONST-1 |        |        |        |        |
| CONST-2 | X      | X      |        | X      |
| CONST-3 |        | X      |        | X      |
| CONST-4 |        |        | X      |        |

Se consideran todo tipo de constraints declarativas (aquellas definidas durante el CREATE TABLE).
-- fin entregable 3 --

## Referencias


