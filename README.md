# Implementación de Indicadores Estratégicos para la Toma de Decisiones de Negocio — Plaza Vea (2025-2026)

Proyecto de **Inteligencia de Negocios** desarrollado para la Facultad de Ingeniería de la Universidad Tecnológica del Perú (UTP), enfocado en integrar la gestión de inventario con el desempeño comercial de **Supermercados Peruanos S.A. (Plaza Vea)**.

## Descripción del proyecto

Plaza Vea no contaba con una visión unificada entre su cadena de suministro y su desempeño comercial, lo que generaba quiebres de stock y dificultaba entender el comportamiento de compra en las distintas regiones donde opera. Este proyecto construye una solución de BI de extremo a extremo (fuente de datos → ETL → modelo dimensional → dashboards) para responder eso.

Se trabajó sobre una base de datos maestra de **23,667 registros transaccionales** (periodo 2025-2026) de cuatro sucursales estratégicas: **Trujillo, Miraflores, Arequipa y Los Olivos**, integrando información de ventas, costos, utilidades y stock disponible.

## Objetivo

Facilitar la toma de decisiones estratégicas, tácticas y operativas mediante el seguimiento de KPIs comerciales y operativos, la identificación de patrones de compra por región y categoría de producto, y su vinculación con los objetivos estratégicos de la organización a través de un Balanced Scorecard (BSC).

## Stakeholders

- **Gerencia Comercial** — define metas de venta y estrategias de precio por región.
- **Gerencia de Suministro y Operaciones** — responsable de niveles de stock e inventario.
- **Jefaturas de Tienda** — gestión operativa diaria de ventas e inventario.
- **Inteligencia de Negocios** — administra el modelo de datos y los dashboards.

## Preguntas de negocio

- ¿Cuál es el comportamiento de las ventas diarias por sucursal y categoría de producto?
- ¿Qué sucursales presentan mayor riesgo de quiebre de stock?
- ¿Cómo varía el ticket promedio y el margen de utilidad entre regiones?
- ¿Existe relación entre el nivel de stock disponible y el volumen de ventas por tienda?

## KPIs definidos

| KPI | Fórmula | Periodicidad | Meta |
|---|---|---|---|
| Ventas totales | Σ Monto_Venta | Diaria / Mensual | +8% vs. periodo anterior |
| Margen de utilidad | (Σ Utilidad / Σ Monto_Venta) × 100 | Mensual | Mantener ≥ 22% |
| Ticket promedio | Σ Monto_Venta / Conteo único (Nro_Ticket) | Diaria / Mensual | +5% vs. periodo anterior |
| Nivel de stock disponible | Promedio (Stock_Disponible_Tienda) | Diaria | Mantener stock mínimo por categoría |
| Rotación de inventario | Cantidad_Vendida / Stock_Disponible_Tienda | Mensual | Optimizar por sucursal |

## Arquitectura de la solución

```
Archivo CSV maestro  →  ETL (Power Query)  →  Modelo dimensional (Esquema Estrella)  →  Dashboards (Power BI)
```

**Modelo dimensional (Star Schema):**

- **Fact_Ventas** (tabla de hechos): Cantidad_Vendida, Monto_Venta, Monto_Costo, Utilidad, Stock_Disponible_Tienda.
- **Dim_Tiempo**: Fecha, Año, Mes, Día, Trimestre.
- **Dim_Sucursal**: ID_Sucursal, Sucursal, Región.
- **Dim_Producto**: ID_Producto, Producto, Categoría_Producto.
- **Dim_Ticket**: Nro_Ticket, Canal_Venta.

## Proceso ETL

1. **Extracción:** conexión de Power BI / Power Query al CSV maestro (23,667 registros, 19 columnas).
2. **Transformación:** limpieza de nulos, duplicados y outliers; estandarización de formatos de fecha y nombres de sucursal/categoría; creación de columnas calculadas (Monto_Venta, Monto_Costo, Utilidad, Margen_Porcentual); conversión de tipos de datos; separación del archivo único en tablas de hechos y dimensiones.
3. **Carga:** consolidación final en Fact_Ventas y las dimensiones del modelo estrella.

## Herramienta de visualización

**Power BI**, elegido por su integración nativa con Power Query, capacidad de modelado dimensional (relaciones y medidas DAX), facilidad para construir dashboards interactivos con segmentadores, y su adopción extendida en retail.

### Dashboard principal incluye:

- KPIs destacados en tarjetas (ventas totales, margen de utilidad, ticket promedio, stock disponible).
- Segmentadores por Año, Mes, Región/Sucursal y Categoría de Producto.
- Gráficos de tendencia de ventas, comparación entre sucursales y composición por categoría.
- Jerarquías de navegación: Año → Mes → Día, y Región → Sucursal.

### Reportes analíticos por tema:

- Comportamiento de ventas diarias por sucursal y categoría.
- Riesgo de quiebre de stock (stock disponible vs. cantidad vendida).
- Ticket promedio y margen por región.
- Relación entre disponibilidad de inventario y volumen de ventas.

## Balanced Scorecard (BSC)

Los KPIs desarrollados se alinean con las cuatro perspectivas del BSC (Financiera, Clientes, Procesos Internos, Aprendizaje y Crecimiento) mediante un mapa estratégico y una propuesta de tablero de control integrado, conectando indicadores de resultado con indicadores de gestión.

## Estructura del repositorio

```
├── Informe_BI_Plaza_Vea.docx      # Informe final completo
├── /dashboards                     # Archivo fuente de Power BI (.pbix)
├── /data                           # Archivo(s) de datos utilizados
├── /scripts                        # Scripts de ETL (Power Query / M, SQL)
└── README.md
```

## Integrantes

- Jose Alberto Farid Bojorquez Huarcaya
- Eduardo Sebastian Lucas Rios
- Nestor Angelo Preciado Quispe
- Fabrizio Jhair Durand Bendezu
- Oscar Fernando Gutierrez Huarcaya

**Docente:** Atilio Julio Soria Leon
**Curso:** Inteligencia de Negocios — Sección 25136
**Universidad Tecnológica del Perú** — Facultad de Ingeniería

## Licencia

Proyecto académico desarrollado con fines educativos para la UTP.
