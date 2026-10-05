
> **Versión utilizada:** Unity 6.6 — `6000.6.3f1`  
> **Materia:** Desarrollo de Videojuegos  
> **Materia relacionada:** Gestión en el Desarrollo de Software

---

## 🎯 Objetivo de la clase

Al finalizar esta clase, el alumno será capaz de:

- Identificar las principales ventanas del **Unity Editor**.
    
- Comprender la función de **Hierarchy, Scene, Game, Inspector y Project**.
    
- Diferenciar los objetos de una escena de los archivos y recursos del proyecto.
    
- Crear una estructura básica y organizada de carpetas.
    
- Comprender la importancia de mantener organizado un proyecto de software.
    
- Relacionar la organización del proyecto con el trabajo colaborativo mediante **Git y GitHub**.
    

---

# 1. 🧩 ¿Qué es el Unity Editor?

El **Unity Editor** es el entorno de trabajo donde construiremos nuestro videojuego.

Unity divide el editor en diferentes ventanas. Cada una tiene una función específica y, al trabajar juntas, permiten construir, configurar, probar y organizar nuestro proyecto.

La distribución puede modificarse dependiendo de las necesidades del desarrollador, pero algunas ventanas son fundamentales.

> 💡 **Idea clave**
> 
> Unity no es una sola ventana donde hacemos todo.
> 
> Cada ventana tiene una responsabilidad diferente.

---

# 2. 🖥️ Interfaz principal del Unity Editor

Las principales áreas que trabajaremos durante esta clase son:

1. **Hierarchy**
    
2. **Scene**
    
3. **Game**
    
4. **Inspector**
    
5. **Project**
    

La documentación de Unity describe estas ventanas como partes fundamentales de la interfaz del Editor.

  

> ⚠️ **Nota:** La distribución visual puede variar dependiendo del layout seleccionado y de la versión de Unity.

---

# 3. 🌳 Hierarchy

## ¿Qué es?

La ventana **Hierarchy** muestra los **GameObjects que forman parte de las escenas actualmente cargadas**.

Ejemplo:

```
Hierarchy
│
├── Main Camera
├── Directional Light
├── Player
├── Enemy
└── Environment
```

Cada objeto que forma parte de una escena aparece representado dentro de la Hierarchy.

Unity describe esta ventana como una representación jerárquica de los GameObjects presentes en la escena.

### 🧠 Pregunta clave

> **Hierarchy = ¿Qué objetos existen en mi escena?**

---

## 🌳 La palabra "Hierarchy"

La palabra **Hierarchy** significa **jerarquía**.

Los objetos pueden organizarse formando relaciones padre-hijo.

Por ejemplo:

```
Player
│
├── Body
├── Weapon
└── Camera
```

Esto será especialmente importante cuando posteriormente trabajemos con personajes, objetos compuestos y estructuras más complejas.

> 💡 Por ahora no necesitamos profundizar en las relaciones padre-hijo. Solo debemos entender que la Hierarchy representa la estructura de los objetos de la escena.

---

# 4. 🎬 Scene

La ventana **Scene** es el espacio donde podemos **visualizar, editar y construir nuestra escena**.

Aquí podemos:

- Mover objetos.
    
- Rotar objetos.
    
- Escalar objetos.
    
- Colocar personajes.
    
- Diseñar escenarios.
    
- Colocar cámaras.
    
- Colocar luces.
    
- Organizar elementos del nivel.
    

Unity permite trabajar la Scene desde una perspectiva 2D o 3D dependiendo del proyecto.

### 🧠 Pregunta clave

> **Scene = ¿Dónde estoy construyendo mi mundo?**

---

# 5. 🎮 Game

La ventana **Game** representa lo que el jugador verá a través de las cámaras del juego.

Es importante comprender que:

> **Scene y Game NO son lo mismo.**

### Scene

Nosotros estamos construyendo y editando el mundo.

### Game

Estamos observando cómo se verá el juego desde la perspectiva de las cámaras.

---

## 🔎 Ejemplo

Podemos estar viendo esto en la Scene:

```
        🏠
   🌳        🌳

       👤

             📷
```

Pero la cámara puede estar apuntando solamente hacia:

```
┌─────────────────────┐
│                     │
│       🏠            │
│                     │
│          👤         │
│                     │
└─────────────────────┘
```

El jugador verá lo que capture la cámara, no necesariamente todo lo que nosotros vemos en la Scene.

Unity define la Game View como una simulación del resultado que se verá a través de las cámaras de la escena.

