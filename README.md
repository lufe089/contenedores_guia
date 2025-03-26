# Sección 1. Introducción a la STL y a los Contenedores en C++

## 1.1 ¿Qué es la STL?

La STL (*Standard Template Library*) es una biblioteca estándar de C++ que proporciona un conjunto de herramientas genéricas reutilizables para facilitar la programación eficiente y estructurada. Esta biblioteca incluye:

- **Contenedores**: estructuras que permiten almacenar y organizar colecciones de datos.
- **Iteradores**: objetos que permiten recorrer los elementos de un contenedor.
- **Algoritmos**: funciones predefinidas para realizar operaciones como ordenamiento, búsqueda, transformación y eliminación.

La STL permite resolver problemas comunes sin necesidad de implementar estructuras de datos desde cero. Es una herramienta fundamental para el desarrollo moderno en C++, ampliamente utilizada en la industria.

---

## 1.2 ¿Qué es un contenedor?

### 1.2.1 Analogías cotidianas

Para comprender qué es un contenedor, puede ser útil considerar algunas analogías:

- Una **fila de supermercado** representa una lista de personas organizadas en orden de llegada.
- Una **agenda de contactos** asocia nombres con números telefónicos, como un diccionario.
- Una **caja de marcadores** donde no se permiten colores repetidos es similar a un conjunto sin duplicados.

En programación, los contenedores cumplen funciones similares: permiten organizar, acceder y manipular colecciones de datos.

### 1.2.2 Tipado de los contenedores

Antes de utilizar un contenedor en C++, es necesario especificar el **tipo de dato** que va a almacenar. Esta característica se basa en el uso de **plantillas (templates)**. Por ejemplo:

```cpp
vector<int> numeros;            // Contenedor de enteros
set<string> nombres;            // Conjunto de cadenas de texto
map<string, float> notas;       // Diccionario de nombres con notas
```

Cuando se almacenan **tipos primitivos** (como `int`, `float`, `char`, etc.), generalmente se hace directamente. En cambio, cuando se trabaja con **objetos**, se recomienda almacenar **punteros a objetos** en lugar de los objetos completos, ya que permite una mejor gestión de la memoria, evita copias costosas y facilita el uso de polimorfismo.

<details>
<summary>📌 Nota: ¿Cuál es la diferencia entre almacenar objetos y punteros?</summary>

- **Paso por copia**: se crea una copia del objeto. Es costoso si el objeto es grande.
- **Paso por referencia**: se accede al mismo objeto original, sin copiarlo.
- **Uso de punteros**: permite crear objetos en memoria dinámica, compartirlos entre estructuras y eliminarlos de forma controlada.

```cpp
vector<Estudiante> lista1;       // Almacena copias completas de objetos Estudiante
vector<Estudiante*> lista2;      // Almacena punteros a objetos Estudiante
```

En programación orientada a objetos, es común trabajar con `vector<Clase*>`, especialmente cuando los objetos tienen métodos virtuales o se comparten entre clases.

</details>

### 1.2.3  Tipos de ciclos para recorrer colecciones

En C++, existen varias formas de recorrer los elementos de una colección. A continuación se describen las tres más utilizadas:

#### Ciclo `for` clásico con índice

Este tipo de ciclo se utiliza especialmente con contenedores que permiten acceso por posición, como `vector`. Su estructura es:

```cpp
for (int i = 0; i < contenedor.size(); i++) {
    // acceso con índice
    cout << contenedor[i] << endl;
}
```
- Se inicializa una variable de control (por lo general `i = 0`).
- Se define una condición que se evalúa antes de cada iteración (`i < contenedor.size()`).
- Se incrementa la variable al final de cada ciclo (`i++`).

#### Ciclo `for` basado en rango

Este ciclo recorre automáticamente todos los elementos de un contenedor sin usar índices. Es útil y claro para la mayoría de los casos:

```cpp
for (const Tipo& elemento : contenedor) {
    cout << elemento << endl;
}
```
- `const` evita modificar el elemento.
- `&` evita realizar una copia innecesaria (especialmente útil si `Tipo` es un objeto).

#### Ciclo usando iteradores explícitos

Se basa en el uso de objetos especiales llamados **iteradores**, que permiten recorrer elementos desde el primero (`begin()`) hasta el final (`end()`):

```cpp
for (auto it = contenedor.begin(); it != contenedor.end(); ++it) {
    cout << *it << endl;
}
```
- `auto` deduce automáticamente el tipo del iterador.
- El asterisco `*it` se usa para acceder al valor que apunta el iterador.

Esta forma es necesaria cuando se quiere modificar elementos directamente o se requiere un mayor control sobre el recorrido.

---

## 1.3 Contenedores fundamentales de la STL

La STL agrupa los contenedores en tres grandes categorías:

- **Contenedores secuenciales**: almacenan elementos en un orden determinado.
  - Ejemplos: `vector`, `list`, `deque`

- **Contenedores asociativos**: organizan los elementos de acuerdo con claves. No mantienen un orden secuencial. NO es posible seleccionar la posición de inserción.
  - Ejemplos: `set`, `map`, `multimap`, `multiset`

- **Contenedores adaptadores**: modifican el comportamiento de otros contenedores.
  - Ejemplos: `stack`, `queue`, `priority_queue`

En esta guía se trabajará principalmente con `vector`, `set` y `map`, por ser los más útiles para el desarrollo de aplicaciones orientadas a objetos en etapas iniciales.


### 1.3.1 `vector<T>`

#### Definición y analogía

Un `vector` es una lista ordenada de elementos, de tamaño variable. Es similar a un arreglo dinámico que puede crecer o reducirse según sea necesario.

#### Beneficios
- Permite acceso rápido por índice.
- Fácil de recorrer.
- Flexible: se pueden añadir o eliminar elementos dinámicamente.

#### Limitaciones
- Inserciones o eliminaciones en medio del `vector` pueden ser costosas.

#### Operaciones básicas y formas de recorrido
```cpp
vector<int> numeros;
numeros.push_back(10);
numeros.push_back(20);

// Recorrido con índice clásico
for (int i = 0; i < numeros.size(); i++) {
    cout << numeros[i] << endl;
}
// Partes del ciclo for clásico:
// - inicialización: int i = 0
// - condición: i < numeros.size()
// - incremento: i++

// Recorrido con for basado en rango
for (const int& n : numeros) {
    cout << n << endl;
}
// Se recomienda usar const y referencia (&) para evitar copias

// Recorrido con iteradores explícitos
for (auto it = numeros.begin(); it != numeros.end(); ++it) {
    cout << *it << endl;
}
```

---

### 1.3.2 `set<T>`

#### Definición y analogía

Un `set` es una colección de elementos únicos, organizados de forma ordenada automáticamente. Es similar a una caja donde no se permiten duplicados.

#### Beneficios
- Garantiza la unicidad de los elementos.
- Permite búsqueda eficiente.

#### Limitaciones
- No permite acceder por índice.
- Los elementos deben ser comparables (operador `<`).

#### Operaciones básicas y formas de recorrido
```cpp
set<string> nombres;
nombres.insert("Ana");
nombres.insert("Luis");
nombres.insert("Ana");

// For basado en rango
for (const string& nombre : nombres) {
    cout << nombre << endl;
}

// Iteradores explícitos
for (auto it = nombres.begin(); it != nombres.end(); ++it) {
    cout << *it << endl;
}
```

---

### 1.3.3 `map<K, V>`

#### Definición y analogía

Un `map` es una estructura que asocia claves con valores. Es comparable a una agenda, donde a cada nombre se le asigna un número telefónico.

#### Beneficios
- Permite acceder a un valor usando una clave.
- No permite claves duplicadas.

#### Limitaciones
- Las claves deben ser únicas y comparables.

