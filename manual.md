# Shipping Sidebar — Manual de uso
- Extensión de Chrome para relevamiento de envíos (benchmark)

## Qué es
- Shipping Sidebar es una extensión de Chrome que permite gestionar tareas de relevamiento de envíos desde un panel lateral del navegador. Cada tarea corresponde a un producto en un sitio de e-commerce, y el objetivo es registrar datos como precio, vendedor, tipo de envío y plazos de entrega.
- La extensión se conecta a una planilla de Google Sheets donde se almacenan las tareas asignadas y los datos completados.

---

## Qué automatiza
- Asignación y lectura de tareas desde Google Sheets por usuario (User).
- Apertura rápida de URL del competidor (COMP_ITEM_URL) desde el panel.
- Formulario guiado para capturar datos clave sin ir/volver a la planilla.
- Escritura automática en la fila correcta usando task_id como clave.
- Medición de tiempo por tarea: Start_time, Finish_time y Time_per_task.
- Cierre de tarea marcando is_Completed al enviar.

##  Por qué es buena / necesaria
- Reduce errores: menos copiar/pegar y menos columnas equivocadas.
- Estandariza: mismo flujo y mismos campos para todos.
- Acelera: baja el tiempo operativo por tarea y la fricción.
- Mejora trazabilidad: datos consistentes + tiempos reales por site/rival.
- Escalable: el backend escribe por headers (no depende del orden de columnas).

## Cómo se usa

### 1. Iniciar sesión

Al abrir el panel lateral aparece un campo para ingresar el nombre de usuario. Este nombre debe coincidir con el que figura en la planilla de tareas. Después de escribirlo, hacer clic en "Cargar tareas" para traer las tareas asignadas.

### 2. Navegar entre tareas

Una vez cargadas las tareas, se puede elegir una tarea específica desde el selector desplegable o avanzar y retroceder con los botones "Tarea anterior" y "Siguiente tarea".

En la parte superior del panel se muestra el número de tarea actual, el sitio web asociado y el código CEP del producto.

### 3. Abrir la tarea
El botón Abrir tarea abre la URL del producto en la pestaña activa.
Al abrir, se registra Start_time (timestamp de inicio).
El cronómetro se reinicia cada vez que se navega a una tarea diferente.

### 4. Completar los campos

El formulario tiene los siguientes campos:
 
- **Precio del producto**: el precio publicado del artículo.  (product_price)
- **Enviado por**: la empresa o entidad que realiza el envío.  (Sent_By)
- **Vendido por**: el vendedor del producto. (Sold_By)
- **Es importado**: indica si el producto es importado o no.  (Imported? si aplica en la hoja)
- **Almacenado por el rival**: indica si el producto está almacenado en un depósito del competidor. (Stored_by_Rival?)
- **Promesas de envío**: se pueden agregar una o más promesas, cada una con tipo de envío, rango de fechas de entrega y precio del envío. unificada en shipping_promise (JSON)
- **Tarea completada**: se marca automáticamente cuando se completa al menos uno de los tres campos principales (precio, enviado por, vendido por). También se puede modificar de forma manual.  (Deadline_to_paybefore)

### 5. Pegado rápido

Para agilizar la carga de datos, la extensión permite copiar texto directamente desde la página web al formulario sin necesidad de usar el portapapeles:

1. Seleccionar el texto deseado en la página web.
2. Presionar una de las siguientes teclas:
   - **1** para pegar en "Precio del producto".
   - **2** para pegar en "Enviado por".
   - **3** para pegar en "Vendido por".

Como alternativa, se puede seleccionar el texto en la página y luego hacer clic en los botones numerados que aparecen junto a cada campo en el formulario.

El pegado rápido solo funciona cuando el texto está seleccionado y el cursor no se encuentra dentro de un campo de texto de la página.

### 6. Enviar la tarea

Al hacer clic en "Enviar tarea", se envían los datos completados junto con la hora de inicio, la hora de finalización y el tiempo total dedicado. Si la tarea se marcó como completada, queda registrada como tal en la planilla.

Después del envío, el panel avanza automáticamente a la siguiente tarea pendiente.

### 7. Cambiar de usuario

En la parte inferior del panel se muestra el nombre de usuario activo. El enlace "Cambiar usuario" permite cerrar la sesión y volver a la pantalla de inicio para cargar tareas de otro usuario.

---

## Consideraciones

- El cronómetro se reinicia cada vez que se navega a una tarea diferente. Solo comienza a contar cuando se abre la URL de la tarea.
- Los datos del formulario se guardan automáticamente como borrador mientras se trabaja. Si se cambia de tarea y se vuelve, los datos ingresados se mantienen.
- Después de actualizar la extensión, es necesario recargar las páginas web abiertas para que el pegado rápido vuelva a funcionar.
