---
date: Enero 2023
title: Plantilla ![arc42](./images/arc42-logo.png)
---

# 

**Acerca de arc42**

arc42, La plantilla de documentación para arquitectura de sistemas y de
software.

Por Dr. Gernot Starke, Dr. Peter Hruschka y otros contribuyentes.

Revisión de la plantilla: 7.0 ES (basada en asciidoc), Enero 2017

© Reconocemos que este documento utiliza material de la plantilla de
arquitectura arc42, <https://www.arc42.org>. Creada por Dr. Peter
Hruschka y Dr. Gernot Starke.

:::: note
::: title
:::

La versión de esta plantilla contiene textos de ayuda y explicación Se
utiliza para familiarizarse con arc42 y comprender sus conceptos. Para
la documentación de su propio sistema puede utilizar la version *plain*.
::::

# Introducción y Metas {#section-introduction-and-goals}

Describe los requerimientos relevantes y las directrices que los
arquitectos de software y el equipo de desarrollo deben considerar.
Entre estas se incluyen:

-   El proyecto tiene como objetivo definir y documentar la arquitectura de un sistema ERP orientado a soportar procesos administrativos y operativos de una organización. El sistema contempla módulos de Compras, Facturación, Stock/Costos, Activos Fijos, Empleados y EIS.

-   Los requerimientos funcionales principales del ERP son:
    
    1. Registrar productos nuevos junto con su información básica
    2. Registrar proveedores con su información comercial
    3. Registrar los activos fijos de la empresa
    4. Visual de indicadores, gráficos e informes de la empresa

## Partes interesadas (Stakeholders) {#_partes_interesadas_stakeholders}

+---------------+---------------------------+
| Rol/Nombre    | Expectativas              |
+===============+===========================+
| Administrador | Gestionar usuarios,       |
| del Sistema   | roles y permisos          |
+---------------+---------------------------+
| Gestor de     | Gestionar productos,      |
| Compras       | proveedores y compras     |
+---------------+---------------------------+
| Gestor de     | Consultar y administrar   |
| Inventario    | inventario                |
+---------------+---------------------------+
| Gestor de     | Gestionar facturas y      |
| Facturas      | pagos                     |
+---------------+---------------------------+
| Gestor de     | Gestionar costos y stock  |
| Costos        |                           |
+---------------+---------------------------+
| Empleado      | Consultar y gestionar sus |
|               | labores                   |
+---------------+---------------------------+
| Ejecutivo     | Consultar información     |
|               | para supervisión y toma   |
|               | de decisiones             |
+---------------+---------------------------+
| Equipo de     | Implementar y mantener el |
| desarrollo    | sistema                   |
+---------------+---------------------------+
| Equipo de     | Definir y mantener la     |
| arquitectura  | arquitectura              |
+---------------+---------------------------+

# Restricciones de la Arquitectura {#section-architecture-constraints}

Entre las decisiones tecnológicas tomadas se mencionan (sobre los tres contenedores):

1. Aplicación Web: Se realizara con JAvaScript y React
2. Backend: Usaremos APIs monolíticas y Python, Django y NodeJS
3. Base de Datos: Se usara PostgreSQL para la almecenación de datos, registros, etc.

# Alcance y Contexto del Sistema {#section-context-and-scope}

![Diagrama de Contexto](/erp-software-architecture/docs/images/c1_contexto.png)

El diagrama de contexto representa el Sistema ERP como una caja negra y muestra los principales actores que interactúan con él, así como el Sistema Contable Externo. Cada relación representa una interacción funcional entre el actor y el ERP.

+---------------+---------------------------+
| Rol/Nombre    | Interacción               |
+===============+===========================+
| Administrador | Administra roles y        |
| del Sistema   | permisos                  |
+---------------+---------------------------+
| Gestor de     | Gestiona productos y      |
| Compras       | proveedores               |
+---------------+---------------------------+
| Gestor de     | Gestiona inventario       |
| Inventario    |                           |
+---------------+---------------------------+
| Gestor de     | Gestiona facturas y pagos |
| Facturas      |                           |
+---------------+---------------------------+
| Gestor de     | Gestiona costos y stock   |
| Costos        |                           |
+---------------+---------------------------+
| Empleado      | Consulta y gestiona sus   |
|               | labores                   |
+---------------+---------------------------+
| Ejecutivo     | Supervisa el desempeño    |
|               |                           |
+---------------+---------------------------+
| Sistema       | Recibe información        |
| Contable      | contable                  |
| Externo       |                           |
+---------------+---------------------------+

