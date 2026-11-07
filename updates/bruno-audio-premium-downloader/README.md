# BRUNO AUDIO PREMIUM DOWNLOADER — canal de actualizaciones

Repositorio: https://github.com/luisbarria2626-lgtm/BRUNO-AUDIO-UPDATES

## Estado actual
Canal preparado; sin versión publicada. No existe todavía `latest.json` en este directorio y el cliente debe permanecer con `enabled: false` hasta la primera versión real.

## Ruta del manifiesto
`https://raw.githubusercontent.com/luisbarria2626-lgtm/BRUNO-AUDIO-UPDATES/main/updates/bruno-audio-premium-downloader/latest.json`

## Contrato de V1.1
```json
{
  "schema": 1,
  "version": "1.0.1",
  "notes": "Notas de la versión realmente publicada.",
  "release_page": "https://github.com/luisbarria2626-lgtm/BRUNO-AUDIO-UPDATES/releases/tag/bruno-downloader-v1.0.1"
}
```

El JSON anterior es solo ejemplo. **No publicarlo como latest.json hasta tener una Release real y verificada.** La versión en `update-config.json` debe coincidir con la versión instalada.

## Protocolo de publicación
1. Compilar el proyecto en Release y ejecutar pruebas de descargas, reproducción y Estudio IA.
2. Crear una GitHub Release con paquete de distribución e instalador firmados, versión y notas.
3. Verificar firma Authenticode y SHA-256 del instalador que se distribuye.
4. Publicar `latest.json` con la misma versión y la URL HTTPS de la Release.
5. Verificar que `latest.json` devuelve HTTP 200 y JSON válido.
6. Solo entonces activar `updates/update-config.json` en clientes que tengan la versión instalada correcta.

## Límites de seguridad
El motor V1.1 **solo notifica** y puede abrir la página HTTPS de lanzamiento. No descarga ni instala ejecutables automáticamente. No cargar claves privadas, tokens, entornos virtuales de Python ni archivos de usuario en este repositorio público.

Módulos de otros productos, incluido `updates/summing-bus-2`, permanecen independientes.
