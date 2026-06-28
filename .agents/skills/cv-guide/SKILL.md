---
name: cv-guide
description: Guía completa para crear y optimizar CVs técnicos de AI/Software Engineers. Cubre diseño visual, arquitectura de información, escaneabilidad para HR, compatibilidad ATS, y mejores prácticas de LaTeX.
---

# CV Guide para AI/Software Engineers

Guía completa para crear CVs técnicos efectivos, basada en análisis de diseñadores visuales, arquitectos técnicos, reclutadores de HR, y principios de Harvard Freshman Resume.

## Flujo de Trabajo: Análisis Visual del CV

**IMPORTANTE**: Antes de hacer recomendaciones, el agente DEBE solicitar imágenes del CV renderizado para análisis visual.

### Pasos obligatorios:

1. **Solicitar compilación del CV**:
   - Pedir al usuario que compile el archivo `.tex` y genere el PDF
   - Comando: `pdflatex -interaction=nonstopmode [archivo].tex`

2. **Solicitar imágenes del CV**:
   - Pedir al usuario que exporte o capture pantallas del PDF renderizado
   - Formato preferido: PNG o JPEG de alta resolución
   - Incluir todas las páginas (si son múltiples)
   - Alternativa: usar `pdftoppm` o `convert` para generar imágenes desde el PDF:
     ```bash
     pdftoppm -png -r 150 [archivo].pdf cv-preview
     ```

3. **Analizar visualmente antes de recomendar**:
   - Revisar jerarquía visual (¿el nombre destaca?)
   - Verificar espaciado y ritmo (¿hay suficiente white space?)
   - Identificar elementos cluttered o densos
   - Detectar problemas de alineación
   - Evaluar coherencia cromática
   - Verificar que las fechas no hagan wrap

4. **Hacer recomendaciones basadas en evidencia visual**:
   - Referirse a elementos específicos visibles en las imágenes
   - No asumir problemas sin ver el renderizado
   - Priorizar cambios basados en impacto visual observado

### Por qué es crucial el análisis visual:

- **El código LaTeX no revela todos los problemas**: Spacing, alineación, y densidad visual solo son evidentes en el renderizado
- **El usuario puede describir problemas subjetivos**: "se ve cluttered", "no me gusta esta línea", "hay mucho espacio vacío" — estas observaciones requieren ver el CV
- **Las decisiones de diseño son visuales**: No se pueden optimizar sin ver el resultado final

---

## 0. Perspectivas de Análisis

Este documento integra recomendaciones de cuatro perspectivas:

- **Diseñador Visual**: Armonía, tipografía, color, ritmo visual, jerarquía tipográfica
- **Arquitecto Técnico**: Jerarquía de información, estructura, densidad de contenido, credibilidad técnica
- **HR / Reclutador**: Escaneabilidad en 30 segundos, ATS, red flags, keywords estándar
- **Harvard Freshman Resume**: Principios universales (white space, bullets cortos, sin itálicas excesivas, fuentes distintivas)

Las reglas incluyen referencias entre corchetes indicando qué perspectiva las respalda (ej: `[Diseñador + Harvard]`).

---

## 1. TIPOGRAFÍA Y FUENTE

### Reglas

- **NO usar `mathptmx` (Times)**: Es genérica y anticuada para perfiles técnicos en 2026 `[Diseñador + Harvard]`
- **Fuentes recomendadas**:
  - `newtxtext` + `newtxmath` (Times mejorado con mejor kerning)
  - XeLaTeX/LuaLaTeX: Inter, IBM Plex Sans, Garamond, Gill Sans
- **Tamaño base**: 10pt mínimo, 11pt preferido para legibilidad `[Harvard]`
- **Jerarquía del nombre**: Contraste mínimo de 8-10pt entre nombre y título `[Diseñador]`
  ```latex
  {\fontsize{20}{22}\selectfont\textbf{Full Name}} \\[4pt]
  {\large Job Title}
  ```
