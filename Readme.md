# Implementación del patrón Repository en Arquitectura Limpia

## 📌 Descripción del trabajo

Este trabajo consiste en la implementación del patrón **Repository** dentro de un proyecto basado en **Arquitectura Limpia (Clean Architecture)**.  

El repositorio base ya contaba con un ejemplo funcional del patrón aplicado a las entidades **Almacén** y **Categoría**. A partir de ese ejemplo se replicó la misma estructura para otras entidades del sistema.

Las nuevas implementaciones se realizaron respetando la separación de capas del proyecto y utilizando las interfaces y clases base existentes.

---

# 🏗 Arquitectura del proyecto

El proyecto está estructurado siguiendo el patrón de **Arquitectura Limpia**, separando las responsabilidades en distintas capas.

## Capas del sistema

### Domain
Contiene las **entidades del dominio**, que representan los modelos de negocio del sistema.

Ejemplos de entidades:

- Almacen
- Categoria
- Producto
- Proveedor
- MovimientoInventario

Estas entidades no dependen de ninguna otra capa.

---

### Application
Contiene la **lógica de aplicación**, interfaces de repositorios y servicios.

Dentro de esta capa se definen las **interfaces de los repositorios**, que establecen qué operaciones se pueden realizar sobre cada entidad.

---

### Infrastructure
Contiene las **implementaciones concretas** de los repositorios y el acceso a la base de datos mediante Entity Framework.

Aquí se implementa el patrón Repository conectando las interfaces de la capa Application con la base de datos.

---

### Presentation
Contiene la **API del sistema**, incluyendo:

- Controllers
- Configuración de servicios
- Program.cs

Esta capa es la encargada de recibir las solicitudes HTTP.

---

# 📦 Repositorios implementados

Tomando como referencia los repositorios existentes de **Almacén** y **Categoría**, se implementaron nuevos repositorios para las siguientes entidades:

- Producto
- Proveedor
- MovimientoInventario

---

# 📁 Archivos creados

## Interfaces (Application)

Archivos agregados:

IProductoRepository.cs
IProveedorRepository.cs
IMovimientoInventarioRepository.cs

Estas interfaces heredan de `IRepositoryBase<T>`, reutilizando la implementación genérica de operaciones CRUD.

---

## Implementaciones (Infrastructure)

Archivos agregados:

ProductoRepository.cs
ProveedorRepository.cs
MovimientoInventarioRepository.cs

Estas clases heredan de `RepositoryBase<T>` e implementan las interfaces definidas en la capa Application.

---

# 🔧 Registro en Dependency Injection

Los nuevos repositorios fueron registrados en el sistema de **inyección de dependencias** dentro del archivo:

ConfigurationServices.cs

Agregando las siguientes líneas:

```csharp
services.AddScoped<IProductoRepository, ProductoRepository>();
services.AddScoped<IProveedorRepository, ProveedorRepository>();
services.AddScoped<IMovimientoInventarioRepository, MovimientoInventarioRepository>();