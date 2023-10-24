## Para iniciar

- `npm install --save-peer-deps`
- `npm run build`
- `npm start`

## Default logins

### Admin

admin1
123456

### Student

aiddamkit@gmail.com
123456789

## Postman 

https://documenter.getpostman.com/view/21621812/2s8ZDR761D#e629c5c9-b937-4e9c-85c1-1111b613fe01

## Tipos de transaccion

- Inscripcion (estudiante, usuario que genero la inscripcion, fecha, tipo, ver)
- Pago de mensualidad 
- Pagos miscelaneos

## Tablas

- Editar (usuario, usuario generador, tipo, fecha)

-  Ordenes (transacciones pendientes) 

- Transacciones (transacciones completadas/pendientes) (usuario, estado, monto, monto pagado, forma de pago, fecha de emision y fecha de pago, referencia)
	- Importantes (estado, usuario admin, fecha de gestion, monto, monto pagado, ver)

- Adjuntar documentos (tipo de arch, fecha de subida, nombre del arch, individual/general, ver)

## Payment Info 

Este es un objeto creado en el estado al inscribir un estudiante o realizar cualquier otro tipo de pago, está estructurado de la siguiente forma:

| Propiedad | Valor                                |
| --------- | ------------------------------------ |
| method    | 'ZELLE','VES','CASH'                 |
| ref       | Numéricos                            |
| email     | Dirección de email                   |
| amount    | valor de la operacion                |
| bill      | id del tipo de inscripción realizado |

