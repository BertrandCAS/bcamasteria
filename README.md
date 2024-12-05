
# **TFM YOLO V8**

Este proyecto implementa y entrena un modelo YOLO (You Only Look Once) versión 8 para la detección de objetos. El proyecto se enfoca en configurar un dataset, entrenar un modelo y validar su rendimiento.

---

## **Tabla de contenido**
- [Descripción](#descripción)
- [Instalación](#instalación)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Uso](#uso)
  - [Preparación del dataset](#preparación-del-dataset)
  - [Entrenamiento del modelo](#entrenamiento-del-modelo)
  - [Validación del modelo](#validación-del-modelo)
- [Resultados](#resultados)
- [Colaboradores](#colaboradores)

---

## **Descripción**

El objetivo principal de este proyecto es utilizar YOLOv8 para detectar equipos de protección individual (EPI) como:
- **Casco**
- **Chaleco**
- **Ausencia de EPI**.

El proyecto sigue un enfoque basado en la organización de datos, entrenamiento supervisado y visualización de resultados.

---

## **Instalación**

### **Requisitos previos**
1. Python 3.x
2. Bibliotecas necesarias:
   - Ultralytics
   - Google Colab (si se usa en línea)
   - Matplotlib, PIL

### **Instalación de bibliotecas**
Instale las dependencias necesarias usando `pip`:
```bash
pip install ultralytics matplotlib pillow
```

---

## **Estructura del proyecto**

La estructura del dataset utilizada para este proyecto es la siguiente:

```
TFM DATASET YOLO/    # Carpeta principal del dataset
│
├── train/           # Datos para el entrenamiento
│   ├── images/      # Imágenes de entrenamiento
│   └── labels/      # Anotaciones correspondientes
│
├── valid/           # Datos para la validación
│   ├── images/      # Imágenes de validación
│   └── labels/      # Anotaciones correspondientes
│
├── test_images/     # (Opcional) Imágenes para pruebas finales
├── predictions/     # Carpeta para guardar las predicciones
└── dataset.yaml     # Archivo de configuración YAML para YOLO
```

---

## **Uso**

### **Preparación del dataset**
Asegúrese de que su dataset respete la estructura mencionada anteriormente. El archivo `dataset.yaml` debe contener:
```yaml
train: path/to/train
val: path/to/valid
nc: 5  # Número de clases
names: ['Casco', 'Chaleco', 'No-Casco', 'No-Chaleco', 'Persona']
```

### **Entrenamiento del modelo**
Para entrenar el modelo YOLOv8, ejecute el siguiente código:
```python
from ultralytics import YOLO

model = YOLO('yolov8n.pt')  # Cargar el modelo YOLO
model.train(
    data='path/to/dataset.yaml',
    epochs=20,
    imgsz=640,
    project='YOLOv8-TFM',
    name='run1'
)
```

### **Validación del modelo**
Valide el rendimiento del modelo con el conjunto de datos de validación:
```python
results = model.val(data='path/to/dataset.yaml', imgsz=640)
```

### **Generación de predicciones**
Use el modelo en imágenes de prueba y guarde los resultados:
```python
results = model.predict(source='path/to/test_images', save=True)
```

---

## **Resultados**

Los resultados incluyen:
- **Precisión (P)**: Predicciones correctas entre todas las predicciones realizadas.
- **Recall (R)**: Objetos detectados entre todos los objetos reales.
- **mAP@50**: Precisión media con un umbral de IoU de 50 %.
- **mAP@50-95**: Precisión media en varios umbrales de IoU.

Ejemplo de visualización de predicciones:

![Ejemplo de predicción](path/to/image.jpg)

---

## **Colaboradores**
- **BertrandCAS**: Desarrollo  del proyecto e implementación de YOLOv8.

Para preguntas o sugerencias, contáctame vía [GitHub](https://github.com/BertrandCAS).

---
