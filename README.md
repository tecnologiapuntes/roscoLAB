# ROSCO LAB V1.4 · Tecnología Insti

Web estática para crear y jugar a roscos de cualquier materia. Sin cuentas ni claves de servicios de IA. Conserva la colección local `roscolab.v1.collection` y la edición original 4D Andalucía.

## Publicación
Sube el contenido del ZIP al mismo repositorio y rama de GitHub Pages de la V1.1, sin cambiar la dirección para conservar Mis roscos en el mismo navegador. `index.html` está compilado y no necesita instalación. Para editar el código fuente usa `src/app.js`, `src/style.css`, `src/shell.html` y ejecuta `python build.py` para reconstruir `index.html`. Los archivos del directorio `andalucia/` son los originales.

## Primera prueba
1. Abre la portada y pulsa **Crear desde PDF** o **Crear con IA**.
2. Elige PDF, Word (.docx), Texto (.txt o apuntes pegados) o Tema. Selecciona el archivo y pulsa Leer documento. El máximo es 10 MB; para PDF se admiten hasta 250 páginas. Puedes indicar las páginas después de leerlo, por ejemplo `1-3, 5`.
3. Para probar sin dependencias externas, selecciona Texto, abre el archivo `ejemplo-electricidad.txt` o pega su contenido y pulsa «10 letras». Elige un nivel y un banco.
4. Selecciona Extracción de definiciones · sin IA y pulsa Generar borrador. Se muestran las letras completas y las pendientes. Puedes probar alternativas o conservar las letras completas comunes a todos los bancos.
5. Pulsa Abrir en editor y revisar. Corrige enunciados, respuestas, explicaciones y fuentes. Guarda el rosco y juega.

## Métodos disponibles
- Automático: usa la IA local si ya está disponible; si no, recurre al extractor. Si la IA local falla, intenta el extractor cuando hay material.
- Extracción de conceptos: solo propone definiciones explícitas reconocibles del material. No genera frases con huecos. No es IA generativa; no garantiza que todas las letras queden cubiertas, que todas las frases sean buenas preguntas, ni que la dificultad quede calibrada. Revisa las propuestas. En el extractor no se inventan textos de referencia.
- IA local de Chrome: utiliza `LanguageModel` (Gemini Nano), si el navegador/dispositivo lo permite. Pulsa Comprobar IA local; si indica que necesita descargar el modelo, selecciona expresamente IA local y pulsa Generar. Lee primero el documento para que el navegador pueda iniciar la descarga tras el clic. Se recomienda HTTPS (GitHub Pages) y Chrome de escritorio actualizado. Para material de más de 16.000 caracteres, selecciona menos páginas. El resultado y las fuentes necesitan revisión. Documentación: https://developer.chrome.com/docs/ai/prompt-api
- ChatGPT, Gemini o Claude: genera el prompt, adjunta el documento en la IA externa y devuelve el JSON a Rosco LAB mediante el importador. Sujeto a los límites de tu propia cuenta. No hay claves API en la web.

## Dependencias y límites
El lector PDF usa PDF.js 4.10.38 cargado desde CDN (cdnjs o jsDelivr); necesita Internet y acceso a uno de ellos. El contenido del archivo se procesa localmente; no se envía a esos CDN. Solo PDF con texto seleccionable; no incluye OCR. Word se lee localmente mediante ZIP/XML y DecompressionStream. No se analiza el contenido de imágenes. Los juegos exportados en HTML siguen siendo autónomos. Mis roscos se guarda en el almacenamiento local del navegador; exporta JSON para hacer copias de seguridad.

## Pruebas
Sintaxis JavaScript validada. Chromium: generación desde texto y DOCX, revisión de las respuestas, apertura en editor, guardado en memoria de la sesión y vista Mis roscos; IA local probada con modelo simulado. No se verificó el lector PDF real ni Gemini Nano real debido al bloqueo de Internet/navegación y falta de modelo en el entorno de pruebas. No se ha publicado en GitHub Pages.

## Cambios V1.3
Se elimina la generación de huecos del extractor. Las definiciones deben estar completas y comenzar con una categoría conceptual reconocible; el filtro es deliberadamente conservador y puede omitir definiciones válidas. La IA local y el asistente externo reciben instrucciones estilo Pasapalabra. El generador local rechaza pistas con huecos y algunos fragmentos incompletos; no garantiza la corrección semántica. Los juegos previos no se modifican.

Pruebas adicionales V1.3: sintaxis JS y Chromium con el HTML cargado en memoria; el texto de ejemplo produjo 10 definiciones válidas de 27 letras seleccionadas, dejando 17 pendientes, sin aceptar las frases problemáticas reproducidas de la captura. Un modelo local simulado devolvió una definición y tres pistas inválidas (dos huecos y una frase truncada): solo se aceptó la definición. No se verificó una ejecución real de Gemini Nano ni del lector PDF en esta revisión.

## Cambios V1.4
- Prioridad estricta a respuestas que empiezan por la letra; las alternativas no desplazan estas respuestas.
- IA local: peticiones en lotes pequeños, segundo intento de iniciales y alternativa final. Se conservan las respuestas válidas.
- Extracción: reconoce más definiciones explícitas y algunos saltos de línea de PDF; no inventa conceptos ausentes.
- El resultado indica cuántas letras quedan pendientes. El documento sigue siendo la referencia si está activada la opción de limitar al material.
- La generación puede tardar más con IA local por las peticiones adicionales.

Pruebas V1.4: Chromium con HTML cargado en memoria, ejemplo de electricidad de diez definiciones (10 de 27 letras, todas de inicio), apertura del editor sin errores y modelo local simulado con respuesta de tipo contiene rechazada y recuperación posterior de A. No se ha probado Gemini Nano real ni el PDF del usuario.