# Vista de Bloques {#section-building-block-view}

![Diagrama de Contenedores](/erp-software-architecture/docs/images/c2_contenedores.png)

El nivel C2 del modelo C4 representa la estructura interna de alto nivel del Sistema ERP. El sistema se divide en tres contenedores principales: una aplicación web para la interacción con los usuarios, una API que concentra la lógica de negocio y una base de datos PostgreSQL encargada de la persistencia de la información.

Contenedores: Existen 3 contenedores por medio de los cuales el usuario puede interacturar con el ERP los cuales son:

   1. Contenedor 1 (WEB): Es el contenedor mediante el cual el usuario puede interactuar directamente con el sistema, maneja una interfas de usuario y permite visualizar cada módulo y funcionalidad requerida.
   2. Contenedor 2 (API): Es el contenedor mediante el cual las acciones realizadas por el usuario se transmiten desde la WEB hasta la Base de Datos.
   3. ContenedorDB: Es el contenedor donde se guargarán los datos y se realizaran las consultas que serán mostradas en el contenedro WEB al usuario.

# Vista de Ejecución {#section-runtime-view}

![Diagrama de Secuancia](/erp-software-architecture/docs/images/product_sequence.png)

En el Diagrama de Secuancia podremos ver dos flujos para dos historias de usuario diferente: El primero explica el registro de un proveedor en el ERP y el otro explica una consulta de actividades según la prioridad seleccionada.

En este caso explicaremos el segundo flujo:

El diagrama de secuancia 2 explica como el usuario interactúa con la plataforma filtrando sus actividades por prioridad; al hacer esta filtración, inmediatamente el sistema envía una consulta mediante la API a la base de datos. En la base de datos se realiza la respectiva consulta con lenguaje SQL, y lo devuelve mediante la API al usuario de manera tal que él pueda ver la lista.

# Glosario {#section-glossary}

Este glosario establece las definiciones de los principales términos utilizados en el diseño y documentación de la arquitectura del Sistema ERP. Su propósito es establecer un vocabulario común entre los integrantes del equipo y evitar ambigüedades durante la definición de requisitos, modelado UML, diseño de arquitectura C4 y documentación mediante arc42.

+----------------------+-----------------------------------------------+
| Término              | Definición                                    |
+======================+===============================================+
| API                  | Interfaz mediante la cual un sistema o        |
|                      | componente permite que otros sistemas o       |
|                      | componentes soliciten operaciones o           |
|                      | intercambien información de manera definida.  |
+----------------------+-----------------------------------------------+
| Base de datos        | Sistema destinado a almacenar, organizar y    |
|                      | recuperar información de manera persistente.  |
|                      | En la arquitectura propuesta se utiliza       |
|                      | PostgreSQL.                                   |
+----------------------+-----------------------------------------------+
| Diagrama de contexto | Representación de alto nivel que muestra el   |
|                      | sistema, sus usuarios, sistemas externos y    |
|                      | principales relaciones. Corresponde al nivel  |
|                      | C1 del modelo C4.                             |
+----------------------+-----------------------------------------------+
| Diagrama de          | Diagrama que representa los principales       |
| contenedores         | contenedores que componen un sistema y las    |
|                      | relaciones existentes entre ellos. Corresponde|
|                      | al nivel C2 del modelo C4.                    |
+----------------------+-----------------------------------------------+
| Diagrama de          | Modelo que representa entidades, atributos y  |
| entidad-relación     | relaciones entre los datos que forman parte   |
|                      | del sistema.                                  |
+----------------------+-----------------------------------------------+
| Diagrama de          | Diagrama UML que representa el intercambio    |
| secuencia            | ordenado de mensajes entre actores y          |
|                      | elementos del sistema durante la ejecución de |
|                      | un escenario.                                 |
+----------------------+-----------------------------------------------+
| ERP                  | Enterprise Resource Planning. Sistema         |
|                      | integrado destinado a gestionar diferentes    |
|                      | procesos y recursos de una organización. En   |
|                      | este proyecto constituye el sistema objeto de |
|                      | estudio.                                      |
+----------------------+-----------------------------------------------+
| Usuario / Actor      | Persona o rol externo que interactúa con el   |
|                      | sistema para ejecutar funcionalidades u       |
|                      | obtener información.                          |
+----------------------+-----------------------------------------------+