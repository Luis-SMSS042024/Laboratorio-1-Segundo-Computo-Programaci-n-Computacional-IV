# Laboratorio 1 - Segundo Cómputo

## Integrantes
- Luis Alexander Rivera
- Walter Jose Ramirez Perez

## Situación problemática
En la biblioteca de la universidad existen cubículos de estudio que se alquilan por un tiempo determinado, pero muchas veces el registro se realiza de forma desordenada. Esto puede ocasionar errores al ingresar los carnets, confusión en el tiempo de préstamo y dificultad para llevar un control de los cubículos ocupados.

## Sectores beneficiados
- Biblioteca universitaria
- Estudiantes
- Personal encargado de préstamos

## Solución propuesta
Se desarrolló una página web en Vue.js para registrar el alquiler de cubículos de forma ordenada. El sistema permite ingresar el nombre del estudiante encargado, registrar tres carnets, seleccionar el cubículo, elegir el tiempo de alquiler y validar que los datos sean correctos antes de guardar el registro.

## Funciones del sistema
- Registrar alquileres de cubículos
- Ingresar tres carnets obligatorios
- Seleccionar tiempo de préstamo
- Validar campos vacíos o incorrectos
- Mostrar la lista de alquileres
- Eliminar registros

## Preguntas

### ¿Qué es Vue.js y cuál es su función en la página?
Vue.js es un framework de JavaScript para crear interfaces dinámicas. En mi proyecto se usó para manejar el formulario y mostrar los alquileres sin recargar la página.

### ¿Qué variables reactivas utilizó y para qué sirven?
Usé `encargado`, `carnet1`, `carnet2`, `carnet3`, `cubiculo`, `tiempo`, `alquileres`, `error` y `mostrarLista`. Sirven para guardar datos del formulario, los registros, los errores y controlar la vista.

### ¿Cuál es la diferencia entre `v-bind` y `v-model`?
`v-bind` enlaza atributos dinámicos en HTML. `v-model` conecta un input con una variable reactiva.

### Mencione un ejemplo de evento usado
Usé `@submit.prevent` para registrar alquileres y `@click` para eliminar registros o mostrar la lista.

### ¿Para qué utilizó `v-for`?
Lo usé para recorrer el arreglo de alquileres y mostrar cada registro en pantalla.

### ¿En qué situación utilizó `v-if`?
Lo usé para mostrar errores y para enseñar u ocultar la lista de alquileres según el estado de la aplicación.

### ¿Cómo se realiza la validación y por qué es importante?
La validación revisa que no haya campos vacíos, que los carnets tengan formato correcto y que no estén repetidos. Es importante para evitar datos incorrectos en el sistema.
