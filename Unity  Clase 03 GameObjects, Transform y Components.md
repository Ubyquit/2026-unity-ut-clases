

> **Versión utilizada:** Unity 6.6 — `6000.6.3f1`  
> **Materia:** Desarrollo de Videojuegos  
> **Materia relacionada:** Gestión en el Desarrollo de Software

---

## 🎯 Objetivo de la clase

Al finalizar esta clase, el alumno será capaz de:

- Comprender qué es un **GameObject**.
    
- Crear y eliminar GameObjects.
    
- Identificar el componente **Transform**.
    
- Comprender **Position, Rotation y Scale**.
    
- Utilizar las herramientas de transformación del Scene View.
    
- Comprender la relación entre **GameObjects y Components**.
    
- Agregar y eliminar componentes.
    
- Comprender que los componentes permiten agregar características y comportamientos.
    
- Guardar los cambios realizados en una escena.
    
- Relacionar los cambios del proyecto con el control de versiones mediante **Git y GitHub**.
    

---

# 1. 🧱 ¿Qué es un GameObject?

En Unity, un **GameObject** es la unidad básica que utilizamos para representar objetos dentro de una escena.

Un GameObject puede representar prácticamente cualquier elemento de nuestro videojuego:

```
Player
Enemy
Bullet
Wall
Tree
Camera
Light
UI
```

Sin embargo, un GameObject por sí solo tiene una función muy básica.

Gran parte de sus características y comportamientos provienen de los **Components** que tiene asociados.

> 💡 **Idea clave**
> 
> Un GameObject es la base sobre la que construimos los elementos de nuestro videojuego.

---

# 2. 🧩 GameObject + Components

Uno de los conceptos más importantes de Unity es:

```
GameObject
     │
     ├── Component
     ├── Component
     ├── Component
     └── Component
```

Por ejemplo, un personaje podría estar formado por:

```
Player
│
├── Transform
├── Sprite Renderer
├── Rigidbody 2D
├── Box Collider 2D
└── PlayerController
```

Cada componente proporciona diferentes características al GameObject.

Por ejemplo:

|Component|Función|
|---|---|
|`Transform`|Posición, rotación y escala|
|`Sprite Renderer`|Permite mostrar un Sprite|
|`Rigidbody 2D`|Permite utilizar física 2D|
|`Collider 2D`|Permite detectar colisiones|
|`Script`|Permite agregar comportamiento mediante código|

> ⚠️ En esta clase solamente conoceremos estos componentes de manera general. Los estudiaremos individualmente más adelante.

---

# 3. 📐 El componente Transform

Todo GameObject tiene un componente fundamental:

```
Transform
```

El Transform determina principalmente:

- 📍 Position
    
- 🔄 Rotation
    
- 📏 Scale
    

Podemos pensar en él como la información que indica:

> **¿Dónde está el objeto, cómo está orientado y qué tamaño tiene?**

---

# 4. 📍 Position

La propiedad **Position** determina la ubicación del GameObject dentro de la escena.

En Unity utilizamos coordenadas:

```
X
Y
Z
```

Por ejemplo:

```
Position

X = 2
Y = 1
Z = 0
```

En un proyecto 2D normalmente trabajaremos principalmente con:

```
X → Horizontal
Y → Vertical
Z → Profundidad
```

### 🧠 Ejemplo

Si tenemos:

```
Player
Position:
X = 0
Y = 1
Z = 0
```

y cambiamos:

```
X = 5
```

el jugador se desplazará horizontalmente.

---

# 5. 🔄 Rotation

La propiedad **Rotation** determina la orientación del GameObject.

Utiliza también tres ejes:

```
X
Y
Z
```

Por ejemplo:

```
Rotation

X = 0
Y = 0
Z = 45
```

En un proyecto 2D será muy común utilizar principalmente el eje:

```
Z
```

para realizar rotaciones sobre el plano.

---

