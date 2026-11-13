# Registro de incidencias

| ID | Severidad | Resultado |
|---|---|---|
| CDEX-001 | Alta | Solo estéreo 2→2; sin posibilidad de insertarlo en pista mono. El prompt sí pedía estéreo. |
| OPUS-001 | Media | `build_mac.sh` falló con `GEN[@]` y `EXTRA[@]` vacíos bajo `set -u`. Corregido externamente. |
| OPUS-002 | Distribución | AU compilado sin firma; firma ad hoc aplicada posteriormente. |
| OPUS-003 | Coexistencia | Bundle ID coincidente entre ambos desarrollos independientes; modificado externamente para Opus. |
| OPUS-004 | Media | Editor de tamaño fijo. |
| OPUS-005 | Alta | Notación científica PUNCH/BODY cerca de cero y entrada escrita `0` que no se aplica correctamente. |
| OPUS-006 | Media | Historial gráfico no reiniciado al detener transporte; los medidores sí se detienen. Potencial decisión de diseño. |
| OPUS-007 | Crítica | Clics audibles persistentes en configuración creativa extrema; no apto para producción en esa condición. Causa DSP sin determinar. |

## OPUS-007 — Configuraciones registradas
En ambas: Threshold −35,6 dB, ratio 9,23:1, knee 19 dB, attack 100 ms, release 10 ms, ADAPT 80,5 %, LINK 61,8 %, MIX 100 %, OUTPUT −7,3 dB.

- A: PUNCH +100 %, BODY +97,3 %, FOCUS 298,5 Hz.
- B: PUNCH −28,6 %, BODY +17,8 %, FOCUS 90,7 Hz.

El productor siguió oyendo clics de similar intensidad tras modificar parámetros. No se infiere que PUNCH o BODY sean la causa exclusiva.