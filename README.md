# TRIS Analytics 🍀

Dashboard estadístico del sorteo TRIS. Está construido en un único `index.html` (HTML, CSS y JavaScript) y utiliza `Tris.csv` como archivo histórico. No requiere backend ni dependencias externas.

## Archivos

- `index.html`: aplicación completa.
- `Tris.csv`: histórico base. Debe estar en la misma carpeta que `index.html`.

## Probar en local

Los navegadores suelen bloquear `fetch()` de archivos locales abiertos con doble clic (`file://`). Inicia un servidor web desde la carpeta que contiene ambos archivos:

```bash
python -m http.server 8000
```

Abre `http://localhost:8000`.

También puedes usar la extensión **Live Server** de Visual Studio Code.

## Publicar en GitHub Pages

1. Crea un repositorio en GitHub.
2. Sube `index.html`, `Tris.csv` y `README.md` a la raíz del repositorio.
3. Entra en **Settings → Pages**.
4. En **Build and deployment**, selecciona **Deploy from a branch**.
5. Selecciona la rama `main` y la carpeta `/ (root)`, y guarda.
6. Espera a que GitHub Pages publique el sitio y abre la URL que aparece en esa sección.

Asegúrate de respetar exactamente el nombre `Tris.csv` (incluidas mayúsculas y minúsculas).

## Administración

- Pulsa **Administración** en el encabezado.
- En **Agregar sorteo manual**, captura concurso, fecha, tipo, multiplicador y los cinco dígitos.
- En **Importar CSV**, selecciona un archivo con las mismas columnas del histórico, revisa la vista previa y confirma.
- La aplicación evita duplicados por `CONCURSO`.
- **Exportar datos completos** descarga un CSV combinado.
- Los sorteos manuales/importados se guardan en `localStorage` del navegador y se marcan como Manual. El histórico original se identifica como CSV base.

### Contraseña opcional

En el JavaScript de `index.html`, modifica:

```js
const ADMIN_PASSWORD = "";
```

Por ejemplo:

```js
const ADMIN_PASSWORD = "admin";
```

Deja la cadena vacía para desactivar la solicitud de contraseña.

**Importante:** esta contraseña es únicamente una barrera visual del lado del navegador. No es seguridad real: cualquier persona con acceso al código fuente puede verla. GitHub Pages es hosting estático y no proporciona autenticación ni sincronización entre usuarios/dispositivos. Para administración segura y multiusuario se necesitaría un backend con autenticación.

## Criterios estadísticos

- Las frecuencias cuentan cada dígito válido en cada posición R1–R5. Las celdas vacías se omiten.
- Tercias y cuartetos son secuencias contiguas de 3 y 4 posiciones dentro de cada sorteo completo.
- El resumen de análisis respeta el filtro de fechas. Los últimos siete días con datos se muestran independientemente del filtro.
- El generador Premium produce cuatro dígitos con paridad 2 pares / 2 impares, porque se solicitaron cuatro dígitos. El patrón 2 pares / 3 impares corresponde a cinco dígitos. Sus ponderaciones son heurísticas y no predicen resultados.

## Aviso

Este análisis es estadístico e informativo. No garantiza premios. Cada sorteo es aleatorio y las frecuencias históricas no cambian la probabilidad matemática de un resultado futuro.
