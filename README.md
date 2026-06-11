# Ejercicios prácticos — POO con Java
**CodiGo by Tecsup · Sesión de refuerzo**

---

## BLOQUE 1 · Clases y Atributos

### Ejercicio 1 — Crear una clase y sus objetos

Crea una clase `Pelicula` con los siguientes atributos (sin modificadores de acceso):
- `titulo` (String)
- `duracionMinutos` (int)
- `calificacion` (double)

En el `Main`:
1. Crea dos objetos de tipo `Pelicula`.
2. Asigna valores distintos a cada uno directamente.
3. Imprime los tres atributos de cada película.

> ⚠️ Nota: acceder a los atributos directamente (`p1.titulo = ...`) **no es buena práctica** en código real — lo hacemos aquí solo para entender el problema que el encapsulamiento (Bloque 3) resuelve.

<details>
<summary>🔍 Ver solución</summary>

```java
// Pelicula.java
public class Pelicula {
    String titulo;
    int duracionMinutos;
    double calificacion;
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Pelicula p1 = new Pelicula();
        p1.titulo = "Inception";
        p1.duracionMinutos = 148;
        p1.calificacion = 8.8;

        Pelicula p2 = new Pelicula();
        p2.titulo = "Interstellar";
        p2.duracionMinutos = 169;
        p2.calificacion = 8.6;

        System.out.println(p1.titulo);           // Inception
        System.out.println(p1.duracionMinutos);  // 148
        System.out.println(p1.calificacion);     // 8.8

        System.out.println(p2.titulo);           // Interstellar
        System.out.println(p2.duracionMinutos);  // 169
        System.out.println(p2.calificacion);     // 8.6
    }
}
```

```
// Salida en consola:
Inception
148
8.8
Interstellar
169
8.6
```

</details>

---

### Ejercicio 2 — Referencias e independencia de objetos

Crea una clase `Producto` con atributos `nombre` (String) y `precio` (double).

En el `Main`:
1. Crea un objeto `p1` con nombre "Auriculares" y precio 120.0.
2. Crea un objeto `p2` con nombre "Teclado" y precio 85.0.
3. Cambia el precio de `p1` a 99.0.
4. Imprime el precio de `p1` y el de `p2`.

¿Cambiar el precio de `p1` afectó a `p2`? ¿Por qué?

<details>
<summary>🔍 Ver solución</summary>

```java
// Producto.java
public class Producto {
    String nombre;
    double precio;
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Producto p1 = new Producto();
        p1.nombre = "Auriculares";
        p1.precio = 120.0;

        Producto p2 = new Producto();
        p2.nombre = "Teclado";
        p2.precio = 85.0;

        p1.precio = 99.0;

        System.out.println(p1.precio);  // 99.0
        System.out.println(p2.precio);  // 85.0 — no cambió
    }
}
```

```
// Salida en consola:
99.0
85.0
```

> `p1` y `p2` apuntan a dos objetos distintos en memoria. Cambiar uno no afecta al otro.

> 💡 Cada `new` reserva un espacio **nuevo** en memoria. La variable (`p1`) no contiene el objeto: contiene la *dirección* donde vive. Por eso si hicieras `Producto p3 = p1;` (sin `new`), `p3` y `p1` apuntarían al **mismo** objeto, y cambiar el precio desde uno se vería desde el otro. Esa diferencia — copiar la referencia vs crear un objeto nuevo — reaparece en el Ejercicio 14.

</details>

---

## BLOQUE 2 · Constructores

### Ejercicio 3 — Constructor con parámetros

Crea una clase `Cancion` con atributos `titulo` (String), `artista` (String) y `duracion` (int, en segundos).

Agrega un constructor con parámetros que inicialice los tres atributos.

En el `Main`:
1. Crea tres objetos `Cancion` usando el constructor.
2. Imprime los datos de cada canción en el formato: `"titulo" - artista (Xs)`

<details>
<summary>🔍 Ver solución</summary>

