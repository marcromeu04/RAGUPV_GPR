# RAG UPV Avanzado - Sistema Inteligente de Análisis de Datos

Sistema RAG (Retrieval-Augmented Generation) avanzado que accede a los datos abiertos de la UPV con capacidades de agente inteligente usando Groq.

## 🚀 Características

### 📊 Acceso a Datos
- **UPV Transparent API**: Conexión directa a datos abiertos de la Universitat Politècnica de València
- **Búsqueda Semántica**: FAISS + SentenceTransformers para encontrar datasets relevantes
- **Carga Automática**: Soporte para CSV y Excel

### 🤖 Agente Inteligente
- **Groq LLM**: Llama 3.1 70B con function calling
- **Razonamiento**: Decide automáticamente qué herramientas usar
- **Conversacional**: Entiende preguntas en lenguaje natural en español

### 🧮 Capacidades Avanzadas
- **Calculadora Matemática**: Evalúa expresiones con numpy, scipy
- **Análisis Estadístico**: Descriptivo, correlaciones, resúmenes
- **Visualizaciones**: Line, bar, scatter, histogram, box, heatmap
- **Ejecución de Código**: Python personalizado para análisis avanzados

## 📋 Requisitos

- Python 3.8+
- API Key de Groq (gratuita en https://console.groq.com)
- Jupyter Notebook

## 🔧 Instalación

1. Clona el repositorio:
```bash
git clone https://github.com/marcromeu04/RAGUPV_GPR.git
cd RAGUPV_GPR
```

2. Instala las dependencias:
```bash
pip install -r requirements.txt
```

3. La API key de Groq ya está configurada en el notebook, o puedes usar la tuya propia.

## 🎯 Uso

### Iniciar el Notebook

```bash
jupyter notebook rag_upv_advanced.ipynb
```

### Ejecutar las Celdas

1. **Instalar dependencias**: Ejecuta la primera celda
2. **Cargar datos**: Ejecuta las celdas de configuración
3. **Hacer preguntas**: Usa el agente para consultas

### Ejemplos de Preguntas

#### Búsqueda de Datasets
```python
agent.query("¿Qué datos hay sobre estudiantes en la UPV?")
```

#### Análisis Estadístico
```python
agent.query("""
Busca datos sobre presupuesto de la UPV,
carga el dataset y muéstrame estadísticas descriptivas
""")
```

#### Visualizaciones
```python
agent.query("""
Encuentra datos de matriculaciones,
carga el dataset y crea un gráfico mostrando la evolución
""")
```

#### Cálculos Personalizados
```python
agent.query("""
Busca datos sobre investigación en la UPV.
Carga el dataset y calcula:
1. El promedio de proyectos por año
2. La desviación estándar
3. El crecimiento porcentual
""")
```

#### Análisis con Código Python
```python
agent.query("""
Busca datos de personal de la UPV.
Carga el dataset y ejecuta código Python para:
- Filtrar solo docentes
- Agrupar por departamento
- Contar y mostrar los 5 departamentos con más personal
""")
```

## 🛠️ Herramientas Disponibles

El agente tiene acceso a 6 herramientas:

### 1. `search_upv_datasets`
Busca datasets relevantes de UPV Transparent basado en consulta semántica.

```python
# Ejemplo interno
search_upv_datasets(query="estudiantes", k=3)
```

### 2. `load_dataset`
Carga datos reales de un dataset específico.

```python
# Ejemplo interno
load_dataset(dataset_id="estudiantes-matriculados", rows=5)
```

### 3. `calculator`
Ejecuta cálculos matemáticos y estadísticos.

```python
# Ejemplo interno
calculator(expression="np.mean([10, 20, 30]) + np.sqrt(144)")
```

### 4. `analyze_dataset`
Realiza análisis estadístico de datasets.

Tipos:
- `descriptive`: Estadísticas descriptivas
- `correlation`: Matriz de correlación
- `summary`: Resumen de estructura

```python
# Ejemplo interno
analyze_dataset(dataset_id="presupuesto", analysis_type="descriptive")
```

### 5. `create_visualization`
Genera visualizaciones de datos.

Tipos de gráficos:
- `line`: Gráfico de línea
- `bar`: Gráfico de barras
- `scatter`: Dispersión
- `histogram`: Histograma
- `box`: Diagrama de caja
- `heatmap`: Mapa de calor

```python
# Ejemplo interno
create_visualization(
    dataset_id="matriculas",
    chart_type="line",
    x_column="año",
    y_column="total",
    title="Evolución de Matrículas"
)
```

### 6. `execute_python`
Ejecuta código Python personalizado.

```python
# Ejemplo interno
execute_python(code="""
filtered = df[df['tipo'] == 'docente']
result = filtered.groupby('departamento').size().nlargest(5)
""")
```

## 📁 Estructura del Proyecto

```
RAGUPV_GPR/
├── rag_upv_advanced.ipynb        # Notebook principal mejorado
├── advanced_rag_calculator.ipynb # Notebook genérico (opcional)
├── requirements.txt              # Dependencias
├── README.md                     # Documentación
├── .gitignore                   # Archivos ignorados
└── .env.example                 # Template de configuración
```

## 🔍 Cómo Funciona

### Flujo de Trabajo

1. **Usuario hace pregunta** en lenguaje natural
2. **Agente analiza** y decide qué herramientas necesita
3. **Búsqueda semántica** encuentra datasets relevantes
4. **Carga datos** del dataset seleccionado
5. **Aplica análisis/visualización** según la pregunta
6. **Presenta resultados** de forma clara en español

### Arquitectura

```
┌─────────────┐
│   Usuario   │
└──────┬──────┘
       │ Pregunta
       ▼
┌─────────────────┐
│  Groq (Llama)   │ ◄── Function Calling
│   LLM Agent     │
└────────┬────────┘
         │
    ┌────┴────┐
    │  Tools  │
    └────┬────┘
         │
    ┌────┴────────────────────┐
    │                         │
┌───▼────┐           ┌───────▼────────┐
│ FAISS  │           │  UPV Datasets  │
│ Search │           │    (API)       │
└───┬────┘           └───────┬────────┘
    │                        │
    └────────┬───────────────┘
             │
       ┌─────▼──────┐
       │  Analysis  │
       │ & Visuals  │
       └────────────┘
```

## 🎨 Ejemplos Avanzados

### Análisis Comparativo
```python
agent.query("""
Compara los datos de estudiantes de grado vs máster.
Carga ambos datasets, calcula estadísticas y crea un gráfico comparativo.
""")
```

### Dashboard Estadístico
```python
agent.query("""
Para el dataset de investigación:
1. Muéstrame estadísticas descriptivas
2. Crea un histograma de distribución
3. Calcula la correlación entre variables numéricas
4. Genera un heatmap de correlaciones
""")
```

### Análisis Temporal
```python
agent.query("""
Analiza la evolución del presupuesto de investigación:
- Carga los datos históricos
- Calcula la tasa de crecimiento anual
- Predice tendencia con regresión
- Visualiza con gráfico de línea
""")
```

## 🚦 Modo Interactivo

El notebook incluye un modo interactivo para sesiones conversacionales:

```python
interactive_mode()
```

Comandos disponibles:
- Pregunta normal: Escribe tu consulta
- `salir` o `exit`: Terminar sesión
- `clear`: Limpiar cache de datasets

## 📊 Datasets Disponibles

Los datos provienen de **UPV Transparent**, que incluye información sobre:

- 👨‍🎓 Estudiantes y matrícula
- 💰 Presupuesto y finanzas
- 🔬 Investigación y proyectos
- 👥 Personal (PDI, PAS)
- 📚 Publicaciones científicas
- 🏛️ Infraestructuras y campus
- 📈 Indicadores y rankings

## ⚡ Funciones de Acceso Rápido

Para consultas frecuentes:

```python
# Búsqueda rápida
quick_search("estudiantes doctorado")

# Análisis rápido
quick_analyze("presupuesto investigacion")

# Visualización rápida
quick_viz("matriculas", chart_type="bar")
```

## 🔐 Configuración de API Key

### Opción 1: En el notebook (actual)
La API key ya está configurada en el código.

### Opción 2: Variable de entorno
```bash
export GROQ_API_KEY="tu-api-key"
```

### Opción 3: Archivo .env
Copia `.env.example` a `.env` y configura:
```
GROQ_API_KEY=tu-api-key-aqui
```

## 📈 Casos de Uso

### 1. Análisis Académico
- Evolución de matrícula por carreras
- Tasas de graduación
- Distribución de estudiantes internacionales

### 2. Gestión Financiera
- Análisis de presupuesto por departamentos
- ROI de proyectos de investigación
- Tendencias de financiación

### 3. Investigación
- Productividad científica
- Análisis de publicaciones
- Colaboraciones internacionales

### 4. Recursos Humanos
- Distribución de personal
- Ratios estudiante/profesor
- Análisis demográfico

## 🤝 Contribuir

¡Las contribuciones son bienvenidas!

1. Fork el proyecto
2. Crea una rama (`git checkout -b feature/AmazingFeature`)
3. Commit cambios (`git commit -m 'Add AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📝 Licencia

Este proyecto está bajo la licencia MIT.

## 🙏 Agradecimientos

- **Groq** por proporcionar acceso a Llama 3.1
- **UPV** por los datos abiertos a través de UPV Transparent
- **FAISS** (Facebook AI) por la búsqueda vectorial
- **Sentence Transformers** por los embeddings
- Comunidad de Python y Data Science

## 📧 Contacto

Marc Romeu - [@marcromeu04](https://github.com/marcromeu04)

Project Link: [https://github.com/marcromeu04/RAGUPV_GPR](https://github.com/marcromeu04/RAGUPV_GPR)

## 🔮 Roadmap

- [x] Sistema RAG básico con UPV datos
- [x] Function calling con Groq
- [x] Calculadora y análisis estadístico
- [x] Visualizaciones automáticas
- [x] Ejecución de código Python
- [ ] Soporte para más formatos (JSON, XML)
- [ ] Cache persistente de datasets
- [ ] Análisis de series temporales avanzado
- [ ] Exportación de reportes (PDF, HTML)
- [ ] Interfaz web con Streamlit
- [ ] Comparación multi-dataset
- [ ] Alertas y notificaciones
- [ ] Integración con bases de datos SQL

## ⚠️ Notas Importantes

- **API de Groq**: Gratuita con límites de uso (consulta https://console.groq.com)
- **Datos UPV**: Los datasets se cargan en tiempo real desde la API
- **Cache**: Los datasets se cachean en memoria durante la sesión
- **Performance**: Primera carga puede tardar (generando embeddings)
- **Privacidad**: No se envían datos sensibles, solo metadatos públicos

## 🐛 Resolución de Problemas

### Error de conexión a UPV API
```python
# Verificar conectividad
import requests
requests.get("https://upvtransparent.upv.es/api/3/action/package_list")
```

### Error cargando datasets
- Algunos datasets pueden no estar en formato CSV/Excel
- Verifica el formato con `search_upv_datasets`

### Embeddings lentos
- Primera ejecución genera embeddings (puede tardar)
- Ejecuciones posteriores usan cache

### Límites de Groq
- Respeta rate limits de la API
- Reduce `max_iterations` si es necesario

## 💡 Tips y Trucos

1. **Preguntas específicas**: Sé específico en tus consultas
2. **Iterar**: Si no obtienes el resultado, reformula la pregunta
3. **Explorar**: Usa `search_upv_datasets` para ver qué hay disponible
4. **Combinar**: Puedes pedir múltiples análisis en una consulta
5. **Código personalizado**: Para análisis muy específicos, pide ejecución de código Python

## 📚 Recursos Adicionales

- [Documentación Groq](https://console.groq.com/docs)
- [UPV Transparent](https://upvtransparent.upv.es/)
- [FAISS Documentation](https://faiss.ai/)
- [Sentence Transformers](https://www.sbert.net/)
- [Pandas Documentation](https://pandas.pydata.org/)

---

**Desarrollado con ❤️ para la comunidad UPV**
