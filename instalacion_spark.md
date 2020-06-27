# Installation de Spark

## En Linux

### Dependencias
* java 8 (openjdk-8)
* python 2.7+/3.4+ (usaremos python 3)
* jupyter y pandas (```pip install jupyter pandas```)

### Instalación
* Descargar spark (https://spark.apache.org/downloads.html), por ejemplo spark-2.4.6-bin-hadoop2.7.tgz
* Unzip por ejemplo en '~/App'
```
ln -s ~/App/spark-2.4.6-bin-hadoop2.7 ~/programs/spark
SPARK_HOME="$HOME/App/spark"
export PATH=$SPARK_HOME/bin:$PATH
```
* ejecutar pyspark en un notebook jupyterhub
```
PYSPARK_DRIVER_PYTHON=jupyter PYSPARK_DRIVER_PYTHON_OPTS='notebook' pyspark
```


## Con Docker

Instalar [Docker Desktop/Docket](https://www.docker.com/products/docker-desktop).

Ejecutar el comando siguiente en bash / powershell:
```
docker run -p 8888:8888 -p 4040:4040 jupyter/pyspark-notebook
```
Para desplegar el contenedor [pyspark-notebook](https://github.com/jupyter/docker-stacks/tree/master/pyspark-notebook), ver otros contenedores en: https://github.com/jupyter/docker-stacks

Esto puede tomar tiempo la primera vez ya que tiene que descargar el contenedor.
Cuando ya está desplegado el contenedor deben aparecer unas líneas de este tipo.

```
To access the notebook, open this file in a browser:
  file:///home/jovyan/.local/share/jupyter/runtime/nbserver-6-open.html
Or copy and paste one of these URLs:
  http://2853919f6050:8888/?token=[...]
  or http://127.0.0.1:8888/?token=[...]
```
Basta con copiar y pegar una de estas url en un navegador para acceder a la interfaz de JupyterHub.


## Referencias
[Documentation oficial de Spark](http://spark.apache.org/docs/2.4.6/)

http://bartek-blog.github.io/python/spark/jupyter/2019/03/27/how-to-install-pyspark.html