```java
// Cancion.java
public class Cancion {
    String titulo;
    String artista;
    int duracion;

    public Cancion(String titulo, String artista, int duracion) {
        this.titulo = titulo;
        this.artista = artista;
        this.duracion = duracion;
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Cancion c1 = new Cancion("Bohemian Rhapsody", "Queen", 354);
        Cancion c2 = new Cancion("Blinding Lights", "The Weeknd", 200);
        Cancion c3 = new Cancion("Shape of You", "Ed Sheeran", 234);

        System.out.println("\"" + c1.titulo + "\" - " + c1.artista + " (" + c1.duracion + "s)");
        System.out.println("\"" + c2.titulo + "\" - " + c2.artista + " (" + c2.duracion + "s)");
        System.out.println("\"" + c3.titulo + "\" - " + c3.artista + " (" + c3.duracion + "s)");
    }
}
```

```
// Salida en consola:
"Bohemian Rhapsody" - Queen (354s)
"Blinding Lights" - The Weeknd (200s)
"Shape of You" - Ed Sheeran (234s)
```

> 💡 `this.titulo = titulo` significa: "el atributo `titulo` **de este objeto** = el parámetro `titulo` que llegó". Sin `this`, Java pensaría que hablas dos veces del parámetro y el atributo quedaría sin asignar. `this` siempre apunta al objeto actual.

</details>

---

### Ejercicio 4 — Constructor vacío vs con parámetros

Crea una clase `Vehiculo` con atributos `marca` (String) y `velocidadMaxima` (int).

Agrega dos constructores:
- Uno vacío que no recibe nada.
- Uno con parámetros que recibe marca y velocidad máxima.

En el `Main`:
1. Crea un vehículo con el constructor vacío e imprime sus atributos — ¿qué aparece?
2. Crea un vehículo con el constructor con parámetros e imprime sus atributos.

<details>
<summary>🔍 Ver solución</summary>

```java
// Vehiculo.java
public class Vehiculo {
    String marca;
    int velocidadMaxima;

    public Vehiculo() {
    }

    public Vehiculo(String marca, int velocidadMaxima) {
        this.marca = marca;
        this.velocidadMaxima = velocidadMaxima;
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Vehiculo v1 = new Vehiculo();
        System.out.println(v1.marca);            // null
        System.out.println(v1.velocidadMaxima);  // 0

        Vehiculo v2 = new Vehiculo("Toyota", 180);
        System.out.println(v2.marca);            // Toyota
        System.out.println(v2.velocidadMaxima);  // 180
    }
}
```

```
// Salida en consola:
null
0
Toyota
180
```

> Java asigna `null` a los String y `0` a los int cuando no se inicializan.

> ⚠️ Detalle importante: si **no** escribes ningún constructor, Java te regala uno vacío automáticamente. Pero apenas escribes uno con parámetros, **el regalo desaparece** — si todavía quieres poder hacer `new Vehiculo()` sin argumentos, tienes que escribir el constructor vacío tú mismo (como en este ejercicio).

</details>

---

## BLOQUE 3 · Encapsulamiento

### Ejercicio 5 — Encapsular una clase

Toma la clase `Cancion` del Ejercicio 3 y encapsúlala:
- Haz todos los atributos `private`.
- Agrega getters para los tres atributos.
- Agrega setters para `titulo` y `artista` (no para `duracion`).

En el `Main`:
1. Crea una canción con el constructor.
2. Cambia el título usando el setter.
3. Intenta cambiar la duración directamente (`cancion.duracion = 200`) — ¿qué pasa?
4. Imprime los datos usando los getters.

<details>
<summary>🔍 Ver solución</summary>

```java
// Cancion.java
public class Cancion {
    private String titulo;
    private String artista;
    private int duracion;

    public Cancion(String titulo, String artista, int duracion) {
        this.titulo = titulo;
        this.artista = artista;
        this.duracion = duracion;
    }

    public String getTitulo() { return titulo; }
    public String getArtista() { return artista; }
    public int getDuracion() { return duracion; }

    public void setTitulo(String titulo) { this.titulo = titulo; }
    public void setArtista(String artista) { this.artista = artista; }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Cancion c = new Cancion("Bohemian Rhapsody", "Queen", 354);

        c.setTitulo("We Will Rock You");
        // c.duracion = 200;  ← ERROR de compilación: duracion es private

        System.out.println(c.getTitulo());    // We Will Rock You
        System.out.println(c.getArtista());   // Queen
        System.out.println(c.getDuracion());  // 354
    }
}
```

