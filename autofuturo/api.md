---
tags:
  - autofuturo
---
# Autofuturo API
[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue.svg)](https://github.com/autofuturo/autofuturo-api)

## 📋 Tareas / Bugs
### 🚨 Prioritarias

- [x] Dividir el schema.prisma en distintos archivos. 
- [x] Crear Crud de Subscripciones.
- [x] Crear Crud de Facturas.
- [x] Crear Crud de pagos.
- [ ] Reconsiderar la aplicacion de codigos de descuento para una sola compra.
- [ ] Crear Crud sencillo de Balance.
- [ ] Crear ingegracion con s3 driver y la subida de la recibos al registrar pago
- [ ] Crear funcion(es) de postgres con respecto a los [[#Flujo de pagos|flujos de pago]].
	- [ ] Endpoint de Subscripciones `POST /subscriptions/purchase` donde se Subscripcion, Factura y el Page registrado desde el formulario junto con el comprobante de pago.
	- [ ] Funcion de postgres para actualizar los estados
	- [ ] Cronjob script para obtener las tasas de las monedas(ves)
	- [ ] Cronjob script diario que mapee las subscripciones y actualice sus estados + envio de notificaciones.
- [ ] Internacionalizacion de la API i18n
- [ ] Definir permisos de roles globales y de organizaciones, asi como validar los casos  __own__

### 😴 Para Después
- [ ] Add listing_type Filter in `GET /sources/categories`
- [ ] Add types to data-fields ENUM (Phone, Date, ...)
- [ ] Evaluar el cambio de vehicle_type por listing_type.

### 🐛 Bugs
- [ ] Validar parent_key no puede ser vacio (si se envía en el body) `POST /sources/categories`
- [ ] Error al crear una organización nueva a un usuario que no posee ninguna, este no le asigna la recién creada por default
### ✅ Completadas

- [x] Agregar order a plan_features
- [x] Remover created_by updated_by de plans y payment_methods

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