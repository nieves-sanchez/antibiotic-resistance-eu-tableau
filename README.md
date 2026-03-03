# Consumo de Antibióticos y Resistencia Bacteriana en la UE (2000-2024)

> **Proyecto Académico** | Módulo 4 del Bootcamp Data Analyst & IA de Adalab

## Descripción del Proyecto

Este proyecto analiza la relación entre el consumo de antibióticos y la resistencia antimicrobiana de bacterias patógenas en los países de la Unión Europea durante el período 2000-2024. El objetivo es identificar patrones, tendencias y correlaciones que permitan entender mejor cómo el uso de antibióticos impacta en el desarrollo de resistencia bacteriana.

Los resultados del análisis se presentan através de **dashboards interactivos en Tableau** que permiten explorar los datos de manera visual y dinámica.

## Importancia del Tema

La resistencia antimicrobiana (RAM) es uno de los mayores desafíos de salud pública global. El uso excesivo e inapropiado de antibióticos acelera la aparición de bacterias resistentes, lo que dificulta el tratamiento de infecciones y aumenta la mortalidad. Este análisis busca proporcionar insights basados en datos para apoyar políticas públicas de control del uso de antibióticos.

## Estructura del Repositorio

``` text
.
├── README.md                        # Este archivo
├── data/
│   ├── raw/                         # Datos sin procesar
│   │   ├── acinetobacter-*.csv      # Resistencia de Acinetobacter a diferentes grupos
│   │   ├── coli-*.csv               # Resistencia de E. coli a diferentes grupos
│   │   ├── pneumoniae-*.csv         # Resistencia de Streptococcus pneumoniae
│   │   └── J01*.CSV                 # Consumo de antibióticos por código ATC
│   │
│   └── processed/                    # Datos procesados y consolidados
│       ├── antibiotic_consumption_2000_2024_processed.csv
│       ├── antimicrobial_resistance_2000_2024_processed.csv
│       └── consumption_resistance_2000_2024_processed.csv
│
└── notebooks/
    ├── 01_union_eda_limpieza_consumo_antibioticos.ipynb
    ├── 02_union_eda_limpieza_resistencia_bacterias.ipynb
    └── 03_integracion_consumo_resistencia.ipynb
```

## Descripción de los Datos

### Datos Crudos (`data/raw/`)

#### Resistencia Bacteriana

Los datos de resistencia se organizan por bacterial y grupo de antibiótico:

- **Acinetobacter spp.**: Resistencia a aminoglucósidos, carbapenemes y fluoroquinolonas
- **E. coli**: Resistencia a aminoglucósidos, carbapenemes, cefalosporinas y fluoroquinolonas
- **Streptococcus pneumoniae**: Resistencia a aminoglucósidos, carbapenemes, cefalosporinas y fluoroquinolonas

**Formato**: Porcentaje de resistencia (0-100%)

#### Consumo de Antibióticos

Los datos de consumo se organizan por código ATC (Anatomical Therapeutic Chemical Classification System):

- **J01D**: Consumo de β-lactámicos
- **J01G**: Consumo de aminoglucósidos
- **J01M**: Consumo de fluoroquinolonas

**Formato**: DDD (Dosis Diaria Definida) por 1000 habitantes por día

### Datos Procesados (`data/processed/`)

#### `antibiotic_consumption_2000_2024_processed.csv`

| Campo | Descripción |
|-------|-------------|
| `year` | Año (2000-2024) |
| `country` | País de la UE |
| `antibiotic_group` | Código ATC del grupo de antibióticos (J01D, J01G, J01M) |
| `ddd_per_1000_inhabitants_per_day` | Consumo en DDD por 1000 habitantes/día |

#### `antimicrobial_resistance_2000_2024_processed.csv`

| Campo | Descripción |
|-------|-------------|
| `year` | Año |
| `country` | País de la UE |
| `bacteria` | Bacteria analizada |
| `antibiotic_group` | Grupo de antibióticos |
| `resistance` | Porcentaje de resistencia (%) |

#### `consumption_resistance_2000_2024_processed.csv`

Dataset consolidado que combina consumo y resistencia en una única tabla:

| Campo | Descripción |
|-------|-------------|
| `Country` | País de la UE |
| `Year` | Año (2000-2024) |
| `Bacteria` | Bacteria analizada |
| `Antibiotic group` | Grupo de antibióticos |
| `Resistance` | Porcentaje de resistencia (%) |
| `Consumption` | Consumo en DDD por 1000 habitantes/día |

## Notebooks de Análisis

### 1. `01_union_eda_limpieza_consumo_antibioticos.ipynb`

**Objetivo**: Limpiar, unificar y analizar exploratorio de datos de consumo de antibióticos

**Tareas principales**:

- Carga de archivos J01B, J01G, J01M
- Análisis exploratorio (EDA) del consumo
- Limpieza de valores faltantes
- Estandarización de nombres de países
- Generación de estadísticas descriptivas

**Salida**: `antibiotic_consumption_2000_2024_processed.csv`

---

### 2. `02_union_eda_limpieza_resistencia_bacterias.ipynb`

