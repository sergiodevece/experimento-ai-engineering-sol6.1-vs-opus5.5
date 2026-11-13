# VITAPLUG — AI Engineering Games 2026
**Codex Sol 6.1 vs Claude Opus 5.5 · Compresor experimental Audio Unit / Logic Pro**  
**Fase 1 cerrada y Fase 2 añadida: 13 de noviembre de 2026**

**[Prompt original íntegro y literal (instrucción común de las tres condiciones)](docs/PROMPT_ORIGINAL.md)**

## Actualización — Fase 2: Claude Code + Opus 5.5

El experimento se amplió usando **el mismo prompt y el mismo modelo Opus 5.5, pero en un entorno diferente: Claude Code (proyecto, modo automático, esfuerzo Extra)**. **No es una revancha dentro del mismo Claude Chat + Artifacts.**

**Resultado observado:** en unos 40 minutos según el usuario, Claude Code desarrolló un compresor distinto (**DYNAMIC LAB AE**, motores CORE + SHAPE, JUCE 8.0.15), compiló y validó un AU universal y lo instaló **tras solicitar autorización**. Declaró 47/47 tests PASS y `auval` PASS en arm64/Rosetta. No requirió nuestra asistencia técnica de compilación. El productor probó el AU en Logic con ajustes exigentes y automatización, **sin detectar clics**, y le otorgó **8/10**. Declaró expresamente que **lo incorporaría a su cadena de trabajo**.

La nueva propuesta supera en valoración musical observada a Codex (**6,5/10**), pero **no convierte retroactivamente en incorrecto el resultado de la Fase 1**: Codex ganó aquella comparación concreta contra Claude Chat + Artifacts. La Fase 2 añade una tercera condición, no una tercera arquitectura idéntica ni una comparación estadísticamente replicada.

| Condición | Valoración de productor | Resultado observable |
|---|---|---|
| **Claude Code + Opus 5.5** (Fase 2) | **8/10** | Mejor candidato musical; AU instalado y smokes creativos sin clics reportados |
| Codex + Sol 6.1 (Fase 1) | **6,5/10** | Ganador de Fase 1, entrega sólida, solo estéreo |
| Claude Chat + Artifacts + Opus 5.5 (Fase 1) | No apto | Clics persistentes y problemas de interfaz en esa entrega |

**Importante:** la prueba de automatización y la exportación extrema fueron satisfactorias según la escucha, pero un archivo Float32 alcanzó un pico de **+12,90 dBFS**. Esto es deliberado y representable en Float32, **no seguro para todas las cadenas de reproducción sin atenuación previa**. No se ha realizado auditoría exhaustiva de discontinuidades sincronizada con automatización ni certificación comercial.

- **[Informe técnico completo de la Fase 2](docs/FASE_2_CLAUDE_CODE.md)**
- **[Mediciones de tres smokes (CSV)](docs/FASE_2_MEDICIONES.csv)**
- **[Informe visible de Claude Code](conversaciones/CLAUDE_CODE_OPUS.md)**

---

## Resultado de la Fase 1 — Codex vs Claude Chat + Artifacts
**Ganador de esta ejecución: Codex Sol 6.1.** Entregó un AU universal instalable y un compresor estéreo competente que superó las pruebas musicales realizadas. Valoración del productor: **6,5/10**. El sonido se juzgó funcional y versátil, pero relativamente convencional frente al proyecto interno LAB2C.

**Claude Opus 5.5** desarrolló un compresor con PUNCH, BODY y ADAPT, compatible con pistas mono y estéreo, pero requirió intervenciones externas para compilarlo e instalarlo en macOS. Presentó defectos de edición numérica y **clics audibles persistentes** al emplear configuraciones creativas exigentes: **candidato rechazado para uso de producción en esas condiciones**.

El resultado se refiere a **estas dos ejecuciones**, no establece un ranking universal entre modelos.

## Diseño del ensayo
Se envió un **mismo prompt inicial** a dos proyectos independientes llamados «COMPRESOR EXPERIMENTAL», ambos en aplicación de escritorio, modo automático y máximo esfuerzo. Claude inició 15 segundos antes de Codex. Se compararon entrega, validaciones, instalación y smoke real en Logic Pro, con capturas y WAV. Las correcciones posteriores se contabilizan por separado del trabajo autónomo. No se hicieron nuevas iteraciones de DSP para arreglar los defectos encontrados.

