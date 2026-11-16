# BT-Lab — Planta virtual benceno/tolueno

Aplicación web académica que reúne cinco módulos didácticos vinculados a un proceso de fraccionamiento benceno–tolueno. Los archivos de origen, suministrados por el equipo, contienen un intercambiador HE-006, una columna DC-001 (con condensador y rehervidor) y un objeto REC-009 de convergencia/reciclaje. **No son cinco equipos de proceso independientes en el archivo DWSIM.**

## Ejecutar

- Método simple: abrir `index.html` desde un navegador actualizado. Si el navegador bloquea módulos JS desde `file://`, emplear un servidor local.
- Python: desde la carpeta del proyecto, ejecutar `python -m http.server 8000` y abrir `http://localhost:8000`.
- Para publicar en GitHub Pages: crear repositorio público; subir *el contenido de esta carpeta* a la rama `main`; en Settings → Pages seleccionar *Deploy from a branch*, rama `main`, carpeta `/ (root)`; guardar y consultar la URL que GitHub proporcione. **No se puede prometer una URL antes de subir el repositorio.**

No requiere dependencias, instalación de paquetes, ni servidor de cálculo. Cálculos en JavaScript puro y gráficos en Canvas 2D.

## Los cinco módulos

1. **Alimentación:** F, z y temperatura de entrada; balance por componentes.
2. **Recuperador HE-006:** modelo de efectividad y capacidades caloríficas efectivas ajustadas al punto base.
3. **Columna DC-001:** balance global y de benceno; indica 24 etapas, etapa de entrada 11, R=10 como referencia (no simula VLE).
4. **Condensador de DC-001:** escala didáctica del deber térmico.
5. **Rehervidor de DC-001:** escala didáctica de deber térmico, diferencia frente a condensador.

La revista presenta cinco artículos introductorios sobre los módulos del simulador.

## Caso base y consistencia

| Variable | Documento original | En web |
|---|---:|---:|
| F | 100 kmol/h | 100 |
| Benceno en alimentación | 0.5 | 0.5 |
| Temperatura alimentación | 25 °C | 25 |
| Temperatura después recuperador | 40.32 °C | calibrada a 40.32 |
| Fondos antes / después recuperador | 110.4 / 83 °C | calibrada a 110.4 / ~83 |
| D/B | 55 / 45 kmol/h | 55 / 45 |
| Benceno en destilado | 0.91 (redondeado) | **0.9082727** (consistente con xB=0.001) |
| Benceno en fondos | 0.001 (a partir de 0.999 tolueno) | 0.001 |
| Relación de reflujo | 10 | 10 |
| Etapas / alimentación | 24 / 11 | solo se muestran como información |
| Magnitud Qc / Qr | 5259 / 5514 kW | 5259 / 5514 en caso base |

El valor 0.91 de benceno destilado resulta en xB = (50 − 55×0.91)/45 = −0.001111..., imposible. Para mantener xB=0.001 se adopta xD=(50−45×0.001)/55≈0.90827, próximo al valor de 0.91 del PDF. Es una **corrección de redondeo para fines de balance**, no una modificación del archivo DWSIM.

## Cálculos y supuestos

- `F_Bz=F*z`, `F_Tol=F*(1-z)`.
- `B=F-D`, `xB=(F*z-D*xD)/B`, con 0 ≤ xB ≤ 1 como condición de factibilidad.
- En el recuperador: `Q = ε*Cmin*(Th-Tin)`, `Tc,out=Tin+Q/Ccold`, `Th,out=Th−Q/Chot`. `C=F*Cp/3600` (kW/K), con `Cp,cold=150 kJ/(kmol·K)` como **valor efectivo ilustrativo**, y `Cp,hot` ajustado matemáticamente para concordar con las temperaturas del punto base. `ε≈0.3208` se aproxima; **no son propiedades reales medidas** y, por tanto, fuera del punto base no hay validez de diseño.
- Condensador: `|Qc|=5259*(D/55)*((R+1)/11)` kW (**escalamiento heurístico**).
- Rehervidor: `|Qr|=|Qc|+255*(F/100)` kW (**escalamiento heurístico**).
- El PDF informa `Qc=5259 kW` y `Qr=-5514 kW` con una convención de signo particular. La app muestra **magnitudes positivas** para evitar mezclar convenciones.
- La app **no implementa** equilibrio líquido-vapor con Raoult, modelo MESH, ciclos termodinámicos, hidráulica real, ni cálculo de convergencia de REC-009; para eso debe abrirse el DWXMZ en DWSIM.

## Pruebas manuales sugeridas

1. Abrir la aplicación y comprobar F=100, D=55, B=45 y balance total 0.
2. Ir a Destilación y comprobar `xB≈0.001`, y balance de benceno ≈0.
3. Ir a Recuperación de calor y comprobar salida de alimentación ≈40.32 °C y salida fondos ≈83 °C.
4. Revisar condensador ≈5259 kW y rehervidor ≈5514 kW en el caso base.
5. Ajustar z=0.2 y xD=0.91 con D=55: debe aparecer una advertencia de imposibilidad física.
6. Restablecer y confirmar recuperación del caso base; navegar por los cinco módulos y los cinco artículos.

## Organización

- `index.html`: hub, flowsheet y navegación.
- `src/app.js`: variables, modelos, validaciones y gráficos.
- `src/style.css`: interfaz adaptable.
- `articulos/`: cinco artículos de divulgación.
- `docs/`: información adicional sobre revisión.
- `origen/`: copia de los archivos originales DWSIM y PDF, para que puedan contrastarse por el profesor.

## Equipo

El proyecto integra cinco módulos de simulación y cinco artículos de divulgación.

## Referencia

*Benzene Toluene Fractionation Unit*, PDF suministrado junto con `benzene_toluene_dist.dwxmz`. El PDF cita McCabe, Smith y Harriott, *Unit Operations of Chemical Engineering*, capítulo 18. No se han verificado externamente ediciones ni páginas de bibliografía.

## Publicación automática con GitHub Pages

Este proyecto incluye `.github/workflows/pages.yml` para publicarse automáticamente desde la rama `main` usando GitHub Actions.

1. Crea un repositorio **público** de GitHub, por ejemplo `bt-lab-planta-virtual`.
2. Sube el **contenido de esta carpeta** a la raíz del repositorio (el archivo `index.html` debe aparecer en la raíz).
3. En **Settings → Pages → Build and deployment**, selecciona **GitHub Actions**.
4. En la pestaña **Actions**, verifica la ejecución `Publicar BT-Lab en GitHub Pages`; si no se ejecutó, abre ese flujo y usa **Run workflow**.
5. La URL aparecerá en **Settings → Pages** cuando termine correctamente. En un repositorio estándar será `https://USUARIO.github.io/bt-lab-planta-virtual/`, sustituyendo `USUARIO` por tu nombre de usuario real.

No se requiere Node ni npm: la plataforma está construida con archivos estáticos HTML, CSS y JavaScript. El workflow publicado no altera los datos de DWSIM.
