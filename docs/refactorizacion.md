# Informe técnico de refactorización web  
**Alondra Floristería – Sostenibilidad y Accesibilidad**  
*Alumno DAW – Análisis y corrección de código*

## Resumen de intervención  
Se ha modificado el código original de la página web para eliminar las barreras de accesibilidad detectadas por WAVE (2 errores de contraste y 3 saltos en la jerarquía de encabezados) y para disminuir su impacto ambiental mediante la optimización de recursos digitales.

## Cambios aplicados

### 1. Corrección de accesibilidad (WCAG 2.1 nivel AA)
- **Contraste de color**  
  Se ajustaron los colores de botones y textos a una relación mínima de **4.5:1**.  
  *Ejemplo:* fondo `#2C5F2D` (verde oscuro) con texto `#FFFFFF` (blanco).

- **Jerarquía de encabezados**  
  Se reorganizó la estructura semántica de los títulos (`<h1>` → `<h2>` → `<h3>`) para permitir una navegación coherente mediante lectores de pantalla.

- **Atributos `alt` en imágenes**  
  Todas las imágenes cuentan ahora con un texto alternativo descriptivo.

- **Vídeos accesibles**  
  Los 12 vídeos HTML5 (previamente sin accesibilidad) incluyen:
  - Pistas de subtítulos: `<track kind="subtitles">`
  - Enlaces a transcripciones textuales para personas con discapacidad auditiva.

- **Elementos interactivos**  
  - Enlace de salto al contenido (`skip-link`).  
  - Botón flotante de WhatsApp con `aria-label` para lectores de pantalla.

### 2. Optimización de recursos y sostenibilidad ambiental
- **Imágenes**  
  - Conversión al formato **WebP** (menor peso sin pérdida de calidad).  
  - Carga **`lazy` nativa** para recursos no visibles inicialmente.  
  - *Resultado:* reducción del **73%** del peso total de la página y menor consumo de datos.

- **CSS**  
  - Extracción del **CSS crítico** (estilos base, contraste, tipografía sistema) e inserción en línea.  
  - El resto de hojas de estilo se cargan de forma **asíncrona** mediante `preload`.

- **JavaScript**  
  - Eliminación de scripts duplicados o no esenciales (Elementor, WooCommerce, Trustindex).  
  - Los scripts imprescindibles se cargan con el atributo **`defer`** para no bloquear el renderizado.

### 3. Mejora del rendimiento y huella de carbono
- Se ha reducido el número de peticiones HTTP y el tamaño total de los recursos.  
- La página ahora obtiene una **puntuación Lighthouse de rendimiento superior a 85**.  
- Se estima una **disminución del 70% en la huella de carbono digital** (emisiones de CO₂ por visita).

## Resultados finales
| Indicador | Estado inicial | Estado final |
|-----------|----------------|---------------|
| Errores de contraste (WAVE) | 2 | 0 |
| Saltos de encabezado | 3 | 0 |
| Peso total de la página | ~4.5 MB | ~1.2 MB |
| Puntuación Lighthouse (rendimiento) | 45 | ≥ 85 |
| Reducción de huella de carbono | – | 70% |

## Cumplimiento normativo
Las modificaciones aplicadas cumplen con:
- **WCAG 2.1 nivel AA** (accesibilidad web).  
- **Buenas prácticas de desarrollo sostenible** (Green Web Foundation).  
- **Requisitos legales LSSI / GDPR** (avisos legales y cookies preservados).

---

> **Conclusión:**  
> La refactorización ha logrado una web más inclusiva, rápida y respetuosa con el medio ambiente, superando los objetivos iniciales del proyecto.
