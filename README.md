# ERP Simulación (ASP.NET Framework)

![.NET Framework](https://img.shields.io/badge/.NET_Framework-4.7.2-blue)
![C#](https://img.shields.io/badge/Language-C%23-green)
![SQL Server](https://img.shields.io/badge/DB-SQL_Server_2026-red)
![Architecture](https://img.shields.io/badge/Architecture-N--Tier-orange)

## 📖 Descripción General

Este repositorio contiene un módulo de simulación de un sistema **ERP (Enterprise Resource Planning)** real. Está desarrollado sobre **ASP.NET Framework 4.7.2** bajo una arquitectura clásica de **N-Capas**. 

El proyecto destaca por su enfoque en la **resiliencia de datos**, implementando políticas de reintento, una gestión global de excepciones y un sistema de logging híbrido para garantizar la trazabilidad total de las operaciones de negocio.

## 🛠️ Especificaciones Técnicas

* **Framework:** .NET Framework 4.7.2
* **Lenguaje:** C#
* **Acceso a Datos:** ADO.NET con Procedimientos Almacenados (SPs).
* **Base de Datos:** SQL Server Express 2026.
* **Patrones:** Repository Pattern, Factory Pattern, DTO (Data Transfer Objects).

## 🏗️ Arquitectura de Software

La solución se divide en capas especializadas para asegurar el desacoplamiento y la mantenibilidad:

### 1. Capa de Datos (Data & Entities)
* **Entities:** Objetos de dominio que mapean el esquema de la base de datos.
* **DBConnectionFactory:** Implementación del patrón Factory para centralizar la gestión de `SqlConnection` y cadenas de conexión.
* **Repository Pattern:** Los repositorios (`AsientoContable`, `Cliente`, `Factura`) encapsulan el acceso a datos mediante SPs, optimizando el rendimiento y la seguridad.

### 2. Capa de Negocio (Business Logic Layer)
Actúa como el orquestador del sistema, incorporando:
* **Políticas de Reintento:** Lógica de resiliencia para mitigar fallos transitorios en operaciones críticas.
* **Gestión Global de Excepciones:** Tratamiento estructurado para evitar la fuga de metadatos técnicos.
* **Clean Logging:** Inserción de trazas de ejecución sin ensuciar la lógica principal.

### 3. Capa Transversal (Utils - Observabilidad)
El sistema utiliza un **Logger especializado** con doble persistencia:
* **File System:** Logs diarios para auditoría rápida en desarrollo.
* **SQL Server (`LogERP`):** Almacenamiento estructurado de errores de inserción y metadatos de excepciones para análisis post-mortem.

### 4. Capa de Exposición y Patrón DTO
Se implementan **Data Transfer Objects (DTOs)** para la comunicación con clientes externos, garantizando:
* **Information Hiding:** Seguridad al no exponer el modelo relacional directamente.
* **Optimización:** Reducción del payload enviando solo campos requeridos.
* **Contratos Estables:** Independencia entre la evolución de la base de datos y la API.

## 🔒 Seguridad y Comunicaciones

> [!NOTE]
> Configuración orientada a un **entorno de desarrollo controlado**.

* **Autenticación:** Acceso *Stateless* (Sin-Auth) para agilizar pruebas de integración.
* **Protocolo:** Comunicación vía **HTTPS** con payloads en JSON plano.
* **Integridad:** Procesamiento de información en formato original para maximizar la compatibilidad en la etapa de simulación.

## 🚀 Requisitos del Entorno

Para desplegar la aplicación es necesario contar con:

1.  **Servidor Web:** Internet Information Services (IIS) 7.5 o superior.
2.  **Runtime:** [.NET Framework 4.7.2](https://dotnet.microsoft.com/download/dotnet-framework/net472).
3.  **Base de Datos:** SQL Server 2026 Express (con los Procedimientos Almacenados del proyecto ejecutados).

---
*Módulo de simulación desarrollado para prácticas de integración y persistencia avanzada.*
