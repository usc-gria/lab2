# LAB2: Evolución del Sistema de Música en Streaming con POO

## **Objetivos Generales**
1. Introducir los principios de la Programación Orientada a Objetos en Python.
2. Aplicar encapsulación para proteger los datos y mejorar la modularidad del código.
3. Utilizar herencia para organizar jerárquicamente las clases del sistema.
4. Implementar composición para estructurar mejor las relaciones entre objetos.
5. Introducir restricciones para un mejor manejo de datos y seguridad en la POO.

---

## **Tareas a realizar**

Debemos evolucionar nuestro sistema para hacer uso de la Programación Orientada a Objetos (POO). Para ello vamos a cambiar nuestros diccionarios por clases y añadir alguna funcionalidad nueva.
Es obligatorio que todas las clases implementen encapsulación (atributos privados y métodos de lectura/escritura). Es posible que sea necesaria la implementación de algún método a mayores para cubrir las funcionalidades que se piden.
Debes implementar la función especial `__str()__` en todas las clases.

Lee con especial atención la práctica COMPLETA, y antes de ponerte a programar, debes diseñar un modelo UML como los vistos en clase (puede ser en papel). Debes entregarlo junto con la práctica, como una imagen en formato PNG.

Todas las funciones de crear/eliminar deben devolver `True` si tienen éxito, o `False` si no consiguen realizarlo. Todas las funcionalidades adicionales necesarias (por ejemplo, antes de añadir una canción a la biblioteca de un usuario, este debe seleccionar qué canción quiere añadir del catálogo) deben implementarse en el `main.py`. 
Pueden implementarse funciones a mayores (siguiendo con el ejemplo anterior, puedo listarle todas las canciones del catálogo de una vez o primero mostrarle los artistas, seleccionar uno de ellos y luego sus canciones para seleccionar una de ellas). Este tipo de funcionalidades queda a decisión de cada uno.

Los nombres de las clases, sus atributos y métodos, así como el orden de los parámetros deben coincidir con lo que se define en este documento.

### **Creación de la Clase `Cancion`**
#### **Descripción:**
Vamos a crear la clase Canción, con las propiedades que teníamos en el diccionario. Cambiamos el valor de reproducciones a un atributo que sea popularidad de la canción y la duración es en segundos.
- `id` (privado): Identificador único autoincrementado (igual que en lab1, no se añade hasta que se agrega al catálogo).
- `titulo` (privado): Título de la canción (str, no puede ser vacío).
- `artista` (privado): Nombre del artista (str, no puede ser vacío).
- `album` (privado): Nombre del álbum (str, permitimos canción sin album).
- `duracion` (privado): Duración de la canción en segundos (float, debe ser mayor a 0).
- `popularidad` (privado): Contador de reproducciones (int, mayor o igual a 0).

#### **Métodos Adicionales:**
- `duracion_formateada()`: Devuelve un string con la duración formateada min:seg (tip: usar la función proporcionada en `utils.py`)
- `es_mas_larga(otra_cancion)`: Devuelve `True` si la canción actual tiene una duración mayor que la otra. En cualquier otro caso, `False`.
- `mismo_artista(otra_cancion)`: Devuelve `True` si ambas canciones pertenecen al mismo artista, ignorando mayúsculas y minúsculas. En cualquier otro caso, `False`.
- `mismo_album(otra_cancion)`: Devuelve `True` si ambas canciones pertenecen al mismo álbum, ignorando mayúsculas y minúsculas. En cualquier otro caso, `False`.
- `es_mas_popular(otra_cancion)`: Devuelve `True` si la canción actual tiene más reproducciones que la otra. En cualquier otro caso, `False`.

### **Creación de la Clase `Catalogo`**
- Contendrá dos lista de canciones: `actuales` y `eliminadas`.
#### **Métodos Adicionales:**
- `agregar_cancion(cancion)`: Añade una canción al catálogo si no está repetida (mismo título y artista).
- `eliminar_cancion(cancion)`: Elimina la canción dada de la lista `actuales` y la mueve a `eliminadas`.
- `buscar_por_artista(artista)`: Devuelve las canciones de un artista.
- `canciones_top_populares(n)`: Igual que la anterior función pero solo las n canciones más populares, de mayor a menos.

