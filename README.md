# Line Check · Rock n' Wok (v1.2 piloto)

App web de validación de apertura. Corre en cualquier navegador y se instala en pantalla de inicio como PWA.

## Actualizar la app en GitHub

Reemplaza `index.html` en tu repositorio (o edítalo con el botón de lápiz) → Commit changes. En 1–2 minutos todos los dispositivos reciben la versión nueva al recargar (si no aparece, cierra y vuelve a abrir la app, o borra caché).

## Novedades v1.2

- Sucursal y Puesto como listas desplegables (obligatorios para firmar)
- Congelador: el signo negativo es automático (solo escribe 18 y se registra –18°C)
- Proteína fría del día: muestra en grande cuál proteína asignó el sistema hoy
- Arroz al vapor: mínimo 3 recetas
- Reporte de WhatsApp disponible AUNQUE NO esté liberado (incluye pendientes y observaciones)
- Descarga del historial en CSV/Excel con cada respuesta, valor, status, comentario y hora

## Historial compartido entre dispositivos (Google Sheets)

Para que todo el equipo vea el historial desde cualquier dispositivo, conecta la app a una hoja de Google:

1. Crea una hoja nueva en Google Sheets (por ejemplo "Line Check Historial").
2. Menú **Extensiones → Apps Script**. Borra el contenido y pega:

```javascript
function doPost(e) {
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var sheet = ss.getSheetByName("Historial") || ss.insertSheet("Historial");
  if (sheet.getLastRow() === 0) {
    sheet.appendRow(["Fecha","Sucursal","Responsable","Puesto","Estado","Score","Bloque","Control","Criticidad","Valor","Status","Comentario","Notificar","Hora"]);
  }
  var d = JSON.parse(e.postData.contents);
  (d.respuestas || []).forEach(function(r) {
    sheet.appendRow([d.fecha, d.sucursal, d.responsable, d.puesto, d.estado, d.score, r.block, r.name, r.crit, r.valor, r.status, r.comment, r.notifica, r.hora]);
  });
  return ContentService.createTextOutput("ok");
}
```

3. Botón **Implementar → Nueva implementación → Tipo: Aplicación web** → "Quién tiene acceso": **Cualquier persona** → Implementar. Copia la URL que te da (termina en `/exec`).
4. Abre `index.html`, busca la línea `const SYNC_URL = "";` (está al inicio) y pega la URL entre las comillas. Sube el archivo actualizado a GitHub.

Listo: cada liberación firmada agrega todas sus respuestas a la hoja automáticamente, y cualquier persona con acceso a la hoja ve el historial de todas las sucursales en tiempo real desde cualquier dispositivo.

## Notas del piloto

- Sin SYNC_URL, el historial vive solo en cada dispositivo (últimos 15 expedientes). Usa un teléfono designado por sucursal.
- Las fotos NO viajan a la hoja (solo los datos); las fotos quedan en el dispositivo y en producción irán a la base de datos central.
- Primera carga requiere internet; después funciona con señal intermitente.
