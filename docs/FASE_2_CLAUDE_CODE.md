# Fase 2 — Claude Code + Opus 5.5

**Fecha:** 13 de noviembre de 2026  
**Estado:** segunda fase documentada; candidato musical prometedor, no producto comercial certificado.  
**Objeto:** explorar el efecto del entorno de ejecución sobre la entrega y el resultado de un mismo encargo. No es una segunda ejecución idéntica dentro de Claude Chat: el entorno cambió de **Claude Chat + Artifacts** a **Claude Code — proyecto**.

## Diseño y condiciones

- **Modelo:** Claude Opus 5.5, esfuerzo Extra, ejecución automática.
- **Encargo:** mismo prompt inicial de compresor experimental AU para Logic Pro utilizado en la primera comparación.
- **Entorno:** proyecto nuevo en Claude Code; se utilizó JUCE 8.0.15, frente a JUCE 8.0.4 del primer Opus.
- **Duración aproximada comunicada:** 40 minutos.
- **Proceso autónomo comunicado:** implementación, tests, compilación AU universal, firma ad hoc, `auval -strict` en arm64 y bajo Rosetta, instalación temporal seguida de retirada para validación.
- **Interacción humana de instalación:** Claude solicitó autorización expresa para instalar el componente definitivamente en el Mac. La autorización del usuario **no constituye asistencia técnica** ni una pérdida de autonomía.
- **Resultado:** `VitaPlug DYNAMIC LAB AE.component`, identidad AU `aufx DlAe VpAe`, sin sobrescribir los dos compresores anteriores, según informe y captura del agente.
- **Control de cambios declarado:** commit `b07a657`, tag `v0.1.0-rc1`; SHA-256 `9600c86c…99e6a3` (abreviado comunicado por el agente).

Estas evidencias de compilación y validación se basan en el informe y las capturas compartidas; no se ha auditado aquí el repositorio de código de Claude Code.

## Arquitectura declarada

Dos motores de ganancia combinados en dB:

- **CORE:** compresor feed-forward logarítmico de rodilla suave, con detector RMS de 5 ms calibrado.
- **SHAPE:** modelador de transitorios independiente del nivel, basado en comparación de envolventes rápidas/lentas; controles **IMPACT** y **BODY**, límite ±12 dB, puerta para evitar elevar ruido.
- **ADAPT:** recuperación dinámica dependiente del material.
- **Look-ahead fijo:** 2 ms (96 muestras a 48 kHz); alineación de señal seca para MIX y bypass.

Se descartaron deliberadamente saturación, multibanda, sidechain externo, oversampling y look-ahead variable. La GUI no es redimensionable. No hay presets.

### Pruebas declaradas por Claude Code

- DSP independiente: **35/35**.
- Integración JUCE: **12/12**.
- Total: **47/47**.
- El agente declaró detección y corrección durante el desarrollo de clics al automatizar Attack, exceso de suma IMPACT+BODY, dos fallos visuales y un error del test.

**Estas cifras no reemplazan los smoke tests manuales posteriores.**

## Pruebas musicales reales en Logic Pro

El productor utilizó nuevamente el Apple Loop «60s Songwriter Drums 02», 48 kHz, en Logic Pro.

**SMOKE AE-01 — control musical general:** carga operativa y escucha positiva. El productor valoró carácter, compresión y versatilidad positivamente, sin clics detectados en esta prueba.

**SMOKE AE-02 — configuración agresiva:** captura con Threshold −30,1 dB, ratio 11,1:1, knee 12,7, SC HPF 320 Hz, Link 100, Attack 55,2, Release 12, ADAPT 71, IMPACT +76, BODY +47, Mix 100 y Output −6,4. El productor informó de comportamiento musical satisfactorio sin clics.

**SMOKE AE-03 — extremos y automatización:** capturas con Threshold −36,4 dB, ratio 20:1, knee 7,3, SC HPF 319 Hz, Link 41, Attack 100, Release 10, ADAPT 71, IMPACT +100, BODY +79, Mix 100 y Output +7,9. Se automatizó bypass en Logic y se forzó deliberadamente la salida. El productor informó de ausencia de clics y comportamiento musical correcto incluso en ese contexto.

### Mediciones verificadas de WAV

Se midieron los tres WAV aportados, mediante lectura digital de archivos estéreo a 48 kHz. Son **exportaciones completas**, no pruebas de discontinuidad específicamente sincronizadas con eventos de automatización.

| Ensayo | Duración | RMS | Pico de muestra | Fotogramas con algún canal > 0 dBFS | NaN/Inf |
|---|---:|---:|---:|---:|---:|
| AE normal | 28,364 s | −22,74 dBFS | −5,04 dBFS | 0 | 0 |
| AE agresivo | 28,364 s | −21,55 dBFS | −3,39 dBFS | 0 | 0 |
| AE extremos + auto | 28,364 s | −6,01 dBFS | **+12,90 dBFS** | **75.355** | 0 |

En la exportación Float32, superar 0 dBFS no equivale necesariamente a recorte de muestras; **sí implica que la señal debe atenuarse antes de una cadena que no tolere esos niveles**. El salto máximo entre muestras de la prueba extrema fue ~2,36 unidades de escala completa. Sin comparación temporal con la señal original y los eventos de automatización no se puede interpretar ese dato aislado como un clic confirmado ni como ausencia garantizada de discontinuidades.

### Valoración del productor

**8/10**, tras los primeros smokes y la prueba creativa. El productor declaró que **lo incorporaría a su cadena de trabajo** y que es una propuesta interesante para continuar desarrollando.

Se trata de una **decisión de utilidad musical observada**, no de la afirmación de que la versión está lista para distribución comercial.

## Comparación y alcance causal

| Criterio | Opus 5.5 en Claude Chat + Artifacts (Fase 1) | Opus 5.5 en Claude Code (Fase 2) |
|---|---|---|
| Entrega inicial | Código y paquete Git, AU macOS no construido | AU universal construido y validado |
| Integración | Requirió intervención técnica externa | Instaló tras pedir autorización |
| DSP | PUNCH/BODY + detector original; sin look-ahead | CORE/SHAPE + detector RMS + 2 ms look-ahead |
| Interfaz | Tamaño fijo y bug de edición numérica | Tamaño fijo; sin defecto equivalente reportado |
| Prueba creativa | Clics persistentes; rechazo | Sin clics detectados por el productor en los smokes |
| Valor musical | No apto en condición exigente | **8/10**, candidato prometedor |

**Interpretación correcta:** en estas ejecuciones se observó una gran diferencia de resultados, al cambiar el entorno de trabajo. **No está aislada causalmente la contribución del entorno**: también pueden variar soluciones estocásticas, herramientas disponibles, contexto de proyecto y versión de JUCE. No sustituye una comparación controlada replicada.

## Pendiente si se convierte en producto

Antes de lanzamiento o distribución: restauración de estado, todos los parámetros bajo automatización rápida, pruebas a distintas frecuencias/buffers, prueba mono real y Mac Intel físico, manejo seguro de picos y estrés, rendimiento prolongado y regresión completa. El cierre documental del experimento no exige realizar ahora estas pruebas.

**Conclusión de Fase 2:** candidato de mayor interés musical observado. Se conserva el resultado histórico de la Fase 1, donde Codex venció a Claude Chat + Artifacts.