```
// Salida en consola:
We Will Rock You
Queen
354
```

> 💡 ¿Por qué `duracion` no tiene setter? Porque encapsular no es solo "poner private y generar todo": es **decidir qué se puede cambiar y qué no**. Una canción puede cambiar de título (remasterización), pero su duración no debería cambiar después de creada. Tú eliges las puertas que abres.

</details>

---

### Ejercicio 6 — Encapsular y agregar comportamiento

Crea una clase `CuentaBancaria` con atributos privados `titular` (String) y `saldo` (double).

Agrega:
- Constructor con parámetros para ambos atributos.
- Getters para ambos.
- Setter solo para `titular`.
- Un método `depositar(double monto)` que sume el monto al saldo e imprima el nuevo saldo.
- Un método `mostrarInfo()` que imprima titular y saldo.

En el `Main`:
1. Crea una cuenta con saldo inicial de 500.0.
2. Deposita 200.0.
3. Imprime la información de la cuenta.

<details>
<summary>🔍 Ver solución</summary>

```java
// CuentaBancaria.java
public class CuentaBancaria {
    private String titular;
    private double saldo;

    public CuentaBancaria(String titular, double saldo) {
        this.titular = titular;
        this.saldo = saldo;
    }

    public String getTitular() { return titular; }
    public double getSaldo() { return saldo; }

    public void setTitular(String titular) { this.titular = titular; }

    public void depositar(double monto) {
        saldo = saldo + monto;
        System.out.println("Nuevo saldo: S/" + saldo);
    }

    public void mostrarInfo() {
        System.out.println("Titular: " + titular + " | Saldo: S/" + saldo);
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        CuentaBancaria cuenta = new CuentaBancaria("Ana García", 500.0);
        cuenta.depositar(200.0);
        cuenta.mostrarInfo();
    }
}
```

```
// Salida en consola:
Nuevo saldo: S/700.0
Titular: Ana García | Saldo: S/700.0
```

> 💡 Fíjate que `saldo` **no tiene setter**, y aun así puedes modificarlo — pero solo a través de `depositar()`. Esa es la idea central del encapsulamiento: en vez de dejar que cualquiera haga `cuenta.saldo = -9999`, la clase ofrece operaciones controladas. Más adelante podrías agregar validación dentro de `depositar()` (rechazar montos negativos) sin tocar el código que la usa.

</details>

---

## BLOQUE 4 · Herencia

### Ejercicio 7 — Crear una jerarquía simple

Crea una clase padre `Dispositivo` con atributos privados `marca` (String) y `precio` (double), constructor con parámetros, getters y un método `mostrarInfo()`.

Luego crea dos subclases:
- `Celular` con atributo extra `memoriaGB` (int)
- `Laptop` con atributo extra `ramGB` (int)

Cada subclase debe tener su propio constructor que llame a `super()` y sobreescribir `mostrarInfo()`.

En el `Main`, instancia un objeto de cada subclase y llama a `mostrarInfo()`.

<details>
<summary>🔍 Ver solución</summary>

