# D&D Music Companion v0.4

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
