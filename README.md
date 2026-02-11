# 🤖📊 🗳️📊 Inteligencia Electoral - Suite de Inteligencia Electoral

**Análisis de Redes y Narrativas PPTX_Generator_JC** — Plataforma de análisis automatizado de narrativas electorales.

![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-1.30+-FF4B4B?logo=streamlit&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4.1-412991?logo=openai&logoColor=white)
![License](https://img.shields.io/badge/License-Proprietary-red)

---

## 📋 Descripción

Suite de inteligencia electoral que procesa datos de redes sociales (exportados desde plataformas de escucha digital) y genera automáticamente reportes completos con:

- **Análisis de narrativas** mediante redes de grafos estilo Gephi
- **Ejes temáticos** identificados con inteligencia artificial
- **Nubes de palabras** por candidato con normalización lingüística
- **KPIs comparativos** de alcance, menciones y autores
- **Autores influyentes** con métricas de alcance por red social
- **Exportación profesional** en HTML interactivo y PowerPoint

---

## 🚀 Características

| Módulo | Descripción |
|--------|------------|
| 📊 **KPIs** | Menciones, alcance y autores únicos por candidato, ordenados por relevancia |
| 📌 **Ejes Temáticos** | Top 5 temas por candidato identificados con GPT-4.1, con detección de temas compartidos |
| 🕸️ **Red de Narrativas** | Grafo ForceAtlas con anti-superposición de etiquetas, candidatos como nodos centrales |
| 🔄 **Red Inversa** | Términos compartidos entre candidatos, visualización de narrativas cruzadas |
| ☁️ **Nubes de Palabras** | Por candidato, con exclusión inteligente de nombres propios y normalización de acentos |
| 👥 **Autores Influyentes** | Top 10 por candidato con red social y alcance, fallback a posts cuando alcance es 0 |
| #️⃣ **Hashtags** | Trending hashtags del período analizado |

---

## 🏗️ Arquitectura
