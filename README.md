# ROSCO LAB · by Tecnología Insti · V1.0
**Crea. Juega. Aprende.**

Plataforma estática para crear, adaptar, jugar y compartir roscos educativos. Sin cuenta, backend ni API de pago.

## Abrir y publicar
1. Descomprime todo el ZIP en una carpeta nueva.
2. Abre `index.html` con Chrome o Edge. La portada, biblioteca, editor y motor universal están integrados en el HTML. La carpeta `andalucia/` es necesaria para abrir la edición 4D original desde la biblioteca.
3. Para GitHub Pages, crea un repositorio independiente (por ejemplo `rosco-lab`) o una subcarpeta `rosco-lab` del repositorio `tecno`. Copia todos los archivos y carpetas, haz commit y push. En GitHub configura Pages desde la rama principal y raíz si se usa un repositorio nuevo. No sustituyas la portada de Tecnología Insti ni la carpeta del Rosco 4D existente.

## Qué incluye
- Nueva portada multicolor, tema claro/oscuro, colores de materia y color personalizado.
- Biblioteca: Andalucía (216 preguntas originales), Electricidad (20), Matemáticas (10), Lengua (10). Total: 256 preguntas.
- Editor tabular: de 2 a 27 letras, de 1 a 4 niveles y de 1 a 4 bancos por nivel; preguntas, respuestas, alternativas, explicaciones y fuentes. Validación de letra y duplicados; los borradores con errores no se pueden jugar ni exportar como HTML.
- Asistente de IA: genera prompts para ChatGPT o Gemini a partir del tema, texto o PDF; pega o importa el JSON que produce el servicio externo. No realiza llamadas de IA ni carga PDFs directamente en Rosco LAB. No requiere clave API. El servicio de IA que elija el docente puede aplicar límites propios.
- Mis roscos: guardado local, búsqueda, duplicación, edición, JSON importable/exportable y HTML autónomo para PDI. Imprimir solucionario/resultados o guardar como PDF desde el navegador.
- Nuevo motor flexible: individual o duelo, dos bancos distintos para duelo, cronómetros separados, corrección escrita u oral/manual, sorteo de salida, pausa, pasar, pista, revelar, deshacer, PDI, sonidos, pantalla completa y revisión final.
- Edición original V5.2 del Rosco 4D conservada sin cambios en `andalucia/`, incluidos sus recursos y guías. El motor universal no reproduce aún todas las funciones avanzadas de aquella edición (p. ej. reanudar partida y diploma). Para esas funciones abre el original.

## Crear desde un PDF
1. En **Crear con IA** elige PDF, materia, curso, letras, niveles y bancos.
2. Copia el prompt y abre ChatGPT o Gemini. Adjunta el PDF allí y pega el prompt. No compartas datos personales del alumnado.
3. Copia la respuesta JSON de la IA y pégala en **Importa el resultado**, o guarda el JSON como archivo y ábrelo.
4. Revisa cada pregunta, verifica y guarda. La verificación automática solo comprueba estructura, letras y repetición; no garantiza la exactitud de los contenidos ni de las referencias.
5. Pulsa **Jugar** o **Descargar HTML autónomo**.

## Guardado y portabilidad
Mis roscos utiliza localStorage del navegador; no hay sincronización ni cuentas. Exporta JSON para disponer de una copia persistente. El comportamiento de localStorage con archivos locales depende del navegador; si no permite guardar, usa JSON. El HTML autónomo de un rosco válido incluye sus datos, CSS, JavaScript y logo, y puede abrirse sin Internet. La biblioteca pública no se modifica al guardar un rosco personal.

## Archivos editables
`src/app.js`, `src/style.css`, `src/shell.html`, `src/catalog.json`; `build.py` genera el `index.html` autónomo. Para modificar el código, edita los archivos fuente y ejecuta `python build.py` (Python 3, sin dependencias externas). El catálogo inicial se define en `build.py` y se obtiene de `andalucia/js/questions.js` para el rosco andaluz. `src/catalog.json` es una copia generada del catálogo.

## Comprobaciones
Se comprobó el JavaScript con Node y Chromium mediante una carga del HTML en un documento de prueba: portada, duelo, corrección escrita, cambio de turno, deshacer, resultados, prompt, importación JSON, edición, almacenamiento simulado, exportación JSON y HTML, ejecución del HTML exportado y modo oral. Se verificó la portada móvil a 390 px sin desbordamiento horizontal. El entorno restringe la navegación directa file:// y localhost; no se ha comprobado una publicación real en GitHub Pages ni el almacenamiento persistente en archivo local. No hay servidor o IA directa configurados en esta versión.
