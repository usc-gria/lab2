# LAB2: Evolución del Sistema de Música en Streaming con POO

## **Objetivos Generales**
1. Introducir los principios de la Programación Orientada a Objetos en Python.
2. Aplicar encapsulación para proteger los datos y mejorar la modularidad del código.
3. Utilizar herencia para organizar jerárquicamente las clases del sistema.
4. Implementar composición para estructurar mejor las relaciones entre objetos.
5. Introducir restricciones para un mejor manejo de datos y seguridad en la POO.

---

## **Tareas a realizar**

Debemos evolucionar nuestro sistema para hacer uso de la Programación Orientada a Objetos. Para ello vamos a cambiar nuestros diccionarios por clases y añadir alguna funcionalidad nueva. 

### **Creación de la Clase `Cancion`**
#### **Descripción:**
Vamos a crear la clase Canción, con las propiedades que teníamos en el diccionario. Todos sus atributos deben ser privados y tendremos que implementar getter y setters para cada uno.
- `id` (privado): Identificador único autoincrementado (igual que en lab1, no se añade hasta que se agrega al catálogo).
- `titulo` (privado): Título de la canción (str, no puede ser vacío).
- `artista` (privado): Nombre del artista (str, no puede ser vacío).
- `album` (privado): Nombre del álbum (str, permitimos canción sin album).
- `duracion` (privado): Duración de la canción en minutos (float, debe ser mayor a 0).
- `reproducciones` (privado): Contador de reproducciones (int, mayor o igual a 0).

#### **Métodos:**
- `reproducir()`: Incrementa el contador de reproducciones.
- Implementa `__str__()`  
- Métodos `getter` y `setter` con validaciones para evitar datos inconsistentes.

### **Creación de la Clase `Catalogo`**
- Contendrá dos lista de canciones: `actuales` y `eliminadas`. Ambos atributos tendrán setters y getters.
#### **Métodos:**
- `agregar_cancion(cancion)`: Añade una canción al catálogo si no está repetida (mismo título y artista).
- `eliminar_cancion(cancion)`: Elimina la canción dada de la lista `actuales` y la mueve a `eliminadas`.
- `buscar_por_artista(artista)`: Devuelve las canciones de un artista.
- `ordenar_por_reproducciones()`: Devuelve las canciones ordenadas por popularidad (nº reproducciones), de mayor a menor.
- `canciones_top_reproducciones(n)`: Igual que la anterior función pero solo las n canciones más populares, de mayor a menos.
- Métodos `getter` y `setter` con validaciones para evitar datos inconsistentes.

### **Creación de la Clase `ListaReproduccion`**
- `nombre` (privado): Nombre de la lista de reproducción.
- `canciones` (privado): Lista de canciones en la lista de reproducción.

#### **Métodos:**
- `agregar_cancion(catalogo,cancion)`: Añade una canción si no está duplicada, debe buscarla en la lista de canciones.
- `eliminar_cancion(cancion)`: Elimina una canción si existe.
- `reproducir_cancion(catalogo, cancion)`: Reproduce una canción y aumenta en uno el número de reproducciones
- `duracion_total_lista()`: Devuelve la duración total de la lista en horas, minutos y segundos (tip: usar la libreria datetime)
- `mostrar_lista_reproduccion()`: Muestra las canciones en la lista de reproducción. 
- Métodos `getter` y `setter` con validaciones para evitar datos inconsistentes.

### **Creación de la Clase `Usuario`**
- `nombre` (privado): Nombre del usuario.
- `favoritas` (privado): Lista de canciones favoritas del usuario.
- `listas_reproduccion` (privado): Lista de objetos `ListaReproduccion` asociadas al usuario.

#### **Métodos:**
  - `agregar_a_biblioteca(cancion)`: Añade una canción a su lista de favoritas si no está duplicada.
  - `ver_biblioteca()`: Muestra las canciones favoritas.
  - `crear_lista(nombre)`: Crea una nueva lista de reproducción y la asocia al usuario.
  - `eliminar_lista(nombre)`: Elimina una lista de reproducción por nombre si existe.
  - `getter` y `setter` con validaciones para proteger los datos.

### **Implementación de Herencia en Usuarios**
#### **Clase `UsuarioPremium` (hereda de `Usuario`)**
- Agrega el atributo `suscripcion_activa` (booleano, por defecto `False`).
- Método `descargar_cancion(cancion)`, que simula la descarga de una canción.
- Método `activar_suscripcion()`, que permite activar la suscripción premium.
- Método `canciones_descargas()` que muestra una lista de todas las canciones descargadas.

#### **Clase `UsuarioFree` (hereda de `Usuario`)**
- Restricción en la cantidad de canciones que puede agregar a la biblioteca (ejemplo: máximo 20 canciones).
- Método `ver_anuncio()`, que simula la visualización de un anuncio antes de reproducir una canción.



### **Implementación en el Programa Principal**
- Crear instancias de `Cancion`.
- Crear usuarios (Premium y Free) y añadir canciones a sus bibliotecas.
- Crear listas de reproducción y asignarlas a usuarios.
- Agregar canciones al catálogo y realizar consultas.
- Aplicar restricciones para validar la consistencia de los datos.

---

## **Entrega Final**
- Código bien estructurado y documentado.
- Uso correcto de encapsulación, herencia y composición.
- Aplicación de restricciones para garantizar un diseño seguro y robusto.
- Pruebas demostrando el funcionamiento de cada clase y método.

