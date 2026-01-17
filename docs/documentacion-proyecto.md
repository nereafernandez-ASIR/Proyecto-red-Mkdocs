# Elementos Incluidos en el Proyecto MkDocs

## Introducción

En este documento voy a explicar que elementos y características utilicé en la documentación del proyecto de red con MkDocs. He utilizado el tema Material `for MkDocs` junto con diversas extensiones para mejorar con ello la presentación y facilitar la comprensión del contenido.

---

## Extensiones de Markdown

### Admonitions (Bloques de Información)

He utilizado la extensión `admonition` para crear bloques de información a lo largo de la documentación. Estos bloques ayudan a resaltar el contenido importante:

```yaml
markdown_extensions:
  - admonition
  - pymdownx.details
```

**Tipos de admonitions que se usaron:**

- **note**: Para notas explicativas sobre comandos o configuraciones
- **info**: Para información adicional del proyecto
- **tip**: Para consejos y recomendaciones
- **warning**: Para advertencias sobre pasos críticos
- **quote**: Para mi experiencia personal

**Uso en el proyecto:**

```markdown
!!! tip "¿Por qué usar VLANs?"
    Separar la red en VLANs me permite tener más seguridad,
    mejor rendimiento y facilita la gestión.
```

He incluido estos bloques en todas las páginas, en `configuracion.md` para explicar comandos importantes y en `index.md` para destacar información clave del proyecto.

### Diagramas con Mermaid

Otra funcionalidad ha sido la integración de diagramas con Mermaid mediante `pymdownx.superfences`:

```yaml
markdown_extensions:
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
```

Se utilizó con un diagrama completo de la topología de red en `index.md` que muestra:
- La estructura de la red en estrella
- Las 4 VLANs con sus dispositivos
- Las conexiones entre el router, switch y equipos
- Códigos de color diferentes para cada VLAN

Facilitando con ello el esquema del proyecto de red.

### Pestañas de Contenido

Para organizar mejor la información de cada VLAN, he usado `pymdownx.tabbed`:

```yaml
markdown_extensions:
  - pymdownx.tabbed:
      alternate_style: true
```

Las pestañas en `index.md` para mostrar las características de cada VLAN de forma organizada, permitiendo navegar entre "VLAN 10 - PCs", "VLAN 20 - Impresoras", "VLAN 30 - WiFi" y "VLAN 40 - Router" sin sobrecargar la página.

### Resaltado de Código

Se configuró el resaltado de sintaxis para los bloques de código Cisco:

```yaml
markdown_extensions:
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.inlinehilite
```

Todos los comandos de configuración del switch, router y verificación aparecen con sintaxis resaltada, lo que facilita su comprensión. Además, se añadió comentarios dentro de los bloques de código para explicar cada paso.

### Tablas

Se utilizó tablas markdown en varias secciones:

- **Tabla de VLANs** en `index.md`: muestra VLAN, nombre, propósito y rango de red
- **Tabla de direccionamiento** en `configuracion.md`: detalla IPs, máscaras y gateways de cada dispositivo
- **Tabla de impresoras**: con sus IPs específicas
- **Tabla de pruebas** en `pruebas.md`: documenta las comprobaciones realizadas

Las tablas permiten presentar información de forma estructurada y fácil de consultar.

### Iconos y Emojis

Se utilizó la extensión `pymdownx.emoji` para añadir iconos visuales:

```yaml
markdown_extensions:
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
```

Los he utilizado principalmente en `index.md` para indicar permisos de las ACLs (✅ permitido, ❌ bloqueado), haciendo más visual la explicación de las reglas de seguridad.

### Otras Extensiones

También se activó:
- `attr_list`: para atributos HTML adicionales
- `md_in_html`: permite combinar Markdown y HTML
- `footnotes`: para notas de pie

---

## Características del Tema Material

### Paleta de Colores

He configurado dos modos de visualización (claro y oscuro) con colores inspirados en Cisco Packet Tracer:

```yaml
palette:
  - scheme: default
    primary: blue
    accent: cyan
  - scheme: slate
    primary: blue grey
    accent: cyan
```
Se puede alternar en el botón superior derecha.

### Funcionalidades de Navegación

Se utilizó las siguientes funcionalidades:

- **navigation.tabs**: secciones principales aparecen como pestañas en la parte superior
- **navigation.sections**: Organiza el contenido en secciones en el menú lateral
- **navigation.top**: Añade un botón para volver al inicio de la página
- **navigation.footer**: Enlaces de navegación en el pie de página
- **search.suggest**: Sugerencias mientras se escribe en el buscador
- **search.highlight**: Resalta los términos buscados

### Funcionalidades de Código

- **content.code.copy**: Añade un botón de copiar en cada bloque de código
- **content.code.annotation**: Permite anotar el código
- **content.tabs.link**: Vincula pestañas entre diferentes páginas

### Iconos Personalizados

He configurado un icono de red como logo del sitio:

```yaml
icon:
  logo: material/network
  repo: fontawesome/brands/github
```

---

## Plugin de Búsqueda

He activado el plugin de búsqueda configurado en español:

```yaml
plugins:
  - search:
      lang: es
```

Esto permite buscar cualquier término en toda la documentación con resultados en español.

---

## Estructura de Navegación

La navegación del sitio está organizada siguiendo un orden lógico:

```yaml
nav:
  - Inicio: index.md
  - Configuración de Red: configuracion.md
  - Seguridad y ACLs: seguridad.md
  - Pruebas y Monitorización: pruebas.md
  - Conclusiones: conclusiones.md
```

Este orden permite seguir el proyecto desde la presentación inicial hasta las conclusiones finales, pasando por la configuración, seguridad y pruebas.

---

## Resumen de Elementos Utilizados

| Categoría | Elementos |
|-----------|-----------|
| **Bloques especiales** | Admonitions (note, info, tip, warning, quote) |
| **Diagramas** | Mermaid para topología de red |
| **Organización** | Pestañas de contenido, tablas avanzadas |
| **Código** | Resaltado de sintaxis, botón de copiar |
| **Visual** | Iconos, emojis, modo claro/oscuro |
| **Navegación** | Pestañas superiores, búsqueda, footer |
| **Extensiones** | 10+ extensiones de pymdownx |
| **Plugins** | Search en español |

---
