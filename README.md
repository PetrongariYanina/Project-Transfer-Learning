# **Project-Transfer-Learning: Fine-Tuning para Clasificación de Tweets Ofensivos y Vulgares**

## **Introducción**

Este proyecto realiza fine-tuning de un modelo de lenguaje natural preentrenado, **DistilBERT**, para clasificar tweets en dos categorías:

- **Ofensivo**: Contenido que puede considerarse inapropiado o insultante.  
- **Vulgar**: Lenguaje con términos explícitos o groseros.  

El objetivo es construir un modelo que pueda integrarse en plataformas donde los usuarios puedan expresar opiniones, ayudando a filtrar mensajes inapropiados.

---

## **Etapa 1: Conceptualización del Proyecto**

El modelo elegido es **DistilBERT**, un transformer preentrenado optimizado para tareas de predicción en lenguaje natural y adaptado al español. Este modelo combina eficiencia y precisión, siendo ideal para esta tarea de clasificación binaria.

### **Principales desafíos:**
- Encontrar un modelo preentrenado en español.
- Optimizarlo para dispositivos con recursos limitados.
- Aprender a usar Pytorch para entrenar el modelo.
  
---

## **Etapa 2: División de Tareas**

La organización del trabajo se realizó mediante **GitHub Projects**, dividiendo el proyecto en tareas específicas por días:

- **Día 1**: Preparación del dataset y configuración del modelo.  
- **Día 2**: Fine-tuning y evaluación.  
- **Día 3**: Revisión y plan de mejora.
  
Se trabajó colaborativamente para resolver problemas emergentes, como la limpieza de datos y la adaptación al framework **PyTorch**.

---

## **Etapa 3: Preparación y Limpieza de los Datos**

### **Fuentes de Datos**
- Dos datasets iniciales con entradas (tweets) y salidas (labels) obtenidos de GitHub.  
- Un dataset adicional de Kaggle, utilizado para pruebas.  

### **Limpieza de Datos**
- Limpieza de iconos, url,etc en tweet y eliminación de 2 registros nulos.  
- Balanceo de datos para asegurar representatividad en las etiquetas.  
- Unificación de los datasets de GitHub, resultando en un total de **10,000 registros**.  

### **Creación de Etiquetas**
El dataset de Kaggle, que contenía solo entradas, fue etiquetado utilizando el modelo entrenado en las etapas iniciales, generando categorías **Ofensivo** y **Vulgar**.

---

## **Etapa 4: Configuración del Modelo y Fine-Tuning**

### **Elección del Modelo**
- Se seleccionó **DistilBERT** por su arquitectura liviana y compatibilidad con español.  
- El preprocesamiento se realizó con la biblioteca **Transformers** de Hugging Face.  

### **Proceso de Fine-Tuning**
1. **Tokenización**: Conversión de textos en tensores mediante un tokenizer preentrenado de DistilBERT.  
2. **Estrategia de Congelamiento Gradual**:
   - Capas iniciales congeladas en las primeras épocas para mantener conocimiento preentrenado.  
   - Descongelamiento gradual con ajuste de la tasa de aprendizaje.  
3. **Función de Pérdida**:  
   - Se utilizó **Binary Cross Entropy with Logits** para tratar etiquetas multiclase.  
4. **Optimización**:
   - Uso del optimizador **AdamW** con un esquema de tasa de aprendizaje variable.  

---

## **Etapa 5: Entrenamiento**

El entrenamiento se realizó en **Google Colab** utilizando GPU.

### **Configuración del Entrenamiento**
- **División de Datos**:  
  - 80% de los datos para entrenamiento.  
  - 20% para validación.  
- **Épocas**: 3, con ajustes en el optimizador para mejorar la precisión.  
- **Batch Size**: 8, logrando un equilibrio entre velocidad y uso de memoria.  

---

## **Etapa 6: Evaluación del Modelo**

El modelo fue evaluado utilizando las siguientes métricas:
- **Precisión**  
- **Recall**  
- **F1-Score**  
- **Exactitud (Accuracy)**  

### **Resultados**
- **Mejor precisión**: ~35%  
- **Mejor exactitud**: ~81%  

Aunque los resultados iniciales son prometedores, se identificaron áreas de mejora, como el ajuste de hiperparámetros y la ampliación del dataset de entrenamiento.

---

## **Etapa 7: Implementación y Predicción**

### **Pruebas**
- Se cargó un dataset de prueba para evaluar el modelo en mensajes reales.  
- Las predicciones se realizaron mediante umbralización simple con la función sigmoide.  

### **Guardado del Modelo**
El modelo y el tokenizer se guardaron localmente para futuras integraciones en la carpeta:



---

## **Conclusión**

Este proyecto demuestra el potencial del fine-tuning para adaptar modelos preentrenados a tareas específicas, incluso en escenarios desafiantes como la clasificación multietiqueta en español.

### **Próximos pasos:**
- Explorar más datos para mejorar la precisión.  
- Optimizar el modelo para despliegue en tiempo real.  

