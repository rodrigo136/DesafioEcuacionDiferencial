# Empleo juvenil en Bolivia: simulador de ecuaciones diferenciales

**Materia:** Métodos Numéricos  
**Desafío:** Modelar la evolución del empleo juvenil mediante una EDO de primer orden  
**Estudiante:** Marca Ariel Rodrigo  
**Ci:** 6796707
**Carrera / mención:** Ingeniería de Sistemas  
**Materia:** Metodos Numericos
**Sigla:** COM - 254
**Contexto:** Bolivia — escenario académico hipotético en la ciudad de La Paz  

---

## 1. Descripción

El proyecto estudia cómo podría evolucionar el número de jóvenes que consiguen empleo después de participar en talleres comunitarios de capacitación laboral. Se plantea un escenario hipotético en La Paz, Bolivia, para 100 jóvenes de 18 a 28 años.

Los talleres considerados incluyen elaboración de currículum, preparación para entrevistas, habilidades digitales y técnicas, y orientación para la búsqueda de empleo.

La aplicación permite modificar parámetros, ejecutar Heun y Runge–Kutta de cuarto orden (RK4), comparar ambos con la solución analítica, visualizar errores y descargar la tabla principal en CSV.

> **Advertencia:** los parámetros numéricos son supuestos didácticos. No son estadísticas oficiales ni una predicción comprobada del mercado laboral boliviano.

## 2. Problema, beneficiarios y pregunta

En Bolivia, parte de la población joven encuentra dificultades para acceder a su primer empleo por factores como la falta de experiencia, la necesidad de fortalecer habilidades solicitadas por empleadores y las condiciones del mercado laboral.

La propuesta consiste en estudiar un programa comunitario de capacitación que busque mejorar las oportunidades de inserción laboral juvenil.

**Beneficiarios:** 100 jóvenes de 18 a 28 años en un escenario hipotético de La Paz, Bolivia.

**Pregunta:** ¿Cómo evoluciona el número de jóvenes empleados después de implementar talleres de capacitación laboral en una comunidad de Bolivia y cuánto tiempo se necesita para alcanzar una meta de empleo?

**Objetivo general:** representar mediante una EDO de primer orden la evolución del número de jóvenes empleados, resolverla analíticamente y aproximarla mediante Heun y RK4.

**Meta cuantificable:** alcanzar el 90 % de una capacidad máxima supuesta de 80 jóvenes:

\[
E_{\text{meta}}=0.90(80)=72\text{ jóvenes}.
\]

El grupo participante es de 100 jóvenes. El valor 80 es la capacidad máxima considerada en el modelo, no el tamaño total del grupo.

## 3. Modelo matemático

### 3.1 Variables y parámetros

| Símbolo | Significado | Unidad | Valor inicial |
|---|---|---|---:|
| \(t\) | Tiempo | meses | 0 a 12 |
| \(E(t)\) | Jóvenes empleados al tiempo \(t\) | jóvenes | variable |
| \(E_0\) | Jóvenes empleados inicialmente | jóvenes | 20 |
| \(E_{\max}\) | Capacidad máxima supuesta | jóvenes | 80 |
| \(k\) | Tasa de incorporación laboral | mes\(^{-1}\) | 0,18 |
| \(h\) | Tamaño del paso | meses | 1 y 0,5 |

### 3.2 Ecuación diferencial y condición inicial

Se supone que la velocidad de incorporación laboral es proporcional a la diferencia entre la capacidad máxima y el número de jóvenes empleados:

\[
\boxed{\frac{dE}{dt}=k(E_{\max}-E)}
\]

Con los parámetros de referencia:

\[
\boxed{\frac{dE}{dt}=0.18(80-E)}
\]

Condición inicial:

\[
\boxed{E(0)=20}
\]

Intervalo:

\[
0\leq t\leq12\text{ meses}.
\]

Al inicio existe una diferencia grande entre los jóvenes empleados y la capacidad máxima supuesta. Conforme \(E(t)\) se acerca a \(E_{\max}\), esa diferencia disminuye y el crecimiento se desacelera.

### 3.3 Supuestos

1. El programa comienza con 100 jóvenes participantes.
2. Al inicio, 20 jóvenes tienen empleo.
3. La capacidad máxima de inserción considerada es 80 jóvenes.
4. La tasa \(k\) permanece constante durante la simulación.
5. Quienes consiguen empleo permanecen contabilizados como empleados durante el período.
6. No se consideran pérdidas de empleo, abandono del programa ni cambios económicos.
7. Los parámetros son hipotéticos y se usan para el ejercicio matemático.

## 4. Solución analítica