#### Operaciones básicas y formas de recorrido
```cpp
map<string, int> edades;
edades["Ana"] = 15;
edades["Luis"] = 16;
edades["Carlos"] = 17;

// Recorrido usando for basado en rango
for (const pair<const string, int>& par : edades) {
    cout << par.first << ": " << par.second << endl;
}

// Iteradores explícitos
for (auto it = edades.begin(); it != edades.end(); ++it) {
    cout << it->first << ": " << it->second << endl;
}
```

🔹 `auto` permite que el compilador infiera el tipo. Se recomienda `const auto&` para evitar copias cuando se recorren objetos complejos.

---

## 1.4 Ejercicios

Para facilitar el desarrollo y la organización de los ejercicios, se propone crear una clase auxiliar denominada `Prueba`. Esta clase contendrá los métodos de prueba para cada tipo de contenedor.

```cpp
class Prueba {
public:
    void probarVector();
    void probarSet();
    void probarMap();
};
```

Uso en el `main`:
```cpp
int main() {
    Prueba* p = new Prueba();
    p->probarVector();
    delete p;
    return 0;
}
```

### Ejercicio 1. Lista de nombres

Crear un `vector<string>` que almacene cinco nombres. Mostrar los nombres por consola usando diferentes formas de recorrido.

<details>
<summary>Solución sugerida</summary>

```cpp
void Prueba::probarVector() {
    vector<string> nombres;
    nombres.push_back("Ana");
    nombres.push_back("Luis");
    nombres.push_back("Carlos");
    nombres.push_back("Marta");
    nombres.push_back("Julián");

    for (const string& nombre : nombres) {
        cout << nombre << endl;
    }
}
```

</details>

---

### Ejercicio 2. Conjunto sin duplicados

Crear un `set<string>` e insertar nombres con duplicados. Mostrar los elementos del conjunto resultante.

<details>
<summary>Solución sugerida</summary>

```cpp
void Prueba::probarSet() {
    set<string> nombres;
    nombres.insert("Ana");
    nombres.insert("Luis");
    nombres.insert("Ana");
    nombres.insert("Carlos");

    for (auto it = nombres.begin(); it != nombres.end(); ++it) {
        cout << *it << endl;
    }
}
```

</details>

---

### Ejercicio 3. Diccionario de edades

Crear un `map<string, int>` para almacenar tres nombres y sus edades. Mostrar todos los pares almacenados.

<details>
<summary>Solución sugerida</summary>

```cpp
void Prueba::probarMap() {
    map<string, int> edades;
    edades["Ana"] = 15;
    edades["Luis"] = 16;
    edades["Carlos"] = 17;

    for (const auto& par : edades) {
        cout << par.first << ": " << par.second << " años" << endl;
    }
}
```

</details>

## Sección 2 Iteradores en C++

### 2.1 ¿Qué es un iterador?

Un **iterador** es un objeto que actúa como un puntero para recorrer una estructura de datos. Permite acceder secuencialmente a los elementos de un contenedor sin exponer cómo están almacenados internamente.

### 📦 Analogía cotidiana

Piensa en una **cinta transportadora** en una fábrica de chocolates. Cada dulce pasa frente a ti, uno por uno. Tú (el iterador) no necesitas saber dónde están almacenados todos los dulces, solo necesitas un mecanismo para ver el siguiente.

<details>
<summary>Código de ejemplo</summary>

```cpp
std::vector<std::string> tareas = {"Lavar", "Cocinar", "Estudiar"};
auto it = tareas.begin(); // Iterador apuntando al primer elemento
std::cout << *it; // El asterisco (*) se usa para acceder al valor al que apunta el iterador         // Accede al valor apuntado: "Lavar"
```

</details>

---

### 2.2 ¿Por qué usar iteradores?

