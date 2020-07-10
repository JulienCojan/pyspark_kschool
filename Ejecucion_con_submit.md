# Spark-submit para ejecutar una applicación en linea de comando

spark-submit permite ejecutar script python (.py) o packages java (.jar).
Vamos a ver aquí como crear y ejecutar un simple script python en Spark.

## Crear una application

En jupyter, las variables ```spark``` (SparkSession) y ```sc``` (SparContext) estàn creadas a la inicialización del notebook.
Aquí hay que crearlas.

```
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("SimpleApp").getOrCreate()
```

Se le puede añadir opciones, por ejemplo:
```
spark = SparkSession\
    .builder\
    .appName("Pyspark course")\
    .config("spark.dynamicAllocation.maxExecutors", 2)\
    .getOrCreate()"
```
aquí para añadir un package "org.apache.hadoop:hadoop-aws:2.7.3" que se puede necesitar.

## Ejemplo de aplicación
Copiemos este codigo en un archivo "simple_app.py":
```
import sys
from pyspark.sql import SparkSession

def main(argv):
    input = argv[0]
    spark = SparkSession.builder.appName("SimpleApp").getOrCreate()
    df = spark.read.text(input).cache()

    sparkOcc = df.filter(df.value.contains('Spark')).count()

    print("Lines with the world Spark: %i" % (sparkOcc))
    spark.stop()

if __name__ == "__main__":
   main(sys.argv[1:])
```

## Ejecución con spark-submit
```
$ spark-submit simple_app.py data/ReleaseNotes_Spark2-4.txt
```

Se le puede añadir optiones, por ejemplo:
```
$ spark-submit\
 --name "SimpleApp"\
 --conf spark.dynamicAllocation.maxExecutors=2\
 simple_app.py data/ReleaseNotes_Spark2-4.txt
```

## Opciones

Hay 3 posibilidades para definir opciones para la ejecucion de la aplicación, por orden de prioridad:
- "Hard-coded" en la definición del objeto sparkSession.
- con opciones al comando spark-submit
- con opciones por defector en el archivo ```${SPARK_HOME}/conf/spark-defaults.conf```

Por ejemplo:
* spark.master (o atasco --master): cluster manager al cual conectarse (por defecto "local[*]")
* spark.app.name (o atasco --name): Nombre del job en los job tracker
* spark.submit.deployMode: puede ser "client" o "cluster"
* spark.files: para enviar archivos a todo los ejecutores
* spark.submit.pyFiles: archivos que añadir al PYTHONPATH
* spark.dynamicAllocation.maxExecutors (idem min): cuantos ejecutores maximo (o minimo) a usar para la ejecución.

Ver la lista completa de opciones en: http://spark.apache.org/docs/latest/configuration.html