Partimos de:

\[
\frac{dE}{dt}=k(E_{\max}-E).
\]

Separamos variables:

\[
\frac{dE}{E_{\max}-E}=k\,dt.
\]

Integramos:

\[
-\ln|E_{\max}-E|=kt+C.
\]

Despejamos:

\[
E_{\max}-E=Ce^{-kt}.
\]

Por tanto:

\[
E(t)=E_{\max}-Ce^{-kt}.
\]

Aplicando \(E(0)=E_0\):

\[
E_0=E_{\max}-C,\quad C=E_{\max}-E_0.
\]

La solución general es:

\[
\boxed{E(t)=E_{\max}-(E_{\max}-E_0)e^{-kt}}.
\]

Con los valores iniciales:

\[
\boxed{E(t)=80-60e^{-0.18t}}.
\]

### 4.1 Verificación por sustitución

Derivamos:

\[
E'(t)=60(0.18)e^{-0.18t}=10.8e^{-0.18t}.
\]

Sustituimos en el lado derecho:

\[
0.18(80-E(t))
=0.18(80-80+60e^{-0.18t})
=10.8e^{-0.18t}.
\]

Ambos lados son iguales: la solución satisface la EDO.

Condición inicial:

\[
E(0)=80-60e^0=80-60=20.
\]

También se cumple la condición inicial.

## 5. Métodos numéricos

Se usa \(f(t,E)=k(E_{\max}-E)\). Los métodos utilizan los mismos parámetros, condición inicial, intervalo y tamaño de paso.

### 5.1 Heun (RK2)

\[
k_1=f(t_n,E_n)
\]

\[
k_2=f(t_n+h,E_n+hk_1)
\]

\[
\boxed{E_{n+1}=E_n+\frac{h}{2}(k_1+k_2)}
\]

Primer paso con \(E_0=20\), \(k=0.18\), \(E_{\max}=80\), \(h=1\):

\[
k_1=0.18(80-20)=10.8
\]

\[
k_2=0.18(80-(20+10.8))=8.856
\]

\[
E_1=20+\frac12(10.8+8.856)=\boxed{29.828}.
\]

### 5.2 Runge–Kutta clásico de cuarto orden (RK4)

\[
k_1=f(t_n,E_n)
\]

\[
k_2=f(t_n+h/2,E_n+hk_1/2)
\]

\[
k_3=f(t_n+h/2,E_n+hk_2/2)
\]

\[
k_4=f(t_n+h,E_n+hk_3)
\]

\[
\boxed{E_{n+1}=E_n+\frac{h}{6}(k_1+2k_2+2k_3+k_4)}
\]

Para el primer paso con \(h=1\):

\[
k_1=10.8,\quad k_2=9.828,\quad
k_3=9.91548,\quad k_4=9.0152136.
\]

\[
E_1=20+\frac{10.8+2(9.828)+2(9.91548)+9.0152136}{6}
\]

\[
\boxed{E_1=29.8836956}.
\]

## 6. Errores y comparación

Error absoluto:

\[
\boxed{EA=|E_{\text{exacto}}-E_{\text{aproximado}}|}
\]

Error relativo porcentual:

\[
\boxed{ER(\%)=\frac{EA}{|E_{\text{exacto}}|}\times100}
\]

El error relativo se calcula cuando el valor exacto es distinto de cero.

### 6.1 Resultados de referencia al mes 12

Con \(h=1\), la solución exacta es:

\[
E(12)=80-60e^{-2.16}\approx73.080493.
\]

Resultados aproximados de referencia:

| Método | Valor al mes 12 | Error absoluto | Error relativo |
|---|---:|---:|---:|
| Heun, \(h=1\) | 72,987495 | 0,092998 | 0,127254 % |
| RK4, \(h=1\) | 73,080341 | 0,000152 | 0,000208 % |
| Heun, \(h=0,5\) | 73,058871 | 0,021622 | 0,029586 % |
| RK4, \(h=0,5\) | 73,080484 | 0,000009 | 0,000012 % |

Los resultados están redondeados. La aplicación calcula los valores con precisión de punto flotante y muestra más decimales.

### 6.2 Interpretación

- Reducir el paso de 1 a 0,5 meses mejora la aproximación de ambos métodos.
- RK4 presenta menor error que Heun en los ensayos de referencia.
- RK4 utiliza cuatro pendientes por paso y Heun utiliza dos.
- La solución analítica sirve como referencia para medir los errores.

La gráfica de la aplicación diferencia las soluciones por color, tipo de línea y marcadores. Incluye además una gráfica de errores absolutos con escala logarítmica para observar diferencias pequeñas.

