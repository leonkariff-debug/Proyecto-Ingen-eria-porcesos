# BT-Lab | Fraccionamiento de benceno y tolueno

Planta virtual académica de Ingeniería de Procesos. HTML, CSS y JavaScript; despliegue estático en GitHub Pages.

## Módulos y artículos integrados

| Módulo | Equipo | Página del simulador | Artículo |
|---|---|---|---|
| M1 | HE-006, precalentador de alimentación | M1 · HE-006 | articulos/recuperacion.html |
| M2 | DC-001, columna de destilación | M2 · DC-001 | articulos/destilacion.html |
| M3 | Condensador total y acumulador de reflujo | M3 · Condensador | articulos/condensador.html |
| M4 | Rehervidor | M4 · Rehervidor | articulos/rehervidor.html |
| M5 | REC-009, convergencia térmica | M5 · REC-009 | articulos/recirculacion.html |

Cada artículo integra el documento académico recibido en formato PDF, con portada, figuras, tablas y referencias. El artículo M3 se convirtió de DOCX a PDF para lectura en el navegador; ambos formatos están conservados en `articulos/originales`.

## Publicación en GitHub Pages

Subir el contenido de esta carpeta a la raíz de la rama `main` y elegir Settings → Pages → Deploy from a branch → `main` → `/(root)`. El archivo `index.html` debe quedar en la raíz.

## Datos y alcance del modelo

Caso de referencia: alimentación 100 kmol/h (50 % molar benceno), 25 °C; precalentamiento a 40.32 °C; columna de 24 etapas, etapa de alimentación 11, R=10, destilado 55 kmol/h y fondos 45 kmol/h. Debido al redondeo de purezas publicado, el programa calcula una composición por balance en lugar de imponer resultados inconsistentes.

La interfaz contiene balances algebraicos, un recuperador calibrado al caso base, cargas térmicas didácticas y demostración numérica de convergencia REC-009. No reproduce los cálculos termodinámicos completos de DWSIM. El modelo original DWSIM está en `origen/`.

## Uso

Abrir `index.html` mediante GitHub Pages o un servidor local. Seleccionar un módulo, cambiar entradas numéricas y consultar resultados y gráficas. El botón «Caso base» restaura las condiciones iniciales.