**Objetivo**: Procesar y analizar los datos de resistencia antimicrobiana

**Tareas principales**:

- Carga de archivos de resistencia (Acinetobacter, E. coli, Streptococcus)
- Análisis exploratorio de patrones de resistencia
- Limpieza de datos inconsistentes
- Normalización de nombres de bacterias y grupos de antibióticos
- Cálculo de estadísticas por país y bacteria

**Salida**: `antimicrobial_resistance_2000_2024_processed.csv`

---

### 3. `03_integracion_consumo_resistencia.ipynb`

**Objetivo**: Integrar ambos datasets y crear análisis correlacional

**Tareas principales**:

- Fusión de consumo y resistencia
- Análisis correlacional entre variables
- Cálculo de tendencias temporales
- Identificación de outliers
- Preparación de datos para visualización en Tableau

**Salida**: `consumption_resistance_2000_2024_processed.csv`

## Configuración del Entorno

### Requisitos

- Python 3.8 o superior
- pip (gestor de paquetes de Python)
- Jupyter Notebook

### Instalación

1. **Clonar el repositorio:**

    ```bash
    git clone <url-del-repositorio>
    cd da-promo-64-modulo-4-proyecto-tableau
    ```

2. **Crear un entorno virtual (recomendado):**

    ```bash
    python -m venv venv
    ```

3. **Activar el entorno virtual:**

    **En Windows:**

    ```bash
    venv\Scripts\activate
    ```

    **En macOS/Linux:**

    ```bash
    source venv/bin/activate
    ```

4. **Instalar las dependencias:**

    ```bash
    pip install -r requirements.txt
    ```

### Cómo Usar este Repositorio

1. **Ejecutar notebooks en orden:**
   - `01_union_eda_limpieza_consumo_antibioticos.ipynb`
   - `02_union_eda_limpieza_resistencia_bacterias.ipynb`
   - `03_integracion_consumo_resistencia.ipynb`

2. **Verificar salidas procesadas** en la carpeta `data/processed/`

3. **Importar a Tableau** los archivos CSV procesados para crear dashboards

### Ejecutar los Notebooks

```bash
jupyter notebook notebooks/
```

## Visualizaciones en Tableau

Los dashboards interactivos en Tableau utilizan principalmente el dataset consolidado (`consumption_resistance_2000_2024_processed.csv`) para explorar:

### Dashboards Esperados

1. **Dashboard de Tendencias Globales**: Evolución del consumo y resistencia en la UE (2000-2024)
2. **Dashboard por País**: Comparativa de consumo vs. resistencia por país
3. **Dashboard por Bacteria**: Análisis específico de Acinetobacter, E. coli y Streptococcus
4. **Dashboard por Grupo de Antibióticos**: Patrones de resistencia por tipo de antibiótico
5. **Correlación Consumo-Resistencia**: Análisis de la relación entre variables

## Hallazgos Clave (Ejemplo)

El análisis explora:

- **Correlación positiva** entre consumo de antibióticos y resistencia
- **Variabilidad geográfica** en patrones de resistencia en la UE
- **Tendencias temporales** de ambos indicadores
- **Bacterias de mayor preocupación** (ej. Acinetobacter multirresistente)

## Países Incluidos

Se analizan **27 países de la UE** más algunos países asociados como Islandia, Noruega, etc.

Ejemplos: Austria, Bélgica, Bulgaria, Croacia, Chipre, Dinamarca, Eslovaquia, Eslovenia, España, Estonia, Finlandia, Francia, Alemania, Grecia, Hungría, Irlanda, Italia, Letonia, Lituania, Luxemburgo, Malta, Países Bajos, Polonia, Portugal, República Checa, Rumania, Suecia, Reino Unido (datos hasta 2019).

## Bacterias Analizadas

- **Acinetobacter baumannii/spp.**: Bacteria oportunista multirresistente, frecuente en entornos hospitalarios
- **Escherichia coli**: Patógeno comunitario e intrahospitalario
- **Streptococcus pneumoniae**: Causa de neumonía, meningitis e infecciones invasivas

## Grupos de Antibióticos

- **J01D** - Tetraciclinas
- **J01G** - Aminoglucósidos
- **J01M** - Fluoroquinolonas

## Fuente de Datos

Todos los datos utilizados en este proyecto han sido extraídos del **ECDC** (European Centre for Disease Prevention and Control), la agencia de la Unión Europea especializada en vigilancia de enfermedades infecciosas. Para más información, visite [ecdc.europa.eu](https://www.ecdc.europa.eu/).

## Autores

**Realizado por:**

- **Nieves Sánchez**
  - [![GitHub](https://img.shields.io/badge/GitHub-100000?style=flat-square&logo=github)](https://github.com/nieves-sanchez)
  - [![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/nieves-sanchez-data)

- **Camila López**
  - [![GitHub](https://img.shields.io/badge/GitHub-100000?style=flat-square&logo=github)](https://github.com/camilalopezmrt)
  - [![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/camila-adriana-lopez-martin)

---

Proyecto académico realizado como parte del **Módulo 4** del Bootcamp **Data Analyst & IA** de Adalab

**Última actualización**: Febrero 2026