---

# 6. 🔍 Inspector

El **Inspector** permite visualizar y modificar las propiedades del objeto actualmente seleccionado.

Por ejemplo, si seleccionamos:

```
Player
```

podemos encontrar componentes como:

```
Transform
Sprite Renderer
Rigidbody 2D
Collider 2D
Player Controller
```

El contenido del Inspector cambia dependiendo del objeto que seleccionemos.

### 🧠 Pregunta clave

> **Inspector = ¿Qué características y componentes tiene este objeto?**

---

# 7. 🧩 GameObjects y Components

Una de las ideas fundamentales que comenzaremos a trabajar en Unity es la relación:

```
GameObject
     +
Components
```

Por ejemplo:

```
Player
│
├── Transform
├── Sprite Renderer
├── Rigidbody 2D
├── Collider 2D
└── PlayerController
```

Cada componente agrega diferentes características o comportamientos al GameObject.

> 💡 **Importante**
> 
> Hoy solamente conoceremos esta idea.
> 
> Más adelante estudiaremos cada componente con mayor profundidad.

---

# 8. 📁 Project

La ventana **Project** muestra los recursos y archivos disponibles dentro del proyecto.

Aquí encontraremos nuestros:

- Scripts
    
- Sprites
    
- Prefabs
    
- Scenes
    
- Materials
    
- Audio
    
- Animations
    
- Configuraciones
    
- Otros Assets
    

Unity describe la Project Window como la biblioteca de Assets disponibles para utilizar dentro del proyecto.

### 🧠 Pregunta clave

> **Project = ¿Qué archivos y recursos existen dentro de mi proyecto?**

---

# 9. ⚠️ Hierarchy vs Project

Esta diferencia es **muy importante**.

## 🌳 Hierarchy

Representa los **GameObjects que existen dentro de la escena**.

```
Hierarchy
│
├── Main Camera
├── Player
└── Enemy
```

## 📁 Project

Representa los **archivos y recursos disponibles en el proyecto**.

```
Project
│
├── Scenes
├── Scripts
├── Prefabs
└── Sprites
```

### 🧠 Ejemplo

Podemos tener:

```
Project
└── Prefabs
    └── Player.prefab
```

aunque ese prefab **todavía no esté colocado dentro de la escena**.

Por lo tanto:

> Un archivo puede existir en el proyecto sin estar actualmente dentro de la escena.

---

# 10. 🗂️ Estructura inicial del proyecto

Unity crea algunas carpetas automáticamente.

Por ejemplo:

```
Assets
│
├── Scenes
└── Settings
```

No necesitamos duplicarlas.

Para comenzar nuestro proyecto agregaremos:

```
Assets
│
├── Scenes
├── Settings
│
├── Scripts
├── Prefabs
└── Sprites
```

---

# 11. 📜 Scripts

La carpeta:

```
Scripts
```

contendrá nuestros archivos de código.

Ejemplo:

```
Scripts
│
├── PlayerController.cs
├── EnemyController.cs
└── GameManager.cs
```

Posteriormente aprenderemos a crear y utilizar estos scripts desde Unity.

---

# 12. 🧱 Prefabs

La carpeta:

```
Prefabs
```

será utilizada para almacenar nuestros **Prefabs**.

Un Prefab permite guardar un GameObject junto con su configuración y componentes para poder reutilizarlo.

Ejemplo:

```
Prefabs
│
├── Player.prefab
├── Enemy.prefab
└── Bullet.prefab
```

> 💡 Los Prefabs los estudiaremos con mayor profundidad posteriormente.

---

# 13. 🖼️ Sprites

La carpeta:

```
Sprites
```

será utilizada principalmente para nuestros recursos gráficos 2D.

Ejemplo:

```
Sprites
│
├── Player.png
├── Enemy.png
├── Coin.png
└── Background.png
```

Más adelante podremos crear estructuras más específicas si el proyecto lo necesita.

---

# 14. 🏗️ ¿Por qué organizar las carpetas?

Aquí aparece una conexión directa con **Gestión en el Desarrollo de Software**.

Organizar las carpetas no es solamente una cuestión estética.

Estamos trabajando con un **proyecto de software**.

Imaginemos que cinco personas trabajan en el mismo videojuego y todos guardan sus archivos de cualquier manera:

```
Assets
│
├── cosas
├── cosas2
├── final
├── final2
├── ahora_si
├── prueba
├── prueba_final
└── NO_BORRAR
```

😅

Encontrar un archivo se convierte rápidamente en un problema.

