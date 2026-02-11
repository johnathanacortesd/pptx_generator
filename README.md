# 🗳️ Inteligencia Electoral - Análisis de Redes y Narrativas PPTX_Generator_JC

**ANÁLISIS DE DATOS ELECTORALES** — Plataforma de análisis automatizado de narrativas para elecciones y política.

[![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python&logoColor=white)](https://python.org)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.30+-FF4B4B?logo=streamlit&logoColor=white)](https://streamlit.io)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4.1-412991?logo=openai&logoColor=white)](https://openai.com)
[![License](https://img.shields.io/badge/License-Proprietary-red)](#-licencia)

---

<div align="center">

<br>

[![Streamlit App](https://img.shields.io/badge/🚀_ABRIR_APLICACIÓN-Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)]([https://tu-app.streamlit.app](https://pptx-generator-jc.streamlit.app)

<br>
<p><em>Acceso protegido por contraseña. Contactar al administrador para credenciales.</em></p>

</div>

---

## 📋 Descripción

Suite de inteligencia electoral desarrollada por **Johnathan Cortés** que procesa datos de redes sociales (exportados desde plataformas de escucha digital como Brandwatch, Meltwater, Sprinklr, etc.) y genera automáticamente reportes ejecutivos completos.

La herramienta transforma datos crudos en insights estratégicos mediante:
- **Análisis de narrativas** con grafos estilo Gephi y layout ForceAtlas.
- **Identificación de ejes temáticos** utilizando inteligencia artificial (GPT-4.1).
- **Generación de entregables** en formatos HTML interactivo y presentaciones PowerPoint nativas.

---

## 🚀 Características Principales

| Módulo | Descripción |
|--------|-------------|
| 📊 **KPIs por Candidato** | Menciones, alcance total y autores únicos, ordenados por volumen de conversación. |
| 📌 **Ejes Temáticos (IA)** | Top 5 temas específicos por candidato identificados con GPT-4.1, con detección automática de temas compartidos. |
| 🕸️ **Red de Narrativas** | Grafo interactivo con layout ForceAtlas, anti-superposición de etiquetas, nodos centrales conectados a palabras clave y autores. |
| 🔄 **Narrativas Compartidas** | Red inversa que muestra términos y hashtags compartidos entre múltiples candidatos. |
| ☁️ **Nubes de Palabras** | Generadas por candidato con colores temáticos, exclusión inteligente de nombres propios y normalización lingüística. |
| 👥 **Autores Influyentes** | Top 10 por candidato con columnas Autor, Red y Alcance (conteo de posts si el alcance es 0). |
| #️⃣ **Hashtags Trending** | Los 12 hashtags más frecuentes del período analizado. |
| 💾 **Cache Inteligente** | Los resultados se guardan en sesión; descargar archivos no re-ejecuta el análisis. |

---

## 🏗️ Arquitectura del Sistema

```
┌──────────────────────────────────────────────────────┐
│                   STREAMLIT APP                       │
│                                                      │
│  ┌────────────┐   ┌───────────┐   ┌───────────────┐  │
│  │  Auth Gate │ → │ File      │ → │  Processing   │  │
│  │  (Password)│   │ Uploader  │   │  Pipeline     │  │
│  └────────────┘   └───────────┘   └───────┬───────┘  │
│                                           │          │
│         ┌─────────────┬───────────┬───────┤          │
│         │             │           │       │          │
│         ▼             ▼           ▼       ▼          │
│  ┌────────────┐ ┌──────────┐ ┌────────┐ ┌────────┐  │
│  │  OpenAI    │ │ForceAtlas│ │ Word   │ │  KPIs  │  │
│  │  GPT-4.1   │ │ Layout   │ │ Clouds │ │ Engine │  │
│  │  (Temas)   │ │ (Grafos) │ │        │ │        │  │
│  └─────┬──────┘ └────┬─────┘ └───┬────┘ └───┬────┘  │
│        │             │           │           │       │
│        ▼             ▼           ▼           ▼       │
│  ┌─────────────────────────────────────────────────┐ │
│  │          st.session_state (Cache)               │ │
│  │  Resultados persistidos durante la sesión       │ │
│  └──────────┬──────────────────┬───────────────────┘ │
│             │                  │                     │
│        ┌────▼─────┐     ┌─────▼──────┐              │
│        │  HTML    │     │  PowerPoint│              │
│        │ Interac. │     │  5 Slides  │              │
│        └──────────┘     └────────────┘              │
└──────────────────────────────────────────────────────┘
```

---

## 📂 Estructura del Proyecto

```
pptx_generator_jc/
├── app.py              # Aplicación principal Streamlit
├── requirements.txt    # Dependencias Python
├── .gitignore          # Exclusión de secrets y temporales
└── README.md           # Documentación
```

---

## ⚙️ Instalación Local

### Prerrequisitos

- Python 3.9 o superior
- API Key de OpenAI (modelo GPT-4.1-nano o compatible)
- Archivo Excel con datos de escucha digital

### Pasos

```bash
# 1. Clonar repositorio
git clone https://github.com/tu-usuario/pptx-generator-jc.git
cd pptx-generator-jc

# 2. Crear entorno virtual
python -m venv venv
source venv/bin/activate      # Linux/Mac
# venv\Scripts\activate       # Windows

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Configurar secrets (solo para desarrollo local)
mkdir -p .streamlit
cat > .streamlit/secrets.toml << EOF
APP_PASSWORD = "tu-contraseña-segura"
OPENAI_API_KEY = "sk-tu-api-key-aqui"
EOF

# 5. Ejecutar aplicación
streamlit run app.py
```

---

## 🛠️ Personalización Técnica

### Ajuste de Fuentes en Grafos (Red de Narrativas)

Para modificar el tamaño de las etiquetas en los grafos (tanto en la versión interactiva HTML como en la imagen estática del PowerPoint), edita los siguientes valores en `app.py`:

| Archivo/Función | Línea/Parámetro a buscar | Qué controla | Valor Recomendado |
|---|---|---|---|
| `crear_red_principal` | `size=15` en `textfont` | Texto nodos Candidatos (HTML/Plotly) | `17` o `18` |
| `crear_red_principal` | `fs=12` / `11` | Texto etiquetas Palabras (HTML/Plotly) | `14` / `13` |
| `renderizar_red_matplotlib` | `fontsize=14` | Texto nodos Candidatos (PNG/PPTX) | `16` o `17` |
| `renderizar_red_matplotlib` | `fontsize=11` | Texto etiquetas Palabras (PNG/PPTX) | `13` o `14` |
| `renderizar_red_matplotlib` | `fontsize=9` | Texto Autores (PNG/PPTX) | `11` o `12` |

---

## 📊 Formato de Datos de Entrada

La app espera un archivo Excel (`.xlsx`) con las siguientes columnas clave:

| Columna | Requerida | Descripción |
|---------|:---------:|-------------|
| `Contenido de la publicación` | ✅ | Texto completo del post |
| `Autor` | ✅ | Nombre o handle del autor |
| `Grupo de dominio` o `Fuente` | ⬜ | Red social (X, Facebook, Instagram, etc.) |
| `followers` | ⬜ | Seguidores (para cálculo de alcance) |
| `fans` | ⬜ | Fans (para cálculo de alcance) |
| `Interacciones totales` | ⬜ | Engagement total |

> **Nota:** La columna `Twitter` se renombra automáticamente a `X`. Si no hay datos de seguidores, el alcance se reporta como 0 (indicando N Posts).

---

## 🎨 Outputs Generados

### 1. HTML Interactivo
Reporte autocontenido con gráficos Plotly (zoom, pan, hover) y CSS embebido. No requiere internet para visualizarse una vez descargado.

### 2. PowerPoint Ejecutivo (5 Slides)
Generación nativa `.pptx` lista para presentar:

| Slide | Contenido |
|:-----:|-----------|
| **1** | Dashboard General: KPIs + Ejes Temáticos + Hashtags |
| **2** | Red de Narrativas (Imagen Alta Resolución - ForceAtlas) |
| **3** | Narrativas Compartidas (Red Inversa) |
| **4** | Nubes de Palabras (Por candidato) |
| **5** | Top 10 Autores Influyentes (Tabla detallada) |

---

## 📝 Configuración de Candidatos

El sistema viene preconfigurado con diccionarios para candidatos (colores y regex). Para modificar, editar `CANDIDATOS_CONFIG` y `COLORES` en `app.py`:

```python
COLORES = {
    'Mauricio Cárdenas': '#B22222',
    'Juan Carlos Pinzón': '#00BFFF',
    # ... agregar más
}

CANDIDATOS_CONFIG = {
    'Nombre Candidato': {
        'nombre_corto': 'N. Candidato',
        'regex': [r'palabra_clave', r'\botra_clave\b'],
        'blacklist': ['palabra', 'comun', 'excluir']
    },
}
```

---

## 🔒 Seguridad

- **Autenticación:** Barrera de entrada por contraseña.
- **Datos Volátiles:** Procesamiento en memoria RAM, sin bases de datos persistentes.
- **API Keys:** Gestión segura vía `st.secrets` (nunca expuestas en código).
- **Limpieza:** Botón de "Cerrar Sesión" que purga el estado de la aplicación.

---

## 👤 Autor

**Johnathan Cortés**

- **Proyecto:** PPTX_Generator_JC
- 📧 Email: [tu@email.com](mailto:tu@email.com)
- 💼 LinkedIn: [linkedin.com/in/tu-perfil](https://linkedin.com/in/tu-perfil)
- 🐙 GitHub: [github.com/tu-usuario](https://github.com/tu-usuario)

---

## 📄 Licencia

```
© 2025 Johnathan Cortés. Todos los derechos reservados.

Este software es propiedad intelectual de Johnathan Cortés.
Se proporciona bajo licencia para uso profesional. Queda prohibida
su reproducción, distribución o uso no autorizado sin permiso expreso.
```

---

<div align="center">

<br>

**🗳️ PPTX_Generator_JC**

*Análisis de Redes y Narrativas Electorales*

<br>

© 2025 Johnathan Cortés 🇨🇴

</div>
