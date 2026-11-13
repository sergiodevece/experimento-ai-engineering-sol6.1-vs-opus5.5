# VITAPLUG — AI Engineering Games 2026
**Codex Sol 6.1 vs Claude Opus 5.5 · Compresor experimental Audio Unit / Logic Pro**  
**Estudio cerrado: 13 de noviembre de 2026**

## Resultado
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

Ninguno de los dos compresores justificó continuar su desarrollo frente al nivel y la identidad musical de LAB2C, según la valoración del productor. **El experimento está cerrado.**

## Documentación
- [Metodología](docs/METODOLOGIA.md) · [Validación](docs/VALIDACION.md) · [Incidencias](docs/INCIDENCIAS.md) · [Conclusiones](docs/CONCLUSIONES.md)
- [Informes de agentes](conversaciones/README.md): textos visibles de Claude y Codex incorporados; no equivalen a exportaciones íntegras de sus sesiones.
- [Manifiesto editorial](MANIFIESTO.md): criterios de preservación y publicación.

Las capturas con otras ventanas, los archivos musicales y los historiales sin revisar permanecen fuera de este repositorio público hasta verificar privacidad y derechos.