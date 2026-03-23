# Notebooks del TFM

## Requisitos generales

- Python 3.x con `pandas`, `numpy`, `matplotlib`, `seaborn`, `holidays`, `scipy` (y otras librerías según cada notebook).
- Carpeta `data/` al mismo nivel que `notebooks/` (o rutas relativas como en cada notebook).
- Ejecutar **`00_introduccion_datos.ipynb`** primero si quieres validar rutas y un vistazo rápido a los CSV; no es obligatorio para el EDA si ya conoces los ficheros.

## Notebooks (visión general)

| Notebook | Rol |
|----------|-----|
| `00_introduccion_datos.ipynb` | Contexto, descripción de CSV y comprobaciones básicas. |
| `01_eda_demanda_productos.ipynb` | EDA de demanda a nivel unidad vendida. |
| `02_eda_ingresos_periodo.ipynb` | EDA de ingresos agregados por día. |

---

## `00_introduccion_datos.ipynb`

- **Qué hace:** Presenta el origen de los datos y los cuatro CSV principales (`orders`, `order-items`, `customers`, `customer-metrics`), carga librerías y rutas, lee los ficheros y muestra dimensiones y estadísticos básicos con salidas en Jupyter (`display`), más un bloque de gráficos exploratorios (pedidos en el tiempo, por día de la semana, por hora, histograma del total del pedido). Opcionalmente guarda `distribucion_pedidos.png`.
- **Para qué sirve:** Tener una referencia rápida de qué contiene cada archivo y el orden de magnitud de los datos antes de los EDA específicos.
- **Datos:** Espera los CSV en `../data/` (ajusta nombres si usas otro export).

---

## `01_eda_demanda_productos.ipynb`

- **Qué hace:** Carga pedidos e ítems (merge por `order_id`), expande líneas a **una fila por unidad** vendida, marca festivos (Venezuela, `holidays`), fin de semana, y variables operativas sin datos externos (promoción/temperatura). Analiza productos, tiempo (día, hora, mes, serie diaria), categorías, top productos, outliers en ventas diarias (Z-score), correlaciones y construye un dataset agregado por fecha–producto guardado como **`../data/datos_demanda_productos_limpio.csv`**.
- **Para qué sirve:** Entender patrones de demanda y dejar la tabla base para el *feature engineering* de demanda.
- **Datos:** Por defecto usa CSV exportados tipo `triplekb-orders-…` y `triplekb-order-items-…`; cambia las rutas si usas `orders.csv` / `order-items.csv`.

---

## `02_eda_ingresos_periodo.ipynb`

- **Qué hace:** A partir de un CSV de pedidos, agrega **por día** ingresos (`total`), número de pedidos, subtotales y delivery, hora modal del día como “hora pico”, y variables de calendario (día de la semana, mes, fin de semana, festivo). Incluye gráficos por día de la semana, por mes, comparativas fin de semana/festivo, serie diaria, hora pico y correlaciones. Exporta **`../data/datos_ingresos_periodo_limpio.csv`** con las columnas usadas después en modelado de ingresos.
- **Para qué sirve:** Caracterizar la evolución del negocio en dinero y volumen diario y alimentar el *feature engineering* de ingresos.
- **Datos:** Misma carpeta `../data/`; ajusta el nombre del fichero de pedidos si no es el export `triplekb-orders-…`.
