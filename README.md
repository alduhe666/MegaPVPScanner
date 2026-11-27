# MegaPVP Scanner

Analizador web para **Pokémon GO** que estima los IVs de un Pokémon a partir de una captura y muestra cómo queda su **megaevolución o forma Primal** en los rankings PvP de **Liga Super, Liga Ultra y Liga Master**.

Está pensado para usarse en el navegador, sin servidor propio: la imagen se procesa en el equipo y los resultados se comparan con los rankings de [PvPoke](https://pvpoke.com/).

---

## Qué hace

- **Escáner de imagen**: sube una captura del Pokémon y la app lee el nombre y estima los IVs mediante OCR (Tesseract.js) y análisis de las barras de IV por píxeles.
- **Ajuste manual**: si la lectura no es fiable, los IVs se pueden corregir con deslizadores y botones (`0`–`15`).
- **Detección de Pokémon oscuro**: si se marca como oscuro/purificado, los IVs efectivos se calculan con `+2` por stat, con tope en `15`.
- **Megas y Primals**: incluye formas clásicas, formas de Leyendas Z-A y formas Primal, con tipos, stats y sprites integrados.
- **Rankings por liga**: evalúa las 4.096 combinaciones de IVs para cada liga y nivel (`50`/`51`) usando `atk × def × hp`.
- **Tablas Top**: `Top 10 / 25 / 50 / 100`, ordenables por columnas, con la fila del usuario resaltada y el puesto CMP.
- **CMP**: muestra el puesto por ataque real dentro del Top 100 (`#X`), o `+Top 100` / `-Top 100` cuando el ataque supera o queda por debajo del Top 100.
- **Barra de PC por nivel**: deslizador del nivel `1` al `51` con la misma fórmula de PC y los IVs efectivos.
- **Historial**: guarda hasta 10 combinaciones con miniatura de la captura, rango por liga/nivel y restauración de cualquier entrada.
- **Comparación**: selecciona una o más entradas de la misma especie y abre un análisis en PvPoke con el Rank `#1` y los IVs elegidos.
- **Enlaces a PvPoke**: matriz con un solo grupo de Pokémon, sin duplicados, usando los alias y los tokens de IVs/nivel de PvPoke.

---

## Uso

1. Abre `index.html` en un navegador moderno (Chrome, Edge, Firefox o Safari).
2. Sube una captura de Pokémon GO o ajusta los IVs manualmente en el paso **2. Especie e IVs**.
3. Escribe o elige la línea evolutiva en el selector (acepta búsqueda parcial).
4. Revisa las tarjetas de Mega/Primal: verás PC, stats, rango por liga, CMP y la tabla Top.
5. Usa los iconos de Super / Ultra / Master para mostrar u ocultar bloques de liga.
6. Pulsa **Guardar combinación** para añadir el análisis al historial.
7. Desde el historial puedes restaurar una entrada o marcar varias de la misma especie y pulsar **Analizar en PvPoke**.

La primera carga necesita conexión para las librerías y fuentes desde CDN; después el análisis se hace en el navegador.

---

## Detalles técnicos

- **Una sola página**: toda la app, la base de datos de megas/primals, los sprites, iconos y logos están dentro del HTML.
- **OCR local**: `tesseract.js@5` se ejecuta en el navegador; las imágenes no se envían a ningún servidor.
- **UI**: Tailwind CSS, Lucide y Google Fonts (`Inter` / `Outfit`).
- **Persistencia**: `localStorage` con dos claves independientes:
  - `ivscan-mega-pvp-state-v1` → estado actual (IVs, ligas, niveles, etc.).
  - `ivscan-mega-pvp-history-v1` → historial (máximo 10 entradas, con miniaturas JPEG).
- **Referencia de datos**: rankings y alias alineados con PvPoke; stats base y megaenergía tomados de *game masters* de PokeMiners; sprites de Pokémon Showdown; iconos de megaenergía de Bulbagarden.

---

## Estructura

```text
.
├── index.html   # aplicación completa (HTML + CSS + JS + datos embebidos)
└── README.md    # este archivo
```

---

## Limitaciones

- Solo se calculan rankings para los niveles **50** y **51**.
- Las barras de IV pueden dar valores aproximados; la app lo indica y permite corregirlos a mano.
- Algunas formas todavía no están incluidas en PvPoke; en esos casos el botón de análisis se deshabilita.
- La matriz de PvPoke acepta hasta 8 Pokémon por grupo.

---

## Aviso

Proyecto no oficial, sin afiliación con Niantic, The Pokémon Company ni PvPoke. Pokémon y sus nombres son marcas registradas de sus respectivos propietarios.
