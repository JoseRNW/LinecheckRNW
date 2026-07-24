# Line Check · Rock n' Wok (v1.1 piloto)

App web de validación de apertura de sucursales. Corre en cualquier navegador y se instala en la pantalla de inicio como PWA (sin App Store).

## Publicar con GitHub Pages

1. Crea un repositorio nuevo (público) llamado `line-check`.
2. Sube TODOS los archivos de esta carpeta: `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`, `README.md`.
3. En el repositorio: **Settings → Pages → Source: Deploy from a branch → Branch: main / (root) → Save**.
4. Espera 1–2 minutos. Tu app quedará en: `https://TU-USUARIO.github.io/line-check/`

## Instalar en el teléfono de la sucursal

- **iPhone (Safari):** abrir la URL → botón Compartir → **"Agregar a pantalla de inicio"**.
- **Android (Chrome):** abrir la URL → menú ⋮ → **"Instalar app"** o "Agregar a pantalla principal".

Queda con ícono propio y pantalla completa, como app nativa.

## Actualizar la app

Edita o reemplaza `index.html` en GitHub (botón lápiz o volver a subir el archivo) → Commit. En 1–2 minutos todos los dispositivos reciben la versión nueva al recargar.

## Notas del piloto

- Los datos (capturas, historial y fotos) se guardan **en cada dispositivo** (localStorage). Usa un solo teléfono o tablet designado por sucursal.
- El historial conserva los últimos 15 expedientes firmados por dispositivo.
- El reporte al grupo se hace con el botón "Copiar resumen para WhatsApp" tras firmar la liberación.
- La primera carga requiere internet; después funciona aún con señal intermitente (service worker).
- En producción (Foodbot) los datos migran a base de datos central con notificaciones automáticas.
