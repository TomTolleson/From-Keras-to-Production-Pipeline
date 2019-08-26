# From Keras to Production

## Daten

https://www.kaggle.com/moltean/fruits

## Notebooks

https://github.com/codecentric/from-keras-to-production-workshop.git

## Images pullen
```bash
docker pull codecentric/from-keras-to-production-baseimage
docker pull codecentric/tensorflow-serving-baseimage
docker pull tsabsch/airflow-baseimage
```

## Jupyterlab starten
### With docker-compose (recommended)
```bash
# Ohne Airflow
docker-compose up

# Mit Airflow
docker-compose -f docker-compose.yml -f optional-airflow.yml up
```

### Without docker-compose
#### Jupyterlab
```bash
# Für Linux/Mac
docker run -p 8888:8888 --mount type=bind,source=$(pwd)/notebooks,target=/keras2production/notebooks codecentric/from-keras-to-production-baseimage

# Für Windows
docker run -p 8888:8888 --mount type=bind,source=%cd%/notebooks,target=/keras2production/notebooks codecentric/from-keras-to-production-baseimage
```
#### TensorFlow Serving
```bash
docker run -p 8501:8501 -p 8500:8500 --mount type=bind,source=$(pwd)/notebooks/6-models/fruits/,target=/models/fruits -e MODEL_NAME=fruits codecentric/tensorflow-serving-baseimage
```

#### Airflow starten
```bash
docker run -p 8080:8080 --mount type=bind,source=$(pwd)/notebooks/8-airflow/dags,target=/usr/local/airflow/dags \
                        --mount type=bind,source=$(pwd)/notebooks/8-airflow/exercise-dataset,target=/exercise-dataset \
                        tsabsch/airflow-baseimage
```

## Alte Folien starten
```bash
pip install -r requirements.txt
cd slides
jupyter nbconvert end2end_ds.ipynb --to slides --post serve --reveal-prefix=reveal.js
```

## Referenzen und weitere Informationen

### Image Kernels

http://setosa.io/ev/image-kernels/

### Kaggle dataset

https://www.kaggle.com/moltean/fruits/kernels

### IPython and Jupyterlab

https://ipython.readthedocs.io/en/stable/interactive/python-ipython-diff.html

### Reinforcement Learning

https://www.youtube.com/watch?v=FCyZplb0ul4

### Free Notebooks from Deep Learning with Python Book

https://github.com/fchollet/deep-learning-with-python-notebooks

### Visualization of activation maps

https://jacobgil.github.io/deeplearning/class-activation-maps


### Combining channels in convolutional layers

https://towardsdatascience.com/intuitively-understanding-convolutions-for-deep-learning-1f6f42faee1

### Using pre-trained word embeddings in a Keras model

https://blog.keras.io/using-pre-trained-word-embeddings-in-a-keras-model.html

### Text Preprocessing

https://keras.io/preprocessing/text/

### Keras examples

https://github.com/keras-team/keras/tree/master/examples

### What’s your ML test score? A rubric for ML production systems

https://ai.google/research/pubs/pub45742
