# Predicción de Captura de Exámenes Médicos (PySpark, GBTClassifier)

> **Nota de privacidad**: Este cuaderno emplea **datos sintéticos** en la etapa de extracción y exploración. Los resultados que se muestran están **agregados** y la terminología de negocio ha sido **neutralizada** (p. ej., “Seguro_Público/Privado”, “Centro A/B/C”). No se exponen identificadores ni fuentes internas.

## Objetivo
Desarrollar un modelo de **propensión a captura** para priorizar acciones comerciales, asignando **incentivos diferenciados** según el nivel de probabilidad estimada y optimizando la relación **impacto / costo**.

## Dataset (sintético)
- Rango temporal reciente (≈ 3 meses).
- Variables de ejemplo: fecha, especialidad, centro, zona, aseguradora (neutralizada), precio promedio, señal de derivación/captura, eventos de citación (creación, anulación), y diagnóstico (simulado).
- La generación incorpora variaciones realistas (volumen diario, tasas de captura, agendamientos futuros/pasados).

## Metodología
1. **Simulación de datos** con reglas coherentes (probabilidad de captura, citaciones, distribución de prestaciones por especialidad).
2. **Preparación y features** (tipos, índices categóricos, ensamblado de vectores, escalado cuando aplica).
3. **Modelo**: `GBTClassifier` (PySpark) con grilla simple de hiperparámetros y validación cruzada.
4. **Métricas**: ROC AUC, matriz de confusión agregada, lift/KS (según visualizaciones disponibles).
5. **Reproducibilidad**: semillas fijadas tanto en la simulación como en el entrenamiento.

## Estrategia de activación (genérica)
Las predicciones se utilizan para orquestar **acciones diferenciadas** por tramo de probabilidad:
- **Baja propensión** → incentivos más atractivos.
- **Propensión intermedia** → estímulo moderado, buscando el mejor equilibrio costo/beneficio.
- **Alta propensión** → evitar beneficios innecesarios, priorizando eficiencia.

> Esta lógica permite **maximizar la efectividad** enfocando recursos donde más se necesitan y **evitar incentivos superfluos**.

## Resultados e impacto
- En una implementación análoga, la estrategia contribuyó a una mejora de **≈ +5 puntos porcentuales** en la tasa de captura (p. ej., **55% → 60%**).
- **Dependencias clave**: El impacto real depende de la **ejecución de los canales de contacto** (claridad del mensaje, **timing**, oportunidad) para materializar la recomendación del modelo.

## Cómo ejecutar
### Local (PySpark)
1. Python 3.10+ y PySpark instalado.
2. Abrir el notebook `*_PORTFOLIO.ipynb` y ejecutar secuencialmente.  
   > La sección de guardado / MLflow es opcional y puede comentarse.

### Databricks (opcional)
- El cuaderno puede ejecutarse en clusters Databricks. La sección de guardado menciona rutas tipo `dbfs:/...` como **placeholder**. Ajustar a la convención del entorno si se desea registrar artefactos en MLflow.

## Estructura del notebook
- **Extracción sintética y EDA**: generación del dataset neutralizado y exploración sin PII.
- **Entrenamiento**: preparación de features, GBT y evaluación.
- **Activación**: ejemplos de segmentación por propensión y medición de impacto (agregado).

## Licencia
Uso con fines demostrativos y de portafolio. No replica procesos internos ni datos reales.