### **Creación de la Clase `ListaReproduccion`**
- `nombre` (privado): Nombre de la lista de reproducción.
- `canciones` (privado): Lista de canciones en la lista de reproducción.
- `fecha_creacion` (privado): Fecha de creación de la playlist (usar la clase `date` de libreria datetime `from datetime import date`)

#### **Métodos Adicionales:**
- `agregar_cancion(cancion)`: Añade una canción del catálogo si no está duplicada.
- `eliminar_cancion(cancion)`: Elimina una canción si existe.
- `ordenar_lista_por_popularidad()`: Devuelve las canciones de una lista, ordenadas de mayor a menor por popularidad
- `duracion_total_lista()`: Devuelve la duración total de la lista en horas, minutos y segundos (tip: usar la función proporcionada en `utils.py`)
- `mostrar_lista_reproduccion()`: Muestra las canciones en la lista de reproducción. 

### **Creación de la Clase `Usuario`**
- `nombre` (privado): Nombre del usuario.
- `password` (privado): Contraseña para entrar en el sistema
- `biblioteca` (privado): Lista de diccionarios de las canciones favoritas de usuarios de la siguiente forma:
  - `{"cancion": cancion, "descargada": False`}, donde `cancion` es un objeto de la clase Cancion que existe en el catálogo. La canción no se encuentra descargada cuando se agrega.
- `listas_reproduccion` (privado): Lista de `ListaReproduccion` del usuario.
- `amigos` (privado): Lista de `Usuarios` amigos.

#### **Métodos Adicionales:**
  - `agregar_a_biblioteca(cancion)`: Añade una canción a su lista de favoritas si no está duplicada.
  - `ver_biblioteca()`: Muestra las canciones favoritas.
  - `eliminar_cancion_biblioteca(cancion)`: Elimina una canción de su lista favorita.
  - `crear_lista(nombre)`: Crea una nueva lista de reproducción y la asocia al usuario.
  - `eliminar_lista(nombre)`: Elimina una lista de reproducción por nombre si existe.

### **Implementación de Herencia**
#### **Clase `UsuarioPremium`**
- Agrega el atributo `listas_reproduccion_seguidas`: Lista de las listas seguidas por el usuario de sus amigos. 
- Son los únicos usuarios que pueden descargar canciones.
- Método `descargar_cancion(cancion)`, que simula la descarga de una canción de la biblioteca cambiando su valor en el diccionario de la biblioteca.
- Método `canciones_descargadas()` que muestra una lista de todas las canciones descargadas.
- Método `eliminar_descarga(cancion)` cambiando su valor en el diccionario de la biblioteca a `False`. 
- Método `seguir_lista_reproduccion(lista_reproduccion)`: Añade una lista de reproducción a listas seguidas por el usuario. Debe ser una lista de alguno de sus amigos.

#### **Clase `UsuarioFree`**
- Agrega el atributo `fecha_registro` (privado): Fecha en la que se dio de alta en el sistema. Debe ser una instancia de alguna clase de la librería datetime.
- Método `ver_anuncio()`: que simula la visualización de un anuncio antes crear una lista de reproducción o agregar una canción a la biblioteca. Puedes usar el método de `utils.py`.
- Método `comprobar_fecha()`: Comprueba si la fecha de registro es mayor a 2 años desde la actualidad. En caso de ser verdadero, debe ver dos anuncios, en vez de uno. Usa la librería datetime

#### **Clase `ListaPublica`**
- Esta lista no está asociada a ningún usuario, son listas por defecto proporcionadas por el sistema.
- Agrega el atributo de `valoraciones`: Lista de valoraciones, con números de estrellas entre 1 y 5.
- Agrega el atributo de `seguidores`: Lista de usuarios que siguen esta lista. 
- Método `valoracion_media()`: Devuelve la media de las valoraciones.
- Método `agregar_seguidor(usuario)`: Añade un usuario a la lista de seguidores si aún no la sigue.
- Método `eliminar_seguidor(usuario)`: Elimina un usuario