- Son **necesarios** cuando se usan funciones genéricas de la STL (como `sort`, `find`, etc.).
- Permiten **modificar elementos** directamente durante el recorrido.
- Funcionan de forma **uniforme** para diferentes tipos de contenedores. Funcionan de forma uniforme para diferentes tipos de contenedores. Esto significa que, sin importar si estamos utilizando un vector, un set o un map, podemos recorrer sus elementos utilizando la misma lógica basada en iteradores. Esta característica facilita el desarrollo de funciones genéricas que pueden aplicarse a distintos tipos de estructuras, sin necesidad de adaptar el código a cada una. Por ejemplo, podemos crear una función que imprima los elementos de cualquier colección utilizando simplemente sus iteradores, sin tener que saber cómo están almacenados internamente los datos ni preocuparse por si el contenedor permite acceso por índice o no.

### Diferencias con otros ciclos

| Tipo de recorrido     | ¿Usa índices? | ¿Requiere conocer tamaño? | ¿Permite modificar? | ¿Usa iteradores? |
|----------------------|---------------|----------------------------|---------------------|------------------|
| `for` clásico        | Sí            | Sí                         | Sí                  | No               |
| `for` basado en rango| No            | No                         | No (si es `const`)  | Internamente sí  |
| Iterador explícito   | No            | No                         | Sí                  | Sí               |

---

### 2.3 ¿Cuándo es obligatorio usar iteradores?

✅ Obligatorio:
- Al usar algoritmos de la STL (`find`, `sort`, etc.).
- Para recorrer `set`, `map`, `list`, donde no hay acceso por índice.
- Para modificar elementos mientras se recorren (sin invalidar el ciclo).

❌ No necesario:
- Para contenedores con acceso aleatorio (`vector`) cuando solo se requiere leer valores.

---


### 📝 Ejemplos

- Crear un `set<string>` con nombres de personas y recorrerlo usando un iterador para imprimir solo los nombres que tienen más de 4 letras.

<details>
<summary>Solución sugerida</summary>

```cpp
#include <iostream>
#include <set>
#include <string>

int main() {
    std::set<std::string> nombres = {"Ana", "Santiago", "Luis", "Camila"};

    for (auto it = nombres.begin(); it != nombres.end(); ++it) {
        if (it->size() > 4) {
            std::cout << *it << std::endl;
        }
    }
    return 0;
}
```

</details>

- Crear un `map<string, float>` de productos y precios. Usar iterador para aplicar un descuento del 10% a todos los productos.

<details>
<summary>Solución sugerida</summary>

```cpp
#include <iostream>
#include <map>
#include <string>

int main() {
    std::map<std::string, float> productos = {
        {"Pan", 1000}, {"Leche", 2500}, {"Queso", 3500}
    };

    for (auto it = productos.begin(); it != productos.end(); ++it) {
        it->second *= 0.9; // Aplicar 10% de descuento
        std::cout << it->first << ": $" << it->second << std::endl;
    }
    return 0;
}
```

</details>

---

## 3 Algoritmos de la STL

### 3.1 ¿Qué son los algoritmos?

Son funciones genéricas que operan sobre secuencias (contenedores). Se definen en `<algorithm>` y requieren **iteradores** como argumentos.

```cpp
#include <algorithm>
#include <vector>
```

---

### 3.2 Ejemplos y analogías de uso

##### 🔍 `find`: Buscar un elemento

⚠️ Nota importante sobre find en distintos contenedores:

* En vector, es posilbe usar std::find para buscar un valor. El iterador obtenido permite acceder y modificar el elemento encontrado.
* En set, es posible usar set.find(valor). El iterador permite leer el valor, pero no modificarlo, ya que los elementos en un set son constantes.
* En map, es posible usar map.find(clave). El iterador obtenido apunta a un par clave-valor (std::pair<const Key, Value>), y puedes modificar el valor usando it->second, pero no la clave.

**Analogía**: Buscar un nombre en una lista de asistencia.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>

