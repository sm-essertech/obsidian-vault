---
tags:
  - autofuturo
---
# Autofuturo API
[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue.svg)](https://github.com/autofuturo/autofuturo-api)

## 📋 Tareas / Bugs
### Pendientes

- [x] Crear un filtro de listingType para las categorías y el buscador en base a la query de listingType
- [x] Hacer que el precio del listing sea opcional
- [x] Corregir filtro de modelos cuando solo hay resultados en una marca, no muestra el filtro.
- [ ] Crear endpoint para duplicar listing


### 😴 Para Después
- [ ] 

### 🐛 Bugs
- [x] Ordenar los resultados de bodyType por cantidad de listings.
- [x] Arreglar filtro de bodyType en listings (no filtra ni las lagrimas).

## Flujo de pagos 
 1. Cuando se modifica una factura debe modificarse tambien los estatus de sus pagos relacionados.
	1.1 Si factura.status = "paid" -> factura.payments.status = "paid"  
 
2. Cuando se modifica el estado de un pago se debe modificar tambien el estado de su factura, y con ello el de su subscripcion.
	2.1 Si pago.status = "paid" y pago.amount >= factura.amount -> factura.status = paid
		2.1.1 Si pago.status = "paid" y pago.amount < factura.amount -> factura.status = "partially_paid" AND organization.balance = balance - factura.amount.
		2.1.2 Si pago.status cambia de "paid" a "peding" o algun otro estado:
			2.1.2.1 si fecha < factura.expires_at ->  factura.status = "pending" & subscription.status = "active"
			2.1.2.2 si fecha < factura_expires_at + x( 3 dias de gracia) dias -> factura.status = "overdue" &  subscription.status = "active"
			2.1.2.2 si fecha < factura_expires_at + x( 5 dias de gracia) dias -> factura.status = "expired" & subscription.status = "inactive"
