### Record architecture decisions

Date: 2025-10-23

---

### ADR-001: Adopción del Estilo Arquitectónico Cliente-Servidor en Capas

**Status:** Accepted
**Date:** 2025-10-23

#### Context
El sistema debe soportar distintos tipos de clientes (escritorio para recepción y web para administración).
Se requiere alta seguridad en manejo de datos, evitando exponer lógica o credenciales en los clientes.

#### Decision
Adoptar una arquitectura Cliente-Servidor distribuida organizada en capas lógicas:
- Presentación
- Negocio / Servicios
- Acceso a Datos

#### Consequences
**Pros:**
- Mayor seguridad: la lógica y credenciales están solo en el servidor.
- Mantenibilidad: permite cambiar la UI sin afectar la lógica de negocio o la base de datos.

**Cons:**
- Aumenta la latencia por el salto de red adicional.

---

### ADR-002: Uso del Patrón DAO (Data Access Object)

**Status:** Accepted
**Date:** 2025-10-23

#### Context
Se requiere desacoplar la lógica de negocio de los detalles específicos de la base de datos para facilitar mantenimiento, flexibilidad y pruebas.

#### Decision
Aplicar el patrón DAO para encapsular operaciones CRUD.
Los Managers no ejecutarán SQL directamente, sino que delegarán en objetos como `ReservaDAO`, `PagoDAO`, etc.

#### Consequences
**Pros:**
- Facilita pruebas unitarias gracias a los mocks de base de datos.
- Reduce el impacto ante cambios de motor de base de datos.

**Cons:**
- Añade una capa adicional de código que se debe mantener.

---

### ADR-003: Estrategia de Auditoría Append-Only (Solo Escritura)

**Status:** Accepted
**Date:** 2025-10-23

#### Context
Por requisitos de negocio (CON-3) y seguridad (QAS-32), es necesario asegurar trazabilidad total de operaciones financieras y evitar alteraciones o eliminaciones.

#### Decision
Crear una tabla de auditoría inmutable bajo una estrategia append-only.
No se permitirá **UPDATE** ni **DELETE** sobre los registros históricos.
El `ReporteManager` será responsable de registrar los eventos críticos.

#### Consequences
**Pros:**
- Garantiza integridad y no-repudio de acciones.

**Cons:**
- La tabla crecerá rápidamente, por lo que a futuro se requerirán mecanismos de archivado.

---