```java
// Dispositivo.java
public class Dispositivo {
    private String marca;
    private double precio;

    public Dispositivo(String marca, double precio) {
        this.marca = marca;
        this.precio = precio;
    }

    public String getMarca() { return marca; }
    public double getPrecio() { return precio; }

    public void mostrarInfo() {
        System.out.println("Marca: " + marca + " | Precio: S/" + precio);
    }
}

// Celular.java
public class Celular extends Dispositivo {
    private int memoriaGB;

    public Celular(String marca, double precio, int memoriaGB) {
        super(marca, precio);
        this.memoriaGB = memoriaGB;
    }

    @Override
    public void mostrarInfo() {
        System.out.println("=== CELULAR ===");
        System.out.println("Marca: " + getMarca());
        System.out.println("Precio: S/" + getPrecio());
        System.out.println("Memoria: " + memoriaGB + "GB");
    }
}

// Laptop.java
public class Laptop extends Dispositivo {
    private int ramGB;

    public Laptop(String marca, double precio, int ramGB) {
        super(marca, precio);
        this.ramGB = ramGB;
    }

    @Override
    public void mostrarInfo() {
        System.out.println("=== LAPTOP ===");
        System.out.println("Marca: " + getMarca());
        System.out.println("Precio: S/" + getPrecio());
        System.out.println("RAM: " + ramGB + "GB");
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Celular c = new Celular("Samsung", 1200.0, 128);
        Laptop l = new Laptop("Lenovo", 2500.0, 16);

        c.mostrarInfo();
        System.out.println("---");
        l.mostrarInfo();
    }
}
```

```
// Salida en consola:
=== CELULAR ===
Marca: Samsung
Precio: S/1200.0
Memoria: 128GB
---
=== LAPTOP ===
Marca: Lenovo
Precio: S/2500.0
RAM: 16GB
```

> 💡 Dos detalles clave aquí:
> - `super(marca, precio)` llama al constructor del padre y **debe ser la primera línea** del constructor hijo. El hijo no inicializa `marca` y `precio` por su cuenta: le delega esa parte al padre, que es quien conoce esos atributos.
> - `@Override` no es decorativo: le pide al compilador que **verifique** que de verdad estás sobreescribiendo un método del padre. Si te equivocas en el nombre (`mostrarinfo()` con minúscula), sin la anotación Java crearía un método nuevo en silencio; con ella, te marca el error de inmediato.

</details>

---

### Ejercicio 8 — Herencia y atributos privados

Usando la jerarquía del Ejercicio 7, dentro del método `mostrarInfo()` de `Celular` intenta usar `marca` directamente en lugar de `getMarca()`.

¿Qué pasa? ¿Por qué puedes usar `getMarca()` pero no `marca` directamente?

<details>
<summary>🔍 Ver solución</summary>

```java
// Dentro de Celular.java — en mostrarInfo():
System.out.println(getMarca());   // ✓ compila — getter es public
System.out.println(marca);        // ✗ ERROR de compilación — marca es private en Dispositivo
```

> `private` significa "solo dentro de esta clase". La herencia da acceso a lo `public` y `protected`, no a lo `private`. El getter es la única puerta de salida.

</details>

---

## BLOQUE 5 · Polimorfismo

### Ejercicio 9 — El mismo método, resultados distintos

Usando la jerarquía `Dispositivo` / `Celular` / `Laptop` del Ejercicio 7, declara en el `Main` tres variables de tipo `Dispositivo`:

```java
Dispositivo d1 = new Celular("Samsung", 1200.0, 128);
Dispositivo d2 = new Laptop("Lenovo", 2500.0, 16);
Dispositivo d3 = new Celular("Apple", 3500.0, 256);
```

Llama a `mostrarInfo()` en cada uno. ¿Por qué funciona si `d1` es de tipo `Dispositivo` y no de tipo `Celular`?

<details>
<summary>🔍 Ver solución</summary>

```java
// Main.java
public class Main {
    public static void main(String[] args) {
        Dispositivo d1 = new Celular("Samsung", 1200.0, 128);
        Dispositivo d2 = new Laptop("Lenovo", 2500.0, 16);
        Dispositivo d3 = new Celular("Apple", 3500.0, 256);

        d1.mostrarInfo();
        System.out.println("---");
        d2.mostrarInfo();
        System.out.println("---");
        d3.mostrarInfo();
    }
}
```

```
// Salida en consola:
=== CELULAR ===
Marca: Samsung
Precio: S/1200.0
Memoria: 128GB
---
=== LAPTOP ===
Marca: Lenovo
Precio: S/2500.0
RAM: 16GB
---
=== CELULAR ===
Marca: Apple
Precio: S/3500.0
Memoria: 256GB
```

