> **Versión utilizada:** Unity 6.6 — `6000.6.3f1`  
> **Materia:** Desarrollo de Videojuegos  
> **Materia relacionada:** Gestión en el Desarrollo de Software

---

# 🎯 Objetivo de la clase

Al finalizar esta clase serás capaz de:

- Comprender qué es un Script dentro de Unity.
    
- Crear un Script utilizando C#.
    
- Asociar un Script a un GameObject.
    
- Comprender la estructura básica de un Script de Unity.
    
- Utilizar `Update()`.
    
- Detectar teclas mediante `Input.GetKey()`.
    
- Comprender qué es el **Legacy Input Manager**.
    
- Configurar Unity para utilizar el sistema de entrada antiguo.
    
- Crear un movimiento básico mediante teclado.
    
- Modificar un Script existente para utilizar diferentes teclas.
    
- Modificar el color de un Sprite mediante código.
    
- Comprender cómo diferentes Scripts pueden trabajar sobre un mismo GameObject.
    
- Investigar y consultar documentación antes de buscar una solución mediante IA.
    

---

# 1. 💻 ¿Qué es un Script?

Hasta ahora hemos trabajado con GameObjects y Components.

Ahora aprenderemos a agregar algo nuevo:

```
GameObject
     │
     ├── Transform
     ├── Sprite Renderer
     ├── Rigidbody 2D
     ├── Collider 2D
     └── Script
```

Un **Script** es un archivo de código que permite agregar comportamiento a nuestros GameObjects.

En Unity utilizaremos principalmente el lenguaje:

> **C#**

Por ejemplo, podemos crear Scripts para:

- Mover un personaje.
    
- Abrir una puerta.
    
- Cambiar un color.
    
- Crear enemigos.
    
- Contar puntos.
    
- Controlar una cámara.
    
- Crear un menú.
    
- Detectar colisiones.
    
- Reproducir sonidos.
    
- Crear reglas del juego.
    

---

# 2. 🧠 GameObject + Components + Scripts

Recordemos el concepto de la clase anterior:

```
GameObject
     │
     ├── Components
     │
     └── Scripts
```

Un Script también puede convertirse en un **Component** de nuestro GameObject.

Por ejemplo:

```
Player
│
├── Transform
├── Sprite Renderer
├── Rigidbody 2D
├── Collider 2D
└── Movimiento
```

Nuestro Script `Movimiento` ahora forma parte del GameObject.

---

# 3. 🧩 ¿Por qué utilizamos Scripts?

Los componentes que ya conocemos permiten darle diferentes características a nuestros objetos.

Por ejemplo:

```
Transform
    ↓
Ubicación

Sprite Renderer
    ↓
Apariencia

Rigidbody 2D
    ↓
Física

Collider 2D
    ↓
Colisiones
```

Pero necesitamos una forma de definir **comportamientos personalizados**.

Ahí entran los Scripts:

```
Script
   ↓
Comportamiento personalizado
```

Por ejemplo:

```
Player
   ↓
Movimiento.cs
   ↓
El jugador puede moverse
```

---

# 4. 🔎 Antes de programar: investigar

Cuando tenemos un problema de programación, no siempre sabemos inmediatamente qué función necesitamos.

Supongamos que queremos detectar cuando el jugador presiona una tecla.

Tenemos que investigar:

> **¿Cómo detectamos una tecla en Unity mediante C#?**

Una buena forma de trabajar es:

```
Problema
   ↓
Investigar
   ↓
Consultar documentación
   ↓
Encontrar una posible solución
   ↓
Probar
   ↓
Analizar
   ↓
Modificar
```

La documentación oficial es una de las principales herramientas de un desarrollador.

---

# 5. 🤖 ¿Y la Inteligencia Artificial?

La IA puede ser una herramienta muy útil para programar.

Sin embargo:

> **Utilizar IA no significa dejar de comprender el código.**

Un mal flujo sería:

```
Necesito mover un personaje
        ↓
"IA, dame el código"
        ↓
Copiar
        ↓
Pegar
        ↓
No funciona
        ↓
No sabemos por qué
```

