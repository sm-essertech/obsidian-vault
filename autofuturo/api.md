---
tags:
  - autofuturo
---
# Autofuturo API
[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue.svg)](https://github.com/autofuturo/autofuturo-api)

## 📋 Tareas / Bugs
### 🚨 Prioritarias

- [ ] Agregar cuentas a los metodos de pago.

### 😴 Para Después
- [ ] Refactorizar relación entre categorías y listing-types (remover CategoryToListingType)

### 🐛 Bugs
### ✅ Completadas

- [x] Seleccionar organizacion por defecto si esta es eliminada.
- [x] Permitir en la creación de la organización los datos del address, dirección, ciudad, etc.
- [X] Error al eliminar un usuario desde el endpoint del API 
- [X] El token al crear varias organizaciones se vuelve pesado
- [X] El API al encontrar un usuario ya creado no devuelve la validación de que el usuario ya existe, este usuario existe en la tabla de usuarios
- [X] Al tratar de crear un nuevo usuario que creo la cuenta a traves de Google, este devuelve un error 500 y no valida si el usuario ya existe
- [x] Crear un endpoint que devuelva todas las organizaciones de un usuario
- [x] Colocar la organización default del usuario dentro del endpoint del me
- [x] Añadir toda la data necesaria del usuario que estaba presente en el user_metadata en el endpoint del me
- [x] Bug en la respuesta del endpoint /me las fechas createdAt and updatedAt todos tienen la misma fecha
- [x] Al crear una organización la respuesta no devuelve el teléfono, el instagram ni el correo
- [x] Remover la sincronizacion de user_metadata con la tabla users
- [x] Remover los datos innecesarios de user_metadata en todos los usuarios
- [x] Agregar filtro de countryId a /billing/payment-methods
- [x] Agregar payment method fields los datos del pago y para el formulario de registro de pago
- [x] Crear Script para Login