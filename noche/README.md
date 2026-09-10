# La Noche · Sticky Knife

La web que abren los comensales **durante** la cena de pasos. Un solo archivo,
`index.html`, sin build ni dependencias.

> Sabores y terpenos — cenas privadas con degustación de extractos, Buenos Aires.

---

## La idea

Un link por comensal que **cambia de estado solo** a lo largo de la noche. Lo
guardan una vez y les sirve las tres veces.

| Momento | Qué muestra |
|---|---|
| **Antes** | Cuenta regresiva, puerta, lugar, cómo venir — y cargan ellos mismos sus restricciones. |
| **Durante** | El paso que se está sirviendo ahora, porque el anfitrión lo avanza desde su teléfono. |
| **Después** | El recuerdo: menú completo, las palabras de la mesa, el álbum, los productores y la próxima cena. |

---

## Las tres restricciones que mandan el diseño

Esto no se usa sentado en un escritorio. Se usa **volado, comiendo, y en una mesa
con otras nueve personas**. Cada decisión sale de ahí.

**Volados** → baja la memoria de trabajo, sube el pensamiento asociativo. Nada de
analizar; todo de asociar.

**Comiendo** → una mano, dedos grasosos. Objetivos táctiles de 44 px para arriba,
casi todo se lee y no se opera.

**En mesa** → un celular en una cena es antisocial por defecto. De ahí sale la
regla estética que ordena la pantalla entera:

### El teléfono se comporta como una vela
A los 28 segundos sin tocarlo la pantalla se apaga sola hasta quedar una brasa
tenue con el nombre del extracto. Un toque la despierta. No compite con la mesa.
Nunca se apaga con un campo de texto enfocado ni con una hoja abierta.

---

## Las dos capturas

### Una palabra, no un puntaje
Nadie quiere puntuar del 1 al 10 lo que está comiendo. Quiere **nombrarlo**.

Un campo de una palabra, más **palabras para tocar sacadas del perfil de terpenos
de ese extracto** — cítrico, humo, pino, tierra. Un toque, cero análisis.

La palabra se suma a la de los otros nueve **en vivo**. Se agrupa por palabra, no
por persona: si tres dicen "humo", es un solo chip que se enciende con `×3`. El
teléfono deja de ser antisocial y pasa a ser disparador de charla.

De regalo, Sticky Knife se queda con el vocabulario real que su gente usa para
cada extracto — copy escrito por los clientes.

### El pulso, no una encuesta
Un arrastre sin números, de *liviano* a *muy volado*. No es para el comensal: es
un **instrumento de servicio**. El anfitrión ve el promedio de la mesa y decide si
el próximo dab va más suave.

Con un botón discreto **"Necesito un momento"** que llega sólo al anfitrión, sin
que se entere el resto. Nadie tiene que levantar la mano y pasar vergüenza.

---

## Modo anfitrión

**Cuatro toques sobre el logo** (o `#anfitrion` en la URL). Desde ahí:

- cambiar el momento de la noche (antes / en la mesa / el día después)
- avanzar y retroceder el paso — los teléfonos de la mesa cambian solos
- ver el pulso de cada comensal y quién pidió una pausa
- leer las restricciones que cargaron
- subir el logo real

No tiene contraseña: es el teléfono del anfitrión y la protección es que nadie
sabe el gesto. Si alguna vez importa, se resuelve con reglas de acceso por nivel.

---

## Datos

Con la capability `db`, el estado de la noche y las palabras se sincronizan en
vivo entre todos los teléfonos. Sin ella cae a `localStorage` y la web sigue
funcionando sola.

Las fotos se reducen a 1100 px y se comprimen antes de guardarse; con `assets`
van a la nube, sin ella quedan en el dispositivo.

Documentos: `noche/estado`, y las colecciones `palabras`, `pulso`, `fotos`, `mesa`.

**La mesa de ejemplo se borra sola.** Mientras un paso tiene menos de tres palabras
reales se completan con palabras de una mesa inventada, marcadas como tales, para
que el gesto se entienda aunque estés probando solo. En cuanto habla la mesa real,
desaparecen.

---

## Marca

Paleta tomada del logo real:

| Token | Valor | De dónde sale |
|---|---|---|
| `--brasa` | `#E9541D` | el naranja del círculo |
| `--rojo` | `#DE3126` | el lettering STICKY KNIFE |
| `--verde` | `#5C8340` | los cogollos, subido para leer en negro |
| `--resina` | `#E8B15C` | el ámbar del extracto |
| `--hueso` | `#F0E9D6` | el crema de la hoja del cuchillo |

Tipografías: **Fraunces** (platos), **Big Shoulders Display** (números y rótulos),
**Archivo** (texto), **JetBrains Mono** (temperaturas, horas, datos).

**Un solo tema, a propósito.** No hay modo claro: esto se usa en una mesa a media
luz y una pantalla blanca arruina la noche y la visión nocturna. Todos los colores
se pintan explícitos para que la página se sostenga sobre cualquier fondo.

El sello dibujado en SVG es provisional — repite la composición del logo real
(círculo naranja, hoja crema, cogollos verdes) hasta que se suba el archivo desde
modo anfitrión.

---

## Pendiente para producción

Un artifact que declara `db` queda restringido a la organización, así que **los
comensales de verdad todavía no pueden abrirlo**. Esto es un prototipo completo y
jugable para decidir la experiencia. Para salir a la mesa hay que deployarlo con
backend propio; el código no depende de nada de acá salvo la capa `conectar()`.
