# 

# 

# Empresa: Florísteria Alondra

# Auditoría ASG y Refactorización Sostenible

## AEE RA6

## Manuel Parrilla Lahoz

# 

## 

## Fase 1: Inventario y Dimensión Ambiental (A)

Analiza el peso y consumo de la web elegida.

1. **Medición inicial**. Utiliza herramientas gratuitas como *Website Carbon Calculator* o *Lighthouse* (pestaña de rendimiento en Chrome/Edge) para obtener la huella de carbono estimada por visita.  
   La pagina Web de Florísteria Alondra genera 4.92g de CO2 cada visita. **\[1\]**  
     
2. **Identificación de *Bloatware***. Inspecciona la red (*Network*) en las herramientas de desarrollador del navegador. Identifica los 3 recursos más pesados que se descargan al abrir la web (imágenes sin comprimir, vídeos de fondo, librerías JavaScript pesadas, etc.).

Aunque el documento HTML inicial carga rápido (30 ms), la página se vuelve "pesada" debido a la acumulación masiva de recursos secundarios que el navegador debe descargar tras procesar ese primer archivo.

**Causas Principales:**

* **Exceso de archivos multimedia:** Carga múltiples videos en formato .mp4 directamente desde el servidor y varias imágenes de alta resolución (identificadas como \-scaled.jpg). **\[2\]**  
* **Bloat de plugins:** Al usar Elementor y WooCommerce, se disparan decenas de peticiones de archivos CSS y JS independientes. Cada plugin añade su propia carga, fragmentando la descarga.  
* **Múltiples librerías de iconos:** Se descargan tres o más sets de fuentes distintos (FontAwesome, Elementor Icons, Ekiticons, Jkiticon), lo que añade peso innecesario.

**Sugerencias:**

* **Aloja los videos en plataformas externas** (YouTube o Vimeo) para que el navegador no tenga que gestionar archivos binarios tan grandes desde tu servidor.  
* **Utiliza un plugin de optimización** para combinar (concatenar) y minificar los archivos CSS y JS, reduciendo el número total de peticiones.  
* **Convierte las imágenes a formato WebP** y asegúrate de que sus dimensiones coincidan con el tamaño en el que se muestran realmente.


  


3. **Análisis**. ¿Crees que la web sufre de "inflación de software"? Justifica tu respuesta.

Si, por varias razones:

* **Demasiadas capas:** Para mostrar una web sencilla, el navegador tiene que leer cientos de líneas de código de Elementor y WooCommerce que no siempre se usan.  
* **Repetición absurda:** Tienes 4 librerías de iconos distintas. Es como llevar 4 diccionarios en la mochila para buscar solo una palabra.  
* **Falta de optimización:** Los vídeos y fotos van "a lo bruto". Es como intentar meter un mueble de IKEA sin montar en un coche pequeño; al final, el motor (el navegador) sufre.


## Fase 2: Dimensión Social y Equidad (S)

La web debe ser utilizable por todos. Evalúa la accesibilidad (Sostenibilidad Social):

1. **Test de Accesibilidad**. Pasa una herramienta como *WAVE Web Accessibility Evaluation Tool* o el propio *Lighthouse* (pestaña *Accessibility*).  
   He pasado la página por WAVE y me ha dado un 9\. Eso significa que no tiene errores graves, solo algunos avisillos. Por ejemplo, puede que falte algún label bien puesto o que algún contraste esté justito, pero en general es accesible. Para llegar a 10 tendría que repasar esos warnings y asegurarme de que todo el mundo, incluso con lectores de pantalla o sin ratón, pueda usarla sin problemas. \[3\]  
     
     
     
     
     
2. **Identificación de barreras**. Documenta al menos 2 problemas graves que impidan a personas con diversidad funcional usar la web correctamente (ej. falta de atributos *alt* en imágenes clave, bajo contraste de colores en botones, formularios sin etiquetas).  
   A pesar de que la página web tiene un 9 en el test de accesibilidad de wave hay 2 errores que todavía habría que corregir:  
* Hay dos elementos cuyo color de fondo y color de texto no tienen suficiente diferencia de brillo. La relación de contraste es inferior a 4.5:1 para texto normal lo cual provoca que personas con baja visión, cataratas, glaucoma o daltonismo no pueden leer el texto con claridad. Para ellos, el texto se “funde” con el fondo, volviéndose invisible o muy difícil de distinguir. 


* La web incluye 12 elementos de vídeo o audio. WAVE advierte que no puede verificar si son accesibles. Si alguno de ellos contiene información relevante (como el proceso de pedido o la descripción de un ramo), una persona sorda no podrá acceder a ese contenido sin subtítulos. Esto supone una barrera grave para la comunicación 


## Fase 3: Dimensión de Gobernanza y Ética (G)

Revisa cómo trata la empresa a sus usuarios y sus datos:

1. **Transparencia**. ¿Es fácil rechazar las cookies no esenciales o utilizan "patrones oscuros" (Dark Patterns) para forzar al usuario a aceptarlas?  
2. **Datos innecesarios**. ¿Pide la web datos personales excesivos en su formulario de contacto o registro?

## Fase 4: Propuesta de Refactorización (Green Coding)

Como desarrollador/a, no basta con encontrar los fallos; debes proponer soluciones. Redacta una propuesta de mejora técnica detallando:

* **Optimización de activos**.   
  * ¿Qué formatos usarías para sustituir las imágenes actuales (ej. WebP, AVIF)?  
  * ¿Implementarías Lazy Loading?  
* **Reducción de peticiones**.  
  * ¿Qué librerías o scripts externos eliminarías o aplazarías para mejorar la eficiencia del código y reducir el procesamiento en el dispositivo del cliente?  
* **Reflexión sobre la Paradoja de Jevons**.  
  * Si optimizamos la web y la carga mucho más rápido, podríamos atraer a muchos más usuarios diarios. ¿Cómo evitarías que este éxito anule el ahorro energético conseguido?

BIBLIOGRAFIA

[https://www.websitecarbon.com/website/mariadefatimabeltransalado-es/](https://www.websitecarbon.com/website/mariadefatimabeltransalado-es/)

[webP files upload larger than the jpg actually is | WordPress.org](https://wordpress.org/support/topic/webp-files-upload-larger-than-the-jpg-actually-is/) 

[WAVE Report of Alondra Floristería](https://wave.webaim.org/report#/https://alondrafloristeria.com/) 