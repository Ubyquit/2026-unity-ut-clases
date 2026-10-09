> **Versión utilizada:** Unity 6.6 — `6000.6.3f1`  
> **Materia:** Desarrollo de Videojuegos  
> **Materia relacionada:** Gestión en el Desarrollo de Software
---
# 1. Objetivo de la clase

En esta práctica aprenderás a controlar el movimiento de los objetos en Unity utilizando diferentes mecanismos. Construirás tres escenas independientes y, al final, integrarás lo aprendido en un pequeño prototipo de videojuego.

Al terminar, serás capaz de:

- Diferenciar el movimiento directo con `Transform` del movimiento mediante física.
    
- Utilizar `Rigidbody2D.AddForce()` para aplicar fuerzas.
    
- Controlar la velocidad mediante `Rigidbody2D.linearVelocity`.
    
- Configurar la gravedad y otras propiedades físicas.
    
- Detectar colisiones entre objetos.
    
- Modificar `Position`, `Rotation` y `Scale` desde el Inspector.
    
- Integrar diferentes comportamientos en una misma mecánica.
    
- Comprobar cómo los valores de configuración afectan el resultado del juego.
    

## 2. Antes de comenzar: ¿cómo se mueve un objeto en Unity?

En las clases anteriores utilizamos instrucciones como:

```
transform.Translate(Vector3.right * velocidad * Time.deltaTime);
```

Esto nos permitió mover un objeto al presionar las teclas del teclado. Sin embargo, cuando intentamos construir una mecánica en la que una nave debía mantener una pelota en equilibrio, apareció un problema: la pelota rebotaba y el comportamiento no era el esperado.

Para comprender qué sucedió, necesitamos distinguir tres formas de controlar el movimiento.

### 2.1. `Transform.Translate()`: cambiar la posición directamente

`Transform` representa la posición, rotación y escala de un objeto en la escena.

Cuando utilizamos `Translate()`, desplazamos el objeto directamente, sin aplicar una fuerza física para producir ese movimiento.

```
transform.Translate(Vector3.right * velocidad * Time.deltaTime);
```

**¿Cuándo puede ser útil?**

- Mover un personaje de manera sencilla.
    
- Desplazar una plataforma siguiendo una ruta.
    
- Animar objetos que no necesitan responder a la física.
    
- Mover elementos decorativos o de interfaz dentro del mundo del juego.
    

**¿Qué debemos considerar?**

Si el objeto tiene un `Rigidbody2D`, moverlo directamente mediante su `Transform` puede interferir con el comportamiento que esperamos de la simulación física. Las colisiones, por sí solas, no convierten ese movimiento en una fuerza.

### 2.2. `Rigidbody2D.AddForce()`: aplicar una fuerza

`Rigidbody2D` permite que un objeto participe en la simulación física de Unity.

Con `AddForce()` no indicamos simplemente a qué posición debe ir el objeto: aplicamos una fuerza que puede modificar su movimiento según su masa, velocidad y otras condiciones físicas.

```
rigidbody2D.AddForce(Vector2.up * fuerza);
```

**¿Cuándo puede ser útil?**

- Impulsar una nave o una pelota.
    
- Crear saltos con un impulso inicial.
    
- Lanzar proyectiles.
    
- Simular empujes, golpes y otras interacciones físicas.
    

La fuerza puede aplicarse de diferentes maneras. Por ejemplo:

```
rigidbody2D.AddForce(Vector2.up * fuerza, ForceMode2D.Force);
```

Este modo aplica fuerza de manera continua mientras se ejecuta la instrucción. Es apropiado cuando queremos mantener una aceleración producida por una fuerza.

```
rigidbody2D.AddForce(Vector2.up * fuerza, ForceMode2D.Impulse);
```

Este modo aplica un impulso instantáneo. Es útil para un salto o un lanzamiento que debe ocurrir una sola vez.

