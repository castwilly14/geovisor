# Geovisor Mesoamérica

Este es un visualizador de mapas interactivo ligero, responsivo y moderno basado en Leaflet. Está diseñado para ejecutarse completamente del lado del cliente, lo que lo hace ideal para ser alojado de forma gratuita en **GitHub Pages** sin necesidad de bases de datos ni servidores activos.

---

## Guía de Publicación Rápida (Crea tu propio Geovisor)

Cualquier persona puede crear una copia de este geovisor y publicar su propio mapa con datos personalizados en su cuenta de GitHub siguiendo estos sencillos pasos desde la interfaz web (sin usar consola).

### Paso 1: Hacer un Fork del Repositorio
Un "Fork" crea una copia idéntica de este repositorio bajo tu propia cuenta de GitHub para que puedas hacer cambios de manera independiente.
1. Inicia sesión en tu cuenta de [GitHub](https://github.com).
2. Ve al repositorio original: [https://github.com/copernicuscentroamerica/geovisor](https://github.com/copernicuscentroamerica/geovisor).
3. Haz clic en el botón **Fork** en la esquina superior derecha.
4. Define el propietario (tu cuenta de usuario) y el nombre del repositorio (ej. `mi-geovisor`).
5. Asegúrate de **desmarcar** la opción *'Copy the main branch only'* si deseas descargar todas las versiones disponibles (como la rama `limpio` para el Geovisor 2).
6. Haz clic en **Create fork**.

### Paso 2: Eliminar las Capas de Ejemplo
Para evitar que se muestren las capas que vienen cargadas por defecto, debes borrarlas:
1. Dentro de tu repositorio recién creado, entra a la carpeta `data/`.
2. Para cada archivo que desees eliminar (por ejemplo, `Areas_Protegidas_corte.json` y `Limite_ZonaEstudio.json`):
   - Haz clic sobre el archivo.
   - Presiona el botón de los tres puntos `...` en la esquina superior derecha y selecciona **Delete file** (Eliminar archivo).
   - Confirma presionando el botón verde **Commit changes** abajo.

### Paso 3: Subir tus Propias Capas
Sube tus archivos espaciales en formato GeoJSON o JSON a la carpeta `data/`:
1. Asegúrate de estar dentro de la carpeta `data/` en tu repositorio.
2. Haz clic en **Add file** (Añadir archivo) en la esquina superior derecha y luego en **Upload files** (Subir archivos).
3. Arrastra y suelta tus archivos GeoJSON/JSON propios (por ejemplo: `mi_bosque_mesoamerica.json`).
4. Haz clic en el botón verde **Commit changes** al final de la página para guardar la subida.

> [!TIP]
> Si tienes archivos en formatos espaciales tradicionales como Shapefile (.shp), KML o GPX, puedes usar la herramienta web gratuita [Mapshaper](https://mapshaper.org/) (cuyo enlace directo está integrado en el panel de capas del geovisor) para convertirlos a GeoJSON antes de subirlos.

### Paso 4: Configurar el Archivo de Identidad (`configuracion_geovisor.json`)
Debes registrar tus nuevas capas en el archivo de configuración central para que el geovisor las renderice y personalice tu sitio:
1. Regresa al directorio raíz de tu repositorio en GitHub y abre el archivo `configuracion_geovisor.json`.
2. Haz clic en el icono del **lápiz** para editarlo.
3. Modifica las siguientes propiedades clave:
   - `"titulo_geovisor"`: El título personalizado de tu mapa (ej. `"Geovisor de Juan"`).
   - `"autor_desarrollador"`: Tu nombre o el nombre de tu organización.
   - `"capas_a_cargar"`: Escribe la lista de nombres exactos de los archivos GeoJSON que subiste en la carpeta `data/`, separados por comas y entre comillas.
4. Ejemplo de configuración corregida:
   ```json
   {
     "titulo_geovisor": "Geovisor de Juan",
     "autor_desarrollador": "Mi Organización",
     "mapa_base_defecto": "dark",
     "capas_a_cargar": [
       "mi_bosque_mesoamerica.json"
     ]
   }
   ```
5. Haz clic en **Commit changes** abajo para confirmar la configuración.

### Paso 5: Activar GitHub Pages (Despliegue)
1. En tu repositorio, haz clic en la pestaña **Settings** (Configuración) de la barra superior.
2. En el menú lateral izquierdo, haz clic en **Pages** (bajo la sección *Code and automation*).
3. En la sección **Build and deployment** -> **Branch**:
   - Selecciona la rama que deseas compilar (usa `main` para el geovisor original, o selecciona la rama `limpio` si deseas desplegar la versión simplificada sin filtros).
   - Deja la carpeta en `/ (root)`.
   - Haz clic en **Save** (Guardar).
4. Espera de 1 a 2 minutos hasta que aparezca un check verde. Copia el enlace web generado (ej: `https://tu-usuario.github.io/mi-geovisor/`) ¡y listo! Ya tienes tu geovisor publicado y en vivo.

---

## Desarrollo Local (Avanzado)
Si eres desarrollador y deseas probar o modificar el código de forma local en tu computadora:

1. Clona el repositorio:
   ```bash
   git clone https://github.com/tu-usuario/mi-geovisor.git
   cd mi-geovisor
   ```
2. Ejecuta un servidor local. Si tienes Node.js instalado, puedes levantar el proyecto corriendo:
   ```bash
   node server.js
   ```
   *(Esto levantará un servidor dinámico local en `http://localhost:8081` que escaneará y recargará automáticamente tus archivos de la carpeta `data/` sin necesidad de editar manualmente el archivo JSON de configuración).*