> Java mira el objeto real en memoria (`Celular`, `Laptop`), no el tipo de la variable (`Dispositivo`). Por eso cada uno ejecuta su propia versión de `mostrarInfo()`.

> ⚠️ Pero ojo con el lado inverso: como la variable `d1` es de tipo `Dispositivo`, **solo puedes llamar lo que `Dispositivo` declara**. `d1.mostrarInfo()` funciona, pero algo exclusivo de `Celular` (como un hipotético `getMemoriaGB()`) daría error de compilación, aunque el objeto real sea un celular. Regla mental: *el tipo de la variable decide qué puedes llamar; el tipo del objeto decide qué versión se ejecuta.*

</details>

---

### Ejercicio 10 — Métodos heredados

Agrega un método `encender()` en la clase padre `Dispositivo` que imprima `"[marca] encendido"`. No lo sobreescribas en ninguna subclase.

En el `Main`, llama a `encender()` desde un objeto `Celular` y uno `Laptop`.

¿Dónde está definido `encender()`? ¿Cómo lo encontró Java si no está en `Celular`?

<details>
<summary>🔍 Ver solución</summary>

```java
// En Dispositivo.java — agregar:
public void encender() {
    System.out.println(getMarca() + " encendido");
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Celular c = new Celular("Samsung", 1200.0, 128);
        Laptop l = new Laptop("Lenovo", 2500.0, 16);

        c.encender();
        l.encender();
    }
}
```

```
// Salida en consola:
Samsung encendido
Lenovo encendido
```

> `encender()` está en `Dispositivo`. Como `Celular` y `Laptop` heredan de él, lo reciben automáticamente sin reescribirlo.

</details>

---

## BLOQUE 6 · Abstracción

### Ejercicio 11 — Clase abstracta

Convierte `Dispositivo` en clase abstracta y declara `mostrarInfo()` como método abstracto.

1. Intenta instanciar `Dispositivo` directamente en el `Main` — ¿qué error aparece?
2. Verifica que `Celular` y `Laptop` siguen funcionando sin cambios.
3. Agrega una tercera subclase `Tablet` con un atributo extra `tieneLapiz` (boolean) e implementa `mostrarInfo()`.

<details>
<summary>🔍 Ver solución</summary>

```java
// Dispositivo.java
public abstract class Dispositivo {
    private String marca;
    private double precio;

    public Dispositivo(String marca, double precio) {
        this.marca = marca;
        this.precio = precio;
    }

    public String getMarca() { return marca; }
    public double getPrecio() { return precio; }

    public void encender() {
        System.out.println(getMarca() + " encendido");
    }

    public abstract void mostrarInfo();
}

// Tablet.java
public class Tablet extends Dispositivo {
    private boolean tieneLapiz;

    public Tablet(String marca, double precio, boolean tieneLapiz) {
        super(marca, precio);
        this.tieneLapiz = tieneLapiz;
    }

    @Override
    public void mostrarInfo() {
        System.out.println("=== TABLET ===");
        System.out.println("Marca: " + getMarca());
        System.out.println("Precio: S/" + getPrecio());
        System.out.println("Tiene lápiz: " + tieneLapiz);
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        // Dispositivo d = new Dispositivo("X", 100); ← ERROR: no se puede instanciar

        Tablet t = new Tablet("Apple", 1800.0, true);
        t.mostrarInfo();
    }
}
```

```
// Salida en consola:
=== TABLET ===
Marca: Apple
Precio: S/1800.0
Tiene lápiz: true
```

> 💡 ¿Para qué sirve que no se pueda instanciar? Piénsalo así: en el mundo real nadie compra "un dispositivo" a secas — compra un celular, una laptop, una tablet. `Dispositivo` es un **concepto**, no una cosa concreta. Y al declarar `mostrarInfo()` como abstracto, obligas a que **toda** subclase futura lo implemente: el que agregue `Smartwatch` mañana no podrá olvidarse. La clase abstracta es un contrato a medias: aporta código común (`encender()`, getters) y exige el resto.

