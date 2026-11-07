# BRUNO AUDIO PREMIUM DOWNLOADER — publicación Windows

**Estado: preparación. No hay release publicada para este producto.**

## A. Requisitos para distribuir
- [ ] Identificar versión semántica real (X.Y.Z) y asociarla con el ejecutable compilado.
- [ ] Ejecutar BRUNO desde una carpeta limpia, fuera del árbol de compilación, en Windows 10/11 compatibles.
- [ ] Verificar despliegue de DLLs Qt y plugins de plataforma mediante `windeployqt --release`.
- [ ] Verificar herramientas externas necesarias (por ejemplo, ffmpeg, ffprobe, yt-dlp) y sus licencias; no asumir que vienen incluidas en el ejecutable.
- [ ] Auditar rutas de carga de recursos, Qt Multimedia, modelos IA y dependencias Python. No publicar `.venv` sin una estrategia de redistribución, licencias y tamaño validados.
- [ ] Probar descarga, reproducción, metadatos, Voice Separation, Music Removal, Dereverb WPE, errores y reinicio desde la distribución real.
- [ ] Verificar integridad SHA-256 del paquete de entrega y firma Authenticode del instalador; conservar evidencia de pruebas.
- [ ] Publicar manualmente una GitHub Release con tag exclusivo de este producto, p.ej. `bruno-downloader-vX.Y.Z`, solo cuando esté aprobado.

## B. Manifiesto (publicar al final)
Ruta: `updates/bruno-audio-premium-downloader/latest.json`.

Esquema consumido por Update Engine V1.1:

```json
{
  "schema": 1,
  "version": "X.Y.Z",
  "notes": "Cambios verificados de la nueva versión.",
  "release_page": "https://github.com/luisbarria2626-lgtm/BRUNO-AUDIO-UPDATES/releases/tag/bruno-downloader-vX.Y.Z"
}
```

Reemplazar `X.Y.Z` por la versión realmente publicada. Verificar URL, JSON y tag antes de activar clientes.

## C. Cliente BRUNO
- URL del manifiesto: `https://raw.githubusercontent.com/luisbarria2626-lgtm/BRUNO-AUDIO-UPDATES/main/updates/bruno-audio-premium-downloader/latest.json`
- `updates/update-config.json` conserva `enabled: false` mientras no exista Release real.
- Sustituir `installed_version: 0.0.0` por la versión *real*, no inferirla del nombre del programa.
- V1.1 **solo compara y notifica**; no descarga ni instala automáticamente. La página enlazada es informativa.

## D. Separación de proyectos
No modificar `updates/summing-bus-2` ni el protocolo de firma de otros productos. No subir archivos personales, secretos, tokens, claves privadas o datos de usuarios.