Un mejor flujo es:

```
Problema
   ↓
Investigar
   ↓
Documentación
   ↓
Intentar resolver
   ↓
Probar
   ↓
Analizar errores
   ↓
Utilizar IA como apoyo
   ↓
Comprender la solución
```

> 💡 **Regla importante**
> 
> La IA puede ayudarte a escribir código, pero debes ser capaz de explicar qué hace el código que estás utilizando.

---

# 6. 🎮 Nuestro primer problema

Tenemos un GameObject:

```
Player
```

Queremos que se mueva utilizando las flechas:

```
        ↑
        |
    ←   Player   →
        |
        ↓
```

Necesitamos detectar si una tecla está siendo presionada.

Una de las funciones disponibles en el sistema de entrada antiguo de Unity es:

```
Input.GetKey()
```

---

# 7. ⌨️ Input.GetKey()

La función:

```
Input.GetKey()
```

permite comprobar si una tecla está siendo presionada.

Por ejemplo:

```
Input.GetKey(KeyCode.Space)
```

significa:

> ¿La tecla `Space` está siendo presionada?

También podemos utilizar:

```
Input.GetKey(KeyCode.LeftArrow)
```

para detectar la flecha izquierda.

---

# 8. 🔎 ¿Cuándo utilizar GetKey?

`Input.GetKey()` es útil cuando queremos realizar una acción **mientras una tecla permanece presionada**.

Ejemplos:

```
Mantener ←
    ↓
Mover jugador

Mantener W
    ↓
Avanzar

Mantener Shift
    ↓
Correr
```

Conceptualmente:

```
Tecla presionada
       ↓
Input.GetKey()
       ↓
Acción continua
```

---

# 9. ⚠️ Un problema importante

Si utilizamos:

```
Input.GetKey()
```

podemos encontrarnos con que el código **no funciona** dependiendo de la configuración de entrada del proyecto.

¿Por qué?

Porque Unity cuenta con diferentes sistemas de entrada.

Actualmente existe un sistema moderno:

> **Input System**

pero también existe el sistema anterior:

> **Input Manager / Legacy Input**

Nuestro código utilizará:

```
Input.GetKey()
```

por lo que necesitamos habilitar el sistema correspondiente.

---

# 10. 🎛️ Legacy Input Manager

El sistema antiguo de entrada permite utilizar APIs como:

```
Input.GetKey()
Input.GetKeyDown()
Input.GetKeyUp()
```

Para utilizar este sistema debemos revisar la configuración del proyecto.

Ruta:

```
Edit
   ↓
Project Settings
   ↓
Player
   ↓
Other Settings
   ↓
Active Input Handling
```

Dependiendo de la configuración encontraremos opciones relacionadas con:

```
Input System Package (New)
Input Manager (Old)
Both
```

Para utilizar nuestro código seleccionaremos:

```
Input Manager (Old)
```

Unity puede solicitar reiniciar el Editor para aplicar el cambio.

---

# 🧠 ¿Por qué es importante?

Esto nos enseña algo importante:

> **El código depende de las herramientas y APIs que estamos utilizando.**

Nuestro código:

```
Input.GetKey()
```

está relacionado con:

```
Input Manager (Old)
```

Por eso, cuando algo no funciona, no debemos asumir inmediatamente que el código está mal.

Debemos revisar:

```
Código
   +
Configuración
   +
Documentación
```

---

# 11. 📜 Crear nuestro primer Script

Dentro de:

```
Assets
└── Scripts
```

crearemos:

```
Movimiento.cs
```

Nuestro primer Script será:

```
using UnityEngine;

public class Movimiento : MonoBehaviour
{
    public float velocidad = 5f;

    void Update()
    {
        if (Input.GetKey(KeyCode.LeftArrow))
        {
            transform.Translate(Vector3.left * velocidad * Time.deltaTime);
        }

        if (Input.GetKey(KeyCode.RightArrow))
        {
            transform.Translate(Vector3.right * velocidad * Time.deltaTime);
        }

        if (Input.GetKey(KeyCode.UpArrow))
        {
            transform.Translate(Vector3.up * velocidad * Time.deltaTime);
        }

        if (Input.GetKey(KeyCode.DownArrow))
        {
            transform.Translate(Vector3.down * velocidad * Time.deltaTime);
        }
    }
}
```

