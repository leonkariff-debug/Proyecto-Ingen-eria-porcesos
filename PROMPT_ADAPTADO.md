# Prompt personalizado para ampliar BT-Lab

Actúa como ingeniero químico especializado en DWSIM y desarrollador frontend. Trabaja **sobre el código incluido en este proyecto**, no generes una simulación industrial distinta.

## Fuente obligatoria

Analiza `origen/benzene_toluene_dist.dwxmz` y `origen/Benzene_Toluene_Fractionation_Unit.pdf`. El proceso original es fraccionamiento de benceno y tolueno con alimentación equimolar de 100 kmol/h a 25 °C, intercambiador HE-006, columna DC-001 de 24 etapas alimentada en etapa 11, razón de reflujo 10, destilado 55 kmol/h y fondos 45 kmol/h. El archivo también tiene un elemento REC-009 para convergencia/reciclaje. No afirmar que hay cinco equipos de proceso separados.

## Entregable

1. Mantener un hub web con flowsheet interactivo enlazado a cinco módulos: (1) alimentación, (2) recuperación térmica, (3) destilación, (4) condensador, (5) rehervidor. Condensador y rehervidor son subsistemas de DC-001.
2. Mantener ejecuciones individuales e integración de las variables compartidas, valores de entrada editables, gráfica actualizable y alertas cuando el balance sea imposible.
3. Completar cinco artículos de divulgación, uno por pareja, con teoría verificable, aplicaciones y bibliografía, sin atribuir autores inventados.
4. Mantener compatibilidad con GitHub Pages, README con instrucciones y repositorio reproducible. Un enlace público solo puede declararse cuando se publique.
5. Validar balance molar de benceno: F*z=D*xD+B*xB. El PDF comunica xD=0.91 y xTol,B=0.999, valores redondeados que no cierran exactamente cuando F=100, z=0.5, D=55, B=45. El caso base web usa xD≈0.9082727 para xB=0.001. Documentar la diferencia.
6. Conservar datos de deberes térmicos indicados: magnitudes del condensador 5259 kW y rehervidor 5514 kW y diferencia 255 kW. Separar siempre cargas DWSIM de reglas de escalamiento didácticas.
7. No presentar las heurísticas actuales de intercambio térmico, condensador o rehervidor como termodinámica validada. Para ampliar a modelo riguroso, especificar equilibrio Raoult, ecuaciones MESH, propiedades y métodos de solución y contrastar numericamente contra DWSIM.

## Criterios de aceptación

- Las cinco pestañas funcionan sin consola de errores, los controles modifican gráficas y resultados, y el caso base puede restablecerse.
- Balances físico-molares cumplen tolerancia de 1e-8 kmol/h dentro del modelo algebraico.
- Se muestra advertencia si xB es menor que 0 o mayor que 1, si B ≤ 0, o si Th ≤ Tin.
- La documentación diferencia equipos que existen en DWSIM, subsistemas docentes y suposiciones.
- Toda cifra nueva se documenta con origen; no inventar datos experimentales ni referencias.
- Presentar todos los archivos completos y pasos reproducibles de publicación.

Comienza revisando el código de `src/app.js`, ejecutando pruebas contra el punto base y proponiendo mejoras justificadas sin sustituir o romper los módulos ya entregados.
