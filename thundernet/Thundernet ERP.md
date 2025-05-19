
# Tasks

## Backend

### Store
- [ ] Configurar el store de archivos para subir imágenes, documentos, etc. (API/Storage)
- [ ] Configurar el túnel para el store de imágenes (Servicios externos/DevOps)

### Usuarios
- [ ] Implementar lógica de invitación de usuarios (endpoints y emails)
- [ ] Crear API para gestionar estatus de usuarios (activar/suspender)
- [ ] Agregar campo de teléfono en la base de datos
- [ ] Configurar endpoint para subida de avatars (resize/validaciones)

### Roles
- [ ] Refactorizar módulos de acceso (lógica de permisos)
- [ ] Crear estructura de subcategorías de permisos en DB
- [ ] Actualizar middleware de autorización (rutas protegidas)

### Planes
- [ ] Desarrollar CRUD API para servicios extras (fibra/IPTV)

### Contratos
- [ ] Implementar endpoints para detalles de contratos (incluyendo borradores)
- [ ] Crear acciones de contrato en API (rechazar/aprobar/eliminar)

### General

- [ ] Corregir cache de redist en el endpoint de los estados que devuelve innecesariamente la lista de ciudades
---

## Frontend

### Usuarios
- [ ] UI para flujo de invitación (formulario + confirmación)
- [ ] Componentes para cambiar estatus de usuarios (toggle/select)
- [ ] Componente de upload para avatars (previsualización)

### Roles
- [ ] Interfaz de administración de permisos por subcategorías
- [ ] Adaptar vistas según nuevos permisos (ocultar/mostrar elementos)

### Planes
- [ ] Tabla/Formularios CRUD para gestión de planes
### Promociones
- [ ] Campo de selección múltiple para establecer el tipo de cliente
- [ ] Agregar posibilidad de configurar el precio de la instalación (de manera porcentual)
- [ ] Campo para configurar el  tipo o estatus del cliente que puede usar da promoción
### Clientes
- [ ] Diseñar vista detallada del cliente (sección información extra)
- [x] Botón para recuperar clientes archivados
- [ ] Colocar campo de tipo de contribuyente dinámico dependiendo del tipo de documento y otro campo booleano para guardar el rif clientes que no son organizaciones

### Contratos
- [ ] Vista de detalle de contrato con historial y estados
- [ ] Botones de acción para contratos (con confirmaciones)
- [ ] Agregar todos los campos nuevos de ubicación a la hora de crear un contrato al cliente

### General
- [ ] Integrar store de archivos en componentes necesarios (ej. uploader de imágenes)

### Bugs
- [ ] 