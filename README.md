# Práctica contenedores, iteradores y algoritmos - Gestión de tareas a estudiantes
> Material introductorio a este tema puede encontrar disponible en: https://github.com/lufe089/POO/blob/main/7.Contendores.
>
##  Ejercicio administración de tareas diarias universitarios


### Contexto

Cada estudiante registra tareas diarias que pueden incluir actividades académicas (como estudiar para un examen), personales (como hacer ejercicio) o domésticas (como cocinar o lavar la ropa). Se desea construir un sistema que permita:

- Registrar estudiantes.
- Registrar tareas para cada estudiante.
- Consultar las tareas de un estudiante.
- Aplicar operaciones como búsqueda, conteo o eliminación sobre las tareas.

### Requisitos funcionales

1. **Gestión de estudiantes**:
   - Cada estudiante tiene un nombre y un código único.
   - Se deben poder registrar nuevos estudiantes.
     
2. **Gestión de tareas**:
   - Cada tarea contiene una descripción, una duración estimada en minutos y un indicador de si ya fue realizada o no.
   - Se deben poder registrar múltiples tareas por estudiante.

3. **Consultas y operaciones**:
   - Consultar todas las tareas de un estudiante.
   - Contar cuántas tareas están pendientes.
   - Eliminar tareas completadas.
   - Buscar una tarea por su descripción.
   - Calcular el tiempo total de las tareas pendientes.
   - Mostrar las tareas en orden alfabético por su descripción.
   - Agregar estudiante, eliminar estudiante, consultar estudiante, actualizar estudiante

### Restricciones técnicas y lineamientos de implementación

- Usar `map<string, Estudiante*>` para almacenar los estudiantes por su código (se trabajará con punteros a objetos).
- Cada objeto `Estudiante` almacenará un `vector<Tarea*>` con sus tareas (también punteros a objetos).
- Es obligatorio hacer una correcta gestión de memoria dinámica:
  - Crear los objetos con `new` y liberarlos con `delete`.
  - Implementar destructores en las clases para evitar fugas de memoria.
- Utilizar `for`, e iteradores explícitos en distintos métodos.
- Usar algoritmos de la STL (`find`, `count`, `remove`, `sort`, `accumulate`, etc.) donde sea apropiado.
- Crear una clase GestorTareas que almacenará el mapa de estudiantes, permitirá agregar estudiantes, eliminar estudiantes.
- Toda interacción con el usuario se realizará desde `main()` o una clase gestora.

📌 *Recordatorio: cuando se almacenan punteros en un contenedor, se debe acceder a sus atributos con el operador flecha (`->`) en lugar del operador punto (`.`).*

Haga el diseño orientadoa objetos para este enunciado, actualice el readme con el diseño y luego haga la codificación. 