Por eso estableceremos desde el inicio una regla:

> **Cada recurso debe almacenarse en la carpeta correspondiente a su función.**

---

# 🔗 Conexión con Gestión del Desarrollo de Software

Esta parte de la clase pertenece principalmente a:

> 🟦 **Desarrollo de Videojuegos**

pero tiene una conexión directa con:

> 🟩 **Gestión en el Desarrollo de Software**

La organización del proyecto facilita:

- Mantenimiento.
    
- Trabajo colaborativo.
    
- Localización de archivos.
    
- Integración de cambios.
    
- Comprensión del proyecto por otros integrantes.
    
- Control de versiones.
    

---

# 15. 🔀 Relación con Git y GitHub

Durante la clase anterior configuramos nuestro proyecto y repositorio.

El proyecto de Unity ya se encuentra relacionado con nuestro repositorio de GitHub.

Por lo tanto, podemos visualizar nuestro flujo de trabajo de esta manera:

```
        UNITY
          │
          │
          ▼
   Modificamos proyecto
          │
          ▼
       Git detecta
       los cambios
          │
          ▼
        Commit
          │
          ▼
         Push
          │
          ▼
       GITHUB
```

Esto nos permite comenzar a entender una idea fundamental:

> **Nuestro videojuego también es un proyecto de software que necesita ser gestionado.**

---

# 16. 🧑‍💻 Actividad práctica

## Actividad 01 — Preparación del proyecto

### Paso 1

Abrir el proyecto creado durante la clase anterior.

---

### Paso 2

Identificar las siguientes ventanas:

- Hierarchy
    
- Scene
    
- Game
    
- Inspector
    
- Project
    

---

### Paso 3

Dentro de:

```
Assets
```

crear las siguientes carpetas:

```
Scripts
Prefabs
Sprites
```

---

### Paso 4

Comprobar que ya existen:

```
Scenes
Settings
```

No crear duplicados.

---

### Paso 5

Guardar los cambios realizados en el proyecto.

---

### Paso 6

Realizar el proceso correspondiente de control de versiones:

```
Cambios
   ↓
Commit
   ↓
Push
   ↓
GitHub
```

El commit deberá describir claramente qué se realizó.

Ejemplo:

```
Organización inicial del proyecto
```

---

# 17. ✅ Resultado esperado

Al terminar la actividad, el proyecto deberá tener una estructura similar a:

```
Assets
│
├── Scenes
│
├── Settings
│
├── Scripts
│
├── Prefabs
│
└── Sprites
```

Y el alumno deberá poder explicar:

> **¿Qué es cada ventana del Unity Editor y para qué sirve?**

---

# 🧠 Resumen de la clase

|Elemento|¿Para qué sirve?|
|---|---|
|🌳 **Hierarchy**|Muestra los GameObjects de la escena|
|🎬 **Scene**|Permite visualizar y editar la escena|
|🎮 **Game**|Muestra la vista del juego mediante las cámaras|
|🔍 **Inspector**|Permite consultar y modificar propiedades y componentes|
|📁 **Project**|Contiene los Assets y archivos del proyecto|

---

# 🎯 Conceptos que debemos recordar

### Hierarchy

> **Objetos que existen en la escena.**

### Scene

> **Lugar donde construimos y editamos nuestro mundo.**

### Game

> **Lo que el jugador verá a través de las cámaras.**

### Inspector

> **Propiedades y componentes del objeto seleccionado.**

### Project

> **Archivos y recursos disponibles en nuestro proyecto.**

---

# 🔗 Relación entre las materias

```
┌──────────────────────────────┐
│    DESARROLLO DE VIDEOJUEGOS │
│                              │
│ Unity                        │
│ Scenes                       │
│ GameObjects                  │
│ Components                   │
│ Assets                       │
└──────────────┬───────────────┘
               │
               │ Integración
               ▼
┌──────────────────────────────┐
│ GESTIÓN DEL DESARROLLO       │
│ DE SOFTWARE                  │
│                              │
│ Organización                 │
│ Git                          │
│ GitHub                       │
│ Control de versiones         │
│ Trabajo colaborativo         │
└──────────────────────────────┘
```

> 💡 **Idea final**
> 
> Un videojuego no solamente se construye.
> 
> También se **organiza, versiona, documenta y gestiona**.

---

## 📚 Referencia

La estructura y descripción general de las ventanas del Editor se basa en la documentación oficial de Unity.

**Versión utilizada en el curso:**

```
Unity 6.6
6000.6.3f1
```