- **Eliminar itálicas excesivas**: Harvard dice explícitamente no usar itálicas excepto para énfasis genuino `[Harvard]`
  - NO usar itálica en: rol, empresa, fechas, grado académico
  - SÍ usar itálica para: nombres de proyectos específicos

### Por qué importa

- **Harvard**: *"generic fonts like Times New Roman are used in most manuscripts, so to stand out use: Garamond, Gill Sans, Cambria, Calibri, Georgia, Avenir"*
- **Diseñador**: Times se siente genérica y anticuada para un AI Engineer en 2026. La fuente comunica profesionalismo y atención al detalle.
- **HR**: Una fuente legible y moderna facilita la lectura rápida. Fuentes genéricas hacen que el CV se vea como "uno más".

---

## 2. ESPACIADO Y RITMO VERTICAL

### Reglas

- **Unificar espaciado inter-sección**: Definir todo en `\titlespacing`, eliminar `\vspace` manuales inconsistentes `[Diseñador]`
  ```latex
  \titlespacing{\section}{0pt}{0.4cm}{0.25cm}
  ```
- **Espacio entre título de sección y contenido**: Mínimo 0.25cm para dar respiro `[Diseñador + Usuario]`
- **Separar visualmente experiencias laborales**: Añadir `\vspace{0.2cm}` entre el último bullet de una experiencia y el header de la siguiente `[Diseñador]`
- **Principio Harvard de white space**: *"having white space helps your readers NOT to be overwhelmed"* `[Harvard]`
- **Bullets espaciados**:
  ```latex
  \begin{itemize}[topsep=0.1cm, itemsep=0.08cm, leftmargin=0.6cm]
  ```

### Por qué importa

- **Harvard**: El white space previene que el lector se sienta abrumado. Un CV denso se abandona.
- **HR**: Un reclutador dedica 6-8 segundos al primer escaneo. El espaciado guía el ojo hacia las secciones importantes.
- **Diseñador**: La inconsistencia en espaciados (ej: usar `.3em`, `.2em`, `0.1em` de forma arbitraria) rompe el ritmo visual y se siente descuidado.

---

## 3. LAYOUT Y ALINEACIÓN

### Reglas

- **Eliminar indentación de `onecolentry`**: Crea desalineación con títulos de sección `[Diseñador]`
- **Migrar `paracol` a `tabularx`**: Más predecible y ATS-friendly `[Diseñador + HR]`
  ```latex
  \newcommand{\entryheader}[2]{
    \par\noindent\textbf{#1}\hfill#2\par
  }
  ```
- **Formato de puestos**: Cargo en **bold** a la izquierda, fecha en texto normal a la derecha `[Usuario]`
  ```
  **AI Engineer**                          May 2026 – Present – On-site
  State Prosecutor's Office of Guanajuato, Mexico
  ```
- **Alinear títulos de sección a `0pt`**: NO usar `-1pt` que desalinea 1pt respecto al cuerpo `[Diseñador]`
- **Datos de contacto en 2 líneas** (no una sola densa) `[Usuario]`
  - Línea 1: email + teléfono
  - Línea 2: ubicación + LinkedIn + GitHub

### Por qué importa

- **Arquitecto**: La desalineación título/contenido crea ruido visual y hace que el documento se vea desorganizado.
- **HR**: El layout de dos columnas con `paracol` es problemático para ATS. Muchos sistemas (Taleo, Greenhouse, Lever) leen de izquierda a derecha y mezclan el contenido de ambas columnas.
- **Diseñador**: La alineación consistente es fundamental para la armonía visual. Cada elemento debe tener una razón para estar donde está.

---

## 4. COLOR Y ELEMENTOS VISUALES

### Reglas

- **Color primario**: Azul vibrante `RGB(0, 92, 163)` (no apagado como `0, 79, 144`) `[Diseñador]`
- **Colorear `\titlerule`** con `primaryColor` a `0.6pt` para coherencia cromática `[Diseñador]`
  ```latex
  \titleformat{\section}{\needspace{3\baselineskip}\bfseries\large}{}{0pt}{}[{\color{primaryColor}\titlerule[0.6pt]}]
  ```