---

# 12. 🔍 Analizando nuestro código

No se trata de memorizar el código.

Lo importante es comprender qué hace cada parte.

---

## `using UnityEngine;`

```
using UnityEngine;
```

Permite utilizar clases y funcionalidades proporcionadas por Unity.

Por ejemplo:

```
MonoBehaviour
Vector3
Input
KeyCode
Time
```

### ¿Cuándo aparece?

Prácticamente en muchos Scripts de Unity que necesiten utilizar funcionalidades del motor.

---

# 13. `public class Movimiento`

```
public class Movimiento : MonoBehaviour
```

Estamos creando una clase llamada:

```
Movimiento
```

y la estamos haciendo heredar de:

```
MonoBehaviour
```

Esto permite que Unity pueda utilizar nuestro Script como un Component.

Podemos imaginarlo así:

```
MonoBehaviour
      ↑
      │
Movimiento
```

---

# 14. 🧩 `MonoBehaviour`

```
MonoBehaviour
```

Es una clase fundamental de Unity para crear Scripts que puedan asociarse a GameObjects.

Gracias a esto podemos utilizar funciones como:

```
Start()
Update()
```

y acceder a elementos del GameObject.

### Ejemplos de uso

Un Script que:

- Controle un personaje.
    
- Controle un enemigo.
    
- Controle una cámara.
    
- Abra una puerta.
    
- Administre un objeto del juego.
    

---

# 15. ⚙️ Variable `velocidad`

```
public float velocidad = 5f;
```

Aquí estamos creando una variable llamada:

```
velocidad
```

de tipo:

```
float
```

y su valor inicial es:

```
5
```

Al utilizar `public`, podremos modificarla desde el Inspector.

Por ejemplo:

```
Movimiento
└── Velocidad
      5
```

Podemos cambiarla a:

```
2
5
10
20
```

sin modificar directamente el código.

### ¿Cuándo es útil?

Por ejemplo, podemos tener:

```
Player
Velocidad = 5

Enemy
Velocidad = 2

Boss
Velocidad = 1
```

Todos pueden utilizar el mismo tipo de comportamiento, pero con diferentes valores.

---

# 16. 🔄 `Update()`

```
void Update()
```

`Update()` es un método que Unity ejecuta continuamente mientras el juego está funcionando.

Conceptualmente:

```
Juego
 ↓
Update()
 ↓
Update()
 ↓
Update()
 ↓
Update()
 ↓
...
```

Por eso es común utilizarlo para revisar entradas del jugador.

### Ejemplos

Dentro de `Update()` podemos comprobar:

- Teclas.
    
- Mouse.
    
- Estados.
    
- Condiciones.
    
- Acciones que deben revisarse constantemente.
    

---

# 17. `if`

Nuestro código utiliza:

```
if (Input.GetKey(KeyCode.LeftArrow))
```

`if` permite ejecutar código solamente cuando una condición es verdadera.

Conceptualmente:

```
¿Se presiona ←?
      │
   ┌──┴──┐
   │     │
  Sí     No
   │     │
Mover   Nada
```

### Ejemplo sencillo

```
if (velocidad > 0)
{
    Debug.Log("El jugador puede moverse");
}
```

---

# 18. `Input.GetKey()`

```
Input.GetKey(KeyCode.LeftArrow)
```

Comprueba si una tecla está siendo presionada.

Algunos ejemplos:

```
Input.GetKey(KeyCode.Space)
Input.GetKey(KeyCode.A)
Input.GetKey(KeyCode.W)
Input.GetKey(KeyCode.LeftArrow)
```

### Situaciones donde puede utilizarse

```
W
 ↓
Avanzar

Space
 ↓
Saltar

Shift
 ↓
Correr

A
 ↓
Mover izquierda
```

---

# 19. `KeyCode`

```
KeyCode.LeftArrow
```

