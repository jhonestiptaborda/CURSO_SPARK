Configuración del entorno local para PySpark
1. Objetivo

El objetivo de esta actividad fue preparar un entorno local para comenzar el aprendizaje de Apache Spark utilizando Python.

La configuración incluyó:

Creación de un repositorio en GitHub.
Clonación del repositorio en el computador.
Creación de un entorno virtual de Python.
Configuración del archivo .gitignore.
Organización inicial del proyecto.
Validación de Python.
Validación de Java.
Instalación de PySpark.
Creación y validación de una sesión de Spark.
Registro de dependencias en requirements.txt.

PySpark es la API de Python para Apache Spark y permite procesar grandes volúmenes de datos utilizando Python.

2. Creación del repositorio

Se creó en GitHub un repositorio público llamado:

CURSO_SPARK

El repositorio se clonó localmente mediante:

git clone https://github.com/jhonestiptaborda/CURSO_SPARK.git

El comando git clone descarga el contenido del repositorio remoto y configura automáticamente la conexión llamada origin.

Después se ingresó a la carpeta:

cd CURSO_SPARK

La conexión se validó mediante:

git remote -v

Resultado esperado:

origin  https://github.com/jhonestiptaborda/CURSO_SPARK.git (fetch)
origin  https://github.com/jhonestiptaborda/CURSO_SPARK.git (push)

También se validó el estado del repositorio:

git status
3. Creación del entorno virtual

Antes de crear el entorno se verificó la versión de Python:

python --version

Resultado:

Python 3.11.9

Se creó un entorno virtual con:

python -m venv .venv

El módulo venv permite crear entornos de Python aislados, cada uno con su propio conjunto de paquetes instalados.

El entorno se activó mediante:

.\.venv\Scripts\Activate.ps1

Cuando está activo, la terminal muestra:

(.venv)

Ejemplo:

(.venv) PS C:\Users\CES\Documents\DATA_ENGINEER\CURSO_SPARK>
4. Validación del entorno virtual

Se validó la ubicación del entorno mediante:

$env:VIRTUAL_ENV

Resultado:

C:\Users\CES\Documents\DATA_ENGINEER\CURSO_SPARK\.venv

También se verificó el ejecutable de Python:

Get-Command python | Select-Object Source

Resultado:

C:\Users\CES\Documents\DATA_ENGINEER\CURSO_SPARK\.venv\Scripts\python.exe

Esto confirmó que Python estaba siendo ejecutado desde el entorno virtual del proyecto.

5. Actualización de pip

pip es el gestor utilizado para instalar paquetes de Python.

Se actualizó mediante:

python -m pip install --upgrade pip

La instalación se validó con:

pip --version

La ruta mostrada debía pertenecer al entorno:

CURSO_SPARK\.venv
6. Creación del archivo .gitignore

Se creó el archivo:

.gitignore

Su contenido inicial fue:

# Entorno virtual
.venv/

# Caché de Python
__pycache__/
*.pyc

# Jupyter
.ipynb_checkpoints/

# Visual Studio Code
.vscode/

# Variables de entorno
.env

# Archivos temporales
*.tmp
~$*

Este archivo evita que Git incluya elementos locales o innecesarios, especialmente el entorno virtual .venv.

7. Estructura inicial del proyecto

Se crearon las carpetas principales mediante:

mkdir data, docs, notebooks, src, tests

Posteriormente se crearon las zonas de datos:

mkdir data\raw, data\processed, data\rejected

La estructura obtenida fue:

CURSO_SPARK
├── data
│   ├── raw
│   ├── processed
│   └── rejected
├── docs
├── notebooks
├── src
├── tests
├── .gitignore
└── requirements.txt
Función de las carpetas
data/raw

Contendrá los archivos originales recibidos por el proyecto.

Estos archivos no deben modificarse directamente.

data/processed

Contendrá datos limpios o transformados por Spark.

data/rejected

Contendrá registros que incumplan las reglas de calidad.

notebooks

Contendrá ejercicios y prácticas progresivas de PySpark.

src

Contendrá código Python reutilizable y componentes del pipeline.

tests

Contendrá pruebas y validaciones automatizadas.

docs

Contendrá la documentación del curso y del proyecto.

8. Creación de archivos .gitkeep

Git no conserva carpetas vacías. Por esta razón, se agregaron archivos .gitkeep en las carpetas que todavía no contenían archivos reales.

Se utilizó:

New-Item `
data\raw\.gitkeep, `
data\processed\.gitkeep, `
data\rejected\.gitkeep, `
docs\.gitkeep, `
notebooks\.gitkeep, `
src\.gitkeep, `
tests\.gitkeep `
-ItemType File

.gitkeep es una convención de proyecto y no una función especial de Git.

9. Creación de requirements.txt

Se creó el archivo:

requirements.txt

Comando utilizado:

New-Item requirements.txt -ItemType File

Este archivo permitirá registrar las librerías necesarias para reproducir el entorno del proyecto.

10. Validación de Java

Apache Spark utiliza la Máquina Virtual de Java para ejecutar su motor de procesamiento.