- **Iconos FontAwesome**: Usar en contacto para escaneo rápido `[Diseñador]`
  ```latex
  \faEnvelope, \faPhone, \faMapMarker*, \faLinkedin, \faGithub
  ```
- **NO usar líneas separadoras decorativas en el header**: La jerarquía visual ya funciona con contraste de tamaño `[Usuario]`
- **Marker de bullets**: Usar `label={\small\textbullet}` en vez del punto negro sólido por defecto `[Diseñador]`
- **NO incluir línea de métricas sueltas** sin contexto (los números ya están en los bullets) `[Usuario]`

### Por qué importa

- **Diseñador**: El color azul apagado `RGB(0, 79, 144)` no transmite modernidad. Un azul más vibrante (`0, 92, 163`) mejora la percepción sin perder profesionalismo.
- **Harvard**: El documento debe verse profesional, no artístico. Las líneas decorativas sin función clara añaden ruido visual.
- **HR**: Los iconos facilitan el escaneo rápido de datos de contacto. Un reclutador puede encontrar el email o LinkedIn en menos de 1 segundo.

---

## 5. ESTRUCTURA DE CONTENIDO

### Header

#### Reglas
- **Dos líneas de contacto** (no una sola densa) `[Usuario]`
- **GitHub obligatorio** para AI/Software Engineers `[Arquitecto + HR]`
- **NO incluir línea de métricas sueltas** sin contexto `[Usuario]`

#### Por qué importa
- **HR**: Un reclutador técnico quiere ver código, repos, contribuciones. La ausencia de GitHub es una señal negativa para roles técnicos senior.
- **Arquitecto**: Los datos de contacto en una sola línea densa son difíciles de escanear. Dos líneas con separadores claros mejoran la legibilidad.

### Profile Summary

#### Reglas
- **Máximo 3-4 líneas**, enfocadas en impacto de negocio, no en jargon técnico `[HR + Harvard]`
- **Fórmula**: "Qué haces + Para quién + Logro clave + Expertise core" `[HR]`
- **NO mezclar logros de negocio con jargon técnico profundo** `[HR]`

#### Ejemplo
```
AI Engineer with 4+ years building production AI systems for government and legal tech.
Currently leading R&D at the State Prosecutor's Office of Guanajuato, Mexico, where
forensic tools I developed have been adopted by 5 jurisdictions. Previously built
AI-powered workflows serving 1,000+ customers at a US legal tech company. Core expertise:
GPU infrastructure, computer vision, LLM systems, and cloud-native AWS architectures.
```

#### Por qué importa
- **HR**: El Profile Summary es lo primero que lee un no-técnico. Si es muy denso o técnico, pierdes la atención en los primeros 6 segundos.
- **Arquitecto**: Un bloque de 5 líneas de texto corrido sin breaks visuales obliga a una lectura lineal completa. Un reclutador técnico salta directamente a buscar nombres de empresas y habilidades clave.
- **Harvard**: *"succinct explanation for research/internship activities"*

### Professional Experience

#### Reglas
- **Bullets de máximo 2 líneas** (Harvard: bullets de 1-2 líneas) `[Harvard + HR]`
- **Fórmula**: "Acción concreta + Resultado medible" `[HR]`
- **Separar bullets que empaquetan múltiples proyectos**: Cada proyecto merece su propio bullet `[Arquitecto]`
- **Agregar métricas cuantitativas** en todos los bullets (latencia, accuracy, throughput, usuarios) `[Arquitecto]`
- **Reemplazar acrónimos sin contexto** `[HR]`:
  - "FGEG" → "State Prosecutor's Office of Guanajuato, Mexico"
  - "SEMEFO" → "forensic services (SEMEFO)"
- **Mencionar infraestructura específica**: "on-premise cluster", "vLLM", "KV-cache optimization" `[Arquitecto]`
- **Agregar contexto de equipo/liderazgo**: "Leading R&D" → ¿cuántas personas? `[Arquitecto + HR]`

