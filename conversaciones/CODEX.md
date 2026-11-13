# Codex Sol 6.1 — Informe final visible

**Origen:** informe proporcionado por el usuario el 13/11/2026. **Tipo:** entrega visible redactada por Codex, no transcripción completa ni razonamiento interno. Los resultados de CI y pruebas indicados son **declaraciones del agente** salvo las comprobaciones posteriores documentadas en [validación](../docs/VALIDACION.md).

## Entrega

**VitaPlug DYNAMIC LAB 0.1.0-rc1**, candidato a validación musical: compresor estéreo AUv2 universal macOS con C++17, JUCE 8 y CMake.

Archivos comunicados:
- Paquete: `dist/VitaPlug-Dynamic-Lab-0.1.0-rc1-macOS-universal.zip`
- README: `README.md`
- Cronología: `docs/EXPERIMENTO.md`
- Captura editor: `docs/evidence/editor.png`

Las rutas absolutas personales se omitieron de esta copia pública. Commit local: `91510de02a7033f43ce9d05eba8db40076e64fec`; tag `v0.1.0-rc1`.

## Sonido y arquitectura declarados

**CONTOUR** regula cuánto se comprime al comienzo de cada golpe: negativo para contener y positivo para preservar. Compara una envolvente rápida de pico con otra lenta de cuerpo. Curva de knee suave y ganancia común estéreo para conservar imagen. Latencia declarada: **0 muestras**.

Con una ráfaga sintética, extremos de CONTOUR: **−3,79 y +5,77 dB RMS** frente al neutro entre 2–8 ms, con diferencia estacionaria inferior a **0,001 dB**. El editor presenta historial GR y picos de entrada/salida. Ocho controles automatizables, estado por instancia, MIX paralelo y bypass con fundido de 8 ms.

## Validación que declaró haber ejecutado

- **18/18** pruebas Release de motor y AUv2 a 44,1/48/96 kHz con bloques de 64/512/4096.
- **16/16** tests DSP bajo ASan y UBSan.
- `auval -strict` superado en **arm64** (dos rondas de estrés) y **x86_64 bajo Rosetta**.
- Recuperación de **8/8** parámetros Core Audio en ambas arquitecturas.
- Firma ad hoc verificada tras extraer ZIP y eliminación de copia temporal de `auval`.
- Pendientes: Logic Pro, escucha y Mac Intel físico.

## Instrucciones de smoke proporcionadas

1. Cerrar Logic, descomprimir ZIP, copiar `VitaPlug Dynamic Lab.component` a `~/Library/Audio/Plug-Ins/Components/`; abortar ante petición de reemplazo; ejecutar `auval -v aufx Dl7q Vp9x -strict` y comprobar `AU VALIDATION SUCCEEDED`.
2. Proyecto a **48 kHz**, batería en pista **estéreo**, insertar `Audio FX → Audio Units → VitaPlug → VitaPlug Dynamic Lab → Stereo`; reescanear solo ese plugin si no se valida.
3. **Ratio 4:1, Attack 2 ms, Release 120 ms, Mix 100 %**; Threshold para **4–8 dB GR**; comparar CONTOUR **−100/0/+100 %** igualando Output; después probar bajo sostenido y Mix 50 %.
4. Automatizar escalones CONTOUR y MIX, alternar bypass del editor y ranura, comprobar clics/panorama/latencia, y repetir buffers de **64 y 512** si disponibles.
5. Desactivar automatización; fijar **CONTOUR −37 %, Mix 63 %, Output −2 dB**; guardar/reabrir y verificar recuperación y respuesta sonora.

Referencia de Apple aportada: https://support.apple.com/es-es/122179

## Contraste posterior

Logic lo reconoció y lo pudo cargar en estéreo. Se constató **ausencia de compatibilidad mono**, limitación importante para un compresor de uso general, aunque el prompt especificaba estéreo. Los smokes de CONTOUR y estrés realizados resultaron útiles, sin clics reportados. Valoración del productor: **6,5/10**. No se completaron todas las comprobaciones propuestas, por lo que no se afirma aceptación comercial total.
