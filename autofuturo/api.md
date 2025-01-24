---
tags:
  - autofuturo
---
# Autofuturo API
[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue.svg)](https://github.com/autofuturo/autofuturo-api)

## 📋 Tareas / Bugs
### 🚨 Prioritarias

- [ ] Dividir el schema.prisma en distintos archivos. 
- [ ] Crear Crud de Facturas.
- [ ] Crear Crud de pagos.
- [ ] Crear Crud de Subscripciones.
- [ ] Recordar a Francisco sobre el redis de desarrollo

### 😴 Para Después
- [ ] Add listing_type Filter in `GET /sources/categories`
- [ ] Add types to data-fields ENUM (Phone, Date, ...)
- [ ] Evaluar el cambio de vehicle_type por listing_type.

### 🐛 Bugs
- [ ] Validar parent_key no puede ser vacio (si se envía en el body) `POST /sources/categories`
### ✅ Completadas

- [x] Agregar order a plan_features
- [x] Remover created_by updated_by de plans y payment_methods