#### Por qué importa
- **Arquitecto**: Los bullets que empaquetan múltiples proyectos diluyen el logro de cada uno. "Built a tattoo-based person search system... and a phone records analysis platform" son dos proyectos distintos con stacks y problemas diferentes.
- **HR**: Sin métricas, un tech lead no puede calibrar la magnitud del impacto. "1,000+ customers" está bien, pero ¿cuánto mejoró el semantic search vs. búsqueda tradicional?
- **Harvard**: Bullets de máximo 2 líneas. Un bullet de 3 líneas se siente como un párrafo, no como un logro.

### Technical Skills

#### Reglas
- **Reordenar por relevancia al rol**: AI/ML primero, Programming Languages al final `[HR + Arquitecto]`
- **Listar herramientas concretas, no conceptos** `[Arquitecto]`:
  - NO: "semantic search, embeddings, vector similarity search"
  - SÍ: nombres de vector DBs (Pinecone, Weaviate, pgvector), frameworks (PyTorch, HuggingFace)
- **Agregar keywords estándar de ATS**: "machine learning", "computer vision", "MLOps", "CI/CD", "microservices", "REST APIs" `[HR]`
- **Consolidar en un solo bloque** con `\\[2pt]` entre líneas, NO un `onecolentry` por categoría `[Diseñador]`
- **Separar categorías mezcladas**: "AI Infrastructure & Computer Vision" → "ML Infrastructure" + "Computer Vision" `[Arquitecto]`
- **Eliminar tecnologías no relevantes**: Si PHP no aparece en experiencia, quitarlo `[HR + Arquitecto]`

#### Ejemplo de orden
```latex
\textbf{AI \& LLMs:} OpenAI, Gemini, prompt engineering, multi-LLM orchestration, AI agents, machine learning, computer vision \\[2pt]
\textbf{ML Infrastructure:} NVIDIA H100 GPU clusters (on-premise), vLLM, model deployment, PyTorch, HuggingFace, MLOps \\[2pt]
\textbf{Computer Vision:} facial aging models, image embeddings, semantic similarity search, tattoo recognition, OpenCV \\[2pt]
\textbf{Cloud \& Infrastructure:} AWS (Lambda, Step Functions, EC2, S3), Docker, CI/CD, microservices \\[2pt]
\textbf{Backend \& Frameworks:} Node.js, Express.js, AdonisJS, Laravel, REST APIs \\[2pt]
\textbf{Data Stores:} MySQL, Redis (queues, caching), Amazon Redshift (columnar analytics) \\[2pt]
\textbf{Programming Languages:} TypeScript, JavaScript (ES6+), Python
```

#### Por qué importa
- **Arquitecto**: Hay redundancia significativa entre Skills y Experience. "Semantic search", "embeddings" aparecen en ambos. La sección de Skills debe ser una referencia rápida de tecnologías concretas, no de conceptos ya demostrados en la experiencia.
- **HR**: Si buscas roles de AI Engineer, "AI Infrastructure & Computer Vision" debería ir primero. "Backend & Frameworks" puede ir al final. El orden comunica prioridades.
- **Diseñador**: Cada skill category en su propio `onecolentry` añade `0.2cm` de `adjustwidth` arriba y abajo, creando micro-espacios irregulares. Un solo bloque con `\\[2pt]` es más limpio.

### Education

#### Reglas
- **Mismo formato que experiencia**: `\entryheader{Institución}{Fechas}` `[Diseñador]`
- **No listar GPA ni SAT scores** (principio Harvard para perfiles senior) `[Harvard]`

### Languages

#### Reglas
- **Formato inline**: `\textbf{Spanish:} Native \quad \textbf{English:} C1 \quad \textbf{French:} B2`
- **Sin entorno `onecolentry`** para secciones tan cortas `[Diseñador]`

---

## 6. COMPATIBILIDAD ATS

### Reglas

- **Preparar versión de una sola columna** para portales corporativos (ATS) `[HR]`
  - Eliminar `paracol`, usar secciones estándar
  - El CV actual es perfecto para envío directo por email/LinkedIn
