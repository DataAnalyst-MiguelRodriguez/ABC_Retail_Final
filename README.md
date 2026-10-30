# 🛒 ABC Retail: Análisis End-to-End de Rentabilidad, Funnel, Retención y A/B Test

Proyecto de analítica de datos de punta a punta para un e-commerce en **México, Colombia y Argentina** (ene–jun 2025): limpieza de datos, KPIs de rentabilidad, funnel de conversión y retención por cohortes en **SQL**, evaluación estadística de un experimento A/B y dashboard ejecutivo en BI.

![Python](https://img.shields.io/badge/Python-3.x-blue) ![SQL](https://img.shields.io/badge/SQL-PostgreSQL-336791) ![Pandas](https://img.shields.io/badge/Pandas-Limpieza-150458) ![Statsmodels](https://img.shields.io/badge/Statsmodels-A/B_test-orange) ![BI](https://img.shields.io/badge/Power_BI_/_Tableau-Dashboard-F2C811)

## 🎯 Preguntas de negocio
1. ¿El negocio es rentable? (ingresos vs. costo de producto vs. inversión en marketing)
2. ¿En qué etapa del funnel de compra se pierden los usuarios?
3. ¿Los usuarios regresan después de registrarse?
4. ¿El cambio de UI en el checkout mejora la conversión?
5. ¿Cómo comunicar todo esto a un directivo? → Dashboard ejecutivo

## 🔎 Resultados clave

### 🔻 Funnel de conversión (SQL)
| Etapa | Usuarios únicos | Caída vs. etapa previa |
|---|---|---|
| first_visit | 7,796 | — |
| select_item | 7,582 | 2.74% |
| add_to_cart | 7,634 | +0.69% (anomalía de datos) |
| begin_checkout | 7,208 | 5.58% |
| add_payment_info | 6,250 | **13.29% (mayor fuga)** |
| purchase | 6,240 | 0.16% |

**Insight:** la mayor pérdida ocurre entre iniciar el checkout y agregar el método de pago, por lo que ahí conviene priorizar mejoras (fricción en formulario, métodos de pago, costos de envío visibles). Además, `add_to_cart` supera a `select_item`, lo que sugiere que hay usuarios que agregan al carrito sin pasar por ese evento: es un problema de instrumentación a revisar.

### 🧪 A/B test del checkout (10,000 usuarios)
| Variante | Usuarios | Conversiones | Tasa |
|---|---|---|---|
| Control | 4,965 | 779 | 15.69% |
| Tratamiento | 5,035 | 820 | 16.29% |

Z-test de dos proporciones: **z = 0.81, p = 0.416** → diferencia de +0.6 pp **no significativa**.
**Recomendación:** no implementar el cambio solo con esta evidencia; completar validaciones (SRM, balance por dispositivo y país) y estimar el intervalo de confianza o ampliar la muestra.

### 🔁 Retención por cohortes semanales (SQL)
22 cohortes semanales con retención a 1, 2 y 3 semanas desde el registro. Patrón estable entre cohortes: semana 1 [COMPLETAR %], semana 2 [COMPLETAR %], semana 3 [COMPLETAR %].

### 💰 Rentabilidad
Se integraron pedidos, catálogo (costo unitario) y gasto de marketing por canal para calcular revenue, costo de producto, inversión en marketing, profit, ticket promedio y producto más vendido.
- Ingreso total: [COMPLETAR tras tratar outliers]
- Profit: [COMPLETAR]
- Ticket promedio (mediana): [COMPLETAR]
- Inversión en marketing: $2.87M (social $918K · organic $914K · paid search $863K · sin canal $177K)

## 🧹 Calidad de datos (Pandas)
- **25,000 pedidos únicos** tras eliminar 100 duplicados por `id_pedido`.
- Fechas convertidas a `datetime` en pedidos y marketing.
- `país` pasó de 6 a 3 categorías al estandarizar mayúsculas y espacios.
- Valores imposibles (`cantidad` y `monto_total` negativos) detectados y corregidos.
- Nulos tratados con reglas por columna: categoría y precio por moda del producto, cantidad como `monto_total / precio_unitario`, y `desconocido` en categóricas.
- Outliers extremos de cantidad (10,000–20,000 unidades) identificados y [COMPLETAR: excluidos / marcados].
- Datasets limpios exportados para el dashboard.

## 📊 Dashboard
- **Overview ejecutivo:** revenue, profit, gasto en marketing, ticket promedio y unidades por orden, con evolución mensual y comparativos por producto y categoría.
- **Detalle / drill-through:** tabla de órdenes con formato condicional de profit, filtros por fecha y categoría.

🔗 [Ver dashboard](COMPLETAR_LINK) · ![Dashboard](dashboard.png)

## 🛠️ Stack
`Python` · `Pandas` · `NumPy` · `SQL (PostgreSQL)` · `SQLAlchemy` · `SciPy` · `Statsmodels` · `Seaborn` · `Matplotlib` · `Power BI / Tableau` · `Jupyter Notebook`

## 📁 Estructura
```
├── ABC_Retail_Proyecto_Final.ipynb
├── data/                  # orders_clean.csv, catalog_clean.csv, marketing_clean.csv
├── dashboard.png
└── README.md
```

## ▶️ Cómo ejecutarlo
```bash
git clone https://github.com/TU_USUARIO/TU_REPO.git
cd TU_REPO
pip install pandas numpy scipy statsmodels seaborn matplotlib sqlalchemy psycopg2-binary jupyter
# Pasos 3–4 (SQL): define DB_USER, DB_PWD, DB_HOST y DB_NAME como variables de entorno
jupyter notebook
```
> Los datasets son de práctica (Practicum). Las secciones de SQL requieren acceso a la base del curso.

## ⚠️ Limitaciones
- Datos de práctica, no de producción.
- Los KPIs de rentabilidad dependen del tratamiento de outliers de cantidad.
- El A/B test no alcanzó significancia; el intervalo de confianza y el chequeo de SRM están pendientes.

## 👤 Autor
**Miguel Angel Rodriguez Vega** · [LinkedIn](https://www.linkedin.com/in/miguel-rodriguez-dataanalyst/) · [Correo](mian.rove04@gmail.com)
Rol objetivo: Data Analyst
Contacto: https://www.linkedin.com/in/miguel-rodriguez-dataanalyst/ 

Este README describe los análisis y resultados que aparecen en el notebook. Los hallazgos se presentan como resultados exploratorios y deben validarse antes de usarse para decisiones operativas.