## 7. Tiempo para alcanzar la meta

La meta es el 90 % de la capacidad máxima:

\[
E_{\text{meta}}=0.9(80)=72.
\]

Usando la solución analítica:

\[
72=80-60e^{-0.18t}
\]

\[
e^{-0.18t}=\frac{8}{60}
\]

\[
t=-\frac{\ln(8/60)}{0.18}
\]

\[
\boxed{t\approx11.19\text{ meses}}.
\]

Es una estimación matemática bajo los supuestos del modelo, no una fecha garantizada de inserción laboral.

## 8. Interpretación, conclusiones y limitaciones

### 8.1 Interpretación social

Con los parámetros iniciales, la solución analítica estima aproximadamente 73,08 jóvenes empleados al cabo de 12 meses. Como se trata de personas, el resultado decimal se interpreta como una aproximación matemática agregada; no significa que exista una fracción de persona empleada.

### 8.2 Conclusiones

1. Una EDO de primer orden permite representar el crecimiento limitado del número de jóvenes empleados bajo los supuestos definidos.
2. La solución analítica de referencia es \(E(t)=80-60e^{-0.18t}\).
3. La meta de 72 jóvenes se alcanza matemáticamente en aproximadamente 11,19 meses.
4. RK4 presentó menor error que Heun en los ensayos realizados.
5. Los métodos numéricos permiten estudiar una situación de interés comunitario en Bolivia, pero no sustituyen una evaluación con datos reales.

### 8.3 Limitaciones

El modelo no incluye informalidad laboral, diferencias regionales, cambios económicos, abandono de la capacitación, pérdida de empleo ni variación de la tasa de contratación. Para un estudio predictivo real se necesitarían datos observados y calibración del modelo.

## 9. Aplicación web

La aplicación está implementada en `index.html` y funciona directamente en un navegador moderno, sin instalación ni servidor.

Incluye:

- Ajuste de \(E_0\), \(E_{\max}\), \(k\), tiempo final y paso \(h\).
- Validación básica de entradas.
- Modelo matemático, variables, parámetros y unidades visibles.
- Solución analítica.
- Ejecución de Heun y RK4.
- Gráfica comparativa con trazos y marcadores diferenciados.
- Gráfica de errores absolutos.
- Tabla de iteraciones.
- Comparación entre \(h\) y \(h/2\).
- Errores absolutos y relativos porcentuales.
- Interpretación automática.
- Descarga de la tabla principal en CSV.

### 9.1 Ejecutar localmente

1. Descarga o clona el repositorio.
2. Abre la carpeta del proyecto.
3. Abre `index.html` en un navegador moderno.
4. Modifica los parámetros y pulsa **Ejecutar simulación**.

No requiere Python, Node.js ni paquetes externos.

### 9.2 Publicar en GitHub Pages

1. Crea un repositorio público en GitHub.
2. Sube `index.html` y `README.md` a la raíz.
3. Entra a **Settings → Pages**.
4. En **Build and deployment**, selecciona **Deploy from a branch**.
5. Selecciona la rama `main` y la carpeta `/ (root)`.
6. Guarda y espera la publicación.
7. Abre la URL pública y verifica la simulación.

## 10. Estructura del repositorio

```text
empleo-juvenil-bolivia/
├── index.html
└── README.md
```

## 11. Fuentes de contexto boliviano

Las fuentes institucionales sirven para contextualizar el problema, no para justificar los parámetros hipotéticos:

- Save the Children Bolivia: https://www.savethechildren.org.bo/
- CEPAL: https://www.cepal.org/
- Naciones Unidas en Bolivia: https://bolivia.un.org/

Antes de entregar, completa la bibliografía con el título exacto, fecha y enlace específico de cada publicación consultada. Los dominios anteriores son portales institucionales, no referencias bibliográficas completas.

## 12. Correspondencia con la consigna

| Requisito | Ubicación |
|---|---|
| Problema y contexto | Sección 2 |
| Variables, parámetros, EDO y condición inicial | Sección 3 |
| Supuestos e intervalo | Sección 3.3 |
| Solución analítica y comprobación | Sección 4 |
| Heun y RK4 | Sección 5 |
| Tabla, gráfica y comparación | Sección 6 y aplicación |
| Errores absolutos y relativos | Sección 6 |
| Dos tamaños de paso | Sección 6.1 y aplicación |
| Interpretación, limitaciones y conclusiones | Sección 8 |
| Aplicación y publicación | Sección 9 |
| Video de un minuto | Apoyarse en la aplicación y este README |

---

**Fin del documento.**