Se validó la versión instalada mediante:

java -version

Resultado:

openjdk version "17.0.19" 2026-04-21
OpenJDK Runtime Environment Temurin-17.0.19+10
OpenJDK 64-Bit Server VM Temurin-17.0.19+10

La documentación oficial de PySpark indica que se necesita Java 17 o una versión posterior y que JAVA_HOME debe estar correctamente configurado.

11. Validación de JAVA_HOME

La variable se consultó mediante:

$env:JAVA_HOME

Resultado:

C:\Program Files\Eclipse Adoptium\jdk-17.0.19.10-hotspot\

Posteriormente se verificó el ejecutable utilizado:

Get-Command java | Select-Object Source

Resultado:

C:\Program Files\Eclipse Adoptium\jdk-17.0.19.10-hotspot\bin\java.exe

Las dos rutas apuntaron a la misma instalación de Java.

12. Instalación de PySpark

Con el entorno virtual activo se instaló PySpark mediante:

pip install pyspark

La documentación oficial permite instalar PySpark con pip para trabajar en un entorno local.

La instalación se validó con:

python -c "import pyspark; print(pyspark.__version__)"

Resultado:

4.2.0

Esto confirmó que PySpark estaba instalado dentro del entorno virtual.

13. Problema con pyspark --version

Al ejecutar:

pyspark --version

Windows mostró un error relacionado con la ubicación de Python:

No se encontró Python

Sin embargo, la importación directa funcionó correctamente:

python -c "import pyspark; print(pyspark.__version__)"

Por esta razón, se confirmó que PySpark sí estaba instalado.

Cuando PySpark se instala mediante pip, las aplicaciones también pueden ejecutarse utilizando directamente el intérprete normal de Python.

14. Creación de la primera SparkSession

Se realizó una prueba para validar que Spark pudiera iniciar correctamente:

python -c "from pyspark.sql import SparkSession; spark = SparkSession.builder.master('local[*]').appName('CursoSpark').getOrCreate(); print('Spark:', spark.version); print('Python:', spark.sparkContext.pythonVer); spark.stop()"

El resultado principal fue:

Spark: 4.2.0
Python: 3.11

Esto confirmó que:

PySpark se encontraba instalado.
Python estaba correctamente configurado.
Java estaba disponible.
Spark podía iniciar una sesión local.
Spark podía cerrar la sesión correctamente.

La documentación oficial de Spark presenta el uso interactivo y la creación de aplicaciones Python como formas válidas de comenzar a trabajar con Spark.

15. Explicación de la SparkSession

La clase principal utilizada fue:

from pyspark.sql import SparkSession

SparkSession representa el punto de entrada principal para trabajar con DataFrames y Spark SQL.

La sesión fue creada con:

spark = (
    SparkSession.builder
    .master("local[*]")
    .appName("CursoSpark")
    .getOrCreate()
)
SparkSession.builder

Inicia la configuración de una sesión Spark.

.master("local[*]")

Indica que Spark debe ejecutarse localmente.

El símbolo * le permite utilizar los núcleos disponibles del computador.

.appName("CursoSpark")

Asigna un nombre a la aplicación Spark.

.getOrCreate()

Crea una nueva sesión o reutiliza una existente.

spark.stop()

Finaliza la sesión Spark y libera los recursos utilizados.

16. Advertencias observadas

Durante la prueba aparecieron mensajes como:

Did not find winutils.exe
HADOOP_HOME and hadoop.home.dir are unset
Unable to load native-hadoop library

A pesar de estas advertencias, Spark inició correctamente y mostró las versiones esperadas.

Para esta etapa local de aprendizaje no se configuró Hadoop ni winutils.exe, debido a que la prueba básica funcionó utilizando las clases Java integradas.

17. Registro de dependencias

Las librerías instaladas se registraron mediante:

pip freeze > requirements.txt

El contenido se validó con:

Get-Content requirements.txt

El archivo incluyó dependencias como:

py4j
pyspark==4.2.0

Esto permitirá reconstruir el entorno en otro equipo mediante:

pip install -r requirements.txt
18. Versionamiento en Git

Los cambios fueron preparados con:

git add .

Se creó un commit:

git commit -m "chore: add PySpark dependency"

Y finalmente se enviaron a GitHub:

git push

Se validó el estado final:

git status

Resultado esperado:

On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
19. Resultado final

Al finalizar esta actividad se obtuvo un entorno local funcional con:

Python 3.11.9
Java 17.0.19
PySpark 4.2.0
Git
GitHub
Visual Studio Code
Entorno virtual .venv

Spark pudo crear una sesión local correctamente.

El siguiente paso del curso será:

Creación del primer notebook de PySpark y estudio de SparkSession

Después de guardar el archivo, súbelo a GitHub con:

git add docs\01_configuracion_entorno_pyspark.md
git commit -m "docs: add local PySpark environment setup guide"
git push

Con esto el repositorio deja de ser solo una carpeta con archivos y empieza a verse como un curso serio, trazable y presentable.