**Importante:** si aplicamos un impulso en cada fotograma mientras una tecla permanece presionada, el objeto recibirá muchos impulsos seguidos. Por eso debemos decidir si queremos aplicar una fuerza continua o un impulso único.

### 2.3. `Rigidbody2D.linearVelocity`: controlar la velocidad

La velocidad lineal representa qué tan rápido y en qué dirección se mueve un cuerpo físico.

```
rigidbody2D.linearVelocity = Vector2.right * velocidad;
```

Con esta instrucción establecemos directamente la velocidad lineal del objeto.

**¿Cuándo puede ser útil?**

- Crear un personaje con velocidad horizontal controlada.
    
- Hacer que un proyectil salga con una velocidad determinada.
    
- Establecer una velocidad de movimiento precisa.
    
- Controlar el movimiento de una pelota cuando el diseño lo requiere.
    

A diferencia de `AddForce()`, que modifica el movimiento mediante fuerzas, `linearVelocity` establece la velocidad deseada en ese momento.

Por eso, asignar continuamente la velocidad de un objeto puede dificultar que la gravedad, las colisiones u otras fuerzas produzcan el resultado que esperamos. Depende de cómo esté escrito el código.

En Unity 6 utilizaremos `Rigidbody2D.linearVelocity`. En tutoriales de versiones anteriores es posible encontrar `Rigidbody2D.velocity`; conviene comprobar qué API corresponde a la versión instalada.

### 2.4. Comparación rápida

|Característica|`Transform.Translate()`|`AddForce()`|`linearVelocity`|
|---|---|---|---|
|¿Qué controla?|Desplazamiento directo|Fuerza aplicada|Velocidad lineal|
|¿Utiliza la simulación física para producir el movimiento?|No por sí mismo|Sí|Sí, mediante el cuerpo físico|
|¿La masa influye en el movimiento resultante?|No directamente|Sí|No determina la velocidad asignada|
|¿La gravedad puede afectar el movimiento?|No genera esa respuesta física por sí mismo|Sí, si el cuerpo está configurado para ello|Sí, pero el código puede contrarrestarla|
|Uso típico|Movimiento directo|Empujes, saltos e impulsos|Velocidad controlada|

Ninguna de las tres técnicas es universalmente mejor. La elección depende de la mecánica que quieras construir.

---

## 3. Conceptos físicos que utilizaremos

Antes de comenzar con las escenas, identifica las propiedades que encontrarás en el componente `Rigidbody2D`.

### Gravedad — `Gravity Scale`

Controla cuánto afecta la gravedad configurada en el proyecto a un cuerpo físico.

- `0`: la gravedad no produce aceleración sobre ese cuerpo.
    
- `1`: utiliza la gravedad del proyecto con su escala normal.
    
- `2`: duplica el efecto de esa gravedad.
    
- Un valor negativo invierte su dirección efectiva, lo que puede ser útil para mecánicas especiales.
    

La gravedad no es lo mismo que una fuerza aplicada con `AddForce()`: es un efecto continuo de la simulación física.

### Masa — `Mass`

Representa la masa del cuerpo físico. En condiciones equivalentes, una masa mayor requiere más fuerza para producir la misma aceleración.

La masa no cambia directamente una velocidad que establecemos mediante `linearVelocity`.

### Amortiguamiento lineal — `Linear Damping`

Reduce gradualmente la velocidad del cuerpo físico. Puede ayudar a simular resistencia al movimiento.

Un valor mayor suele hacer que el objeto pierda velocidad más rápidamente. No sustituye la gravedad ni las colisiones.

### Tipo de cuerpo — `Body Type`

- **Dynamic:** responde a la gravedad, fuerzas y colisiones físicas.
    
- **Kinematic:** su movimiento se controla principalmente mediante el código o el sistema que lo anima; no responde a las fuerzas como un cuerpo dinámico.
    
- **Static:** representa un objeto que permanece fijo, como una pared o el suelo.
    