`KeyCode` permite identificar diferentes teclas del teclado.

Algunos ejemplos:

```
KeyCode.A
KeyCode.D
KeyCode.W
KeyCode.S

KeyCode.Space

KeyCode.LeftArrow
KeyCode.RightArrow
KeyCode.UpArrow
KeyCode.DownArrow
```

---

# 20. `transform`

En nuestro código encontramos:

```
transform.Translate(...)
```

`transform` hace referencia al componente **Transform del GameObject al que está asociado el Script**.

Recordemos:

```
Player
│
├── Transform
└── Movimiento
```

Por lo tanto:

```
transform
```

se refiere al Transform del Player.

---

# 21. `Translate()`

```
transform.Translate(...)
```

Permite desplazar el Transform.

Por ejemplo:

```
transform.Translate(Vector3.right);
```

mueve el objeto hacia la derecha.

```
transform.Translate(Vector3.left);
```

mueve el objeto hacia la izquierda.

---

# 22. `Vector3`

```
Vector3.right
Vector3.left
Vector3.up
Vector3.down
```

Representan direcciones.

Podemos visualizarlo:

```
        Vector3.up
             ↑
             |
Vector3.left ← + → Vector3.right
             |
             ↓
       Vector3.down
```

### ¿Cuándo puede utilizarse?

Las direcciones pueden servir para:

- Movimiento.
    
- Posición.
    
- Dirección de proyectiles.
    
- Movimiento de enemigos.
    
- Movimiento de cámaras.
    

---

# 23. `Time.deltaTime`

En nuestro movimiento tenemos:

```
velocidad * Time.deltaTime
```

`Time.deltaTime` representa el tiempo transcurrido desde el frame anterior.

Esto permite realizar movimientos más consistentes independientemente de la velocidad de actualización del juego.

En términos sencillos:

> `Time.deltaTime` ayuda a que el movimiento esté relacionado con el tiempo y no solamente con la cantidad de frames.

---

# 24. 🧪 Actividad 1 — Movimiento con flechas

Crear un GameObject y asociarle:

```
Movimiento.cs
```

El objeto deberá poder desplazarse mediante:

```
↑
↓
←
→
```

El movimiento deberá utilizar:

```
Input.GetKey()
```

---

# 25. ⌨️ Actividad 2 — Cambiar las teclas

Ahora modificaremos el mismo Script.

En lugar de:

```
↑ ↓ ← →
```

utilizaremos:

```
W A S D
```

La correspondencia será:

```
W → arriba
S → abajo
A → izquierda
D → derecha
```

Por ejemplo:

```
Input.GetKey(KeyCode.W)
```

y:

```
Input.GetKey(KeyCode.A)
```

### 🎯 Objetivo

No escribir un programa completamente nuevo.

Modificar el programa existente.

> **Programar también significa leer, comprender, modificar y reutilizar código.**

---

# 26. 🎨 Segundo Script: cambiar el color

Ahora crearemos:

```
Assets
└── Scripts
    ├── Movimiento.cs
    └── CambioColor.cs
```

El objetivo será modificar el color del Sprite mediante código.

Código:

```
using UnityEngine;

public class CambioColor : MonoBehaviour
{
    private SpriteRenderer spriteRenderer;

    void Start()
    {
        spriteRenderer = GetComponent<SpriteRenderer>();
    }

    void Update()
    {
        if (Input.GetKey(KeyCode.Space))
        {
            spriteRenderer.color = Color.red;
        }
    }
}
```

---

# 27. 🔍 Analizando `CambioColor.cs`

Aquí aparecen algunos conceptos nuevos.

---

## `private`

```
private SpriteRenderer spriteRenderer;
```

Estamos creando una variable que solamente será accesible desde este Script.

La variable almacenará una referencia a un:

```
SpriteRenderer
```

---

# 28. `GetComponent<>()`

Encontramos:

```
GetComponent<SpriteRenderer>()
```

Esto significa:

> Buscar un componente `SpriteRenderer` que pertenezca al mismo GameObject.

Si tenemos:

```
Player
│
├── Transform
├── Sprite Renderer
└── CambioColor
```

