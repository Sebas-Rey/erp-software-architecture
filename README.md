# Sistema ERP - Arquitectura de Software

Repositorio correspondiente al taller académico de **Arquitectura de Software y UML** de la **Universidad Manuela Beltrán (UMB)**.

El propósito de este proyecto es aplicar un ciclo básico de desarrollo de software, comenzando con la identificación y organización de requisitos mediante metodologías ágiles y continuando con el diseño, representación y documentación de una arquitectura de software utilizando el modelo **C4**, diagramas **UML** y la plantilla de documentación arquitectónica **arc42**.

---

## 📋 Tabla de contenidos

- [Descripción del proyecto](#-descripción-del-proyecto)
- [Objetivos](#-objetivos)
- [Alcance](#-alcance)
- [Gestión ágil del proyecto](#-gestión-ágil-del-proyecto)
- [Arquitectura propuesta](#-arquitectura-propuesta)
- [Modelo C4](#-modelo-c4)
- [Diseño UML](#-diseño-uml)
- [Tecnologías y herramientas](#-tecnologías-y-herramientas)
- [Estructura del repositorio](#-estructura-del-repositorio)
- [Documentación arc42](#-documentación-arc42)
- [Módulos del ERP](#-módulos-del-erp)
- [Historia de usuario seleccionada](#-historia-de-usuario-seleccionada)
- [Flujo arquitectónico](#-flujo-arquitectónico)
- [Base de datos](#-base-de-datos)
- [Instalación y ejecución](#-instalación-y-ejecución)
- [Estado del proyecto](#-estado-del-proyecto)
- [Autores](#-autores)
- [Referencias](#-referencias)

---

# 📌 Descripción del proyecto

El presente proyecto consiste en el diseño arquitectónico de un **Sistema ERP (Enterprise Resource Planning)** destinado a integrar y gestionar diferentes procesos administrativos y operativos de una organización.

El proyecto se desarrolla como ejercicio académico y tiene como finalidad demostrar la aplicación de conceptos relacionados con:

- Ingeniería de requisitos.
- Metodologías ágiles.
- Historias de usuario.
- Criterios de aceptación.
- Priorización de requisitos.
- Arquitectura de software.
- Modelo C4.
- UML.
- Modelado de datos.
- Documentación arquitectónica.

El sistema se plantea como una aplicación web que permite a diferentes tipos de usuarios interactuar con los módulos y funcionalidades del ERP de acuerdo con sus responsabilidades dentro de la organización.

La arquitectura propuesta utiliza una estructura **monolítica**, compuesta por una aplicación web, una API/backend y una base de datos relacional.

---

# 🎯 Objetivos

## Objetivo general

Diseñar y documentar la arquitectura de alto nivel de un sistema ERP mediante la aplicación de metodologías ágiles, el modelo C4, diagramas UML y la plantilla arc42.

## Objetivos específicos

- Identificar las principales funcionalidades del sistema ERP.
- Organizar los requisitos mediante un Product Backlog.
- Definir épicas correspondientes a los principales módulos del ERP.
- Redactar historias de usuario utilizando el formato:

  > Como `<rol>`, quiero `<acción>`, para que `<beneficio>`.

- Establecer criterios de aceptación utilizando el formato Dado-Cuando-Entonces.
- Priorizar las historias de usuario mediante la técnica MoSCoW.
- Representar el contexto del sistema mediante un diagrama C4 de nivel 1.
- Representar los principales contenedores del sistema mediante un diagrama C4 de nivel 2.
- Documentar escenarios relevantes mediante diagramas de secuencia UML.
- Modelar las principales entidades relacionadas con el módulo seleccionado.
- Documentar las decisiones arquitectónicas mediante arc42.
- Mantener la documentación y los diagramas en un repositorio GitHub.

---

# 📐 Alcance

El alcance del presente trabajo corresponde principalmente al **análisis, diseño arquitectónico y documentación** del sistema ERP.

El proyecto contempla:

1. Gestión del Product Backlog.
2. Definición de épicas.
3. Definición de historias de usuario.
4. Criterios de aceptación.
5. Priorización mediante MoSCoW.
6. Diseño del contexto del sistema.
7. Diseño de contenedores.
8. Diseño de escenarios mediante UML.
9. Modelo de datos simplificado.
10. Documentación mediante arc42.

La implementación completa del software ERP no forma parte del alcance principal de este taller. Las tecnologías de frontend, backend y base de datos representan la arquitectura tecnológica propuesta para una futura implementación.

---

# 📊 Gestión ágil del proyecto

La gestión de requisitos y del trabajo se realiza mediante **Jira**.

El tablero contiene las épicas correspondientes a los principales módulos del sistema y las historias de usuario asociadas.

## Épicas

Las principales épicas definidas para el ERP son:

+-------------------------+----------------------------------------------------------------------------------------------------+
|          Épica          |                                         Descripción                                                |
|-------------------------|----------------------------------------------------------------------------------------------------|
| Módulo de Compras       | Gestiona productos, proveedores y procesos relacionados con las compras.                           |
| Módulo de Facturación   | Gestiona las operaciones relacionadas con facturas y pagos.                                        |
| Módulo Stock/Costos     | Gestiona existencias, stock y costos de productos y servicios.                                     |
| Módulo de Activos Fijos | Gestiona los activos fijos de la organización.                                                     |
| Módulo de Empleados     | Gestiona información y procesos relacionados con los empleados.                                    |
| Módulo EIS              | Módulo funcional del ERP destinado a las funcionalidades definidas en los requisitos del proyecto. |
+-------------------------+----------------------------------------------------------------------------------------------------+

## Priorización

Las historias de usuario se priorizan mediante la técnica **MoSCoW**:

- **Must Have:** funcionalidades indispensables.
- **Should Have:** funcionalidades importantes que deberían implementarse.
- **Could Have:** funcionalidades deseables, pero no indispensables.
- **Won't Have:** funcionalidades que no forman parte del alcance actual.

---

# 🏗️ Arquitectura propuesta

Para este proyecto se propone una **arquitectura monolítica web** debido al alcance académico del taller y a la necesidad de mantener una solución sencilla de comprender, documentar y evolucionar.

La arquitectura está compuesta por tres contenedores principales:

```text
                    SISTEMA ERP
┌─────────────────────────────────────────────────┐
│                                                 │
│  ┌─────────────────┐                            │
│  │ Aplicación Web  │                            │
│  │ React + JS      │                            │
│  └────────┬────────┘                            │
│           │ HTTPS / JSON                        │
│           ▼                                     │
│  ┌─────────────────┐                            │
│  │ API Monolítica  │                            │
│  │ Python + Django │                            │
│  └────────┬────────┘                            │
│           │ Django ORM                          │
│           ▼                                     │
│  ┌─────────────────┐                            │
│  │ Base de Datos   │                            │
│  │ PostgreSQL      │                            │
│  └─────────────────┘                            │
│                                                 │
└─────────────────────────────────────────────────┘