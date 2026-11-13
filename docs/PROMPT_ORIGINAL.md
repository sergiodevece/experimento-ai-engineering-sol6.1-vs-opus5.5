# EXPERIMENTO AI ENGINEERING — COMPRESOR EXPERIMENTAL AUTÓNOMO

Actúa como arquitecto senior de DSP, ingeniero C++/JUCE y diseñador de herramientas profesionales de producción musical.

## OBJETIVO

Diseña, implementa, compila, prueba y documenta un compresor de audio estéreo experimental para Logic Pro, en formato Audio Unit.

El objetivo musical es crear un procesador capaz de modificar la percepción del impacto, el movimiento y la dinámica de una interpretación de forma creativa y musical.

No quiero una simple emulación de un compresor comercial. Quiero una propuesta con identidad propia y posibilidades expresivas interesantes.

Tienes libertad para elegir la arquitectura DSP, los algoritmos y los controles.

No presupongas una topología FET, VCA, óptica o vari-mu. Justifica tus elecciones y evita complejidad innecesaria.

## IDENTIDAD Y DISEÑO

Nombre provisional: **VitaPlug — DYNAMIC LAB**.

Diseño visual:
- Estética de laboratorio vintage con interpretación contemporánea.
- Paleta verde oscuro, negro y verde luminoso.
- Interfaz profesional, legible y funcional.
- Visualización útil del comportamiento dinámico.
- Controles agrupados con lógica musical.
- Sin copiar interfaces existentes.

Prioriza la funcionalidad y legibilidad sobre la ornamentación.

## REQUISITOS TÉCNICOS

- C++17 o posterior.
- JUCE 8 y CMake.
- Audio Unit AUv2 para macOS.
- Compatible con Apple Silicon y arquitectura Intel cuando el entorno lo permita.
- Procesamiento estéreo.
- Parámetros automatizables.
- Guardado y recuperación del estado.
- Procesamiento seguro en tiempo real.
- Sin asignaciones dinámicas, bloqueos ni operaciones de E/S en el callback de audio.
- Suavizado de parámetros para evitar discontinuidades.
- Protección frente a NaN, infinitos y niveles descontrolados.
- Gestión correcta de latencia y su comunicación al host.
- Bypass coherente y sin clics.
- Arquitectura modular y DSP separado de la interfaz.

## LIBERTAD CREATIVA

Propón una arquitectura propia que pueda aportar posibilidades musicales que no sean evidentes en un compresor convencional.

Puedes explorar ideas como control diferenciado de transitorios y cuerpo, detección adaptativa, envolventes complejas o tratamiento perceptual de la dinámica.

Son ejemplos, no funcionalidades obligatorias.

No implementes características simplemente para impresionar. Cada función debe justificar su utilidad musical.

Limita el proyecto a un conjunto coherente y suficientemente pequeño para garantizar calidad.

## MÉTODO DE EJECUCIÓN — MODO AVIÓN

Esta es una prueba de autonomía técnica.

Dispones de **una única instrucción inicial y debes entregar una versión candidata completa**, sin necesitar conversaciones intermedias.

Toma las decisiones técnicas que estén dentro del alcance autorizado, documentándolas.

Proceso obligatorio:

1. Diseña la arquitectura y define los criterios de aceptación.
2. Implementa el motor DSP.
3. Desarrolla tests automatizados independientes de JUCE.
4. Construye la interfaz gráfica.
5. Integra el Audio Unit.
6. Compila y ejecuta las pruebas disponibles.
7. Investiga y corrige los errores detectados.
8. Repite las verificaciones necesarias.
9. Documenta las decisiones, las pruebas y las limitaciones.
10. Entrega una versión candidata identificada mediante commit.

No solicites aprobación de decisiones menores. Si aparece una decisión irreversible, destructiva o fuera del alcance autorizado, detente y solicita confirmación.

**No reduzcas las pruebas para conseguir que pasen. Corrige el problema real.**

Si no puedes finalizar una parte, explica exactamente qué ha quedado pendiente. No declares superadas pruebas que no hayas ejecutado.

## VALIDACIÓN OBLIGATORIA

Implementa pruebas para:

- Señal en silencio y ruido.
- Impulsos y transitorios.
- Señales senoidales y material de distinta dinámica.
- Comportamiento del detector y envolventes.
- Relación de compresión y ganancia.
- Diferentes frecuencias de muestreo: 44,1 / 48 / 96 kHz.
- Diferentes tamaños de buffer, incluyendo 64, 512 y 4096 muestras.
- Cambios bruscos de parámetros.
- Estabilidad numérica.
- Funcionamiento estéreo.
- Guardado y recuperación de parámetros cuando sea verificable.
- Ausencia de discontinuidades detectables mediante pruebas automatizadas razonables.

Evita resultados ambiguos: cada test debe tener criterios de aceptación explícitos.

## ENTORNO Y SEGURIDAD

Trabaja en un repositorio nuevo e independiente.

No modifiques ningún proyecto existente de VITALAB ni sus componentes compartidos.

No instales ni sustituyas automáticamente plugins que ya estén funcionando en el equipo.

El identificador AU debe ser único y no entrar en conflicto con otros productos.

Puedes usar las herramientas de compilación y pruebas disponibles en el entorno, pero no supongas que tienes acceso a Logic Pro si no puedes verificarlo.

## DOCUMENTACIÓN

Crea un README profesional con:

- Concepto musical.
- Arquitectura DSP.
- Explicación de cada control.
- Diagramas de señal.
- Instrucciones de compilación.
- Resultados de las pruebas.
- Limitaciones conocidas.
- Decisiones autónomas adoptadas.
- Problemas detectados y soluciones.
- Instrucciones de instalación y validación en Logic.

Incluye un archivo específico con la cronología del experimento y las evidencias verificables.

## ENTREGA FINAL

Quiero recibir en una única respuesta final:

1. Resumen del producto construido.
2. Explicación de su identidad sonora.
3. Arquitectura DSP elegida y justificación.
4. Funcionalidades implementadas.
5. Resultados reales de tests.
6. Estado de compilación y validación AU.
7. Ruta del artefacto instalable, si existe.
8. Commit final y enlace al repositorio, si se ha publicado.
9. Problemas pendientes y limitaciones.
10. Instrucciones exactas para el smoke test físico en Logic Pro.

No des por validada la calidad sonora hasta que el usuario realice una escucha.

La versión final debe ser una **candidata a validación musical**, no un producto comercial declarado terminado.

Prioriza estabilidad, coherencia, trazabilidad y calidad técnica sobre velocidad y cantidad de funcionalidades.

**Comienza y desarrolla el proyecto de forma autónoma hasta alcanzar los criterios de entrega o identificar un bloqueo real.**
