# Hadoop_practicas
ejemplos de  hadoop  materia de herramientas avanzadas para el manejo de grande volumenes de UNRC

Se inicio abriendo una terminal en docker-hadoop  en la cual se uso el siguiente comando, este servira para cargar los 5 contenedores requeridos 
 ```ruby
 docker-compose up -d
``` 
ya que se ejecuto lo anterior se llevara acabo el comanado
```ruby
docker-compose.yml
``` 
mismo que se utilizara para el procesar ,descargar las imagenes necesaria (en caso de que no esten disponibles para comprobar que los comandos se esten ejecutando se usara el comando
 ```ruby  
 docker ps
  ```
para entrar al nodo maestro se va a ejecutar el comando
```ruby
docker exec -it namenode bash
``` 
# Ejercicio de contar palabras
se da inicio a descargar  el arhivo 
```ruby
hadoop-mapreduce-examples-2.7.1-sources.jar
``` 
el cual vamos a encontrar en la pagina https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-mapreduce-examples/2.7.1/ ,asi menciondo con anterioridad vamos a mover el archivo a una carpeta que creamos con nombre hadoop, para seguir con el proceso vamos a descargar cualquier archivo de TEXTO (txt) en este caso nosotros lo nombramos ejemplo 2.
se movera el archivo  ejemplo2_wc.txt a la carpeta de hadoop estas dos instrucciones simpre se aran de forma manual 
para ejecutar los archivos  en el contenedor se  ejecutara  
```ruby
docker cp hadoop-mapreduce-examples-2.7.1-sources.jar namenode:/tmp
``` 
 este procedimeto se llevara acabo para el mismo archivo 
 ```ruby
docker cp ejemplo2_wc.txt namenode:/tmp
``` 
vamos a ingresar al contenedor
```ruby 
docker exec -it namenode bash
``` 
y en seguida  vamos a ejecutar
```ruby
hdfs dfs -mkdir /user/root/input_contador
```  
para poder copiar el archivo de texto vamos a ejecutar  el comando 
```ruby
cd /tmp
``` 
despues vamos a ejecutar 
```ruby
hdfs dfs -put ejemplo2_wc.txt /user/root/input_contador
```
para ejecutar el MapReduce vamos a copiar esta linea de codigo 
```ruby
hadoop jar hadoop-mapreduce-examples-2.7.1-sources.jar org.apache.hadoop.examples.WordCount input_contador output_contador
``` 
para ver los resultados de todo el proceso ejecutamos el comando  
```ruby
hdfs dfs -cat /user/root/output_contador/*
```
y para ver los resultados ven la carpeta misma que al ejecutar el comando se vera en el blog de notas el resultado 
```ruby
hdfs dfs -ls /user/root/output_contador
```
para exportartar los resultados al la carpeta base (hadoop)  ejecutamos 
```ruby
hdfs dfs -cat /user/root/output_contador/part-r-00000 > /tmp/ejemplo2_wc.txt
```
 despues

 exit
 ```
 por ultimo
 ```ruby
 docker cp namenode:/tmp/ejemolo2_wc.txt .
```
# Ejercicio de ordenr numeros de menor a menor
como primer paso tenemos que iniciar descargando un scrip el cual vamos a encontar en la sig. liga https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-mapreduce-examples/2.7.1/
despues vamos a descargar el archivo de nombre 
```ruby
hadoop-mapreduce-examples-2.7.1-sources.jar 
```
despues proedemos a mover el archivo Temperature.txt a la carpeta de hadoop 
mismo archivo que lo vamos a mover a la carpeeta de docker-hadoop 
para copiar los archvos .jar y .txl al contenedor vamos a ejecutar el codigo 
 ```ruby
docker cp hadoop-mapreduce-examples-2.7.1-sources.jar namenode:/tmp
```
como se realizo el anteior proceso se realizara para el achivo Temperature.txt debemos ingresar a la carpeta de entrada que se encuenra en el contenedor namenode el cual para logrsrlo vamos a ejecutar el codigo 
```ruby
docker exec -it namenode bash
```
ejecutamos el sig codigo para entrar al cotenedor donde estara el archivo de temperturas 
 ```ruby
hdfs dfs -mkdir /user/root/input_temperaturas
 ```
en caso de que salga error agrega un 1 ala parte de input por que anterior mente tenemos el archivo de texto de ejemplo2
ejecutamos el comando 
```ruby
cd /tmp
``` 
el cual va a servir  para cambiar el directorio actual de trabajo al directorio de tmp ,en seguida pasamos a ejecutar 
```ruby
hdfs dfs -put Temperature.txt /user/root/input_temperaturas
```
ejejutamos el MapReduce 
 ```ruby
hadoop jar hadoop-mapreduce-examples-2.7.1-sources.jar org.apache.hadoop.examples.SecondarySort input_temperaturas output_temperaturas
 ```
para concluir vamos a ejecutar los sig comandos 
 ```ruby
hdfs dfs -cat /user/root/output_temperaturas/*
 ```
ese comando nos servira para ver los resultados de dicho proceso
para comprobar los resultados ejecutamos 
 ```ruby
hdfs dfs -ls /user/root/output_temperaturas
 ```
# nota :Para guardar los resultados del proceso se llevara acabo la misma ejecucon de comandoos que el anterior ejercico de conteo de palabras solamnte sera modificado el nombre del archivo en lugar de ser ejemplo2 sera temperaturas_ordenadas.
# Resolucion de suduku
como primer paso vamos a descargar el archivo para ejecutar el algoritmo https://drive.google.com/file/d/1m6uSyzNCQV1617fmhQyW59sMQ2DYef2E/view?usp=classroom_web&authuser=0
asi mismo lo vamos a mover a la carpeta de hadoop y descargamos el archivo txt,en seguida ejecutamos este codigo  
 ```ruby
docker cp puzzle1.dta namenode:/tmp 
 ```
asi mismo iniciammos ejecutando 
 ```ruby
cd/tmp
 ```
y ejecutamos el sig codigo
 ```ruby
hadoop jar hadoop-examples-0.20.205.0.jar sudoku puzzle1.dta
 ```
para ver los resultados ejecutamos 
 ```ruby
hadoop jar hadoop-examples-0.20.205.0.jar sudoku puzzle1.dta > solucion_puzzle1.txt
 ```
despues 
 ```ruby
exit
 ```
por ultimo revisamos la carpeta y buscamos el archivo correspondiente 

# nota todo codigo tiene como referencia 
https://hadoop.apache.org/docs/stable/api/org/apache/hadoop/examples/dancing/package-summary.html
