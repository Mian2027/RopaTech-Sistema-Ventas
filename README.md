[README.md](https://github.com/user-attachments/files/25224788/README.md)
# 🛍️ RopaTech - Sistema Inteligente de Gestión para Tiendas de Ropa

Sistema de gestión de inventario y ventas desarrollado en Java para tiendas de ropa urbanas en Perú. Automatiza procesos de control de stock, registro de ventas, gestión de clientes y generación de reportes.

![Java](https://img.shields.io/badge/Java-17-orange?style=flat-square&logo=java)
![MySQL](https://img.shields.io/badge/MySQL-8.0-blue?style=flat-square&logo=mysql)
![NetBeans](https://img.shields.io/badge/NetBeans-IDE-green?style=flat-square&logo=apache-netbeans-ide)
![License](https://img.shields.io/badge/License-Academic-yellow?style=flat-square)

---

## 📋 Descripción del Proyecto

RopaTech es un sistema de gestión empresarial diseñado específicamente para tiendas de ropa de pequeña y mediana escala que operan con métodos manuales. El sistema digitaliza y automatiza los procesos operativos clave, reduciendo errores y mejorando la eficiencia.

### Problemática
Las tiendas de ropa urbanas en Perú dependen de registros en papel, lo que genera:
- ❌ Errores frecuentes en el conteo de stock
- ❌ Demoras en la atención al cliente
- ❌ Falta de datos históricos para toma de decisiones

### Solución
✅ Sistema digital integrado que automatiza la gestión de inventario, ventas y clientes
✅ Interfaz gráfica intuitiva para usuarios sin conocimientos técnicos
✅ Reportes y análisis en tiempo real

---

## ✨ Funcionalidades Principales

### 🔐 Gestión de Usuarios
- Autenticación segura con roles (Administrador, Vendedor, Almacenero)
- CRUD completo de usuarios
- Control de permisos por rol

### 📦 Gestión de Inventario
- Registro de entrada y salida de productos
- Control de stock en tiempo real
- Alertas automáticas de stock bajo
- Actualización de precios
- Organización por categorías

### 🛒 Gestión de Ventas
- Registro rápido de transacciones
- Generación automática de facturas en PDF
- Cálculo automático de subtotal, IVA y descuentos
- Actualización automática de inventario post-venta

### 👥 Gestión de Clientes
- Registro de datos de clientes
- Historial de compras por cliente
- Búsqueda rápida de clientes

### 📊 Reportes y Consultas
- Reporte de inventario actual
- Historial completo de ventas
- Filtros por fecha y cliente
- Productos con stock bajo destacados
- Exportación de reportes a PDF

### 🔍 Búsqueda Inteligente
- Búsqueda de productos por nombre
- Filtrado por categoría
- Resultados en tiempo real

---

## 🛠️ Tecnologías Utilizadas

| Tecnología | Uso |
|------------|-----|
| **Java 17** | Lenguaje de programación principal |
| **Java Swing** | Desarrollo de interfaz gráfica (GUI) |
| **MySQL 8.0** | Base de datos relacional |
| **JDBC** | Conexión Java-MySQL |
| **iText 5** | Generación de facturas PDF |
| **NetBeans IDE** | Entorno de desarrollo |
| **Git & GitHub** | Control de versiones y colaboración |

---

## 🏗️ Arquitectura del Sistema

El proyecto implementa el patrón **MVC (Modelo-Vista-Controlador)** con arquitectura de **3 capas**:

```
┌─────────────────────────────────────┐
│    CAPA DE PRESENTACIÓN (Vista)     │
│         Java Swing Forms            │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  CAPA DE LÓGICA DE NEGOCIO (Ctrl)   │
│    Controladores y Validaciones     │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│   CAPA DE ACCESO A DATOS (Modelo)   │
│        JDBC + MySQL Database        │
└─────────────────────────────────────┘
```

### 📁 Estructura del Proyecto

```
RopaTech/
├── src/
│   ├── modelo/              # Clases entidad (POJOs)
│   │   ├── Usuario.java
│   │   ├── Cliente.java
│   │   ├── Producto.java
│   │   ├── Categoria.java
│   │   ├── CabeceraVenta.java
│   │   └── DetalleVenta.java
│   │
│   ├── controlador/         # Lógica de negocio
│   │   ├── Ctrl_Usuario.java
│   │   ├── Ctrl_Cliente.java
│   │   ├── Ctrl_Producto.java
│   │   ├── Ctrl_Categoria.java
│   │   ├── Ctrl_RegistrarVenta.java
│   │   ├── Reportes.java
│   │   └── VentaPDF.java
│   │
│   ├── vista/               # Interfaces gráficas
│   │   ├── FrmLogin.java
│   │   ├── FrmMenu.java
│   │   ├── InterUsuario.java
│   │   ├── InterCliente.java
│   │   ├── InterProducto.java
│   │   ├── InterFacturacion.java
│   │   └── ...
│   │
│   ├── conexion/            # Gestión de BD
│   │   └── Conexion.java
│   │
│   └── img/                 # Recursos gráficos
│
├── database/                # Scripts SQL
│   └── bd_sistema_ventas.sql
│
└── docs/                    # Documentación
    └── ...
```

---

## 💾 Base de Datos

### Diagrama Entidad-Relación

```
┌─────────────┐        ┌──────────────┐        ┌─────────────┐
│  tb_usuario │        │ tb_categoria │        │ tb_cliente  │
├─────────────┤        ├──────────────┤        ├─────────────┤
│ idUsuario   │        │ idCategoria  │        │ idCliente   │
│ nombre      │        │ descripcion  │        │ nombre      │
│ usuario     │        │ estado       │        │ cedula      │
│ password    │        └──────────────┘        │ telefono    │
└─────────────┘               │                └─────────────┘
                              │                       │
                        ┌─────▼──────┐               │
                        │ tb_producto│               │
                        ├────────────┤               │
                        │ idProducto │               │
                        │ nombre     │               │
                        │ cantidad   │               │
                        │ precio     │               │
                        │ idCategoria├───────────────┘
                        └────────────┘
                              │
                    ┌─────────▼──────────┐
                    │ tb_cabecera_venta  │
                    ├────────────────────┤
                    │ idCabeceraVenta    │
                    │ idCliente          │◄─────────┐
                    │ valorPagar         │          │
                    │ fechaVenta         │          │
                    └────────────────────┘          │
                              │                     │
                    ┌─────────▼──────────┐          │
                    │ tb_detalle_venta   │          │
                    ├────────────────────┤          │
                    │ idDetalleVenta     │          │
                    │ idCabeceraVenta    │──────────┘
                    │ idProducto         │
                    │ cantidad           │
                    │ precioUnitario     │
                    │ subtotal           │
                    │ descuento          │
                    │ iva                │
                    │ totalPagar         │
                    └────────────────────┘
```

### Principales Tablas

- **tb_usuario**: Gestión de usuarios del sistema
- **tb_cliente**: Información de clientes de la tienda
- **tb_categoria**: Categorización de productos
- **tb_producto**: Inventario de productos
- **tb_cabecera_venta**: Registro principal de ventas
- **tb_detalle_venta**: Detalle de productos por venta

---

## 🚀 Instalación y Configuración

### Requisitos Previos

- ✅ Java JDK 17 o superior
- ✅ MySQL 8.0 o superior
- ✅ NetBeans IDE 12.0 o superior
- ✅ Git (opcional, para clonar)

### Paso 1: Clonar el Repositorio

```bash
git clone https://github.com/TU-USUARIO/RopaTech.git
cd RopaTech
```

### Paso 2: Configurar la Base de Datos

1. Abrir MySQL Workbench o línea de comandos MySQL

2. Crear la base de datos:
```sql
CREATE DATABASE bd_sistema_ventas;
USE bd_sistema_ventas;
```

3. Ejecutar el script SQL ubicado en `/database/bd_sistema_ventas.sql`

4. Verificar que las tablas se crearon correctamente:
```sql
SHOW TABLES;
```

### Paso 3: Configurar la Conexión

1. Abrir el archivo `src/conexion/Conexion.java`

2. Modificar los parámetros de conexión según tu configuración:
```java
Connection cn = DriverManager.getConnection(
    "jdbc:mysql://localhost/bd_sistema_ventas",
    "root",        // Tu usuario MySQL
    "tu_password"  // Tu contraseña MySQL
);
```

### Paso 4: Importar en NetBeans

1. Abrir NetBeans IDE
2. File → Open Project
3. Seleccionar la carpeta del proyecto
4. Esperar a que NetBeans resuelva dependencias

### Paso 5: Agregar Librerías (si es necesario)

El proyecto requiere las siguientes librerías en `/src/conector/`:
- `mysql-connector-java-5.1.46-bin.jar`
- `itext5-itextpdf-5.5.12.jar`
- `jcalendar-1.4.jar`

Si no están incluidas:
1. Click derecho en el proyecto → Properties
2. Libraries → Add JAR/Folder
3. Seleccionar los archivos .jar

### Paso 6: Ejecutar el Proyecto

1. Click derecho en el proyecto → Clean and Build
2. Click derecho en `FrmLogin.java` → Run File
3. Usar credenciales por defecto:
   - **Usuario**: `Miguel`
   - **Contraseña**: `123456`

---

## 👥 Equipo de Desarrollo

| Integrante | Rol | GitHub |
|------------|-----|--------|
| **Taquire Arquinigo Alondra Yhadira** | Desarrollador Full Stack | [@usuario](https://github.com/usuario) |
| **Rojas Casas Misael Benjamin** | Desarrollador Full Stack | [@usuario](https://github.com/usuario) |
| **Angulo Ubillus Miguel Angel** | Desarrollador Full Stack | [@usuario](https://github.com/usuario) |

---

## 📚 Metodología de Desarrollo

El proyecto se desarrolló bajo la metodología **Scrum** con sprints de 2 semanas:

### Sprint 1 (Semanas 1-2)
- ✅ Configuración de Git y GitHub
- ✅ Estructura base del proyecto
- ✅ Módulo de autenticación
- ✅ Gestión de productos e inventario
- ✅ Sistema de categorías

### Sprint 2 (Semanas 3-4)
- ✅ Módulo de clientes
- ✅ Sistema completo de ventas
- ✅ Generación de facturas PDF
- ✅ Reportes de inventario
- ✅ Historial de ventas

### Sprint 3 (Semanas 5-6) - En desarrollo
- 🔄 Optimización de consultas SQL
- 🔄 Reportes avanzados con gráficos
- 🔄 Mejoras en la interfaz de usuario

### Sprint 4 (Semanas 7-8) - Planificado
- 📅 Pruebas de integración
- 📅 Documentación final
- 📅 Presentación del sistema

---

## 🎯 Objetivos del Proyecto

### Objetivo General
Desarrollar una aplicación eficaz para la gestión de inventarios y ventas en tiendas de ropa del Perú, mejorando la eficiencia operativa mediante una solución digital.

### Objetivos Específicos
1. ✅ Permitir el registro y control de entradas/salidas de productos
2. ✅ Desarrollar una interfaz amigable y accesible
3. ✅ Implementar búsqueda rápida de productos
4. ✅ Crear sistema de autenticación con roles
5. ✅ Generar reportes de ventas e inventario

---

## 📊 Resultados Esperados

- ✅ Sistema funcional de gestión de inventario y ventas
- ✅ Interfaz gráfica intuitiva para distintos roles
- ✅ Base de datos robusta y normalizada
- ✅ Documentación técnica completa
- ✅ Aplicación de principios de POO y MVC
- ✅ Colaboración efectiva mediante Git/GitHub

---

## 🔮 Mejoras Futuras

- [ ] Integración con facturación electrónica SUNAT
- [ ] Módulo de compras y proveedores
- [ ] Dashboard con gráficos estadísticos
- [ ] Exportación de reportes a Excel
- [ ] Sistema de backup automático
- [ ] Versión web con Spring Boot
- [ ] Aplicación móvil para vendedores
- [ ] Integración con sistemas de pago en línea

---

## 📖 Documentación Adicional

- 📄 [Manual de Usuario](docs/manual-usuario.pdf)
- 📄 [Documento Técnico Completo](docs/RopaTech_Proyecto_COMPLETO_FINAL.docx)
- 📄 [Diagramas UML](docs/diagramas/)
- 📄 [Plan de Pruebas](docs/plan-pruebas.pdf)

---

## 🎓 Contexto Académico

**Universidad**: Universidad Tecnológica del Perú (UTP)  
**Curso**: Lenguajes de Programación  
**Docente**: Ivan Robles Fernandez  
**Ciclo**: 2026 - Verano  
**Carrera**: Ingeniería de Sistemas y Software

---

## 📄 Licencia

Este proyecto fue desarrollado con fines académicos para el curso de Lenguajes de Programación de la Universidad Tecnológica del Perú.

---

## 🙏 Agradecimientos

- A nuestro profesor Ivan Robles Fernandez por su guía durante el desarrollo
- A la Universidad Tecnológica del Perú por brindarnos las herramientas necesarias
- A las tiendas de ropa que inspiraron este proyecto

---

<div align="center">

**⭐ Si este proyecto te fue útil, no olvides darle una estrella ⭐**



</div>
