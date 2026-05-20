


# Análisis de Sostenibilidad y Optimización Web  
## Floristería Alondra  

## Manuel Parrilla Lahoz

### Fase 1: Inventario y Dimensión Ambiental (A)  

**Medición inicial**  
La página web de Floristería Alondra genera **4.92 g de CO₂ por visita**. [1]  

<img width="458" height="253" alt="image" src="https://github.com/user-attachments/assets/5e3b6b78-5bcb-4b4d-b6f4-aec3c104d6e3" />



**Identificación de Bloatware**  
Aunque el documento HTML inicial carga rápido (30 ms), la página se vuelve pesada debido a la acumulación masiva de recursos secundarios.  

**Causas principales**  
- **Exceso de archivos multimedia**: múltiples videos en formato `.mp4` alojados directamente en el servidor e imágenes de alta resolución (identificadas como `-scaled.jpg`). [2]  
- **Bloat de plugins**: Elementor y WooCommerce disparan decenas de peticiones de archivos CSS y JS independientes, fragmentando la descarga.  
- **Múltiples librerías de iconos**: se descargan tres o más sets de fuentes distintos (FontAwesome, Elementor Icons, Ekiticons, Jkiticon), añadiendo peso innecesario.  

**Sugerencias**  
- Alojar los vídeos en plataformas externas (YouTube o Vimeo) para que el navegador no gestione archivos binarios grandes desde el servidor.  
- Utilizar un plugin de optimización que combine (concatene) y minifique los archivos CSS y JS, reduciendo el número total de peticiones.  
- Convertir las imágenes a formato WebP y ajustar sus dimensiones al tamaño real de visualización.  

**Análisis: ¿sufre la web de “inflación de software”?**  
Sí, por varias razones:  
- **Demasiadas capas**: para mostrar una web sencilla, el navegador tiene que leer cientos de líneas de código de Elementor y WooCommerce que no siempre se usan.  
- **Repetición absurda**: 4 librerías de iconos distintas; es como llevar cuatro diccionarios en la mochila para buscar una sola palabra.  
- **Falta de optimización**: los vídeos y fotos van “a lo bruto”; el motor (navegador) sufre innecesariamente.  

---

### Fase 2: Dimensión Social y Equidad (S)  

**Test de accesibilidad**  
He pasado la página por WAVE y ha obtenido un **9/10**. No tiene errores graves, solo algunos avisos (faltan etiquetas `label` bien colocadas o algún contraste justito). Para llegar a 10 habría que revisar esos warnings y asegurar que todo el mundo, incluso con lectores de pantalla o sin ratón, pueda usarla sin problemas. [3]  

<img width="308" height="151" alt="image" src="https://github.com/user-attachments/assets/037ca5d0-25ca-44a9-8a09-09ccda2a3920" />


**Barreras identificadas**  
A pesar de la buena puntuación, existen dos problemas relevantes:  

1. **Contraste insuficiente**  
   Hay dos elementos cuyo color de fondo y color de texto no tienen suficiente diferencia de brillo. La relación de contraste es inferior a **4.5:1** para texto normal. Esto provoca que personas con baja visión, cataratas, glaucoma o daltonismo no puedan leer el texto con claridad; el texto se “funde” con el fondo.  

2. **Vídeos/audio sin alternativas accesibles**  
   La web incluye 12 elementos de vídeo o audio. WAVE advierte que no puede verificar si son accesibles. Si alguno contiene información relevante (como el proceso de pedido o la descripción de un ramo), una persona sorda no podrá acceder a ese contenido sin subtítulos. Supone una barrera grave para la comunicación.  

---

### Fase 3: Dimensión de Gobernanza y Ética (G)  

#### Transparencia y cookies  
Al analizar la web de Alondra Floristería con la guía de la AEPD sobre cookies, comprobé que **no muestra ningún banner de cookies**, ni siquiera un aviso informativo. Esto incumple la normativa porque el usuario no puede aceptar o rechazar las cookies no esenciales, y el consentimiento tácito por seguir navegando no es válido. La ausencia total de opciones constituye un **patrón oscuro por omisión**. Además, el informe de Lighthouse revela que se cargan scripts de terceros como `trustindex.io` (21,9 KB) y `subventic.com` (11,9 KB) sin ningún control previo, lo que agrava la falta de transparencia. [4][5]  

#### Datos innecesarios  
Al evaluar si el formulario pedía datos excesivos, apliqué el principio de minimización del RGPD (artículo 5.1.c) y consulté las guías de Termly e iubenda. Al inspeccionar el código HTML con las herramientas de desarrollador y revisar el informe de Lighthouse, comprobé que **no existe ningún formulario de contacto funcional**: no aparecen etiquetas `<form>` ni campos como nombre, email o teléfono.  