</details>

---

### Ejercicio 12 — Interfaz

Crea una interfaz `Conectable` con un método `conectarWifi()`.

1. Implementa `Conectable` en `Celular` y `Laptop`, pero no en `Tablet`.
2. En cada clase, `conectarWifi()` imprime un mensaje distinto.
3. En el `Main`, declara una variable de tipo `Conectable` y asígnale un `Celular`. Llama a `conectarWifi()`.

¿Puedes llamar a `mostrarInfo()` desde esa variable? ¿Por qué?

<details>
<summary>🔍 Ver solución</summary>

```java
// Conectable.java
public interface Conectable {
    void conectarWifi();
}

// Celular.java — agregar implements:
public class Celular extends Dispositivo implements Conectable {
    // ... mismo código de antes ...

    @Override
    public void conectarWifi() {
        System.out.println(getMarca() + " conectado al WiFi");
    }
}

// Laptop.java — agregar implements:
public class Laptop extends Dispositivo implements Conectable {
    // ... mismo código de antes ...

    @Override
    public void conectarWifi() {
        System.out.println(getMarca() + " conectado a la red");
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Conectable c = new Celular("Samsung", 1200.0, 128);
        c.conectarWifi();

        // c.mostrarInfo(); ← ERROR: mostrarInfo() no existe en Conectable
    }
}
```

```
// Salida en consola:
Samsung conectado al WiFi
```

> Desde una variable de tipo `Conectable` solo puedes llamar a los métodos definidos en esa interfaz.

> 💡 ¿Cuándo interfaz y cuándo clase abstracta? La clase abstracta dice **qué ES** algo (`Celular` ES un `Dispositivo`) y solo se puede heredar de una. La interfaz dice **qué SABE HACER** (`Celular` sabe conectarse) y una clase puede implementar varias. Por eso `Tablet` puede ser `Dispositivo` sin ser `Conectable`: ser y saber hacer son cosas distintas.

</details>

---

## BLOQUE 7 · Composición y colecciones

### Ejercicio 13 — Una clase que agrupa objetos

Crea una clase `TiendaDispositivos` que use la jerarquía `Dispositivo` / `Celular` / `Laptop` / `Tablet` de los bloques anteriores.

La clase debe tener:
- Un atributo privado `dispositivos` de tipo `ArrayList<Dispositivo>`, inicializado en el constructor.
- Un método `agregar(Dispositivo d)` que añada un dispositivo a la lista.
- Un método `listarTodos()` que recorra la lista con un `for` y llame a `mostrarInfo()` en cada elemento.

En el `Main`:
1. Crea una tienda.
2. Agrega un `Celular`, una `Laptop` y una `Tablet` (¡los tres entran en la misma lista!).
3. Llama a `listarTodos()`.

¿Por qué una lista de tipo `Dispositivo` puede guardar celulares, laptops y tablets a la vez? ¿Qué versión de `mostrarInfo()` se ejecuta para cada uno?

<details>
<summary>🔍 Ver solución</summary>

```java
// TiendaDispositivos.java
import java.util.ArrayList;

public class TiendaDispositivos {
    private ArrayList<Dispositivo> dispositivos;

    public TiendaDispositivos() {
        this.dispositivos = new ArrayList<>();
    }

    public void agregar(Dispositivo d) {
        dispositivos.add(d);
    }

    public void listarTodos() {
        for (int i = 0; i < dispositivos.size(); i++) {
            dispositivos.get(i).mostrarInfo();
            System.out.println("---");
        }
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        TiendaDispositivos tienda = new TiendaDispositivos();

        tienda.agregar(new Celular("Samsung", 1200.0, 128));
        tienda.agregar(new Laptop("Lenovo", 2500.0, 16));
        tienda.agregar(new Tablet("Apple", 1800.0, true));

        tienda.listarTodos();
    }
}
```

```
// Salida en consola:
=== CELULAR ===
Marca: Samsung
Precio: S/1200.0
Memoria: 128GB
---
=== LAPTOP ===
Marca: Lenovo
Precio: S/2500.0
RAM: 16GB
---
=== TABLET ===
Marca: Apple
Precio: S/1800.0
Tiene lápiz: true
---
```

