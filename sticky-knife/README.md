# Sticky Knife · Mesa

Panel interno para las cenas de pasos con cata de extractos: reservas, quién es cada
cupo, menú de maridajes y las cuentas de cada noche.

Es un solo archivo, `index.html`. No necesita build ni dependencias: se abre y anda.

---

## Qué resuelve

**Cupos y reservas.** Cada cena se dibuja como una mesa: los cupos son asientos, no
filas de una tabla. De un vistazo se ve quién está sentado dónde, quién señó, quién
pagó todo y quién vino. Tocás un asiento y cargás o editás la reserva ahí mismo.

**Quién es cada cupo.** Libreta de comensales con Instagram, teléfono, restricciones
alimentarias, tolerancia e historial completo (cuántas veces vino, cuánto gastó,
cuánto debe). Las restricciones y las tolerancias bajas suben solas a la pantalla
*Hoy* como alertas antes de cada cena.

**Los pasos.** Cada paso lleva plato + extracto maridado, con tipo, micras,
temperatura de dabeo en °C y perfil de terpenos. Abajo, el recorrido térmico de toda
la cata en un gráfico.

**Los números.** Vista mensual con lo que entró, lo que salió, el margen y lo que
falta cobrar. Comparativa cena por cena y ranking de gastos por categoría.
Exportación a CSV.

### Una decisión de contabilidad
Los cupos cobrados **no** se cargan a mano: se suman solos desde lo que está pagado
en cada mesa. En *Movimientos* van únicamente los gastos y los ingresos extra
(merch, colaboraciones, propinas). Así no hay doble conteo, que es el error clásico
cuando reserva y caja se llevan en planillas separadas.

---

## Dónde viven los datos

Publicado como Artifact, usa la capability `db`: los datos se guardan en la nube y
los cambios aparecen en todos los dispositivos que abran el link. El indicador del
pie del riel lo dice — *Sincronizado* o *Guardado local*.

Si `db` no está disponible, la app no se rompe: cae a `localStorage` y sigue
funcionando en ese navegador. El logo se sube con la capability `assets`; las
exportaciones a CSV usan `downloads`, con copiado al portapapeles como respaldo.

Colecciones: `cenas`, `reservas`, `pasos`, `comensales`, `movimientos`, más el
documento `config/marca`.

---

## Marca

**Pendiente: el logo y los hex reales.** No pude acceder al Instagram de la marca
desde el entorno donde se construyó esto (bloqueado por el proxy de red), así que la
paleta es una propuesta razonada, no la paleta oficial.

La dirección parte del nombre: *Sticky Knife* refiere a los **hot knives**, calentar
dos hojas para vaporizar hachís. De ahí el concepto: **acero al fuego**.

| Token | Oscuro | Claro | Rol |
|---|---|---|---|
| `--brand-accent` | `#E0561F` | `#B8431A` | Brasa. Botones, cupos ocupados, número de paso |
| `--brand-second` | `#C4862B` | `#8F5F13` | Resina. Maridajes, ingresos |
| fondo | `#0C0D10` | `#F1EEE8` | Casi negro con sesgo acero / hueso cálido |
| `--chart-out` | `#2196B8` | `#0079A8` | Acero frío. Egresos |

Tipografías: **Big Shoulders Display** (títulos y cifras), **Archivo** (texto),
**JetBrains Mono** (plata, fechas, temperaturas).

Los dos colores de marca se editan en vivo desde la pantalla **Marca**, junto con el
logo, la moneda y los precios por defecto. La versión clara de cada color se deriva
sola para que el texto siga legible. El cuchillo con la gota de resina es un dibujo
provisional hasta tener el logo real.

### Accesibilidad del color
Las dos series de los gráficos (`entró` / `salió`) se validaron contra los seis
chequeos de paleta en ambos temas: banda de luminosidad, piso de croma, separación
para daltonismo (ΔE 18.6 protan en oscuro, 19.7 en claro), piso de visión normal y
contraste contra la superficie. Además nunca van solas: siempre hay leyenda y
rótulo directo.

---

## Datos de ejemplo

Al abrirse por primera vez la app se carga con una cena armada, doce comensales, un
menú de seis pasos y movimientos de dos meses, todo inventado y marcado como tal con
un cartel. **Empezar de cero** lo borra y arranca limpio.
