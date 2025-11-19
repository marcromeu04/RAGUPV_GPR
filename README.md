# Advanced RAG Calculator - RAG con Capacidades de Agente

Sistema RAG avanzado que combina recuperación de información con capacidades de cálculo, análisis estadístico y generación de visualizaciones usando Claude de Anthropic.

## 🚀 Características

- **📚 RAG (Retrieval-Augmented Generation)**: Búsqueda semántica en documentos usando ChromaDB
- **🧮 Calculadora Avanzada**: Ejecución de expresiones matemáticas complejas
- **💻 Ejecución de Código**: Ejecuta código Python para análisis personalizado
- **📊 Visualizaciones**: Genera gráficos (línea, barras, dispersión, histogramas, etc.)
- **📈 Análisis Estadístico**: Estadística descriptiva, correlación, regresión, tests
- **🤖 Agente Inteligente**: Orquesta herramientas usando function calling de Claude

## 📋 Requisitos

- Python 3.11+
- API Key de Anthropic
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

3. Configura tu API Key de Anthropic:
```bash
export ANTHROPIC_API_KEY="tu-api-key-aqui"
```

O directamente en el notebook editando la variable `ANTHROPIC_API_KEY`.

## 🎯 Uso

### Modo Notebook

1. Abre el notebook:
```bash
jupyter notebook advanced_rag_calculator.ipynb
```

2. Ejecuta las celdas secuencialmente para:
   - Instalar dependencias
   - Inicializar el sistema RAG
   - Cargar documentos de ejemplo
   - Probar ejemplos de uso

### Ejemplos Rápidos

#### Cálculos Matemáticos
```python
agent.chat("Calcula la raíz cuadrada de 144 multiplicada por el promedio de 10, 20, 30, 40, 50")
```

#### Análisis Estadístico
```python
agent.chat("Analiza estadísticamente estos datos: [45, 52, 61, 68, 75] y dame media, mediana y desviación estándar")
```

#### Crear Visualizaciones
```python
agent.chat("Crea un gráfico de barras con ventas mensuales: Enero=45000, Febrero=52000, Marzo=61000")
```

#### Búsqueda en Documentos
```python
agent.chat("¿Cuáles son las ventas totales del Q1 2024 según los documentos?")
```

#### Análisis Complejo
```python
agent.chat("""
Analiza estos datos de ventas y marketing:
- Ventas: [45, 52, 61, 68, 75]
- Marketing: [10, 15, 20, 25, 30]

1. Calcula la correlación
2. Crea un modelo de regresión
3. Genera un gráfico de dispersión con línea de tendencia
4. Dame el ROI promedio
""")
```

## 🛠️ Herramientas Disponibles

El agente tiene acceso a las siguientes herramientas:

### 1. **calculator**
Evalúa expresiones matemáticas complejas con acceso a NumPy y SciPy.

```python
agent.chat("Calcula: np.sqrt(144) + np.mean([1,2,3,4,5])")
```

### 2. **execute_python**
Ejecuta código Python arbitrario para análisis personalizado.

```python
agent.chat("""
Ejecuta un código que genere 100 números aleatorios,
calcule cuántos son mayores a 50 y su promedio.
""")
```

### 3. **create_visualization**
Genera visualizaciones de datos.

Tipos soportados:
- `line`: Gráfico de línea
- `bar`: Gráfico de barras
- `scatter`: Diagrama de dispersión
- `histogram`: Histograma
- `box`: Diagrama de caja
- `heatmap`: Mapa de calor
- `pie`: Gráfico circular

### 4. **statistical_analysis**
Realiza análisis estadístico.

Tipos soportados:
- `descriptive`: Estadística descriptiva
- `correlation`: Análisis de correlación
- `regression`: Regresión lineal
- `t_test`: Test t de Student
- `anova`: Análisis de varianza

### 5. **search_documents**
Busca información en documentos cargados usando búsqueda semántica.

## 📁 Estructura del Proyecto

```
RAGUPV_GPR/
├── advanced_rag_calculator.ipynb  # Notebook principal
├── requirements.txt               # Dependencias
└── README.md                     # Documentación
```

## 🔍 Cómo Funciona

