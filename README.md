# ROSCO LAB · by Tecnología Insti · V1.1
**Crea. Juega. Aprende.**

Plataforma estática para crear, adaptar, jugar y compartir roscos educativos. Sin cuenta ni backend propio. Generación directa opcional mediante una clave personal de Gemini; el proveedor puede aplicar costes.

## Abrir y publicar
1. Descomprime todo el ZIP en una carpeta nueva.
2. Abre `index.html` con Chrome o Edge. La portada, biblioteca, editor y motor universal están integrados en el HTML. La carpeta `andalucia/` es necesaria para abrir la edición 4D original desde la biblioteca.
3. Para GitHub Pages, crea un repositorio independiente (por ejemplo `rosco-lab`) o una subcarpeta `rosco-lab` del repositorio `tecno`. Copia todos los archivos y carpetas, haz commit y push. En GitHub configura Pages desde la rama principal y raíz si se usa un repositorio nuevo. No sustituyas la portada de Tecnología Insti ni la carpeta del Rosco 4D existente.

## Qué incluye
- Nueva portada multicolor, tema claro/oscuro, colores de materia y color personalizado.
- Biblioteca: Andalucía (216 preguntas originales), Electricidad (20), Matemáticas (10), Lengua (10). Total: 256 preguntas.
- Editor tabular: de 2 a 27 letras, de 1 a 4 niveles y de 1 a 4 bancos por nivel; preguntas, respuestas, alternativas, explicaciones y fuentes. Validación de letra y duplicados; los borradores con errores no se pueden jugar ni exportar como HTML.
- Generación directa: carga PDF de hasta 10 MB, o introduce texto o tema. Conecta una clave personal de Gemini, consulta modelos disponibles, acepta el envío del material a Google y genera preguntas por bancos con progreso y cancelación. Las letras no resueltas quedan vacías para revisión. Las consultas pueden consumir cuota o generar costes en el proyecto del docente.
- Asistente sin clave: conserva los prompts para ChatGPT o Gemini y la importación de JSON.
- Mis roscos: guardado local, búsqueda, duplicación, edición, JSON importable/exportable y HTML autónomo para PDI. Imprimir solucionario/resultados o guardar como PDF desde el navegador.
- Nuevo motor flexible: individual o duelo, dos bancos distintos para duelo, cronómetros separados, corrección escrita u oral/manual, sorteo de salida, pausa, pasar, pista, revelar, deshacer, PDI, sonidos, pantalla completa y revisión final.
- Edición original V5.2 del Rosco 4D conservada sin cambios en `andalucia/`, incluidos sus recursos y guías. El motor universal no reproduce aún todas las funciones avanzadas de aquella edición (p. ej. reanudar partida y diploma). Para esas funciones abre el original.

## Crear desde un PDF directamente en la web
1. Abre Crear con IA → Generación directa. Selecciona PDF y configura materia, curso, niveles, bancos y letras. Sube un PDF de hasta 10 MB.
2. Obtén tu propia clave en https://aistudio.google.com/apikey. Pégala en la web, pulsa Consultar modelos y selecciona un modelo Gemini compatible. Comprueba precios y cuota en https://ai.google.dev/gemini-api/docs/pricing; la disponibilidad del plan gratuito depende del proyecto, modelo y región. No hay una clave compartida.
3. Acepta el envío del material a Google y pulsa Generar rosco con IA. Cada banco implica una solicitud y el PDF se vuelve a enviar en cada una. El procesamiento puede incluir texto, tablas e imágenes, según el modelo y la calidad del documento.
4. Al terminar, se abre el editor. Comprueba todas las respuestas, explicaciones y referencias de página; la IA puede cometer errores. Las letras sin respuesta válida se quedan vacías. Completa los errores o ajusta las letras antes de jugar. Si se interrumpe tras completar algún banco, puedes revisar el borrador parcial.
5. Guarda en Mis roscos y exporta JSON o HTML. No se almacena la clave ni el PDF original; las preguntas y referencias generadas sí se guardan al pulsar Guardar.

### Seguridad y límites
La clave personal se introduce en un campo de contraseña y permanece en el navegador solo mientras se utiliza la pantalla; no se escribe en localStorage, repositorio ni archivos exportados. La petición HTTPS se envía directamente al servicio de Google, sin backend de Rosco LAB. Como cualquier clave utilizada en un cliente web, puede verse desde herramientas del navegador o extensiones con acceso, por lo que esta opción es para uso individual de confianza, no para una clave de producción compartida. No uses claves en equipos públicos ni materiales confidenciales o con datos del alumnado. Un despliegue institucional con clave común requiere backend, autenticación y límites de uso. Es necesario disponer de Internet para generar preguntas. La API puede rechazar la petición por permisos, cuota, modelo, restricciones de red o compatibilidad. Consulta https://ai.google.dev/gemini-api/docs/api-key.

### Alternativa sin clave
En Crear con IA selecciona Asistente sin clave, copia el prompt, abre ChatGPT o Gemini, adjunta allí tu PDF y pega el prompt. Importa el JSON resultante en Rosco LAB y revisa las preguntas. No requiere API propia.

## Guardado y portabilidad
Mis roscos utiliza localStorage del navegador; no hay sincronización ni cuentas. Exporta JSON para disponer de una copia persistente. El comportamiento de localStorage con archivos locales depende del navegador; si no permite guardar, usa JSON. El HTML autónomo de un rosco válido incluye sus datos, CSS, JavaScript y logo, y puede abrirse sin Internet. La biblioteca pública no se modifica al guardar un rosco personal.

## Archivos editables
`src/app.js`, `src/style.css`, `src/shell.html`, `src/catalog.json`; `build.py` genera el `index.html` autónomo. Para modificar el código, edita los archivos fuente y ejecuta `python build.py` (Python 3, sin dependencias externas). El catálogo inicial se define en `build.py` y se obtiene de `andalucia/js/questions.js` para el rosco andaluz. `src/catalog.json` es una copia generada del catálogo.

## Comprobaciones
Se comprobó el JavaScript con Node y Chromium mediante una carga del HTML en un documento de prueba: portada, duelo, corrección escrita, cambio de turno, deshacer, resultados, prompt, importación JSON, edición, almacenamiento simulado, exportación JSON y HTML, ejecución del HTML exportado y modo oral. Se verificó la portada móvil a 390 px sin desbordamiento horizontal. El entorno restringe la navegación directa file:// y localhost; no se ha comprobado una publicación real en GitHub Pages ni el almacenamiento persistente en archivo local. V1.1: se verificó adicionalmente la selección de PDF, consulta de modelos, generación, respuesta JSON, apertura del editor, guardado sin clave, recuperación parcial ante HTTP 429 y alternativa de prompts mediante respuestas de API simuladas en Chromium. Se repitieron las pruebas de regresión de V1.0. No se dispone de una clave real para verificar la API de Google, cuotas, disponibilidad del modelo o CORS en producción.