- **`\section{}` con `titlesec` puede no ser reconocido** por algunos parsers `[HR]`
  - Asegurar nombres estándar: "Experience", "Education", "Skills"
- **Hyperlinks con `hyperref` pueden causar ruido** en algunos ATS `[HR]`
  - El texto visible es legible, pero el URL subyacente puede generar problemas
- **Keywords estándar obligatorias**: "machine learning", "computer vision", "MLOps", "CI/CD", "microservices", "REST APIs" `[HR]`

### Por qué importa

- **HR**: Muchos ATS (Taleo, Greenhouse, Lever) leen de izquierda a derecha, de arriba a abajo. Cuando encuentran dos columnas, pueden mezclar el contenido de ambas, resultando en texto garbled. Las fechas que aparecen a la derecha podrían intercalarse con el texto de la izquierda.
- **Arquitecto**: Faltan keywords estándar que los filtros automáticos buscan. Tu CV menciona "OpenAI", "Gemini", "embeddings", pero no tiene términos estándar de la industria como "machine learning", "computer vision" (como keyword aislada), "MLOps".
- **HR**: Si aplicas a "AI Engineer", el ATS busca keywords específicas: "machine learning", "deep learning", "Python", "TensorFlow/PyTorch", "MLOps", etc.

---

## 7. DETALLES FINOS

### LaTeX

- **Agregar `fontenc[T1]` e `inputenc[utf8]`** para renderizado correcto de acentos `[Diseñador]`
  ```latex
  \usepackage[T1]{fontenc}
  \usepackage[utf8]{inputenc}
  ```
- **Eliminar `footskip` de geometry** si usas `\pagestyle{empty}` `[Diseñador]`
- **Reducir `needspace` de `4\baselineskip` a `3\baselineskip`** en CVs de 1 página `[Diseñador]`
- **Comillas tipográficas**: Cambiar `"texto"` por ``` ``texto'' ``` o `\textit{texto}` `[HR]`

### Contenido

- **Agregar "Mexico" en la ubicación**: "Leon, Guanajuato" → "Leon, Guanajuato, Mexico" `[HR]`
- **Aclarar timeline** si un rol tiene solo 1-2 meses pero mucho detalle `[Arquitecto + HR]`
- **Agregar contexto de equipo/liderazgo**: "Leading R&D" → ¿cuántas personas? `[Arquitecto + HR]`

### Por qué importa

- **Diseñador**: El `footskip=1.0cm` es innecesario si usas `\pagestyle{empty}`. Cada milímetro cuenta en un CV de 1 página.
- **HR**: Un reclutador detallista podría notar que empezaste a trabajar antes de graduarte. Esto en realidad es positivo (trabajabas mientras estudiabas), pero podría aclararse.
- **Diseñador**: Las comillas rectas `"Rostros..."` se ven como errores tipográficos en el PDF. Las comillas tipográficas ``` ``Rostros...'' ``` son profesionales.

---

## 8. CHECKLIST DE REVISIÓN

### Antes de enviar

- [ ] ¿Cabe en 1 página?
- [ ] ¿El nombre tiene contraste jerárquico suficiente (mínimo 8-10pt de diferencia con el título)?
- [ ] ¿Los datos de contacto están en 2 líneas?
- [ ] ¿Hay GitHub en el header?
- [ ] ¿El Profile Summary es ≤4 líneas y enfocado en impacto (no jargon)?
- [ ] ¿Los bullets son ≤2 líneas cada uno?
- [ ] ¿Hay métricas cuantitativas en los bullets de experiencia?
- [ ] ¿Los acrónimos tienen contexto internacional?
- [ ] ¿Las skills están reordenadas por relevancia al rol?
- [ ] ¿Hay keywords estándar de ATS (machine learning, computer vision, MLOps, CI/CD)?
- [ ] ¿Las comillas son tipográficas?
- [ ] ¿Compila sin warnings?
- [ ] ¿No hay líneas separadoras decorativas sin función clara?
- [ ] ¿No hay itálicas excesivas (solo para énfasis genuino)?
- [ ] ¿No hay tecnologías listadas que no aparezcan en experiencia?