### **Implementación en el Programa Principal**
Implementa un programa principal que permita gestionar usuarios, catálogo y listas de reproducción.

El programa debe empezar ya con al menos 10 canciones en el catálogo, 4 usuarios (2 Premium y 2 Free) y 3 Listas Públicas (e.g., Clásicos, Rock, Urbana) con al menos 3 canciones cada lista. 
Puedes implementar una función en el `main.py` que "rellene" tus listas con los objetos necesarios por defecto. 
Tienes un archivo `utils.py` con tres funciones que pueden ser de ayuda:

- `buscar_canciones_apple_music(query, numero_canciones)` (necesario internet): Hace una petición a la base de datos de Apple Music con los siguientes parámetros:
  - query: puedes usar una o varias palabras (por ejemplo: `the rapants` o `boyanka kostova`, también funcionaría con títulos como `Muinheira De Interior`)
  - numero_de_canciones: número de canciones máximas que te devuelve de la búsqueda, por defecto su valor es 1.
  - Devuelve un diccionario de canciones con el siguiente formato (duración en segundos): `{"titulo": nombre, "artista": artista, "album": album, "duracion": duracion_seg, "popularidad": popularidad}`
- `convertir_seg_a_min_seg(segundos)`: Convierte un tiempo en segundos al formato MM:SS, en formato string
- `mostrar_anuncio(anuncio)`: Que simula la visión de un anuncio y lo ejecuta 3 segundos.

El primer menú que se debe mostrar debería ser la entrada del usuario administrador:
```python
print("\n=== SISTEMA DE MÚSICA EN STREAMING ===")
print("1. Iniciar sesión como Usuario")
print("2. Gestionar catálogo de canciones")
print("3. Gestionar listas de reproducción públicas")
print("4. Gestionar usuarios")
print("5. Salir")
```
La opción `2` deben permitir añadir o eliminar canciones al catálogo, además de llamar a las funcionalidades implementadas (del catálogo y de canciones).
La opción `3` debe permitir añadir o eliminar listas públicas. 
La opción `4` debe permitir añadir o eliminar usuarios del sistema.

El menú de usuario, una vez iniciada correctamente la sesión (comprobándolo en la lista_usuarios con nombre y password), debe permitir:
```python
print("1. Ver mi biblioteca")
print("2. Gestionar canciones de la biblioteca")
print("3. Gestionar lista de reproducción")
print("4. Gestionar amigos")
print("5. Cerrar sesión")
```

Donde la opción `2` permite añadir o eliminar canciones de la biblioteca. Si es UsuarioPremium, también se le permitirá descargar las canciones de su lista.

La opción `3` permite crear o eliminar listas de reproducción y añadir o eliminar canciones de listas ya creadas. Permite buscar listas públicas, seguirlas y valorarlas.
Además, permite buscar en las listas y ejecutar las funciones implementadas `ordenar_lista_por_popularidad(), duracion_total_lista(), mostrar_lista_reproduccion()`
Si es usuario premium, además permitirá seguir otras listas de reproducción de los amigos del usuario.

La opción `4` permite gestionar a los amigos, añadiéndolos o eliminándolos según la lista de usuarios dados de alta en el sistema.


## **Consejos**
Comienza desarrollando y PROBANDO cada una de las clases individualmente. Vete paso a paso implementando cada una de las funcionalidades y testando cada parte individualmente.
Ten en cuenta que si eliminamos un objeto de alguna de las listas, debemos eliminar ese objeto en el resto de listas asociadas. 
Por ejemplo, si se elimina un usuario, y ese usuario es seguidor de listas públicas, debería eliminarse de esa lista. Igualmente con las canciones del catálogo.


## **Entrega Final**
- Código bien estructurado y documentado.
- Uso correcto de encapsulación, herencia y composición.
- Aplicación de restricciones para garantizar un diseño seguro y robusto.
- Pruebas demostrando el funcionamiento del programa en general