| Criterio | Codex Sol 6.1 | Claude Opus 5.5 |
|---|---|---|
| Concepto | CONTOUR | PUNCH, BODY y ADAPT |
| Entrega | ZIP AU universal macOS instalable | Fuentes `.tar.gz` y repo `.bundle` |
| `auval` | PASS | PASS tras construcción externa en Mac |
| Canales | Solo estéreo | Mono y estéreo cargan |
| Interfaz | Redimensionable | Fija; defectos de entrada y visualización numérica |
| Compresión básica | Funcional | Funcional |
| Estrés creativo | Sin clics reportados en ensayos realizados | Clics audibles persistentes |
| Dictamen | 6,5/10 · Ganador | No apto en esta candidata |

## Primer smoke: misma batería y parámetros básicos
Apple Loop «60s Songwriter Drums 02», 48 kHz estéreo. Threshold −12,1 dB, ratio 4:1, attack 2 ms, release 120 ms, mix 100 % y output 0 dB; controles creativos neutralizados cuando correspondía.

| Señal | RMS | Pico de muestra |
|---|---:|---:|
| Bypass | −19,40 dBFS | −2,07 dBFS |
| Codex activo | −23,43 dBFS | −4,99 dBFS |
| Opus activo | −23,78 dBFS | −5,07 dBFS |

El productor percibió Opus **ligeramente más agresivo** y una compresión algo más audible en esta prueba básica; diferencia muy sutil, sin preferencia musical concluyente. La igualdad aproximada de RMS no demuestra identidad de sonido.

## Registro de incidencias
- **CDEX-001 · Alta:** AU solo estéreo; no aparece en pistas mono. El prompt exigía estéreo, no mono, por lo que es carencia de diseño de producto, no incumplimiento literal.
- **OPUS-001:** `build_mac.sh` falló al expandir arrays vacíos (`GEN[@]` y `EXTRA[@]`) con `set -u`; corrección externa.
- **OPUS-002:** AU construido inicialmente sin firma; se firmó ad hoc externamente. No se demostró que firmarlo fuera requisito absoluto para instalar.
- **OPUS-003:** colisión de Bundle ID entre entregas independientes con igual nombre; incidente de coexistencia, no responsabilidad exclusiva de Opus.
- **OPUS-004:** ventana de tamaño fijo.
- **OPUS-005 · Alta:** etiquetas PUNCH/BODY en notación científica cerca de cero y fallo de entrada manual del valor `0`.
- **OPUS-006 · Media:** historial visual retenido al detener Logic mientras los medidores sí se detienen; puede ser decisión de diseño.
- **OPUS-007 · Crítica:** clics audibles persistentes en procesamiento creativo exigente, aun variando PUNCH/BODY/FOCUS. **Sin causa raíz atribuida a módulo específico.**

## Metodología y límites
Los tests automatizados y `auval` **no sustituyen el smoke musical físico**. Las pruebas comunicadas por los agentes no equivalen por sí solas a auditoría independiente. Una sola ejecución por modelo no permite generalización estadística; no hubo ABX ciego formal ni verificación exhaustiva de automatización y hardware. Los entornos de herramientas macOS no fueron equivalentes o no se conocen plenamente sus permisos efectivos.

Fable 5.2 / Impossible Spaces fue un experimento paralelo de referencia, **no un tercer competidor bajo el mismo prompt**.

Ninguno de los dos compresores justificó continuar su desarrollo frente al nivel y la identidad musical de LAB2C, según la valoración del productor. **La Fase 1 está cerrada; la Fase 2 está documentada y la versión DYNAMIC LAB AE se conserva como candidata musical, con validaciones profesionales adicionales pendientes.**

## Documentación
- [Metodología](docs/METODOLOGIA.md) · [Validación](docs/VALIDACION.md) · [Incidencias](docs/INCIDENCIAS.md) · [Conclusiones](docs/CONCLUSIONES.md)
- [Informes de agentes](conversaciones/README.md): textos visibles de Claude y Codex incorporados; no equivalen a exportaciones íntegras de sus sesiones.
- [Manifiesto editorial](MANIFIESTO.md): criterios de preservación y publicación.

Las capturas con otras ventanas, los archivos musicales y los historiales sin revisar permanecen fuera de este repositorio público hasta verificar privacidad y derechos.