> La lista acepta los tres porque `Celular`, `Laptop` y `Tablet` **son** `Dispositivo` (herencia). Y al recorrerla, cada objeto ejecuta **su propia** versión de `mostrarInfo()` (polimorfismo). Este ejercicio junta los dos conceptos: la lista del padre + el comportamiento del hijo.

> 💡 Esto que hace `TiendaDispositivos` se llama **composición**: la tienda **TIENE** dispositivos (no ES un dispositivo). Herencia = "es un", composición = "tiene un". Los sistemas reales usan ambas, como `Library` con sus `ArrayList`. Y usamos `ArrayList` en vez de un array (`Dispositivo[]`) porque crece solo: no necesitas decidir de antemano cuántos dispositivos tendrá la tienda.

</details>

---

### Ejercicio 14 — Buscar y modificar: el poder de las referencias

Agrega a `TiendaDispositivos` un método:

```java
public Dispositivo buscarPorMarca(String marca)
```

que recorra la lista y devuelva el primer dispositivo cuya marca coincida. Si no encuentra ninguno, devuelve `null`.

En el `Main`:
1. Crea la tienda y agrega los tres dispositivos del ejercicio anterior.
2. Busca el dispositivo de marca "Samsung" y guárdalo en una variable `encontrado`.
3. Llama a `encontrado.encender()`.
4. Busca una marca que no existe — ¿qué devuelve? ¿Qué pasa si llamas a `encender()` sobre ese resultado?

**Pregunta clave:** el objeto que devolvió `buscarPorMarca()`, ¿es una copia del que está en la lista, o es el mismo?

<details>
<summary>🔍 Ver solución</summary>

```java
// En TiendaDispositivos.java — agregar:
public Dispositivo buscarPorMarca(String marca) {
    for (int i = 0; i < dispositivos.size(); i++) {
        if (dispositivos.get(i).getMarca().equals(marca)) {
            return dispositivos.get(i);
        }
    }
    return null;
}

// Main.java
public class Main {
    public static void main(String[] args) {
        TiendaDispositivos tienda = new TiendaDispositivos();
        tienda.agregar(new Celular("Samsung", 1200.0, 128));
        tienda.agregar(new Laptop("Lenovo", 2500.0, 16));
        tienda.agregar(new Tablet("Apple", 1800.0, true));

        Dispositivo encontrado = tienda.buscarPorMarca("Samsung");
        encontrado.encender();

        Dispositivo fantasma = tienda.buscarPorMarca("Nokia");
        System.out.println(fantasma);  // null
        // fantasma.encender();  ← NullPointerException si lo descomentas
    }
}
```

```
// Salida en consola:
Samsung encendido
null
```

> **No es una copia: es el mismo objeto.** El método devuelve una *referencia* al objeto que vive en la lista. Si lo modificas a través de `encontrado`, el cambio se ve también desde la tienda, porque ambos apuntan al mismo lugar en memoria. Y por eso `null` es peligroso: es una referencia que no apunta a nada — llamarle un método lanza `NullPointerException`. (Esto es exactamente el problema que `Optional` resuelve en el ejemplo de la biblioteca.)

> ⚠️ Detalle que causa muchos bugs: para comparar Strings usamos `.equals(marca)`, **nunca** `==`. El `==` compara si las dos referencias apuntan al mismo objeto en memoria; `.equals()` compara el contenido del texto. Con `==` la búsqueda podría fallar aunque las marcas se escriban igual.

</details>

---

## Ejercicio integrador

### Ejercicio 15 — Sistema de música

Construye desde cero un pequeño sistema de música con las siguientes clases:

**Clase abstracta `Contenido`:**
- Atributos privados: `titulo` (String), `artista` (String)
- Constructor con parámetros y getters
- Método abstracto `reproducir()`

**Interfaz `Descargable`:**
- Método `descargar()`