Para las pelotas de nuestros ejercicios utilizaremos normalmente `Dynamic`. Para el suelo utilizaremos `Static`.

### Colliders — formas de colisión

Los componentes `BoxCollider2D`, `CircleCollider2D` y otros colliders definen las formas utilizadas para detectar contactos físicos.

Un `Rigidbody2D` no sustituye a un collider. Para que una pelota choque con una plataforma, ambos objetos deben tener colliders compatibles y una configuración física adecuada.

---

# Ejercicio 1 — Movimiento directo con Transform

**Objetivo:** construir una escena donde un objeto se mueva horizontalmente mediante `Transform.Translate()`.

En esta escena estudiaremos el movimiento directo, la velocidad, la posición y la escala. No necesitamos aplicar fuerzas ni simular una pelota que rebota.

## Paso 1. Crear la escena

1. Abre tu proyecto en Unity.
    
2. Crea una escena nueva.
    
3. Guárdala con el nombre `Escena01_Transform`.
    
4. En la jerarquía, crea un objeto `2D Object > Sprites > Square`.
    
5. Renómbralo como `Jugador`.
    
6. Cambia su escala a:
    
    - X: `1`
        
    - Y: `1`
        
    - Z: `1`
        
7. Coloca su posición inicial en:
    
    - X: `-5`
        
    - Y: `0`
        
    - Z: `0`
        
8. Cambia el color del `SpriteRenderer` para distinguirlo del fondo.
    

## Paso 2. Crear el script

Dentro de la carpeta `Scripts`, crea `MovimientoTransform.cs`.

Copia el siguiente código:

```
using UnityEngine;

public class MovimientoTransform : MonoBehaviour
{
    public float velocidad = 5f;

    void Update()
    {
        float movimiento = Input.GetAxisRaw("Horizontal");

        transform.Translate(
            Vector3.right * movimiento * velocidad * Time.deltaTime
        );
    }
}
```

Guarda el archivo y regresa a Unity.

> Si el teclado no responde por la configuración del sistema de entrada, revisa la propiedad `Active Input Handling` en `Edit > Project Settings > Player > Other Settings`. Para esta práctica, configura el sistema de entrada antiguo (`Input Manager (Old)`) si estás utilizando `Input.GetAxisRaw()` y tu proyecto no lo tiene habilitado.

## Paso 3. Asociar el script

1. Selecciona el objeto `Jugador`.
    
2. Arrastra `MovimientoTransform.cs` desde `Scripts` al Inspector.
    
3. Comprueba que el componente aparece.
    
4. Ejecuta la escena.
    
5. Utiliza las flechas izquierda y derecha para mover el objeto.
    

## Paso 4. Analizar el código

- `public float velocidad = 5f;`: permite cambiar la velocidad desde el Inspector.
    
- `Update()`: se ejecuta una vez por fotograma.
    
- `Input.GetAxisRaw("Horizontal")`: obtiene el valor del eje horizontal, normalmente `-1`, `0` o `1`.
    
- `Vector3.right`: representa la dirección positiva del eje X.
    
- `Time.deltaTime`: permite que el desplazamiento sea más consistente entre diferentes tasas de fotogramas.
    

La instrucción principal es `transform.Translate()`. El objeto cambia de posición directamente.

## Paso 5. Experimentar

Sin cambiar el código, prueba lo siguiente:

1. Cambia `velocidad` a `2`, `5` y `10`.
    
2. Cambia la escala del jugador a X = `2`, Y = `0.5`.
    
3. Cambia su posición inicial a X = `0`.
    
4. Ejecuta la escena después de cada modificación.
    
5. Observa cómo cambia el tamaño del objeto y dónde aparece al comenzar.
    

### Preguntas de análisis

- ¿Qué sucede cuando duplicas la velocidad?
    
- ¿Cambiar la escala modifica la velocidad?
    
