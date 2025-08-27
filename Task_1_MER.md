# Diseño de Base de Datos Personal de una Compañía

## Enunciado del Problema

Diseñe un diagrama E/R para la base de datos personal de una compañía con las siguientes consideraciones:

* La compañía tiene un conjunto de departamentos.
* Cada departamento tiene un conjunto de empleados, un conjunto de proyectos y un conjunto de oficinas.
* Cada empleado tiene una historia laboral (conjunto de puestos que ha ocupado).
* Para cada uno de estos puestos el empleado tiene una historia salarial.
* Cada oficina tiene un conjunto de teléfonos.
* La base de datos deberá almacenar la siguiente información:
    * Para cada departamento: número de departamento (único), presupuesto y número de empleado (único) del gerente del departamento.
    * Para cada empleado: número de empleado (único), número de proyecto actual, número de oficina y número telefónico; además el nombre de cada puesto que ha ocupado el empleado más la fecha y salario para cada salario distinto recibido en ese puesto.
    * Para cada proyecto: número de proyecto (único) y presupuesto.
    * Para cada oficina: número de oficina (único), área del piso y número telefónicos (únicos) de todos los teléfonos de esa oficina.

Declare cualquier suposición que haga sobre los atributos y claves primarias usadas.

---

## Resolución y Diseño

### Entidades y Atributos

#### **Entidades fuertes**

* **departamentos**
    * **dep_id**: Clave primaria (PK), identificador único para cada departamento.
    * **presupuesto**: Atributo para almacenar el presupuesto del departamento.
    * **empG_id**: Clave foránea (FK), que hace referencia al `emp_id` del empleado que es gerente de ese departamento.

* **empleados**
    * **emp_id**: Clave primaria (PK), identificador único para cada empleado.
    * **nombre**: Atributo para almacenar el nombre del empleado.
    * **proyecto_id**: Clave foránea (FK), que se relaciona con el proyecto actual del empleado.
    * **ofi_id**: Clave foránea (FK), que se relaciona con la oficina asignada al empleado.
    * **dep_id**: Clave foránea (FK), que se relaciona con el departamento al que pertenece el empleado.

* **proyecto**
    * **proyecto_id**: Clave primaria (PK), identificador único para cada proyecto.
    * **presupuesto**: Atributo para almacenar el presupuesto del proyecto.
    * **dep_id**: Clave foránea (FK), que se relaciona con el departamento responsable del proyecto.

* **oficinas**
    * **ofi_id**: Clave primaria (PK), identificador único para cada oficina.
    * **areaPiso**: Atributo para almacenar el área del piso de la oficina.
    * **dep_id**: Clave foránea (FK), que se relaciona con el departamento al que pertenece la oficina.

* **puesto**
    * **puesto_id**: Clave primaria (PK), identificador único para cada puesto.
    * **nombrePuesto**: Atributo para almacenar el nombre del puesto.

#### **Entidades dependientes**

* **Teléfono**
    * **tel_id**: Clave primaria (PK), identificador único para cada teléfono.
    * **numero**: Atributo para almacenar el número de teléfono, que es único.
    * **ofi_id**: Clave foránea (FK), que se relaciona con la oficina a la que pertenece el teléfono.

* **HistorialLaboral**
    * **histLab_id**: Clave primaria (PK), identificador único para cada entrada del historial laboral.
    * **emp_id**: Clave foránea (FK), que se relaciona con el empleado del que se registra el historial.
    * **puesto_id**: Clave foránea (FK), que se relaciona con el puesto que ha ocupado el empleado.

* **HistorialSalarial**
    * **histSal_id**: Clave primaria (PK), identificador único para cada salario.
    * **histLab_id**: Clave foránea (FK), que se relaciona con una entrada específica en el historial laboral.
    * **fecha**: Atributo para la fecha en que se recibió el salario.
    * **salario**: Atributo para el monto del salario.

---

### Relaciones entre entidades

* **Departamento - Empleado**: Un departamento tiene muchos empleados, y un empleado pertenece a un solo departamento (relación 1:N).
* **Departamento - Proyecto**: Un departamento puede tener muchos proyectos, pero un proyecto pertenece a un solo departamento (relación 1:N).
* **Departamento - Oficina**: Un departamento puede tener muchas oficinas, pero una oficina pertenece a un solo departamento (relación 1:N).
* **Oficina - Teléfono**: Una oficina puede tener muchos teléfonos, pero un teléfono pertenece a una sola oficina (relación 1:N).
* **Empleado - Historial Laboral**: Un empleado tiene un historial laboral, que consiste en múltiples registros de los puestos que ha ocupado (relación 1:N).
* **Historial Laboral - Historial Salarial**: Un registro en el historial laboral puede tener varios salarios asociados a él (relación 1:N).
* **Empleado - Proyecto (actual)**: Un empleado está asignado a un solo proyecto actual, pero un proyecto puede tener muchos empleados (relación N:1).
* **Empleado - Oficina (actual)**: Un empleado tiene asignada una sola oficina, pero una oficina puede tener muchos empleados (relación N:1).
* **Historial Laboral - Puesto**: Un registro en el historial laboral se asocia a un solo puesto, pero un puesto puede estar en múltiples registros de historial laboral (relación N:1).

---

### Diagrama E/R
Aquí puedes encontrar el diagrama E/R que acompaña esta resolución.

![Diagrama E/R del modelo de datos de la compañía](Task_1_MER_v2.png)
