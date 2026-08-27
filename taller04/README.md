# Taller 04 — Clustering con K-means

Cuaderno: `taller_04_clustering (1).ipynb`

## Qué hicimos

1. **Generamos datos sintéticos 2D** con 6 grupos gaussianos isotrópicos (150 puntos cada uno, distinta desviación estándar), dos grupos superpuestos (G4 y G5) y 60 outliers uniformes en `[-10, 10]`.

2. **Detectamos y removimos outliers** con Local Outlier Factor (LOF) antes de clusterizar, porque K-means es sensible a puntos atípicos.

3. **Aplicamos K-means** sobre los datos limpios (900 puntos) y probamos distintos valores de **K entre 2 y 12**.

4. **Elegimos K óptimo** con tres métodos:
   - **Silhouette** → K = 5
   - **Método del codo** → K = 5
   - **Ground truth (ARI)** → K = 6 (número real de grupos)

5. **Validamos** con accuracy (~0.93), F1 y matriz de confusión usando las etiquetas verdaderas.

## Resultado principal

| Método | K sugerido | ¿Acertó el K real (6)? |
|--------|------------|-------------------------|
| Silhouette | 5 | No |
| Codo | 5 | No |
| ARI (ground truth) | 6 | Sí |

Silhouette y codo sugieren **5** porque G4 y G5 están tan cerca que, geométricamente, parecen un solo grupo. Solo el método con etiquetas reales (ARI) recupera el **K = 6** correcto.

Los métodos internos (Silhouette, codo) no siempre detectan el número real de grupos cuando hay solapamiento; por eso conviene comparar varios criterios y, si existen etiquetas, usar métricas como ARI.