el Script puede encontrar:

```
Sprite Renderer
```

utilizando:

```
GetComponent<SpriteRenderer>()
```

---

# 29. ¿Por qué es útil `GetComponent`?

Es una de las funciones que utilizaremos muchísimo en Unity.

Por ejemplo:

```
GetComponent<Rigidbody2D>()
```

puede obtener el Rigidbody 2D.

```
GetComponent<Collider2D>()
```

puede obtener un Collider 2D.

```
GetComponent<SpriteRenderer>()
```

puede obtener el Sprite Renderer.

### Situaciones comunes

```
Necesito mover físicamente un objeto
        ↓
GetComponent<Rigidbody2D>()

Necesito cambiar su imagen/color
        ↓
GetComponent<SpriteRenderer>()

Necesito revisar su Collider
        ↓
GetComponent<Collider2D>()
```

---

# 30. `Start()`

```
void Start()
```

`Start()` se ejecuta cuando comienza el juego, antes de que el objeto comience su ciclo normal de actualización.

Por eso podemos utilizarlo para preparar referencias iniciales:

```
void Start()
{
    spriteRenderer = GetComponent<SpriteRenderer>();
}
```

Después podemos utilizar:

```
spriteRenderer
```

en otras partes del Script.

---

# 31. `SpriteRenderer.color`

Tenemos:

```
spriteRenderer.color = Color.red;
```

Esto modifica el color del Sprite.

Algunos colores disponibles:

```
Color.red
Color.blue
Color.green
Color.yellow
Color.white
Color.black
```

### Ejemplos de uso

Podríamos utilizar colores para:

```
❤️ Vida baja
💚 Vida completa

🔴 Enemigo peligroso
🟢 Enemigo neutral

🟡 Objeto interactivo
```

O para indicar estados:

```
Normal → blanco
Daño → rojo
Invulnerable → amarillo
```

---

# 32. 🧩 Dos Scripts en un mismo GameObject

Ahora nuestro objeto puede tener:

```
Player
│
├── Transform
├── Sprite Renderer
├── Movimiento
└── CambioColor
```

Tenemos dos Scripts:

```
Movimiento.cs
      ↓
Movimiento

CambioColor.cs
      ↓
Color
```

Cada uno tiene una responsabilidad diferente.

---

# 33. 🏆 Reto — Integrar los Scripts

Ahora tenemos el reto de la clase.

Queremos conseguir:

```
W → mover arriba + cambiar color
S → mover abajo + cambiar color
A → mover izquierda + cambiar color
D → mover derecha + cambiar color
```

Por ejemplo:

```
W → 🟢 Verde
S → 🟡 Amarillo
A → 🔴 Rojo
D → 🔵 Azul
```

El objetivo es conseguir que:

```
Movimiento.cs
      ↓
Detecta dirección
      ↓
CambioColor.cs
      ↓
Cambia el color
```

---

# 34. 🧠 Comunicación entre Scripts

Para conseguirlo necesitaremos investigar cómo un Script puede acceder a otro Script.

Una posibilidad consiste en obtener el componente:

```
GetComponent<CambioColor>()
```

Por ejemplo:

```
private CambioColor cambioColor;
```

y posteriormente:

```
cambioColor = GetComponent<CambioColor>();
```

Después podemos llamar a un método del otro Script.

Por ejemplo:

```
cambioColor.CambiarColor(Color.red);
```

---

# 35. 🧩 Un método personalizado

Nuestro Script `CambioColor` puede tener:

```
public void CambiarColor(Color nuevoColor)
{
    spriteRenderer.color = nuevoColor;
}
```

Aquí estamos creando nuestro propio método:

```
CambiarColor()
```

que recibe un color.

Entonces:

```
cambioColor.CambiarColor(Color.red);
```

significa:

> Ejecutar el método `CambiarColor` y enviarle el color rojo.

---

# 36. 🧠 ¿Dónde podemos utilizar métodos?

Los métodos son útiles cuando queremos encapsular una acción.

Por ejemplo:

```
AbrirPuerta();
```