1. **Inicialización**: Se crea un cliente de Anthropic y una base de datos vectorial ChromaDB
2. **Carga de Documentos**: Los documentos se vectorizan y almacenan en ChromaDB
3. **Procesamiento de Consultas**:
   - El usuario hace una pregunta
   - El agente decide qué herramientas usar (function calling)
   - Ejecuta las herramientas necesarias
   - Procesa los resultados y genera una respuesta

## 🎨 Ejemplos de Casos de Uso

### Análisis de Ventas
```python
# Cargar datos
rag.add_document("""
Ventas Q1:
- Enero: $45,000
- Febrero: $52,000
- Marzo: $61,000
""")

# Analizar
agent.chat("Analiza las ventas de Q1 y muéstrame un gráfico de tendencia")
```

### Análisis Financiero
```python
agent.chat("""
Tengo estos datos de inversión y retornos:
Inversión: [1000, 1500, 2000, 2500]
Retornos: [1200, 1900, 2500, 3200]

Calcula el ROI de cada inversión, el ROI promedio,
y crea un gráfico mostrando la relación.
""")
```

### Análisis Científico
```python
agent.chat("""
Tengo estos datos experimentales:
Grupo A: [23, 25, 27, 24, 26]
Grupo B: [30, 32, 31, 33, 29]

Realiza un t-test para verificar si hay diferencia significativa
y muestra un box plot comparativo.
""")
```

## 📊 Funciones Auxiliares

El notebook incluye funciones de acceso rápido:

```python
# Cálculo rápido
quick_calc("np.sqrt(144) + 10")

# Visualización rápida
quick_viz({'x': [1,2,3], 'y': [4,5,6]}, chart_type='line', title='Mi Gráfico')

# Estadísticas rápidas
quick_stats([10, 20, 30, 40, 50])

# Búsqueda en documentos
ask_documents("¿Cuáles son las ventas totales?")
```

## 🔄 Modo Interactivo

El notebook incluye un modo interactivo para chatear con el agente:

```python
interactive_mode()
```

Comandos especiales:
- `/reset`: Reiniciar conversación
- `/docs`: Ver documentos cargados
- `/add`: Agregar nuevo documento
- `/exit`: Salir

## 🧪 Testing

Ejecuta los ejemplos en las celdas del notebook para probar las diferentes capacidades:

1. **Ejemplo 1**: Cálculos matemáticos
2. **Ejemplo 2**: Análisis estadístico con RAG
3. **Ejemplo 3**: Creación de visualizaciones
4. **Ejemplo 4**: Análisis complejo multi-herramienta
5. **Ejemplo 5**: Ejecución de código Python
6. **Ejemplo 6**: Correlación y regresión

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Por favor:

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📝 Licencia

Este proyecto está bajo la licencia MIT.

## 🙏 Agradecimientos

- [Anthropic](https://www.anthropic.com/) por Claude API
- [ChromaDB](https://www.trychroma.com/) por la base de datos vectorial
- Comunidad de Python y Data Science

## 📧 Contacto

Marc Romeu - [@marcromeu04](https://github.com/marcromeu04)

Project Link: [https://github.com/marcromeu04/RAGUPV_GPR](https://github.com/marcromeu04/RAGUPV_GPR)

## 🔮 Roadmap

- [ ] Soporte para múltiples tipos de archivos (PDF, CSV, Excel)
- [ ] Integración con más modelos de visualización (Plotly interactivo)
- [ ] Cache de resultados para consultas frecuentes
- [ ] API REST para uso como servicio
- [ ] Interfaz web con Streamlit/Gradio
- [ ] Soporte para bases de datos SQL
- [ ] Exportación de análisis a PDF/Word
- [ ] Integración con herramientas de BI

## ⚠️ Notas Importantes

- **API Key**: Necesitas una API key válida de Anthropic
- **Costos**: El uso de la API de Claude tiene costos asociados
- **Seguridad**: El código Python se ejecuta con `eval()` - usa con precaución en producción
- **Límites**: Respeta los rate limits de la API de Anthropic

## 📚 Recursos Adicionales

- [Documentación de Claude](https://docs.anthropic.com/)
- [ChromaDB Docs](https://docs.trychroma.com/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [Matplotlib Gallery](https://matplotlib.org/stable/gallery/)
- [Seaborn Tutorial](https://seaborn.pydata.org/tutorial.html)
