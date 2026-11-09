# Red de comercio internacional de productos químicos

> ✅ **Proyecto finalizado.**

Proyecto aplicado del curso *Network Science for Data Analysis*. Identifica qué países son más centrales en la red de comercio de productos químicos (sección Chemical del Sistema Armonizado, capítulos 28 a 38) y describe cómo está organizada esa red. Toma como referencia a Silva, Wilhelm & Amancio (2024), *Machine learning and economic forecasting: The role of international trade networks* (Physica A 649, 129977).

## Pregunta y enfoque

- ¿Qué tipo de red es: aleatoria, de mundo pequeño o libre de escala?
- ¿Qué países son los más importantes, y por qué criterio (número de socios, volumen, intermediación, calidad de sus conexiones)?
- ¿Existen comunidades o bloques de países?
- ¿Qué tan robusta es la red frente a la salida de nodos o de comunidades completas?

La red es **dirigida y ponderada**: cada nodo es un país y cada enlace va de un país exportador (`Origen`) a un importador (`Destino`), con el volumen comercial como peso.

## Datos

Datos crudos descargados de [UN Comtrade](https://comtradeplus.un.org/), en la carpeta `Data_Set/raw_data/`. Están divididos en dos archivos por el límite de códigos de producto por consulta:

| Archivo | Códigos SA (HS) |
|---|---|
| `TradeData_10_13_2026_4_37_2.csv` | 28 al 33 |
| `TradeData_10_13_2026_4_38_34.csv` | 34 al 38 |

La red depurada queda en `Data_Set/network/Red_Quimica_Comercio.csv` con las columnas `Origen`, `Destino`, `Peso_Volumen` y `Resistencia_Ruta` (distancia usada en las medidas ponderadas por caminos).

## Estructura del repositorio

```
Proyecto/
├── Data_Set/
│   ├── raw_data/        # Datos crudos de UN Comtrade
│   ├── network/         # Red depurada (lista de aristas)
│   └── results/         # Medidas, comunidades y escenarios de ataque
├── Imagenes/            # Figuras: distribución de grado, grafo de comercio y de comunidades
├── Notebook/
│   ├── depuracion.ipynb # Limpieza de los datos crudos y construcción de la lista de aristas
│   ├── Red.ipynb        # Construcción y visualización de la red
│   └── Medidas.ipynb    # Medidas globales, centralidades, comunidades y ataques
└── Readme.md
```

## Resultados

| Archivo | Contenido |
|---|---|
| `results/medidas_globales.csv` | Medidas de la red completa (densidad, reciprocidad, caminos, clustering, asortatividad, comunidades) |
| `results/centralidades_nodos.csv` | Centralidades y medidas locales por país |
| `results/red_comunidades.csv` | Comunidad asignada a cada país |
| `results/comparacion_escenarios_ataque.csv` | Comparación de escenarios de remoción de nodos |
| `results/ataque_comunidades/` | Resultados de los ataques dirigidos a comunidades |
| `results/red_interactiva_comunidades.html` | Visualización interactiva de la red por comunidades |

### Conclusiones principales

- **Tipo de red.** Es una red muy densa y recíproca, de mundo pequeño en un sentido débil (caminos muy cortos, en gran parte por la densidad). No es aleatoria ni libre de escala.
- **Núcleo y periferia.** Un grupo de grandes economías comercia entre sí de forma casi total, y los países pequeños se conectan sobre todo a ese núcleo.
- **Comunidades débiles.** Los algoritmos de detección no coinciden y los grupos que encuentran son poco marcados: el comercio de químicos es global y no se divide en bloques regionales claros.
- **Número de socios frente a poder real.** El número de socios está repartido de forma relativamente homogénea. En cambio, el volumen y la intermediación se concentran en pocas economías (Estados Unidos, China y Alemania, entre las más destacadas).
- **Proveedores y destinos.** Los roles se distinguen: países como China, Países Bajos o Corea actúan sobre todo como proveedores, y países como Francia, Irlanda o Canadá como destinos.

## Cómo reproducir

1. Descargar los datos de UN Comtrade (capítulos 28 al 38 del SA) y guardarlos en `Data_Set/raw_data/`.
2. Ejecutar `Notebook/depuracion.ipynb` para generar `Data_Set/network/Red_Quimica_Comercio.csv`.
3. Ejecutar `Notebook/Red.ipynb` para construir y visualizar la red.
4. Ejecutar `Notebook/Medidas.ipynb` para generar los archivos de `Data_Set/results/`.

Requiere Python con `pandas`, `numpy`, `networkx`, `matplotlib` y `jupyter` (ver las primeras celdas de cada notebook para el resto de dependencias).

## Referencia

Silva, T. C., Wilhelm, P. V. B. & Amancio, D. R. (2024). *Machine learning and economic forecasting: The role of international trade networks*. Physica A, 649, 129977.