```
RecibirDaño();
```

```
ReproducirSonido();
```

```
CambiarColor();
```

```
ActualizarPuntuacion();
```

En un videojuego, los métodos permiten organizar el comportamiento en acciones claras.

---

# 37. 🔗 Separación de responsabilidades

Tenemos:

```
Movimiento.cs
```

que se encarga del movimiento.

Y:

```
CambioColor.cs
```

que se encarga del color.

Esto es mejor que crear un único Script que haga absolutamente todo.

```
❌ Juego.cs
   ├── Movimiento
   ├── Color
   ├── Sonido
   ├── Enemigos
   ├── Puntuación
   ├── Menús
   └── ...
```

En su lugar:

```
Player
│
├── Movimiento.cs
├── CambioColor.cs
├── Vida.cs
└── Sonido.cs
```

Cada Script tiene una responsabilidad más específica.

---

# 🔗 Conexión con Gestión del Desarrollo de Software

Esta forma de trabajar se relaciona directamente con conceptos de desarrollo de software:

- Modularidad.
    
- Separación de responsabilidades.
    
- Reutilización.
    
- Mantenimiento.
    
- Organización del código.
    

En un proyecto colaborativo, dividir responsabilidades permite que diferentes integrantes puedan trabajar sobre distintas partes del sistema.

---

# 🧪 Reto final — Player reactivo

Crear un GameObject que cumpla:

## Movimiento

```
W → arriba
S → abajo
A → izquierda
D → derecha
```

## Color

```
W → verde
S → amarillo
A → rojo
D → azul
```

## Requisitos

- Utilizar un Script para el movimiento.
    
- Utilizar un Script para el cambio de color.
    
- Ambos Scripts deben estar asociados al mismo GameObject.
    
- Los Scripts deben comunicarse entre sí.
    
- Utilizar `Input.GetKey()`.
    
- Utilizar el Legacy Input Manager.
    
- Consultar documentación cuando sea necesario.
    
- Registrar los cambios en GitHub.
    

---

# 🔀 GitHub

Al terminar el trabajo debemos registrar los cambios realizados.

Nuestro flujo:

```
Modificar proyecto
       ↓
Guardar escena
       ↓
Revisar cambios
       ↓
Commit
       ↓
Push
       ↓
GitHub
```

Un mensaje de Commit puede ser:

```
Implementa movimiento y cambio de color
```

---

# 🧠 Preguntas de comprensión

### 1. ¿Qué es un Script en Unity?

---

### 2. ¿Qué lenguaje utilizamos para crear Scripts en Unity?

---

### 3. ¿Qué función cumple `MonoBehaviour`?

---

### 4. ¿Para qué sirve `Update()`?

---

### 5. ¿Qué diferencia existe entre `GetKey`, `GetKeyDown` y `GetKeyUp`?

---

### 6. ¿Qué es `KeyCode`?

---

### 7. ¿Por qué nuestro Script necesita el Legacy Input Manager?

---

### 8. ¿Para qué sirve `GetComponent<>()`?

---

### 9. ¿Qué hace `Time.deltaTime`?

---

### 10. ¿Por qué es conveniente separar el movimiento y el cambio de color en diferentes Scripts?

---

### 11. ¿Cómo pueden comunicarse dos Scripts?

---

### 12. ¿Por qué debemos consultar documentación antes de copiar una solución?

---

# 🎯 Conceptos fundamentales

Al terminar esta clase debemos comprender:

```
GameObject
     │
     ▼
Component
     │
     ▼
Script
     │
     ▼
Comportamiento
```

Y también:

```
Problema
   ↓
Investigación
   ↓
Documentación
   ↓
Código
   ↓
Prueba
   ↓
Error
   ↓
Análisis
   ↓
Solución
```

# 🔑 Idea principal de la clase

> **Programar no consiste únicamente en escribir código.**
> 
> También consiste en investigar, comprender la tecnología que utilizamos, consultar documentación, probar soluciones y analizar los errores que aparecen.

Y en Unity:

> **Los Scripts permiten transformar GameObjects estáticos en objetos con comportamiento.**