Por tanto, la web actualmente **no solicita ningún dato personal**, lo que evita el problema de pedir información innecesaria. Sin embargo, la ausencia de un medio real de contacto también es un problema de usabilidad. Si en el futuro implementaran un formulario, lo correcto sería pedir solo nombre, correo y mensaje, nunca DNI o dirección postal. En resumen, no se puede decir que pida datos excesivos porque directamente no hay formulario, pero esa falta de funcionalidad es igualmente criticable.  

---

### Fase 4: Propuesta de Refactorización (Green Coding)  

#### Optimización de activos  
**¿Qué formatos usarías para sustituir las imágenes actuales?**  

Para optimizar las imágenes de la web de Alondra Floristería, usaría **WebP como formato principal** por su excelente compatibilidad (97% de navegadores) y su capacidad de reducir el peso hasta un 30% respecto a JPEG, tal como recomienda el informe de Lighthouse que estima un ahorro de **822 KiB**. Además, implementaría **AVIF como formato de respaldo** para navegadores modernos (compresión hasta un 50% menor que JPEG).  

También generaría múltiples resoluciones con `srcset` para evitar descargar imágenes más grandes de lo necesario, como la imagen de 768×922 píxeles que se muestra en 372×447, desperdiciando ancho de banda. En ningún caso mantendría PNG o JPEG sin comprimir, y solo conservaría PNG para el logotipo si requiere transparencia. Esta estrategia mejoraría drásticamente la velocidad de carga y el **LCP** (Largest Contentful Paint).  

<img width="396" height="430" alt="image" src="https://github.com/user-attachments/assets/c6e87c49-9a9b-4ec1-a280-eb715d7e8994" />


#### Reducción de peticiones  
**¿Qué librerías o scripts externos eliminarías o aplazarías?**  

Para reducir las peticiones y el procesamiento en el cliente, eliminaría o aplazaría varios scripts que el informe de Lighthouse señala como problemáticos:  

- **Eliminaría**  
  - `jQuery Migrate` (no necesario si los plugins no usan versiones antiguas).  
  - El script de emojis de WordPress (`wp-emoji-release.min.js`, 22,8 KB), porque los navegadores modernos los renderizan nativamente.  

- **Aplazaría con `defer` o `async`**  
  - Scripts de terceros como Trustindex (`loader.js`, 21,9 KB).  
  - Fuentes de Google Fonts (bloquean el renderizado; ahorrarían 1,8 segundos).  
  - jQuery (87,5 KB) y Swiper (143,7 KB), que tienen mucho código sin usar; se cargarían solo cuando sean necesarios (al hacer scroll o interactuar con carruseles).  

- **Carga condicional**  
  - Evaluaría si los scripts de Elementor Pro y WooCommerce se pueden cargar solo en páginas donde realmente se usan.  

Con estas medidas se reducirían las peticiones innecesarias y se mejoraría el rendimiento general.  

#### Reflexión sobre la Paradoja de Jevons  
**Si optimizamos la web y carga mucho más rápido, podríamos atraer muchos más usuarios diarios. ¿Cómo evitarías que este éxito anule el ahorro energético conseguido?**  

Si optimizamos la web de Alondra Floristería y consigue cargar mucho más rápido, es probable que atraigamos a más usuarios diarios. Pero aquí surge la **Paradoja de Jevons**: el éxito comercial podría anular el ahorro energético conseguido, ya que el aumento del tráfico podría disparar el consumo total en servidores y dispositivos.  

Para evitarlo, no basta con optimizar imágenes o aplazar scripts; hay que adoptar una **estrategia de sostenibilidad digital** que incluya:  
- Medir el consumo energético por visita.  
- Priorizar funcionalidades esenciales (evitando añadir peso innecesario con cada nuevo plugin o animación).  
- Configurar auditorías automáticas con Lighthouse que alerten si la web supera un presupuesto de carbono o rendimiento.  
- Diseño frugal y *mobile‑first* que minimice la transferencia de datos.  
- Buena política de caché para que los recursos no se descarguen repetidamente.  

Así, el crecimiento de usuarios no se traduce en un aumento desproporcionado del impacto ambiental.  

---

Referencias (formato IEEE)

[1] Website Carbon Calculator, “Carbon estimate for Floristería Alondra,” websitecarbon.com. [En línea]. Disponible en: https://www.websitecarbon.com/ (Consultado: 20 de mayo de 2026).

[2] Google Chrome DevTools, “Network panel analysis for mariadefatimabeltransalado.es,” Chrome Developer Tools, mayo de 2026.

[3] WAVE, “Web Accessibility Evaluation Tool report for mariadefatimabeltransalado.es,” wave.webaim.org. [En línea]. Disponible en: https://wave.webaim.org/ (Consultado: 20 de mayo de 2026).

[4] AEPD, “Guía sobre el uso de las cookies,” Agencia Española de Protección de Datos, 2020. [En línea]. Disponible en: https://www.aepd.es/guias/guia-cookies.pdf

[5] H. Brignull, “Deceptive Patterns (Dark Patterns),” deceptive.design. [En línea]. Disponible en: https://www.deceptive.design/ (Consultado: 20 de mayo de 2026).
