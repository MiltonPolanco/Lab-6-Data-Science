# Laboratorio 6 — Análisis de redes sociales (YouTube)

**CC3084 — Data Science, Universidad del Valle de Guatemala**
**Integrantes:** Milton Polanco y Osman de León
**Repositorio:** https://github.com/MiltonPolanco/Lab-6-Data-Science

## Descripción

Análisis de la estructura de participación de usuarios, la relación entre canales y temas, y el
contenido de las conversaciones observadas en dos conjuntos de datos de YouTube (`youtube_videos.csv`
y `youtube_comments.csv`). El trabajo cubre carga e integración, limpieza y calidad de datos, análisis
exploratorio, construcción de la red bipartita autor-video, sus proyecciones, topología y
fragmentación, detección de comunidades, centralidad y participantes puente, y análisis de sentimiento.

## Estructura del repositorio

```
.
├── data/
│   ├── youtube_videos.csv              # dataset original (293 videos)
│   ├── youtube_comments.csv            # dataset original (406 comentarios)
│   ├── youtube_videos_limpio.csv       # generado al ejecutar el notebook
│   ├── youtube_comments_limpio.csv     # generado al ejecutar el notebook
│   └── youtube_integrado.csv           # generado al ejecutar el notebook
├── notebooks/
│   └── Laboratorio_6_Analisis_de_redes_sociales_YouTube.ipynb
├── reporte/
│   ├── figuras/                        # ~14 figuras PNG, generadas al ejecutar el notebook
│   └── tablas/                         # ~25 tablas CSV, generadas al ejecutar el notebook
├── README.md
└── requirements.txt
```

> El notebook detecta automáticamente si se ejecuta desde `notebooks/` (usa `..` como raíz) o desde
> la raíz del proyecto, así que puede colocarse en cualquiera de las dos ubicaciones sin cambiar rutas.

## Dependencias

Python 3.10+ y las siguientes librerías (incluidas en `requirements.txt`):

```
pandas>=2.0
numpy>=1.24
matplotlib>=3.7
seaborn>=0.12
networkx>=3.2
jupyter
```

`networkx>=3.2` es necesario porque el notebook usa `networkx.algorithms.community.louvain_communities`
(detección de comunidades) y `networkx.algorithms.bipartite` (proyecciones y clustering bipartito),
disponibles de forma nativa a partir de esa versión — no se requiere instalar `python-louvain` por
separado.

### Instalación

```bash
python3 -m venv .venv
source .venv/bin/activate          # en Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## Cómo ejecutar el análisis

1. Colocar `youtube_videos.csv` y `youtube_comments.csv` dentro de `data/` (ya están en el repositorio).
2. Abrir Jupyter desde la raíz del proyecto:
   ```bash
   jupyter notebook notebooks/Laboratorio_6_Analisis_de_redes_sociales_YouTube.ipynb
   ```
3. Ejecutar todas las celdas en orden (`Kernel → Restart & Run All`). El notebook:
   - Crea automáticamente `reporte/figuras/` y `reporte/tablas/` si no existen.
   - Exporta ~25 tablas CSV (diagnóstico de calidad, resúmenes exploratorios, tablas de nodos/aristas
     de la red bipartita y sus proyecciones, topología, comunidades, centralidad, sentimiento, etc.).
   - Exporta ~14 figuras PNG con las visualizaciones del informe.
   - Guarda copias limpias de los datasets (`*_limpio.csv`) y el dataset integrado.

No se requiere descargar ningún modelo ni recurso externo: el análisis de sentimiento usa un léxico en
español construido dentro del propio notebook (ver justificación metodológica en la sección 9), ya que
el entorno de ejecución puede no tener acceso a internet para descargar modelos preentrenados.

## Notas metodológicas relevantes

- Los identificadores (`video_id`, `channel_id`, `comment_id`, `author_channel_id`) nunca se sustituyen
  por nombres visibles; estos últimos solo se usan como etiquetas para tablas y gráficas.
- `reply_count` **no** se usa para construir aristas entre usuarios: no identifica a los autores de las
  respuestas, tal como indica el enunciado del laboratorio.
- Una arista en la red bipartita autor-video indica únicamente que un autor publicó al menos un
  comentario principal en ese video; no implica amistad, respuesta directa, conversación ni aprobación.
- Todas las conclusiones están acotadas a la muestra entregada (19 de 293 videos con comentarios,
  recolectados mediante consultas de búsqueda dirigidas) y no se generalizan a todos los usuarios de
  YouTube ni a la población de Guatemala.

## Entrega

- **Avance** (ejercicios 1 a 4): entregado el 3 de septiembre de 2026.
- **Documento final completo**: entregado el 6 de septiembre de 2026.