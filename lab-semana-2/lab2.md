# Laboratorio 2

Brayan Stiven Chaparro Cataño

### Actividad  #1

Se realizo el respectivo diagrama de modelo entida relacion (ER)

![alt entidad_relacion](img/ER_JOYERIA.SVG)

Se detectaron la siguiente entidades  CLIENT, SALE, EMPLOYEE, BRANCH, PRODUCT  Y por utlimo SALE_DATAIL(como entidad debil)

Sus relaaciones son:
 
 * CLIENT 1:N SALE: Un cliente realiza multiples ventas que se registra en un historial , pero cada venta esta vinculada a un solo cliente.
 * SALE N:1 EMPLOYEE: Múltiples VENTAS son atendidas por un Único EMPLEADO, que es el encargado de esa transacción.
 * SALE 1:N SALE_DETAIL: Si hay una venta por ende puede existir un detalle de venta, lo que permite manejar varios productos en un solo recibo.
 * SALE_DETAIL N:1 PRODUCT: Puede dar el caso que uno o más productos esten presentes en el detalle de venta
 * BRANCH N:M PRODUCT: Hace referencia que la surcursal distribuye mucho productos y que un producto se vende en multiples sucursales

