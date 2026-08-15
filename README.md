# Leonardo's D&D companion v0.5.2

Companion musical web/PWA para sesiones de D&D.

## Archivos

- `index.html`: aplicación completa.
- `library.json`: biblioteca canónica.
- `manifest.webmanifest`: instalación PWA.
- `sw.js`: shell offline.
- `icon.svg`: icono.

## Publicación

GitHub Pages debe publicar `main` desde `/ (root)`.

## Persistencia

1. Al abrir, la app lee `library.json` desde GitHub Pages.
2. Las ediciones se guardan de inmediato en `localStorage`.
3. `Sync` actualiza `library.json` mediante GitHub Contents API.
4. El token se guarda solo en el navegador del dispositivo.

## Token

Crear un fine-grained Personal Access Token limitado a este repositorio con:

- Repository permissions → Contents → Read and write.

No insertar el token directamente en el repositorio.

## Playlist import

El importador usa YouTube IFrame Player API para:
- cargar/cue una playlist pública o no listada;
- obtener `getPlaylist()` con los IDs;
- leer metadata básica al hacer `cueVideoById`.

Las playlists privadas pueden requerir autenticación adicional y no forman parte de esta versión.


## Cambios v0.4.1

- Se elimina Acceso rápido del menú principal.
- La edición pasa a ser centrada en cada categoría.
- Al editar una categoría se muestran y administran únicamente sus pistas.
- Agregar pista e importar playlist se realizan directamente dentro de la categoría.


## Cambios v0.4.2

- Lock global `syncInProgress`: nunca puede haber dos operaciones de Sync concurrentes.
- Los botones con `data-action="sync"` se deshabilitan durante la operación.
- `writeLibraryToGitHub()` encapsula GET SHA + validación + PUT.
- Ante `409 Conflict`, relee el SHA y reintenta exactamente una vez.
- No existe loop de reintentos.
- `dirty=0` solo se escribe después de un PUT exitoso.
- Ante cualquier error o cancelación, el borrador local se conserva y queda `dirty=1`.


## Cambio v0.4.3

- Nombre oficial de la app: `Leonardo's D&D companion`.


## Cambios v0.4.4

- El importador de playlists deja de depender de YouTube IFrame `cuePlaylist()`.
- Usa YouTube Data API `playlistItems.list`.
- Requiere una YouTube Data API key guardada solo en el navegador.
- Paginación automática de 50 elementos por página.
- Conserva el orden original de la playlist.
- Evita duplicados por `videoId`.
- Detecta videos privados/eliminados.
- Resumen final: importadas, duplicadas y no disponibles.

## Cambios v0.4.5
- Sidebar colapsable, con preferencia persistente por dispositivo.
- Cada escena agrega reproducción en orden y aleatoria.
- La reproducción de escena continúa automáticamente al terminar una pista.
- Tarjetas de canciones más compactas y sin enlace YouTube Music.
- Estilos: Legacy, Simple, Light y Medieval.
- Selector colapsable con 60 emojis útiles.
- Importación de playlist con previsualización y selección individual.


## Cambios v0.5.0

### Navegación
- Sidebar colapsable y con opción de fijarlo.
- Secciones: Música, Mapas y Personajes.

### Música
- Controles Anterior / Siguiente en reproducción de escena.
- Fade/crossfade configurable de 0 a 30 segundos.
- Tema Simple conserva tarjetas visibles, cuadradas y sin redondeos.
- Tipografía Sans Serif condensada.

### Mapas
- Múltiples mapas PNG/JPG.
- Escala por ancho y alto reales del mapa.
- Medición lineal origen/destino.
- Ruta a mano alzada con cálculo acumulado.
- Importar/exportar `maps.json`.

### Personajes
- PCs, NPCs, aliados, enemigos y facciones.
- Retrato, raza/especie, clase/rol, nivel, CA, HP, velocidad, percepción pasiva.
- Personalidad, objetivos, vínculos, secretos del DM, notas y tags.
- HP editable durante la sesión.
- Importar/exportar `characters.json`.


## Cambios v0.5.1

- Corrección de persistencia de mapas:
  - imágenes en IndexedDB;
  - metadata en localStorage;
  - ya no se guardan PNG/JPG base64 dentro de localStorage.
- Migración automática de mapas antiguos que sí tengan `imageData`.
- Exportar `maps.json` sigue incluyendo las imágenes para portabilidad.
- Importar `maps.json` restaura imágenes en IndexedDB.
- Tema Simple recupera 10 px de separación entre boxes.
- Fuente preferida: Audrey Sans / Audrey, con fallback sans serif condensado.


## Cambios v0.5.2

- Los mapas se muestran ajustados al espacio disponible en pantalla.
- La resolución original se conserva solo como referencia interna para medición.
- Controles de zoom:
  - Alejar
  - Ajustar
  - Acercar
- Zoom máximo: 400%.
- Las mediciones siguen usando coordenadas de resolución original y no cambian al hacer zoom.
- El botón Ajustar vuelve a encajar completamente el mapa en el visor.
