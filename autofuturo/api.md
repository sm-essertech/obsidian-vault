---
tags:
  - autofuturo
---
# Autofuturo API
[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue.svg)](https://github.com/autofuturo/autofuturo-api)

## 📋 Tareas / Bugs
### 🚨 Prioritarias

- [ ] Añadir toda la data necesaria del usuario que estaba presente en el user_metadata en el endpoint del me
- [ ] Crear un endpoint que devuelva todas las organizaciones de un usuario
- [ ] Colocar la organización default del usuario dentro del endpoint del me
- [ ] Finalizar Crud Métodos de pago.
- [ ] Bug en la respuesta del endpoint /me las fechas createdAt and updatedAt todos tienen la misma fecha
- [ ] Al crear una organización la respuesta no devuelve el teléfono, el instagram ni el correo

### 😴 Para Después
- [ ] Refactorizar relación entre categorías y listing-types (remover CategoryToListingType)
- [ ] Crear Script para Login

### 🐛 Bugs
### ✅ Completadas

- [X] Error al eliminar un usuario desde el endpoint del API 
- [X] El token al crear varias organizaciones se vuelve pesado
- [X] El API al encontrar un usuario ya creado no devuelve la validación de que el usuario ya existe, este usuario existe en la tabla de usuarios
- [X] Al tratar de crear un nuevo usuario que creo la cuenta a traves de Google, este devuelve un error 500 y no valida si el usuario ya existe

