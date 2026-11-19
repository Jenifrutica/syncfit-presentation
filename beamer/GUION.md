# Guion de la exposición · SyncFit Edge

**5 minutos de presentación + 10 de demostración en vivo**, con la presentación
[`syncfit-pitch.pdf`](./syncfit-pitch.pdf) (13 diapositivas). Las tres personas
que exponen son **Juan López** (abre), **Jenifer Urbano** y **Juan Cuarán**.

El texto de cada parte es una guía para decirlo con tus palabras, no para leerlo.
Los **[clic]** marcan cuándo avanzar: algunas diapositivas revelan sus tarjetas
una por una.

## Reparto y tiempos

| # | Diapositiva | Quién | Tiempo |
|---|---|---|---|
| 1 | Portada | Juan López | 0:20 |
| 2 | El contexto cambia | Juan López | 0:35 |
| 3 | ¿Qué cambia hoy? | Juan López | 0:35 |
| 4 | Cada fase tiene su clima | Jenifer Urbano | 0:40 |
| 5 | Dos IAs y un guardián | Jenifer Urbano | 0:45 |
| 6 | Cómo está construido | Juan Cuarán | 0:45 |
| 7 | Estructuras de datos (1) | Juan Cuarán | 0:40 |
| 8 | Estructuras de datos (2) | Juan Cuarán | 0:40 |
| | **Fin de la presentación** | | **5:00** |
| 9 | Tres accesos, tres tareas | Juan Cuarán | 0:30 |
| 10 | Registra una máquina (demo) | Juan Cuarán | 2:30 |
| 11 | Agrega un grupo muscular (demo) | Jenifer Urbano | 2:30 |
| 12 | Genera la rutina (demo) | Juan López | 3:30 |
| 13 | ¿Preguntas? | Jenifer Urbano | 1:00 |
| | **Fin de la demostración** | | **10:00** |

Cada persona habla unos 5 minutos en total.

---

## Presentación (5:00)

### 1 · Portada — Juan López (0:20)

> Buenas, somos Juan Cuarán, Jenifer Urbano y yo, Juan López. Ella es Pulsi, la
> guía de **SyncFit Edge**: una app que adapta el entrenamiento a la fisiología
> de cada atleta, a su fase del ciclo o a su semana de embarazo, con sensores, dos
> inteligencias artificiales y las máquinas reales de su gimnasio.

### 2 · El contexto cambia — Juan López (0:35)

> Imaginen a una atleta que llega al gimnasio con menos energía de lo normal, y
> además su máquina de siempre está ocupada. Casi todos los planes de
> entrenamiento se diseñaron con datos de cuerpos masculinos y no cambian con el
> ciclo.

**[clic]**

> Entonces, ¿qué debería entrenar hoy?

### 3 · ¿Qué cambia hoy? — Juan López (0:35)

> Les pregunto a ustedes: ¿qué debería cambiar la rutina de hoy?

Deja que el público responda y revela una tarjeta por respuesta.

> **Ciclo o gestación:** la fase en la que está da el contexto.
> **[clic]** **Energía:** lo que ella siente, más lo que miden los sensores: su
> pulso, su temperatura y su fuerza, comparados con los suyos de siempre.
> **[clic]** **Equipo:** las máquinas que de verdad tiene su gimnasio.

Pase: *"Jenifer les cuenta cómo cambia cada fase."*

### 4 · Cada fase tiene su clima — Jenifer Urbano (0:40)

> Cada fase del ciclo cambia la propuesta. En la menstrual bajamos el impacto; en
> la folicular hay energía para subir cargas; en la ovulatoria hay mucha fuerza,
> pero evitamos saltos de alto impacto; y en la lútea llega antes la fatiga, así
> que hay más descanso. Y si está embarazada también funciona: tres trimestres con
> reglas propias, por ejemplo, nada boca arriba desde la semana 16.

### 5 · Dos IAs y un guardián — Jenifer Urbano (0:45)

> El dato viaja en cuatro paradas. Primero el **sensor**: nuestro prototipo mide
> el pulso durante 15 segundos, la temperatura en la frente durante 10 y la
> fuerza de empuje. Luego una **IA local** limpia la señal, estima la fatiga y
> fija la carga del día. Después la **IA generativa**, DeepSeek, diseña la rutina
> con su objetivo, su fase y sus máquinas. Y al final un **validador** con reglas
> fijas bloquea lo que sea riesgoso. Lo importante: la matemática de la carga
> nunca la hace un modelo generativo.

Pase: *"Juan Cuarán les muestra cómo está construido por dentro."*

### 6 · Cómo está construido — Juan Cuarán (0:45)

> El backend está organizado en capas, y cada una hace una sola cosa. La **API**
> recibe lo que pide la app y lo que manda el prototipo. Los **servicios** tienen
> las reglas: crear la rutina, unirse a un gimnasio, manejar las cuentas. La
> **analítica** ordena los datos para responder rápido. Y la capa de **datos** lo
> guarda todo.

**[clic]**

> Las contraseñas van cifradas y cada rol ve solo lo suyo.

**[clic]**

> Si se cae la red mientras se crea una rutina, no se crea dos veces.

**[clic]**

> Y casi 500 pruebas automáticas revisan solas que ningún cambio rompa nada.

### 7 · Estructuras de datos (1) — Juan Cuarán (0:40)