- ¿Por qué el objeto puede seguir desplazándose sin tener un `Rigidbody2D`?
    
- ¿Qué pasaría si intentaras utilizar este mismo enfoque para simular una pelota que rebota sobre una plataforma?
    

**Conclusión del ejercicio:** `Transform.Translate()` es una forma sencilla de mover un objeto, pero no genera por sí mismo una respuesta física a las fuerzas y colisiones.

---

# Ejercicio 2 — Impulsos y fuerzas con Rigidbody2D

**Objetivo:** construir una escena donde una pelota reciba un impulso y se mueva bajo la influencia de la gravedad.

En esta práctica veremos cómo una fuerza puede cambiar el movimiento de un objeto físico y cómo la gravedad modifica su trayectoria.

## Paso 1. Crear la escena

1. Crea una escena nueva.
    
2. Guárdala como `Escena02_AddForce`.
    
3. Crea un objeto `2D Object > Sprites > Square`.
    
4. Renómbralo como `Suelo`.
    
5. Configura su posición:
    
    - X: `0`
        
    - Y: `-3`
        
    - Z: `0`
        
6. Configura su escala:
    
    - X: `12`
        
    - Y: `1`
        
    - Z: `1`
        
7. Comprueba que tiene un `BoxCollider2D`. Si no lo tiene, agrégalo.
    
8. En la jerarquía, crea `2D Object > Sprites > Circle`.
    
9. Renómbralo como `Pelota`.
    
10. Configura su posición inicial:
    
    - X: `0`
        
    - Y: `0`
        
    - Z: `0`
        
11. Cambia su escala a X = `0.8`, Y = `0.8`, Z = `1`.
    
12. Comprueba que tiene un `CircleCollider2D`.
    
13. Agrega el componente `Rigidbody2D`.
    
14. Configura su `Body Type` como `Dynamic`.
    
15. Deja `Gravity Scale` en `1`.
    

## Paso 2. Crear el script de impulso

Crea `ImpulsoPelota.cs` dentro de la carpeta `Scripts`.

```
using UnityEngine;

public class ImpulsoPelota : MonoBehaviour
{
    public float fuerza = 5f;

    private Rigidbody2D rb;

    void Awake()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            rb.AddForce(
                Vector2.up * fuerza,
                ForceMode2D.Impulse
            );
        }
    }
}
```

## Paso 3. Asociar el script

1. Selecciona `Pelota`.
    
2. Arrastra `ImpulsoPelota.cs` al Inspector.
    
3. Comprueba que el componente `Rigidbody2D` está presente.
    
4. Ejecuta la escena.
    
5. Presiona la barra espaciadora.
    

La pelota recibirá un impulso hacia arriba. Después, la gravedad hará que su trayectoria cambie y vuelva a caer.

## Paso 4. Comprender el script

- `Awake()`: obtiene una referencia al componente físico antes de comenzar la simulación habitual.
    
- `GetComponent<Rigidbody2D>()`: busca el componente `Rigidbody2D` del mismo objeto.
    
- `Input.GetKeyDown(KeyCode.Space)`: detecta el instante en que se presiona la barra espaciadora.
    
- `AddForce()`: aplica una fuerza al cuerpo físico.
    
- `ForceMode2D.Impulse`: aplica un impulso instantáneo.
    

Utilizamos `GetKeyDown()` porque queremos aplicar un solo impulso por pulsación, no repetirlo durante todos los fotogramas en que se mantenga presionada la tecla.

## Paso 5. Experimentar con la fuerza

Prueba estos valores desde el Inspector:

- `fuerza = 2`
    
- `fuerza = 5`
    
- `fuerza = 10`
    
- `fuerza = 20`
    

Después, realiza una segunda ronda de pruebas:

1. Cambia `Gravity Scale` a `0`.
    
2. Ejecuta la escena y aplica el impulso.
    
3. Cambia `Gravity Scale` a `2`.
    
