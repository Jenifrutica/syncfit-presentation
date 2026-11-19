# Guion de la exposición · SyncFit Edge

Una presentación **corta** ([`syncfit-pitch.pdf`](./syncfit-pitch.pdf), 8
diapositivas, unos 4 minutos y medio) con la idea y las estructuras de datos.
Después viene la **demostración en vivo en la app**, sin diapositivas, y al final
se vuelve a la última diapositiva para las preguntas.

Exponen **Juan López** (abre), **Jenifer Urbano** y **Juan Cuarán**. Los textos
son una guía para decirlos con tus palabras, no para leerlos. Cada diapositiva
muestra todo su contenido de una vez: se avanza una sola vez por diapositiva.

## Reparto y tiempos

| # | Diapositiva | Quién | Tiempo |
|---|---|---|---|
| 1 | Portada | Juan López | 0:20 |
| 2 | El contexto cambia | Juan López | 0:30 |
| 3 | ¿Qué cambia hoy? | Juan López | 0:40 |
| 4 | Dos IAs y un guardián | Jenifer Urbano | 0:45 |
| 5 | Cómo está construido | Juan Cuarán | 0:45 |
| 6 | Estructuras de datos (lineales) | Juan Cuarán | 0:45 |
| 7 | Estructuras de datos (las que conectan) | Jenifer Urbano | 0:45 |
| | **Demostración en vivo**, en la app | los tres | según el tiempo |
| 8 | ¿Preguntas? | Jenifer Urbano | 0:15 |

---

## La idea

### 1 · Portada — Juan López (0:20)

> Buenas, somos Juan Cuarán, Jenifer Urbano y yo, Juan López. Ella es Pulsi, la
> guía de **SyncFit Edge**: una app que adapta el entrenamiento a la fisiología
> de cada atleta, a su fase del ciclo o a su semana de embarazo, con sensores, dos
> inteligencias artificiales y las máquinas reales de su gimnasio.

### 2 · El contexto cambia — Juan López (0:30)

> Imaginen a una atleta que llega al gimnasio con menos energía de lo normal, y
> además su máquina de siempre está ocupada. Casi todos los planes de
> entrenamiento se diseñaron con datos de cuerpos masculinos y no cambian con el
> ciclo.

> Entonces, ¿qué debería entrenar hoy?

### 3 · ¿Qué cambia hoy? — Juan López (0:40)

> Tres cosas cambian la rutina de hoy.

> **Ciclo o gestación:** cada fase pide algo distinto. En la menstrual bajamos el
> impacto, en la ovulatoria evitamos saltos, y en el embarazo hay reglas propias,
> como nada boca arriba desde la semana 16.

> **Energía:** lo que ella siente, más lo que miden los sensores: su pulso, su
> temperatura y su fuerza, comparados con los suyos de siempre.

> **Equipo:** las máquinas que de verdad tiene su gimnasio.

Pase: *"Jenifer les cuenta cómo se convierte eso en una rutina."*

### 4 · Dos IAs y un guardián — Jenifer Urbano (0:45)

> El dato viaja en cuatro paradas:
> - **Sensor:** nuestro prototipo mide el pulso durante 15 segundos, la
>   temperatura en la frente durante 10 y la fuerza de empuje.
> - **IA local:** limpia la señal, estima la fatiga y fija la carga del día.
> - **IA generativa:** DeepSeek diseña la rutina con su objetivo, su fase y sus
>   máquinas.
> - **Validador:** con reglas fijas, bloquea lo que sea riesgoso.
>
> La matemática de la carga nunca la hace un modelo generativo.

Pase: *"Juan Cuarán les muestra cómo lo construimos."*

## Cómo se construyó

### 5 · Cómo está construido — Juan Cuarán (0:45)

> El backend está en capas, y cada una hace una sola cosa:
> - **API:** recibe lo que pide la app y lo que manda el prototipo.
> - **Servicios:** las reglas, como crear la rutina o unirse a un gimnasio.
> - **Analítica:** ordena los datos para responder rápido.
> - **Datos:** lo guarda todo.

> Las contraseñas van cifradas y cada rol ve solo lo suyo.

> Si se cae la red mientras se crea una rutina, no se crea dos veces.

> Y casi 500 pruebas automáticas revisan solas que ningún cambio rompa nada.

### 6 · Estructuras de datos (lineales) — Juan Cuarán (0:45)