---

## 9. ERRORES COMUNES A EVITAR

1. **Línea de métricas sueltas sin contexto** (los números ya están en los bullets) `[Usuario]`
2. **Datos de contacto en una sola línea densa** (usar 2 líneas) `[Usuario]`
3. **Líneas separadoras decorativas en el header** (la jerarquía visual ya funciona) `[Usuario]`
4. **Itálicas excesivas** (solo para énfasis genuino) `[Harvard]`
5. **Bullets que empaquetan múltiples proyectos** (separar) `[Arquitecto]`
6. **Skills con conceptos en vez de herramientas concretas** `[Arquitecto]`
7. **Acrónimos sin contexto internacional** `[HR]`
8. **Profile Summary demasiado técnico y denso** `[HR]`
9. **Falta de GitHub** (obligatorio para AI/Software Engineers) `[Arquitecto + HR]`
10. **Tecnologías listadas pero no usadas en experiencia** (ej: PHP) `[HR + Arquitecto]`
11. **Falta de métricas cuantitativas** en bullets de experiencia `[Arquitecto]`
12. **Spacing inconsistente** entre secciones (usar `\titlespacing` unificado) `[Diseñador]`
13. **Fuente genérica** (Times/mathptmx) `[Diseñador + Harvard]`
14. **Falta de keywords estándar de ATS** `[HR]`
15. **Layout de dos columnas con `paracol`** para portales ATS `[HR]`

---

## 10. EJEMPLO DE ESTRUCTURA IDEAL

```latex
\documentclass[a4paper, 10pt]{article}

% Encoding
\usepackage[T1]{fontenc}
\usepackage[utf8]{inputenc}

% Packages
\usepackage[ignoreheadfoot, top=1.5cm, bottom=1.5cm, left=1.5cm, right=1.5cm]{geometry}
\usepackage{newtxtext}
\usepackage{newtxmath}
\usepackage{titlesec}
\usepackage{tabularx}
\usepackage[dvipsnames]{xcolor}
\definecolor{primaryColor}{RGB}{0, 92, 163}
\usepackage{enumitem}
\usepackage{fontawesome5}
\usepackage[
  pdftitle={CV},
  pdfauthor={Name},
  colorlinks=true,
  urlcolor=primaryColor
]{hyperref}
\usepackage{needspace}

\pagestyle{empty}
\setcounter{secnumdepth}{0}
\setlength{\parindent}{0pt}

\titleformat{\section}{\needspace{3\baselineskip}\bfseries\large}{}{0pt}{}[{\color{primaryColor}\titlerule[0.6pt]}]
\titlespacing{\section}{0pt}{0.4cm}{0.25cm}

\newenvironment{highlights}{
  \begin{itemize}[topsep=0.1cm,itemsep=0.08cm,leftmargin=0.6cm,label={\small\textbullet}]
    }{
  \end{itemize}
}

\newcommand{\entryheader}[2]{
  \par\noindent\textbf{#1}\hfill#2\par
}

\begin{document}

\begin{center}
  {\fontsize{20}{22}\selectfont\textbf{Full Name}} \\[4pt]
  {\large Job Title} \\[10pt]
  {\small
    \href{mailto:email@domain.com}{\faEnvelope\ email@domain.com}
    \quad\textbar\quad
    \faPhone\ (+XX) XXX XXX XXXX
  } \\[3pt]
  {\small
    \faMapMarker*\ City, Country
    \quad\textbar\quad
    \href{https://linkedin.com/in/user}{\faLinkedin\ linkedin.com/in/user}
    \quad\textbar\quad
    \href{https://github.com/user}{\faGithub\ github.com/user}
  }
\end{center}

\vspace{0.3cm}

\section{Profile Summary}
Concise summary focused on impact, not jargon. Maximum 3-4 lines.
What you do + For whom + Key achievement + Core expertise.

\section{Professional Experience}

\entryheader{Job Title}{Date Range -- Location}
Company Name

\begin{highlights}
\item Action verb + concrete result + metric. Maximum 2 lines.
\item Another achievement with measurable impact.
\item Separate bullets for separate projects.
\end{highlights}

\vspace{0.2cm}

\entryheader{Previous Job}{Date Range -- Location}
Previous Company

\begin{highlights}
\item Achievement with metrics.
\item Include context for acronyms (international audience).
\end{highlights}

\section{Technical Skills}

\textbf{AI \& LLMs:} Tool1, Tool2, Tool3 \\[2pt]
\textbf{ML Infrastructure:} Tool4, Tool5, Tool6 \\[2pt]
\textbf{Computer Vision:} Tool7, Tool8, Tool9 \\[2pt]
\textbf{Cloud \& Infrastructure:} Tool10, Tool11, Tool12 \\[2pt]
\textbf{Backend \& Frameworks:} Tool13, Tool14, Tool15 \\[2pt]
\textbf{Data Stores:} Tool16, Tool17, Tool18 \\[2pt]
\textbf{Programming Languages:} Language1, Language2, Language3

\section{Education}

\entryheader{University}{Year -- Year}
Degree

\vspace{0.15cm}

\entryheader{Exchange University}{Year -- Year}
Program

\section{Languages}
\textbf{Language 1:} Level \quad \textbf{Language 2:} Level \quad \textbf{Language 3:} Level

\end{document}
```

