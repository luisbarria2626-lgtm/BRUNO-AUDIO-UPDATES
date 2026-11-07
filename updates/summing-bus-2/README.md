# SUMMING BUS 2+ — Canal oficial de actualizaciones

Editor: **BRUNO AUDIO**  
Producto: **SUMMING BUS 2+**  
Rama de publicación: `main`

## Estado de publicación

**NO PUBLICADO — versión 1.0.1 pendiente de validación.**

El actualizador C++/JUCE ya dispone de una interfaz local con `WHAT'S NEW`, estado de descarga y verificación de un manifiesto firmado. Esto **no** acredita todavía una actualización completa, un instalador publicado ni pruebas exitosas en un DAW.

Endpoint de producción previsto:

`https://raw.githubusercontent.com/luisbarria2626-lgtm/BRUNO-AUDIO-UPDATES/main/updates/summing-bus-2/latest.json`

Firma separada obligatoria: `latest.json.sig` (misma URL más `.sig`).

La ausencia de estos archivos causa **HTTP 404** y es deliberada hasta que se cumplan las condiciones de publicación.

## Contrato del manifiesto — ejemplo NO publicable

```json
{
  "product": "SUMMING BUS 2+",
  "version": "1.0.1",
  "installer_url": "https://github.com/luisbarria2626-lgtm/BRUNO-AUDIO-UPDATES/releases/download/v1.0.1/BRUNO-AUDIO-SUMMING-BUS-2-Setup.exe",
  "sha256": "SUSTITUIR_POR_SHA256_REAL_DEL_INSTALADOR_FIRMADO",
  "release_notes": [
    "Describir aqui exclusivamente cambios comprobados en la compilacion distribuida"
  ]
}
```

Este JSON ilustra la estructura únicamente: **no copiarlo a `latest.json` para publicación**.

Los campos `release_notes` deben describir mejoras reales (perillas, medidores, DSP, estabilidad, compatibilidad) y verificadas. No afirmar optimizaciones ni correcciones no demostradas.

## Seguridad del actualizador

1. Generar un instalador definitivo desde la compilación VST3 1.0.1 verificada. Conservar los identificadores originales del plugin y el `AppId` del instalador.
2. Probar instalación 1.0.0 → 1.0.1 con Ableton cerrado. Probar expresamente el error de archivo bloqueado y la recuperación ante fallo; nunca borrar a la fuerza un plugin utilizado por un host.
3. Firmar el ejecutable instalador mediante certificado Authenticode válido y comprobar su cadena de confianza. La configuración local `publisher_cert_sha256` deberá coincidir con el certificado del editor utilizado; no conservar marcadores `REPLACE_WITH...`.
4. Calcular SHA-256 **después** de firmar el ejecutable. Publicar el ejecutable inalterado como recurso de GitHub Release y comprobar que la URL permite descargarlo con los redireccionamientos admitidos por JUCE.
5. Generar el `latest.json` con URL, SHA-256 y notas de versión reales. Firmar **los bytes exactos** del archivo con la clave privada RSA correspondiente a `BrunoManifestKey.h`; publicar la firma hexadecimal separada como `latest.json.sig`. No almacenar la clave privada en GitHub.
6. Verificar en un equipo de prueba: firma RSA válida; alteración del manifiesto rechazada; firma del instalador comprobada; descarga completa; tratamiento de 404; host abierto; cancelación; error de permisos; versión instalada correcta.
7. **No marcar `UPDATE COMPLETE` solo porque se inició el instalador**. El actualizador necesita recibir el resultado de finalización y verificar la versión realmente instalada.

## Protocolo de experiencia del usuario

- `CHECK FOR UPDATES` → descargar y validar el manifiesto firmado.
- `WHAT'S NEW` → mostrar únicamente `release_notes` autentificadas.
- `UPDATE` → descargar y verificar el instalador firmado.
- `DOWNLOADING UPDATE` → mostrar progreso real a partir de bytes recibidos; si no se conoce el tamaño, usar progreso indeterminado.
- `INSTALLING` → gestionar el instalador externo, solicitando guardar y cerrar el DAW cuando corresponda.
- `UPDATE COMPLETE` → solo tras instalación exitosa y comprobación final.

## Trabajo pendiente confirmado

- No existe `latest.json` ni `latest.json.sig` en `main`.
- No hay instalador de 1.0.1 firmado y publicado verificado.
- La integración con Inno Setup para progreso de instalación, finalización y confirmación todavía requiere implementación y pruebas.
- No se ha demostrado instalación automática integral de 1.0.0 a 1.0.1.

**Regla:** no activar el endpoint de producción antes de validar estos requisitos.