> Cada parte de la idea se apoya en una estructura, y elegimos la que resuelve
> ese problema:
> - **Arreglos** para las últimas muestras del pulso y del peso. Siempre son la
>   misma cantidad, así que un tamaño fijo es lo más rápido.
> - **Listas** para tu rutina, tus máquinas y tus suplementos, que
>   crecen o se achican.
> - Una **cola circular** para el pulso, que llega 100 veces por
>   segundo. Solo importan los últimos segundos: el dato nuevo reemplaza al más
>   viejo.
> - Una **cola de prioridad** para las alertas de salud: la grave va
>   primero, aunque llegue después.

Pase: *"Jenifer sigue con las que conectan los datos."*

### 7 · Estructuras de datos (las que conectan) — Jenifer Urbano (0:45)

> - Un **árbol** para ver tus estadísticas entre dos fechas sin recorrer todo el
>   historial.
> - Un **grafo** para las fases: una lleva a la siguiente y el ciclo
>   vuelve a empezar, como vimos al principio.
> - **Tablas hash** para encontrar al instante qué máquina del
>   gimnasio sirve para cada ejercicio.
> - **Claves únicas** en la base de datos para que una rutina nunca
>   se genere dos veces.
>
> No usamos pilas: ningún proceso necesita deshacer en orden inverso.

Pase: *"Ahora lo vemos funcionando."* Cambien a la app.

---

## Demostración en vivo (en la app, sin diapositivas)

**Antes de empezar:** abran tres perfiles del navegador con los accesos de prueba
de `/entrar`:
- **Admin**, en el panel del gimnasio de prueba.
- **Nicolasa** (atleta), con el código del gimnasio a mano.
- **Superadmin**, en Catálogos.

Si el servidor tarda, la app avisa sola con "Conectando con el servidor…":
esperen unos segundos y sigan.

1. **Juan Cuarán · registra una máquina** (panel del gimnasio).
   - Crea, por ejemplo, *"Prensa de piernas"*. La IA deduce para qué sirve por el
     nombre.
   - Vincúlala con un ejercicio y guarda.
   - Al recargar, el inventario cambia.
   - *Conexión con las estructuras:* la tabla hash relaciona esa máquina con el
     ejercicio.
2. **Jenifer Urbano · agrega un grupo muscular** (superadmin, Catálogos).
   - En Opciones, crea un grupo.
   - En Ejercicios, añádelo a un ejercicio de la misma zona. El sistema valida
     que encajen, así que ensáyenlo antes con el mismo grupo.
   - La atleta recarga Rutina y el grupo nuevo aparece, sin tocar código.
3. **Juan López · crea la rutina de hoy** (atleta).
   - El panel empieza en blanco: activa el gimnasio, elige el grupo, cuántos
     ejercicios y la energía.
   - Haz la captura guiada con el prototipo, o con **Simular**.
   - Muestra los cuatro pasos mientras se crea.
   - En el resultado muestra cómo los sensores cambiaron la rutina, el porqué de
     cada ejercicio y, en **Cambiar**, las alternativas por nombre.
   - *Conexión con las estructuras:* la cola circular guarda el pulso y la clave
     única evita una rutina duplicada.

### 8 · ¿Preguntas? — Jenifer Urbano (0:15)

Vuelvan a la presentación.

> Su próxima rutina ya sabe en qué fase está. La app está en línea en
> syncfit.jenilarper.dev, en español, inglés y chino. ¿Preguntas?

---

## Preguntas probables y quién responde

| Pregunta | Responde |
|---|---|
| ¿Por qué esas estructuras y no otras? | Juan Cuarán: cada una responde a una necesidad de la idea. Tamaño fijo para las muestras, orden para la rutina, prioridad para las alertas, rangos de fechas para las estadísticas y búsqueda por nombre para las máquinas. |
| ¿Hay estructuras que no se usan? | Juan Cuarán: hay dos colas más, implementadas y probadas, que hoy no están en el flujo. No hay pilas. |
| ¿Por qué dos IAs y no una sola? | Jenifer: la carga la calcula un modelo que siempre da el mismo resultado y se puede probar. La IA generativa solo elige entre opciones válidas, y el validador revisa al final. |
| ¿Qué pasa si la IA generativa falla? | Jenifer: hay un modelo de respaldo y, si tampoco responde, una rutina armada con reglas fijas. Nunca se queda sin rutina. |
| ¿Cómo protegen los datos? | Juan Cuarán: las contraseñas van cifradas, cada rol ve solo lo suyo y se puede borrar la cuenta con todos sus datos. |
| ¿Qué tan preciso es el sensor? | Juan López: mide el pulso unas 100 veces por segundo y usa la mediana de varios segundos. Además compara con las referencias de la propia atleta, no con un promedio general. |
| ¿Qué falta? | Juan López: conectar varios prototipos a la vez y probar con más atletas reales. |