---

## 11. CUÁNDO USAR ESTE SKILL

### Requisito previo: Análisis visual obligatorio

**Antes de aplicar cualquier recomendación de este skill, el agente DEBE:**

1. Solicitar al usuario que compile el CV y genere el PDF
2. Solicitar imágenes/capturas del CV renderizado (PNG o JPEG)
3. Analizar visualmente el CV antes de hacer recomendaciones
4. Referirse a elementos específicos visibles en las imágenes

Ver sección "Flujo de Trabajo: Análisis Visual del CV" al inicio de este documento.

### Usar cuando:
- Creando un nuevo CV técnico desde cero
- Optimizando un CV existente para aplicaciones de trabajo
- Revisando el CV antes de enviarlo a reclutadores o portales
- Necesitando compatibilidad con ATS
- Buscando mejorar la escaneabilidad para HR no técnico
- Aplicando a roles de AI Engineer, ML Engineer, Software Engineer, o similares
- El usuario menciona problemas visuales subjetivos ("se ve cluttered", "no me gusta esta línea", "hay mucho espacio vacío")

### No usar cuando:
- Creando CVs académicos (research-focused, con publicaciones)
- Creando CVs para roles no técnicos (marketing, diseño, etc.)
- Diseñando CVs con layouts creativos/artísticos (infografías, etc.)
- Creando resumes para industrias específicas con formatos estándar (legal, médico)
- El usuario no puede proporcionar imágenes del CV renderizado

---

## 12. RECURSOS ADICIONALES

### Harvard Freshman Resume Template
- URL: https://scienceeducation.fas.harvard.edu/sites/g/files/omnuum7836/files/lifesci/files/instructions_template_for_freshman_resume.pdf
- Principios clave: white space, bullets cortos, fuentes distintivas, sin itálicas excesivas

### Fuentes Recomendadas
- `newtxtext` + `newtxmath` (pdflatex)
- Inter, IBM Plex Sans, Garamond, Gill Sans (XeLaTeX/LuaLaTeX)

### Keywords ATS para AI/ML Roles
- machine learning, deep learning, computer vision, natural language processing
- MLOps, model deployment, CI/CD, microservices, REST APIs
- PyTorch, TensorFlow, HuggingFace, OpenCV
- AWS, Docker, Kubernetes, Redis, MySQL

### Iconos FontAwesome Disponibles
- `\faEnvelope`, `\faPhone`, `\faMapMarker*`, `\faLinkedin`, `\faGithub`
- `\faGlobe`, `\faTwitter`, `\faStackOverflow`, `\faGitlab`