4. Vuelve a probar.
    
5. Cambia la masa del cuerpo físico.
    
6. Observa las diferencias entre las pruebas.
    

Recuerda que debes volver a ejecutar o reiniciar la escena cuando sea necesario para comparar las pruebas desde condiciones similares.

### Preguntas de análisis

- ¿Qué sucede cuando aumentas la fuerza del impulso?
    
- ¿Qué cambia cuando `Gravity Scale` es igual a cero?
    
- ¿Por qué la pelota cae más rápidamente cuando aumentas la escala de gravedad?
    
- ¿Qué diferencia hay entre mantener una fuerza continua y aplicar un impulso?
    
- ¿Qué función cumple el `Rigidbody2D` en esta escena?
    

**Conclusión del ejercicio:** las fuerzas modifican el movimiento de los cuerpos físicos. La gravedad también participa en ese movimiento y puede cambiar su trayectoria después del impulso inicial.

---

# Ejercicio 3 — Velocidad, gravedad y colisiones

**Objetivo:** establecer la velocidad de un objeto con `linearVelocity`, observar la influencia de la gravedad y comprobar cómo interactúa con una plataforma.

En esta escena compararemos la asignación directa de velocidad con el comportamiento físico de la pelota.

## Paso 1. Crear la escena

1. Crea una escena nueva.
    
2. Guárdala como `Escena03_LinearVelocity`.
    
3. Crea un objeto cuadrado y renómbralo `Plataforma`.
    
4. Configura su posición:
    
    - X: `0`
        
    - Y: `-2`
        
    - Z: `0`
        
5. Configura su escala:
    
    - X: `8`
        
    - Y: `0.5`
        
    - Z: `1`
        
6. Comprueba que tiene un `BoxCollider2D`.
    
7. Crea un objeto circular y renómbralo `Pelota`.
    
8. Configura su posición inicial:
    
    - X: `-3`
        
    - Y: `1`
        
    - Z: `0`
        
9. Configura su escala en X = `0.8`, Y = `0.8`, Z = `1`.
    
10. Comprueba que tiene un `CircleCollider2D`.
    
11. Agrega `Rigidbody2D`.
    
12. Configura `Body Type` como `Dynamic` y `Gravity Scale` como `1`.
    

## Paso 2. Crear el script

Crea `VelocidadPelota.cs`.

```
using UnityEngine;

public class VelocidadPelota : MonoBehaviour
{
    public float velocidadHorizontal = 4f;

    private Rigidbody2D rb;

    void Awake()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Start()
    {
        rb.linearVelocity = new Vector2(
            velocidadHorizontal,
            0f
        );
    }
}
```

## Paso 3. Asociar el script

1. Selecciona `Pelota`.
    
2. Arrastra `VelocidadPelota.cs` al Inspector.
    
3. Comprueba que `Rigidbody2D` está configurado como `Dynamic`.
    
4. Ejecuta la escena.
    

La pelota comenzará con una velocidad horizontal determinada. La gravedad la acelerará hacia abajo y el collider de la plataforma permitirá detectar el contacto físico.

Cuando la pelota choque con la plataforma, su movimiento dependerá de la velocidad que tenga, la gravedad y la configuración de los colliders y materiales físicos.

## Paso 4. Analizar `linearVelocity`

La instrucción:

```
rb.linearVelocity = new Vector2(
    velocidadHorizontal,
    0f
);
```

establece una velocidad horizontal inicial.

- El primer valor controla la componente X.
    
- El segundo valor controla la componente Y.
    
- `0f` significa que inicialmente no asignamos velocidad vertical.
    

Aunque la velocidad vertical inicial sea cero, la gravedad puede generar velocidad vertical después de comenzar la simulación.

Esto es importante: **asignar una velocidad inicial no significa que el objeto conservará esa velocidad para siempre**. Las fuerzas, la gravedad y las colisiones pueden modificar su movimiento.

