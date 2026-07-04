# Dashboard de Análisis Operativo y Financiero - Red de Clínicas Médicas

Este repositorio contiene una solución integral de Inteligencia de Negocios (BI) que abarca desde la estructuración de la infraestructura de datos en el backend hasta el diseño de una interfaz analítica interactiva de nivel corporativo en el frontend.

---

## Arquitectura del Data Warehouse y Proceso ETL (SQL Server & SSIS)

El pilar de esta solución es un **Data Warehouse corporativo** desarrollado en **Microsoft SQL Server** (`ClinicaDB`) bajo un **Modelo Estrella (Star Schema)**. Para la ingesta, limpieza y movimiento de los datos desde los sistemas transaccionales hacia el repositorio analítico, se diseñó e implementó un flujo formal de **ETL (Extracción, Transformación y Carga)** utilizando **SQL Server Integration Services (SSIS)** en **Visual Studio**.

### Flujo de Ingeniería de Datos (ETL)
* **Extracción & Transformación:** Consolidación, limpieza y homogeneización de los tipos de datos transaccionales, controlando las coherencias de tiempo y campos de texto mediante componentes nativos de SSIS.
* **Carga Dinámica:** Automatización del flujo para alimentar la estructura dimensional optimizando los tiempos de procesamiento.
* **Modelo Multidimensional Resultante:**
    * **Tabla de Hechos:** `vFact_CitaMedica` (Centraliza métricas de facturación, volumen de consultas y estados operativos).
    * **Tablas de Dimensiones:** `vDim_Sede`, `vDim_Doctor`, `vDim_Paciente` y dimensión temporal integrada (`CALENDARIO`).

*Nota: Todas las llaves subrogadas (Surrogate Keys - SK) fueron debidamente ocultas en la capa de modelado de Power BI para asegurar una vista de informe intuitiva y orientada 100% al negocio.*
---

## Vista General del Dashboard (Power BI)

El entregable final fue diseñado en **Power BI Desktop**, implementando contenedores blancos redondeados con sombreado sutil sobre un fondo gris claro, logrando una interfaz de usuario (*UI*) limpia, intuitiva y con aspecto de aplicación web premium.

![Vista Previa del Dashboard](Dashboard_Clinica_Medica.png)

---

## Objetivos Analíticos Cumplidos

El reporte interactivo cubre al 100% las necesidades operativas y comerciales solicitadas por la gerencia:

1.  **Indicadores Clave de Rendimiento (KPIs Principales):**
    * **Monto Total:** Suma global y transparente de la facturación registrada ($18,007.04).
    * **Citas Totales:** Conteo exacto del volumen analizado (127 citas en el segmento activo).
    * **Tasa de Cancelación:** Porcentaje de citas canceladas calculado mediante DAX avanzado (`KEEPFILTERS` y `ALL`), aislando correctamente las métricas y manteniéndolas dinámicas frente a las interacciones del usuario (12.60%).
    * **Ingresos Proyectados:** Métrica de valor agregado para monitorear los montos financieros en riesgo o en espera debido a citas en estado pendiente.

2.  **Bloques de Análisis Visual:**
    * **Evolución Temporal:** Gráfico de líneas que expone las fluctuaciones mensuales de la facturación real vs. la proyectada para identificar picos de demanda estacionales.
    * **Monto por Sede:** Gráfico de columnas que audita los ingresos de cada clínica ordenados de mayor a menor, identificando a la *Clínica Central* como sede líder.
    * **Ingresos por Especialidad:** Gráfico de embudo con degradado de color automatizado según facturación, destacando las áreas médicas con mayor impacto económico.
    * **Enfermedades más Atendidas:** Un mapa de árbol (*Treemap*) en escala monocromática que agrupa las consultas según el diagnóstico para la correcta planificación de campañas de prevención y stock de farmacia.
    * **Segmentación por Edad:** Gráfico circular de distribución demográfica por `RangoEdad`, revelando que el *Adulto Mayor* representa el público objetivo principal (94.49%).

3.  **Filtros Interactivos Avanzados:**
    * Segmentadores superiores horizontales para conmutación rápida de estados (*Cancelada, Completada, Pendiente*).
    * Filtros dinámicos de jerarquía temporal (*Año* y *Mes*).
    * Menú desplegable para el análisis aislado por *Sede*.

---

## Tecnologías Utilizadas

* **Motor de Base de Datos:** Microsoft SQL Server (Diseño de tablas transaccionales, consultas de transformación DDL/DML y vistas optimizadas).
* **Herramienta de BI:** Power BI Desktop (Conexión al Data Warehouse, modelado de datos dimensional, optimización de tipos de datos de fechas y diseño de interfaz de usuario).
* **Lenguaje DAX:** Desarrollo de medidas dinámicas e inteligentes robustas ante el cruce de filtros cruzados.
