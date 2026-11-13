# Validación real en Logic

## Codex
Entrega declarada: AU universal instalable, 18/18 pruebas Release y 16/16 sanitizadores, `auval -strict` arm64/Rosetta PASS. Carga y procesamiento en estéreo verificados. **No funciona en pista mono**. Primer smoke (48 kHz, Apple Loop «60s Songwriter Drums 02»): Threshold −12,1 dB; ratio 4:1; attack 2 ms; release 120 ms; CONTOUR 0 %; MIX 100 %; OUTPUT 0 dB. Bypass RMS −19,40 dBFS/pico −2,07; activo RMS −23,43/pico −4,99. CONTOUR produjo respuestas diferentes en −100/0/+100 %. Estrés con ratios 3/8/12:1, manteniendo los demás parámetros: RMS −13,14/−14,04/−14,21 dBFS; picos +6,20/+5,71/+5,61 dBFS en Float, deliberados. Productor: **6,5/10**.

## Opus
Entregó fuentes e historial, declaró 21/21 tests DSP y 9/9 JUCE Linux. El script macOS falló dos veces por arrays vacíos; después de corregirlo externamente, se compiló AU universal (arm64/x86_64), CTest 2/2 suites PASS, firma ad hoc válida y `auval` PASS. Carga confirmada en mono y estéreo. Con mismos parámetros básicos del smoke: activo RMS −23,78 dBFS/pico −5,07. Productor percibió compresión levemente más agresiva y audible que Codex. Al forzar los ajustes creativos aparecen clics audibles persistentes, por lo que no superó el smoke de aceptación. No se determinó causa raíz.

**Los datos de pruebas declaradas por agentes y las verificaciones físicas posteriores se distinguen expresamente.**