## Paso 5. Experimentar con la gravedad

Ejecuta varias pruebas:

1. Utiliza `velocidadHorizontal = 2`.
    
2. Cambia el valor a `5`.
    
3. Cambia `Gravity Scale` a `0`.
    
4. Cambia `Gravity Scale` a `2`.
    
5. Cambia la altura inicial de la pelota.
    
6. Modifica el ancho de la plataforma.
    
7. Observa si la pelota alcanza la plataforma, cuánto tarda en caer y cómo cambia su trayectoria.
    

Para comparar las pruebas, mantén constantes las demás propiedades siempre que sea posible.

## Paso 6. Investigar el rebote

Opcionalmente, crea un `Physics Material 2D` desde la ventana Project y asígnalo al collider de la pelota.

Experimenta con:

- `Bounciness`: controla la capacidad de rebote.
    
- `Friction`: modifica la fricción durante el contacto.
    

Prueba valores diferentes y observa el resultado. El rebote real también depende de las velocidades, las condiciones del contacto y la configuración física.

### Preguntas de análisis

- ¿Por qué la pelota comienza a moverse horizontalmente?
    
- ¿Por qué termina cayendo si su velocidad vertical inicial es cero?
    
- ¿Qué diferencia observas entre asignar `linearVelocity` y aplicar un impulso con `AddForce()`?
    
- ¿Qué sucede cuando desactivas la gravedad?
    
- ¿Qué papel desempeñan los colliders?
    
- ¿Por qué cambiar el material físico puede modificar el rebote?
    

**Conclusión del ejercicio:** `linearVelocity` permite establecer una velocidad concreta, mientras que la gravedad y las colisiones pueden cambiar el movimiento posterior.

---

# Reto final — Nave de equilibrio

**Objetivo:** integrar movimiento directo, fuerzas, velocidad y colisiones para construir una mecánica sencilla de equilibrio.

En este reto recuperarás la idea de la nave que debe mantener una pelota sobre ella. La diferencia es que ahora utilizarás lo aprendido para decidir qué mecanismo corresponde a cada objeto.

## 1. Diseñar la escena

Crea una escena nueva y guárdala como `Reto_Final_Equilibrio`.

Construye los siguientes objetos:

### Nave

1. Crea un cuadrado y renómbralo `Nave`.
    
2. Configura su posición inicial en `(0, -1, 0)`.
    
3. Configura su escala en `(3, 0.5, 1)`.
    
4. Cambia su color para distinguirla.
    
5. Agrega un `BoxCollider2D`.
    
6. Agrega `Rigidbody2D`.
    
7. Configura `Body Type` como `Dynamic`.
    
8. Configura `Gravity Scale` como `0`.
    

La nave utilizará fuerzas para desplazarse sin caer por la gravedad. Las colisiones físicas seguirán formando parte de la simulación.

### Pelota

1. Crea un círculo y renómbralo `Pelota`.
    
2. Colócalo encima de la nave, aproximadamente en `(0, 0, 0)`.
    
3. Configura su escala en `(0.5, 0.5, 1)`.
    
4. Comprueba que tiene `CircleCollider2D`.
    
5. Agrega `Rigidbody2D`.
    
6. Configura `Body Type` como `Dynamic`.
    
7. Configura `Gravity Scale` como `1`.
    

### Suelo

1. Crea un cuadrado y renómbralo `Suelo`.
    
2. Colócalo en `(0, -4, 0)`.
    
3. Configura su escala en `(14, 1, 1)`.
    
4. Comprueba que tiene `BoxCollider2D`.
    
5. No necesita un `Rigidbody2D` dinámico; puede permanecer como objeto estático con su collider.
    

Asegúrate de que la pelota comienza encima de la nave y que la nave dispone de espacio suficiente para moverse.

## 2. Script de movimiento de la nave

Crea `NaveEquilibrio.cs`.