> No elegimos estructuras por elegir: cada una resuelve un problema concreto.
> **Arreglos** para las últimas muestras del pulso y del peso en el prototipo:
> siempre son la misma cantidad, así que un tamaño fijo es lo más rápido.
> **[clic]** **Listas** para tu rutina, tus máquinas y tus suplementos, que crecen
> o se achican. **[clic]** Una **cola circular** para el pulso, que llega 100
> veces por segundo: solo importan los últimos segundos, y el dato nuevo
> reemplaza al más viejo. **[clic]** Y una **cola de prioridad** para las
> alertas de salud: la grave va primero, aunque llegue después.

### 8 · Estructuras de datos (2) — Juan Cuarán (0:40)

> Un **árbol** para ver tus estadísticas entre dos fechas sin recorrer todo el
> historial. **[clic]** Un **grafo** para las fases: una lleva a la siguiente y el
> ciclo vuelve a empezar. **[clic]** **Tablas hash** para encontrar al instante
> qué máquina del gimnasio sirve para cada ejercicio. **[clic]** Y **claves
> únicas** en la base de datos para que una rutina nunca se genere dos veces. No
> usamos pilas porque ningún proceso necesita deshacer en orden inverso.

Pase: *"Ahora lo vemos funcionando."*

---

## Demostración (10:00)

**Antes de empezar** (no se cuenta en el tiempo): tres perfiles del navegador
abiertos con los accesos de prueba de `/entrar`: **Admin** en el panel del
gimnasio de prueba, **Nicolasa** (atleta) con el código del gimnasio a mano y
**Superadmin** en Catálogos. Si el servidor tarda, la app lo avisa sola con
"Conectando con el servidor…": esperen unos segundos y sigan.

### 9 · Tres accesos, tres tareas — Juan Cuarán (0:30)

> Vamos a usar tres cuentas a la vez: el **gimnasio**, la **atleta** y el
> **superadministrador**. **[clic] [clic]** Cada uno ve solo lo suyo.

### 10 · Registra una máquina — Juan Cuarán (2:30)

En el panel del gimnasio:

1. Crea una máquina, por ejemplo *"Prensa de piernas"*.
   > La IA lee el nombre y deduce para qué sirve y cuánto pesa la carga.
2. **[clic]** Vincúlala con un ejercicio y guarda.
3. **[clic]** Recarga.
   > El inventario y el contador cambian, y la atleta ya puede usar esa máquina
   > en su rutina.

Pase: *"Jenifer va a agregar algo al catálogo sin tocar código."*

### 11 · Agrega un grupo muscular — Jenifer Urbano (2:30)

Como superadministradora, en Catálogos:

1. **Opciones:** crea un grupo muscular de prueba.
   > Todo lo que ven en la app sale de la base de datos.
2. **[clic]** **Ejercicios:** añade el grupo a un ejercicio de la misma zona.
   El sistema valida que grupo y zona encajen; ensáyenlo antes con el mismo
   grupo.
3. **[clic]** En la sesión de la atleta, recarga Rutina.
   > Ahí está el grupo nuevo, sin tocar una línea de código.

Pase: *"Juan crea la rutina de hoy con ese gimnasio."*

### 12 · Genera la rutina — Juan López (3:30)

Como atleta:

1. Activa el gimnasio de prueba, elige el grupo y **cuántos ejercicios** quiere.
   El panel empieza en blanco.
2. **[clic]** Registra su energía.
3. **[clic]** Haz la captura guiada con el prototipo, o con **Simular** si no
   está conectado: pulso 15 s, temperatura 10 s y empuje.
   > Miren los cuatro pasos: sensor, IA local, IA generativa y validador. Tarda
   > unos segundos porque de verdad está midiendo y razonando.
4. En el resultado muestra:
   > Esta tarjeta dice cómo sus sensores cambiaron la rutina de hoy. Cada
   > ejercicio trae su porqué, las series y el peso sugerido, y la máquina de su
   > gimnasio. Si una máquina está ocupada, en **Cambiar** le sugiere
   > alternativas por nombre.

Pase: *"Jenifer cierra."*

### 13 · ¿Preguntas? — Jenifer Urbano (1:00)

> Tres ideas para llevarse. **Mide, no adivina:** usa su pulso, su temperatura y
> su fuerza. **Seguridad primero:** lo riesgoso se bloquea y le dice por qué.
> **Con su gimnasio:** usa las máquinas que de verdad tiene. Su próxima rutina
> ya sabe en qué fase está. La app está en línea en syncfit.jenilarper.dev, en
> español, inglés y chino. ¿Preguntas?

---

## Preguntas probables y quién responde

| Pregunta | Responde |
|---|---|
| ¿Por qué dos IAs y no una sola? | Jenifer: la carga la calcula un modelo determinista que se puede probar; la IA generativa solo elige entre opciones válidas, y el validador revisa al final. |
| ¿Qué pasa si la IA generativa falla? | Juan Cuarán: hay un modelo de respaldo y, si tampoco responde, una rutina determinista. La app nunca se queda sin rutina. |
| ¿Por qué esas estructuras de datos? | Juan Cuarán: diapositivas 7 y 8. Cada una responde a una necesidad: tamaño fijo, orden, prioridad, rango de fechas, búsqueda por nombre. |
| ¿Hay estructuras que no se usan? | Juan Cuarán: una cola sin bloqueos en el firmware y una cola de prioridad en la IA están implementadas y probadas, pero hoy no están en el flujo. No hay pilas. |
| ¿Cómo protegen los datos? | Juan Cuarán: contraseñas cifradas, cada rol ve solo lo suyo y se puede borrar la cuenta con todos sus datos. |
| ¿Qué tan preciso es el sensor? | Juan López: mide el pulso a unos 100 Hz con la mediana de varios segundos, y compara con las referencias de la propia atleta, no con un promedio general. |
| ¿Qué falta? | Juan López: conectar más prototipos a la vez y probar con más atletas reales. |