int main() {
    std::vector<std::string> lista = {"Ana", "Luis", "Carlos"};
    auto it = std::find(lista.begin(), lista.end(), "Luis");

    if (it != lista.end()){
        std::cout << "Encontrado: " << *it << std::endl;
    }
    else {
        std::cout << "No está en la lista." << std::endl;
    }
    return 0;
}
```

---

#### 🔢 `count`: Contar ocurrencias

**Analogía**: Contar cuántas veces alguien llegó tarde en un mes.
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> llegadas = {1, 0, 1, 1, 0};
    int total = std::count(llegadas.begin(), llegadas.end(), 1);
    std::cout << "Días tarde: " << total << std::endl;
    return 0;
}
```

---

##### 🔠 `sort`: Ordenar elementos

**Analogía**: Ordenar calificaciones de mayor a menor.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> notas = {3, 5, 4, 2};
    std::sort(notas.begin(), notas.end(), std::greater<int>());

    for (int n : notas) {
        std::cout << n << " ";
    }
    return 0;
}
```

##### 🧮 `accumulate`: Sumar elementos

**Analogía**: Calcular el total de gastos del mes.

```cpp
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    std::vector<int> gastos = {100, 200, 150};
    int total = std::accumulate(gastos.begin(), gastos.end(), 0);
    std::cout << "Total: " << total << std::endl;
    return 0;
}
```

##### 🧹 `remove`: Eliminar (lógicamente) un elemento

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> numeros = {1, 2, 3, 2, 4};
    auto fin = std::remove(numeros.begin(), numeros.end(), 2);
    numeros.erase(fin, numeros.end());

    for (int n : numeros) {
        std::cout << n << " ";
    }
    return 0;
}


> 🛑 `remove` solo mueve los elementos no eliminados al principio. Hay que llamar `erase()` para ajustar el tamaño.

---

## 🧩 3.4 Relación entre iteradores y algoritmos

Los algoritmos **no trabajan directamente con contenedores**, sino con sus **iteradores**. Esto los hace más flexibles: un mismo algoritmo puede usarse sobre `vector`, `set`, `list`, etc.

---

## 📝 Ejercicios prácticos

### Ejercicio 1: Buscar

Crear un `vector<string>` con nombres. Pedir al usuario un nombre y usar `find` para verificar si está en la lista.

<details>
<summary>Solución sugerida</summary>

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

int main() {
    std::vector<std::string> nombres = {"Ana", "Luis", "Carlos"};
    std::string buscar;
    std::cout << "Ingrese el nombre a buscar: ";
    std::cin >> buscar;

    auto it = std::find(nombres.begin(), nombres.end(), buscar);
    if (it != nombres.end()){
        std::cout << "Encontrado: " << *it << std::endl;
    }
    else {
        std::cout << "No encontrado." << std::endl;
    }
    return 0;
}
```

</details>

### Ejercicio 2: Contar

Usar `count` para contar cuántas veces aparece un número en un `vector<int>`.

<details>
<summary>Solución sugerida</summary>

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> numeros = {2, 3, 2, 5, 2, 1};
    int total = std::count(numeros.begin(), numeros.end(), 2);
    std::cout << "El número 2 aparece " << total << " veces." << std::endl;
    return 0;
}
```

</details>

### Ejercicio 3: Ordenar

Crear un vector de calificaciones y ordenarlas de mayor a menor usando `sort`.

<details>
<summary>Solución sugerida</summary>

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> calificaciones = {3, 5, 4, 2};
    std::sort(calificaciones.begin(), calificaciones.end(), std::greater<int>());

    for (int nota : calificaciones){
        std::cout << nota << " ";
    }
    return 0;
}
```

</details>

### Ejercicio 4: Acumular

Sumar todos los gastos registrados en un vector.

<details>
<summary>Solución sugerida</summary>

```cpp
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    std::vector<int> gastos = {1000, 2500, 3200};
    int total = std::accumulate(gastos.begin(), gastos.end(), 0);
    std::cout << "Total de gastos: $" << total << std::endl;
    return 0;
}
```

</details>