**Subclase `Cancion` que extiende `Contenido`:**
- Atributo extra `duracionSegundos` (int)
- `reproducir()` imprime: `Reproduciendo: titulo - artista (Xs)`

**Subclase `Podcast` que extiende `Contenido` e implementa `Descargable`:**
- Atributo extra `episodio` (int)
- `reproducir()` imprime: `Episodio N: titulo`
- `descargar()` imprime: `Descargando episodio N...`

En el `Main`:
1. Crea dos canciones y un podcast.
2. Llama a `reproducir()` en los tres.
3. Llama a `descargar()` en el podcast.
4. Declara una variable de tipo `Contenido` y asígnale una canción. Llama a `reproducir()`.

<details>
<summary>🔍 Ver solución</summary>

```java
// Contenido.java
public abstract class Contenido {
    private String titulo;
    private String artista;

    public Contenido(String titulo, String artista) {
        this.titulo = titulo;
        this.artista = artista;
    }

    public String getTitulo() { return titulo; }
    public String getArtista() { return artista; }

    public abstract void reproducir();
}

// Descargable.java
public interface Descargable {
    void descargar();
}

// Cancion.java
public class Cancion extends Contenido {
    private int duracionSegundos;

    public Cancion(String titulo, String artista, int duracionSegundos) {
        super(titulo, artista);
        this.duracionSegundos = duracionSegundos;
    }

    @Override
    public void reproducir() {
        System.out.println("Reproduciendo: " + getTitulo()
            + " - " + getArtista()
            + " (" + duracionSegundos + "s)");
    }
}

// Podcast.java
public class Podcast extends Contenido implements Descargable {
    private int episodio;

    public Podcast(String titulo, String artista, int episodio) {
        super(titulo, artista);
        this.episodio = episodio;
    }

    @Override
    public void reproducir() {
        System.out.println("Episodio " + episodio + ": " + getTitulo());
    }

    @Override
    public void descargar() {
        System.out.println("Descargando episodio " + episodio + "...");
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Cancion c1 = new Cancion("Bohemian Rhapsody", "Queen", 354);
        Cancion c2 = new Cancion("Blinding Lights", "The Weeknd", 200);
        Podcast p  = new Podcast("Historia del Jazz", "Radio Clásica", 5);

        c1.reproducir();
        c2.reproducir();
        p.reproducir();
        p.descargar();

        System.out.println("---");
        Contenido contenido = new Cancion("Shape of You", "Ed Sheeran", 234);
        contenido.reproducir();
    }
}
```

```
// Salida en consola:
Reproduciendo: Bohemian Rhapsody - Queen (354s)
Reproduciendo: Blinding Lights - The Weeknd (200s)
Episodio 5: Historia del Jazz
Descargando episodio 5...
---
Reproduciendo: Shape of You - Ed Sheeran (234s)
```

</details>

---

## Ejercicio final · Diseña tú el sistema

### Ejercicio 16 — Sin plano

Hasta ahora cada ejercicio te dijo qué clases crear y con qué atributos. Esta vez **tú decides todo**.

Elige uno de estos dominios (o propón otro):
- 🐶 Veterinaria
- 🎬 Cine
- 🏋️ Gimnasio
- 🍔 Restaurante

Tu sistema debe usar, como mínimo:
1. Una **clase abstracta** padre con al menos un método abstracto.
2. **Dos subclases** que la extiendan, cada una con un atributo propio y su propia versión del método abstracto.
3. Una **interfaz** implementada por al menos una de las subclases.
4. Una **clase agrupadora** (como `TiendaDispositivos`) con un `ArrayList` del tipo padre, y métodos para agregar, listar y buscar.
5. Un `Main` que demuestre todo funcionando, incluyendo al menos una variable de tipo padre apuntando a un objeto hijo.

Antes de escribir código, dibuja en papel tus clases: nombres, atributos, métodos y flechas de herencia. Si el diagrama no te queda claro, el código tampoco va a quedar.

**No hay solución incluida.** Cuando lo termines, envíamelo y lo revisamos juntos. No importa si no compila a la primera — los errores son parte del ejercicio.