```
using UnityEngine;

public class NaveEquilibrio : MonoBehaviour
{
    public float fuerza = 8f;

    private Rigidbody2D rb;

    void Awake()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void FixedUpdate()
    {
        float horizontal = Input.GetAxisRaw("Horizontal");
        float vertical = Input.GetAxisRaw("Vertical");

        Vector2 direccion = new Vector2(
            horizontal,
            vertical
        );

        rb.AddForce(direccion * fuerza);
    }
}
```

Asocia el script al objeto `Nave`.

### ¿Qué hace este script?

1. Lee la dirección horizontal y vertical del teclado.
    
2. Construye un vector con la dirección deseada.
    
3. Aplica una fuerza al cuerpo físico.
    
4. Permite que la nave acelere y responda a las fuerzas.
    

Utilizamos `FixedUpdate()` para aplicar la fuerza dentro del ciclo de actualización física. Esto resulta apropiado para operaciones que interactúan con `Rigidbody2D`.

La nave puede continuar moviéndose por inercia cuando se dejan de presionar las teclas. Esa respuesta es parte de la simulación física.

## 3. Script para controlar la pelota

Crea `ControlPelota.cs`.

```
using UnityEngine;

public class ControlPelota : MonoBehaviour
{
    public float velocidadHorizontal = 3f;
    public float fuerzaImpulso = 4f;

    private Rigidbody2D rb;

    void Awake()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Start()
    {
        rb.linearVelocity = new Vector2(
            velocidadHorizontal,
            0f
        );
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            rb.AddForce(
                Vector2.up * fuerzaImpulso,
                ForceMode2D.Impulse
            );
        }
    }
}
```

Asocia el script a `Pelota`.

### ¿Qué hace este script?

- Establece una velocidad horizontal inicial.
    
- Permite aplicar un impulso vertical con la barra espaciadora.
    
- Conserva el comportamiento físico de la pelota.
    
- Permite que la gravedad y las colisiones influyan en su movimiento.
    

En esta configuración, la pelota se mueve de manera independiente del Transform de la nave. La interacción física entre ambos objetos dependerá de los colliders y de sus cuerpos físicos.

## 4. Ejecutar y probar el reto

1. Ejecuta la escena.
    
2. Utiliza las flechas para mover la nave.
    
3. Presiona la barra espaciadora para impulsar la pelota.
    
4. Intenta mantener la pelota sobre la nave.
    
5. Observa qué sucede cuando la nave acelera, cambia de dirección o se mueve demasiado rápido.
    
6. Ajusta los valores del Inspector y vuelve a intentarlo.
    

Prueba distintas combinaciones de `fuerza`, `velocidadHorizontal`, `fuerzaImpulso` y `Gravity Scale`.

No existe un único conjunto de valores correcto: el objetivo es experimentar y explicar por qué una configuración funciona mejor que otra.

## 5. Mejoras obligatorias del reto

Una vez que la mecánica básica funcione, realiza las siguientes mejoras:

### Mejora A. Cambiar la apariencia

Integra el script de cambio de color utilizado en la clase anterior.

- Al presionar una tecla, la nave debe cambiar de color.
    
- El cambio de color no debe impedir el movimiento físico.
    
- Comprueba que ambos scripts pueden coexistir en el mismo GameObject.
    

### Mejora B. Modificar el comportamiento

Investiga qué ocurre al cambiar:

- La masa de la nave.
    
- La masa de la pelota.
    
- El `Linear Damping` de la nave.
    
- El `Gravity Scale` de la pelota.
    
- La fuerza aplicada por la nave.
    

Registra una configuración que facilite el equilibrio y otra que lo dificulte.

### Mejora C. Detectar una colisión

Agrega un comportamiento que detecte cuándo la pelota toca el suelo. Por ejemplo, puedes utilizar `OnCollisionEnter2D()` para mostrar un mensaje en la consola.

