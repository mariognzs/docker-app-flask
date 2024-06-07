# Docker Flask App

Este repositorio contiene un pequeño programa en Python que utiliza Flask para crear una aplicación web simple. La aplicación se ejecuta dentro de un contenedor Docker basado en Ubuntu.

## Contenido del repositorio

- `Dockerfile`: Archivo de configuración para construir la imagen Docker.
- `app.py`: Archivo de la aplicación Python con Flask.

## Estructura del proyecto

```
.
├── Dockerfile
└── app.py
```
### Dockerfile
```dockerfile
FROM ubuntu
RUN apt-get update && apt-get install -y python3 python3-pip
RUN rm /usr/lib/python3.*/EXTERNALLY-MANAGED
RUN pip install flask
COPY app.py /opt/
ENTRYPOINT FLASK_APP=/opt/app.py flask run --host=0.0.0.0 --port=8080
```

### app.py

```python
import os
from flask import Flask

app = Flask(__name__)

@app.route("/")
def main():
    return 'Bienvenido!'

@app.route('/Como estas')
def hello():
    return 'Estoy bien, y tu como andas?'

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)
```

## Instrucciones de uso

### Construir la imagen Docker

Para construir la imagen Docker, ejecuta el siguiente comando en el directorio donde se encuentra el `Dockerfile`:

```sh
docker build -t flask-app .
```

### Comprobar que la imagen Docker existe

Para verificar que la imagen Docker ha sido creada exitosamente, puedes listar las imágenes Docker en tu sistema con el siguiente comando:

```sh
docker images
```

Deberías ver `flask-app` listado en las imágenes disponibles.

### Ejecutar el contenedor Docker

Una vez que la imagen ha sido construida, puedes ejecutar el contenedor con el siguiente comando:

```sh
docker run -p 8080:8080 flask-app
```

### Acceder a la aplicación

Abre tu navegador web y dirígete a `http://localhost:8080`. Deberías ver el mensaje "Bienvenido!".

Para ver el segundo endpoint, ve a `http://localhost:8080/Como%20estas`. Deberías ver el mensaje "Estoy bien, y tu como andas?".

## Notas

- Asegúrate de tener Docker instalado y ejecutándose en tu máquina.
- La aplicación Flask se ejecuta en el puerto 8080 dentro del contenedor y se mapea al puerto 8080 de tu máquina local.

## Autor

Mario González Solas
- [Mi LinkedIn](https://www.linkedin.com/in/mario-gonz%C3%A1lez-solas/)

