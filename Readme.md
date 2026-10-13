# Red de comercio internacional de productos químicos

> 🚧 **Proyecto en desarrollo.**

Proyecto aplicado del curso *Network Science for Data Analysis*. Busca identificar qué países son más centrales en la red de comercio de productos químicos (sección Chemical del Sistema Armonizado, capítulos 28 a 38), tomando como referencia a Silva, Wilhelm & Amancio (2024), *Machine learning and economic forecasting: The role of international trade networks* (Physica A 649, 129977).

## Datos

Datos crudos descargados de [UN Comtrade](https://comtradeplus.un.org/), en la carpeta `data set/`. Están divididos en dos archivos por el límite de códigos de producto por consulta:

| Archivo | Códigos SA (HS) |
|---|---|
| `TradeData_10_13_2026_4_37_2.csv` | 28 al 33 |
| `TradeData_10_13_2026_4_38_34.csv` | 34 al 38 |