```
void OnCollisionEnter2D(Collision2D collision)
{
    if (collision.gameObject.name == "Suelo")
    {
        Debug.Log("La pelota cayó al suelo.");
    }
}
```

Agrega este método dentro de la clase `ControlPelota`, antes de la última llave `}`.

Para que funcione, el suelo debe tener un collider, la pelota debe tener `Rigidbody2D` y `Collider2D`, y la colisión debe estar habilitada. Si cambias el nombre del objeto en la jerarquía, actualiza también la condición del código.

### Mejora D. Documentar los experimentos

Realiza al menos tres pruebas y registra los resultados:

|Prueba|Fuerza de nave|Gravedad de pelota|Resultado observado|
|---|---|---|---|
|1|4|1|Describe lo que ocurrió|
|2|8|1|Describe lo que ocurrió|
|3|8|2|Describe lo que ocurrió|

Los resultados deben provenir de tus propias pruebas. No basta con completar la tabla: explica qué cambió y por qué crees que ocurrió.

---

## 6. Entrega y control de versiones

Guarda las tres escenas y el reto final dentro de la carpeta `Scenes` de tu proyecto.

Verifica que los scripts estén dentro de `Scripts` y que cada escena abra correctamente.

Antes de entregar:

- La escena `Escena01_Transform` funciona.
    
- La escena `Escena02_AddForce` funciona.
    
- La escena `Escena03_LinearVelocity` funciona.
    
- El reto final permite mover la nave y controlar la pelota.
    
- El cambio de color está integrado.
    
- La colisión con el suelo se detecta.
    
- Las pruebas experimentales están documentadas.
    
- Los cambios están guardados en GitHub.
    

Utiliza un mensaje de commit descriptivo, por ejemplo:

`Implementa prácticas de física y reto de equilibrio`

No subas únicamente capturas: asegúrate de incluir los archivos del proyecto que permitan revisar las escenas y los scripts.

---

## 7. Reflexión final

Responde con tus propias palabras:

1. ¿En qué se diferencia `Transform.Translate()` de `Rigidbody2D.AddForce()`?
    
2. ¿Qué diferencia hay entre aplicar un impulso y asignar `linearVelocity`?
    
3. ¿Qué papel desempeña la gravedad?
    
4. ¿Por qué necesitamos colliders para detectar contactos físicos?
    
5. ¿Qué propiedad modificaste para mejorar el equilibrio?
    
6. ¿Qué problema encontraste durante las pruebas y cómo lo resolviste?
    
7. Si tuvieras que construir un proyectil, ¿qué técnica elegirías y por qué?
    
8. ¿Qué cambiarías si quisieras una nave que se desplazara de manera más controlada y sin inercia?
    

## 8. Documentación oficial

Consulta la documentación de Unity cuando tengas dudas sobre los componentes o las instrucciones utilizadas:

- [Rigidbody2D](https://docs.unity3d.com/6000.6/Documentation/ScriptReference/Rigidbody2D.html)
    
- [Rigidbody2D.AddForce](https://docs.unity3d.com/6000.6/Documentation/ScriptReference/Rigidbody2D.AddForce.html)
    
- [Rigidbody2D.linearVelocity](https://docs.unity3d.com/6000.6/Documentation/ScriptReference/Rigidbody2D-linearVelocity.html)
    
- [Transform.Translate](https://docs.unity3d.com/6000.6/Documentation/ScriptReference/Transform.Translate.html)
    
- [MonoBehaviour.OnCollisionEnter2D](https://docs.unity3d.com/6000.6/Documentation/ScriptReference/MonoBehaviour.OnCollisionEnter2D.html)
    

---

**Idea central de la clase:** en el desarrollo de videojuegos no siempre basta con conseguir que algo se mueva. Hay que elegir cómo debe moverse, qué fuerzas lo afectan, cómo interactúa con otros objetos y qué cambios necesita la mecánica para funcionar como fue diseñada.