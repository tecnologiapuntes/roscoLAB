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

## Cambios V1.5 — IA externa recomendada
- Crear con IA abre por defecto el asistente externo. ChatPDF y Smallpdf anuncian uso inicial sin cuenta para PDF, sujeto a límites; ChatGPT, Gemini y Claude son alternativas. Estos enlaces no realizan cargas ni llamadas automáticas. Adjunta el documento en el servicio elegido y copia el prompt de Rosco LAB.
- Formato recomendado: tabla de texto delimitada por `|`, con columnas Nivel, Banco, Letra, Tipo, Pregunta, Respuesta, Explicación y Fuente. También se aceptan tablas Markdown, CSV/TSV de una fila por pregunta, JSON parcial o completo en el esquema Rosco LAB y tablas sencillas Letra/Pregunta/Respuesta para un único banco. No se interpreta cualquier texto libre ni CSV multilínea. Selecciona antes los niveles y bancos correctos. Para recuperar un JSON completo con sus metadatos usa la importación habitual de Mis roscos.
- La vista previa indica preguntas aceptadas, rechazadas y pendientes; calcula el tipo a partir de la respuesta, favorece iniciales, rechaza huecos y duplicados dentro de cada banco. No valida semánticamente los hechos ni la correspondencia con el PDF.
- En el editor, Completar / mejorar con IA construye un prompt para las letras pendientes. Opcionalmente busca alternativas de inicio para las respuestas de tipo Contiene. La aplicación de nuevas filas conserva las preguntas válidas no seleccionadas. Las preguntas deben revisarse y guardarse.
- El extractor y Gemini Nano permanecen en la pestaña experimental. WebLLM se ha estudiado como alternativa (https://webllm.mlc.ai/); requiere WebGPU y descarga de modelos y no se integra en esta versión. Sin API, sin servidor nuevo y sin registro obligatorio en Rosco LAB.
- Prueba rápida: en Crear con IA, elige 10 letras, un nivel y un banco. Abre `ejemplo-importacion-electricidad.txt` en el paso 3; comprueba las preguntas y abre el editor.
- Pruebas: JavaScript validado y Chromium con HTML cargado en memoria. Tabla Markdown, rechazo de huecos, corrección del tipo, reparación CSV no destructiva, JSON parcial con dos niveles y dos bancos, guardado en sesión. El entorno bloqueó navegación a archivos locales; no se ha probado la publicación, la persistencia real, las respuestas reales de servicios externos ni los modelos locales. Los servicios externos pueden cambiar sus condiciones. No compartas datos personales del alumnado.

## V1.6 — Instrucciones más sencillas
- Opción 1: IA externa recomendada, copia de instrucciones, elección de plataforma, envío del documento y pegado de preguntas guiados en tres pasos. Formato avanzado y vista del prompt plegables.
- Opción 2: generación en esta web, experimental, con indicaciones propias.
- Se conserva el generador y el importador de V1.5, así como los datos locales y el juego de Andalucía.


## V1.7 — Guardado y juego de roscos incompletos
- Se mantiene la clave de almacenamiento local existente. Los roscos personales aparecen también en Biblioteca, solo en el mismo navegador y origen.
- Se puede jugar con al menos dos preguntas válidas del banco seleccionado. Las demás letras se omiten temporalmente sin borrar datos. En duelo se usan las letras válidas comunes a los dos bancos.
- La configuración informa de las letras omitidas antes de empezar. El HTML autónomo aplica el mismo comportamiento.
- Guardar confirma el éxito únicamente si el almacenamiento local acepta la escritura.


## V1.8 — Interfaz de juego más visual para PDI

- Nueva pantalla de juego con botones grandes para **Correcto**, **Incorrecto** y **Pasapalabra**.
- Campo de respuesta escrita opcional, manteniendo la corrección automática cuando se pulsa **Comprobar**.
- Barra superior más clara para PDI: modo presentador, pantalla completa, reiniciar, pausar y finalizar.
- Pistas ocultas de momento, tal como se pidió.
- Se mantiene **Ver solución** y **Deshacer** como acciones auxiliares.


## V1.9 — Guardado más claro y ajuste automático de pantalla

- Las tarjetas de los roscos muestran ahora **preguntas completas / preguntas totales**, para no confundir los huecos con contenido realmente rellenado.
- En el editor se muestra un resumen por **nivel** y por **banco** con las preguntas completas de cada uno.
- Al guardar, Rosco LAB indica cuántas preguntas completas tiene el rosco y avisa si hay niveles sin contenido completo.
- La pantalla de juego se ajusta mejor de forma automática a distintos tamaños de monitor, pantalla o PDI.