# 6. 📏 Scale

La propiedad **Scale** determina el tamaño relativo del GameObject.

Un objeto normalmente comienza con:

```
Scale

X = 1
Y = 1
Z = 1
```

Si modificamos:

```
X = 2
Y = 2
Z = 1
```

el objeto aumentará de tamaño en X e Y.

---

# 7. 🧭 Los tres ejes

Es importante comenzar a familiarizarse con:

```
        Y
        ↑
        │
        │
        └────────→ X

       Z
```

En un proyecto 2D:

```
X → izquierda / derecha
Y → arriba / abajo
Z → profundidad
```

> 💡 **Importante**
> 
> Los ejes forman parte del sistema de coordenadas que utilizaremos constantemente durante el desarrollo del videojuego.

---

# 8. 🛠️ Herramientas de transformación

Dentro del Scene View podemos utilizar diferentes herramientas para modificar nuestros GameObjects.

Las principales son:

### 🖐️ Hand Tool

Permite desplazarnos por la vista de la escena.

---

### ↔️ Move Tool

Permite mover un GameObject.

Podemos modificar su posición utilizando los ejes:

```
X
Y
Z
```

---

### 🔄 Rotate Tool

Permite modificar la rotación del objeto.

---

### 🔍 Scale Tool

Permite modificar el tamaño del objeto.

---

## 🧠 Relación entre las herramientas y Transform

Podemos visualizarlo así:

```
Herramienta
     │
     ▼
Transform
     │
     ├── Position
     ├── Rotation
     └── Scale
```

Por ejemplo:

```
Move Tool
     ↓
Position

Rotate Tool
     ↓
Rotation

Scale Tool
     ↓
Scale
```

---

# 9. 🧪 Primera práctica

Vamos a crear nuestro primer GameObject.

Podemos utilizar una figura básica:

```
GameObject
└── Cube
```

Una vez creado, seleccionamos el objeto y observamos su componente:

```
Transform
```

---

## Ejercicio 1 — Position

Modificar:

```
Position

X = 2
Y = 1
Z = 0
```

Observar el cambio en la Scene View.

---

## Ejercicio 2 — Rotation

Modificar:

```
Rotation

X = 0
Y = 0
Z = 45
```

Observar cómo cambia la orientación del objeto.

---

## Ejercicio 3 — Scale

Modificar:

```
Scale

X = 2
Y = 2
Z = 1
```

Observar cómo cambia su tamaño.

---

# 10. 🧩 Agregar componentes

Una de las características más importantes de Unity es que podemos agregar componentes a nuestros GameObjects.

Seleccionamos un GameObject y utilizamos:

```
Add Component
```

Desde ahí podemos buscar diferentes componentes.

Por ejemplo:

```
Rigidbody
```

o:

```
Box Collider
```

---

# 11. 🧠 ¿Por qué usamos Components?

Los componentes permiten construir objetos de manera modular.

Por ejemplo:

```
Player
│
├── Transform
│
├── Sprite Renderer
│
├── Rigidbody 2D
│
├── Collider 2D
│
└── PlayerController
```

Cada componente tiene una responsabilidad diferente.

Podemos pensarlo así:

```
Transform
    ↓
¿Dónde está?

Sprite Renderer
    ↓
¿Cómo se ve?

Collider
    ↓
¿Con qué puede chocar?

Rigidbody
    ↓
¿Cómo participa en la física?

Script
    ↓
¿Qué comportamiento tiene?
```

---

# 12. 🧠 Analogía

Podemos imaginar un GameObject como un personaje al que vamos agregando capacidades.

```
Player
│
├── Transform
│   └── Tiene una posición
│
├── Sprite Renderer
│   └── Tiene una apariencia
│
├── Collider
│   └── Puede detectar colisiones
│
├── Rigidbody
│   └── Puede participar en la física
│
└── Script
    └── Tiene comportamiento
```

De esta manera:

> **No necesitamos crear un tipo de objeto diferente para cada comportamiento. Podemos construirlo agregando componentes.**

Esta idea será fundamental durante todo el curso.

---

# 13. 🔗 Conexión con Gestión del Desarrollo de Software

Aunque esta clase corresponde principalmente a **Desarrollo de Videojuegos**, aquí aparece una conexión importante con:

> 🟩 **Gestión en el Desarrollo de Software**

Los componentes permiten trabajar de forma **modular**.

Un objeto puede estar formado por diferentes partes, cada una con una responsabilidad específica.

Por ejemplo:

```
Player
│
├── Movimiento
├── Física
├── Colisiones
├── Apariencia
└── Comportamiento
```

Esto posteriormente nos permitirá hablar de conceptos como:

- Modularidad.
    
- Reutilización.
    
- Mantenimiento.
    
- Separación de responsabilidades.
    
- Organización del código.
    

> 💡 **Idea clave**
> 
> La forma en que construimos nuestros objetos también afecta la facilidad con la que podremos mantener y modificar nuestro proyecto.

---

# 14. 🎮 Primera escena

Ahora vamos a crear una escena sencilla utilizando varios GameObjects.

Crearemos:

```
Player
Enemy
Platform
```

Para esta actividad podemos utilizar primitivas de Unity.

Por ejemplo:

```
Player → Cube
Enemy → Sphere
Platform → Cube
```

---

# 15. 📍 Configuración de los objetos

## Player

```
Player
Position

X = 0
Y = 1
Z = 0
```

---

## Enemy

```
Enemy
Position

X = 4
Y = 1
Z = 0
```

---

## Platform

```
Platform
Position

X = 2
Y = -1
Z = 0
```

Podemos modificar posteriormente la escala para que la plataforma sea más grande.

Por ejemplo:

```
Scale

X = 5
Y = 0.5
Z = 1
```

---

# 16. 🧪 Experimentación

Ahora los alumnos deberán experimentar libremente con:

- Position
    
- Rotation
    
- Scale
    

El objetivo no es obtener una escena específica.

El objetivo es observar:

> **¿Qué sucede cuando modificamos cada propiedad del Transform?**

---

# 17. 🧩 Agregar un componente adicional

Seleccionar:

```
Player
```

y agregar:

```
Rigidbody
```

> ⚠️ Todavía no necesitamos estudiar física en profundidad.

El objetivo es únicamente comprender que podemos agregar nuevas capacidades a un GameObject.

---

# 18. 💾 Guardar la escena

Después de realizar los cambios:

```
Guardar Scene
```

Es importante comenzar a adquirir el hábito de guardar frecuentemente.

Nuestro flujo será:

```
Modificar
   ↓
Guardar
   ↓
Probar
   ↓
Guardar nuevamente
```

---

# 19. 🔀 Relación con Git y GitHub

Ya tenemos nuestro repositorio configurado desde la primera clase.

Por lo tanto, los cambios que realizamos en Unity forman parte del proyecto que estamos gestionando mediante Git.

Nuestro flujo comienza a ser:

```
Crear GameObjects
        ↓
Modificar Transform
        ↓
Agregar Components
        ↓
Guardar Scene
        ↓
Git detecta cambios
        ↓
Commit
        ↓
Push
        ↓
GitHub
```

---

## 📝 Ejemplo de Commit

Un mensaje apropiado podría ser:

```
Agrega primeros GameObjects a la escena
```

o:

```
Crea escena inicial del videojuego
```

> 🔗 **Conexión con Gestión del Desarrollo de Software**
> 
> El objetivo no es solamente aprender a utilizar GitHub, sino comenzar a desarrollar el hábito de registrar los avances importantes del proyecto.

---

# 20. 🧪 Actividad de clase

## Actividad 02 — Construyendo nuestra primera escena

### Parte A — Crear objetos

Crear los siguientes GameObjects:

```
Player
Enemy
Platform
```

Utilizar primitivas de Unity.

---

### Parte B — Configurar Transform

Cada objeto deberá tener una posición diferente.

Ejemplo:

```
Player
X = 0
Y = 1
Z = 0
```

```
Enemy
X = 4
Y = 1
Z = 0
```

```
Platform
X = 2
Y = -1
Z = 0
```

---

### Parte C — Experimentar

Modificar libremente:

- Position
    
- Rotation
    
- Scale
    

Observar los resultados.

---

### Parte D — Components

Seleccionar uno de los GameObjects y agregar un componente adicional.

Ejemplo:

```
Player
└── Rigidbody
```

---

### Parte E — Guardar

Guardar la escena.

---

### Parte F — GitHub

Registrar los cambios:

```
Commit
   ↓
Push
   ↓
GitHub
```

---

# 21. 🧠 Preguntas de cierre

Antes de terminar la clase, responder:

### 1. ¿Qué es un GameObject?

---

### 2. ¿Qué componente tiene todo GameObject?

---

### 3. ¿Qué tres propiedades principales encontramos en Transform?

---

### 4. ¿Qué diferencia existe entre Position y Scale?

---

### 5. ¿Cómo podemos agregar nuevas capacidades a un GameObject?

---

### 6. ¿Para qué sirve un Component?

---

### 7. ¿Por qué puede ser útil dividir las características de un objeto en diferentes componentes?

---

# 22. 🎯 Resultado esperado

Al terminar la actividad, la escena deberá contener al menos:

```
Hierarchy
│
├── Main Camera
├── Directional Light
│
├── Player
├── Enemy
└── Platform
```

Y cada alumno deberá ser capaz de modificar:

```
Position
Rotation
Scale
```

desde el Inspector y mediante las herramientas de transformación.

---

# 🧠 Resumen de la clase

|Concepto|Función|
|---|---|
|**GameObject**|Unidad básica de una escena|
|**Component**|Agrega características o capacidades|
|**Transform**|Controla posición, rotación y escala|
|**Position**|Ubicación del objeto|
|**Rotation**|Orientación del objeto|
|**Scale**|Tamaño relativo del objeto|
|**Move Tool**|Modifica posición|
|**Rotate Tool**|Modifica rotación|
|**Scale Tool**|Modifica escala|
|**Add Component**|Permite agregar componentes|

---

# 🔑 Concepto fundamental

Durante esta clase debemos comenzar a pensar en Unity de esta manera:

```
┌─────────────────┐
│   GameObject    │
└────────┬────────┘
         │
         ▼
   ┌───────────┐
   │Components │
   └─────┬─────┘
         │
         ▼
┌────────────────────┐
│ Características y  │
│ comportamientos    │
└────────────────────┘
```

> **GameObject + Components = elementos que construyen nuestro videojuego.**

---

# 🔗 Integración entre materias

```
┌─────────────────────────────────┐
│     DESARROLLO DE VIDEOJUEGOS   │
│                                 │
│ GameObjects                     │
│ Transform                       │
│ Components                      │
│ Scenes                          │
│ Unity Editor                    │
└───────────────┬─────────────────┘
                │
                │ Integración
                ▼
┌─────────────────────────────────┐
│ GESTIÓN DEL DESARROLLO          │
│ DE SOFTWARE                     │
│                                 │
│ Modularidad                     │
│ Organización                    │
│ Separación de responsabilidades │
│ Git                             │
│ GitHub                          │
│ Control de versiones            │
└─────────────────────────────────┘
```

---

# 💡 Idea final

> Un videojuego no está formado simplemente por imágenes y escenarios.
> 
> Cada elemento que vemos en Unity está construido a partir de **GameObjects y Components**, y la manera en que organizamos estos elementos influirá directamente en qué tan fácil será desarrollar, mantener y trabajar en equipo sobre nuestro proyecto.
