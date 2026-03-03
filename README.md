# challenge_telecomx_latam_parte2

## Descripción del Proyecto
Este proyecto tiene como objetivo analizar los factores que contribuyen a la evasión (churn) de clientes en la empresa de telecomunicaciones Telecom X. Utilizando Python y sus principales bibliotecas de análisis de datos, se procesarán y analizarán los datos para identificar patrones y construir modelos predictivos. La información obtenida servirá de base para que el equipo de Data Science desarrolle estrategias efectivas de retención de clientes.

## Problema de Negocio
Telecom X enfrenta una alta tasa de cancelación de clientes. Comprender las razones detrás de esta evasión es crucial para reducir la pérdida de clientes, mantener la base de usuarios y asegurar la sostenibilidad del negocio. La identificación proactiva de clientes en riesgo permite implementar acciones de retención dirigidas y más eficientes.

## Origen de los Datos
Los datos utilizados en este análisis provienen del archivo `telecom_churn_cleaned.csv`, que contiene información detallada sobre los clientes de Telecom X, incluyendo datos demográficos, servicios contratados, información de facturación y el estado de churn.

## Metodología
El análisis se llevó a cabo siguiendo una serie de pasos:

### Preprocesamiento de Datos
*   **Eliminación de Columnas Irrelevantes**: Se eliminó la columna `customerID` por ser un identificador único que no aporta valor predictivo.
*   **Codificación de Variables Categóricas**: Todas las variables categóricas (tipo 'object') fueron transformadas a formato numérico utilizando One-Hot Encoding (`pd.get_dummies`). Esto las hace compatibles con los algoritmos de machine learning.
*   **Normalización de Características Numéricas**: Para el modelo de Regresión Logística, las columnas numéricas `customer_SeniorCitizen`, `customer_tenure`, `account_Charges.Monthly` y `account_Charges.Total` fueron escaladas utilizando `StandardScaler` para asegurar que todas las características contribuyan equitativamente al modelo.

### Análisis Exploratorio de Datos (EDA)
*   **Verificación de la Proporción de Churn**: Se calculó la proporción de clientes que cancelaron versus los que permanecieron para evaluar el desbalance de clases. Se encontró una proporción de aproximadamente 26.5% de churn, lo cual, aunque desbalanceado, fue considerado manejable para los modelos iniciales.
*   **Análisis de Correlación**: Se generó una matriz de correlación para todas las variables y un heatmap para visualizar las relaciones. Se prestó especial atención a la correlación con la variable `Churn_Yes` para identificar los factores más influyentes.
*   **Análisis Dirigido**: Se utilizaron boxplots para visualizar la relación entre `customer_tenure` y `account_Charges.Total` con la cancelación, observando patrones y tendencias específicas.

### Modelado Predictivo
*   **Separación de Datos**: El conjunto de datos se dividió en entrenamiento y prueba con una proporción de 80/20, utilizando `stratify=y` para mantener la proporción de churn en ambos conjuntos.
*   **Creación de Modelos**: Se entrenaron dos modelos:
    *   **Regresión Logística**: Modelo sensible a la escala, entrenado con las características numéricas normalizadas.
    *   **Árbol de Decisión**: Modelo no sensible a la escala, entrenado con las características numéricas sin normalizar.

## Hallazgos Clave sobre el Churn
Los análisis de correlación y la importancia de las características de los modelos revelaron los siguientes factores clave que influyen en la cancelación:

*   **Contratos mes a mes (`account_Contract_Month-to-month`)**: Es el predictor más fuerte de churn. Los clientes con este tipo de contrato son mucho más propensos a cancelar.
*   **Antigüedad del Cliente (`customer_tenure`)**: A menor antigüedad, mayor es la probabilidad de churn. Los clientes con pocos meses de servicio son de alto riesgo.
*   **Falta de Servicios de Seguridad Online (`internet_OnlineSecurity_No`) y Soporte Técnico (`internet_TechSupport_No`)**: Los clientes que no tienen estos servicios adicionales son más propensos a cancelar.
*   **Servicio de Internet de Fibra Óptica (`internet_InternetService_Fiber optic`)**: Sorprendentemente, los usuarios de fibra óptica mostraron una correlación positiva con el churn, lo que podría indicar problemas de calidad o expectativas no cumplidas.
*   **Método de Pago `Electronic check` (`account_PaymentMethod_Electronic check`)**: Los clientes que usan este método de pago tienden a cancelar más.
*   **Contratos de Dos Años (`account_Contract_Two year`)**: Reducen significativamente la probabilidad de churn, mostrando la importancia del compromiso a largo plazo.

## Comparación de Modelos
Se evaluaron dos modelos utilizando métricas clave como Accuracy, Precision, Recall y F1-Score.

| Métrica     | Regresión Logística (Normalizada) | Árbol de Decisión (Sin Normalizar) |
| :---------- | :-------------------------------- | :---------------------------------- |
| Accuracy    | 0.7935                            | 0.7289                              |
| Precision   | 0.6352                            | 0.4890                              |
| Recall      | 0.5214                            | 0.4733                              |
| F1-Score    | 0.5727                            | 0.4810                              |

La **Regresión Logística** demostró un desempeño superior en todas las métricas. Esto se debe en parte a la normalización de los datos, que es crucial para modelos basados en distancia y optimización de parámetros como la Regresión Logística, permitiéndole aprender relaciones de manera más efectiva. El Árbol de Decisión, sin optimización de hiperparámetros, mostró un rendimiento inferior, con mayor cantidad de Falsos Positivos y menor capacidad para identificar verdaderos churners, sugiriendo un posible underfitting o falta de generalización.

## Estrategias de Retención Propuestas
Basadas en los hallazgos, se proponen las siguientes estrategias para Telecom X:

1.  **Programas de Fidelización para Clientes Nuevos**: Implementar programas de bienvenida y seguimiento intensivo durante los primeros 6-12 meses para reducir el churn temprano.
2.  **Incentivar Contratos a Largo Plazo**: Promover contratos de 1 y 2 años con descuentos o beneficios para fomentar el compromiso.
3.  **Mejorar la Propuesta de Valor en Servicios Adicionales**: Reforzar la importancia de servicios como Seguridad Online y Soporte Técnico, ofreciendo pruebas gratuitas o paquetes combinados.
4.  **Optimizar la Experiencia del Servicio de Fibra Óptica**: Investigar y mejorar la calidad del servicio de fibra óptica, ya que sus usuarios muestran una mayor tasa de churn.
5.  **Diversificar Opciones y Promociones de Pago**: Evaluar la relación entre el método de `Electronic check` y el churn, incentivando métodos de pago más estables.
6.  **Segmentación y Ofertas Personalizadas**: Utilizar el modelo de Regresión Logística para identificar proactivamente clientes en riesgo y ofrecerles ofertas de retención personalizadas antes de que cancelen.
 
