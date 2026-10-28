# P1: Que tempo fixo? — Pipeline de Datos Meteorolóxicos

## 1. Descrición do proxecto e estación
- **Estación:** A Coruña / Alvedro (Aeroporto)
- **Indicativo:** 08002
- **Coordenadas:** 43.3020° N, 8.3773° W
- **Período:** 01/01/2021 – 31/12/2025

## 2. Fonte dos datos e condicións
- **Orixe:** Meteostat (exportación simulada)
- **URL de descarga:** [Insertar URL de Moodle]
- **Data de descarga:** [Data actual]

## 3. Instrucións de execución
1. Iniciar a base de datos PostgreSQL con Docker:
   ```bash
   docker-compose up -d
   ```

1. Instalar dependencias:
```bash
pip install -r requirements.txt
```
2. Executar o notebook notebooks/p1_que_tempo_fixo.ipynb de principio a fin.
## 4. Táboa de Decisións de Limpeza
| Problema detectado | Detección | Acción realizada | 
| ----- | ----- | ----- | 
| **Nomes de columna con espazos / maiúsculas** | `df.columns` | Homoxeneización a minúsculas e sen espazos. | 
| **Valores ausentes representados como `-`, `NA` ou `-9999`** | `na_values` en `pd.read_csv` | Conversión automática a `NaN`. | 
| **Filas duplicadas para a mesma data** | `df.duplicated('date')` | Eliminación conservando a primeira aparición. | 
| **Datas que faltan na secuencia** | Reindexación con `pd.date_range` | Inserción de filas con `NaN` para manter continuidade temporal. | 
| **Temperaturas fóra de rango (>45ºC)** | Gráfica de liñas / `df.describe()` | Substitución por `NaN` e interpolación liñal. | 
| **Precipitacións negativas** | Outliers / valores `< 0` | Conversión a `0.0`. | 
| **Inconsistencia `tmin` > `tmax`** | Validación lóxica `df['tmin'] > df['tmax']` | Reemplazo por `NaN` e interpolación. | 

## 5. Uso da Intelixencia Artificial
Ferramentas utilizadas: ChatGPT / Gemini

Uso: Asistencia na xeración das consultas de agregación de PostgreSQL, estruturación de gráficos con Matplotlib/Seaborn e formateo do readme. Todo o código foi probado e verificado localmente.
