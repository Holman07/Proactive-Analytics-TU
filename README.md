# Proactive-Analytics-TU
## Tips de Uso en Spark
A continuación veremos algunos tips que el equipo de ProActive Analytics TU ha identificado como importantes para la ejecución de códigos desde la terminal especialmente de R.

### Control de Paralelismo y Aumento de Particiones
Con este código se amplian las particiones que se corren por default al máximo permitido en Spark TU (800)

```R
spark-sql --master yarn 
	--hiveconf spark.default.parallellism="800" 
	--hiveconf spark.sql.shuffle.partitions="800" 
 -f "Coloque su código extensión sql".sql
```

### Manejo especializado Fechas TUCA
Con este código se hace la ejecucion conjunta de TUCA o corrida especifica para Nicaragua.
```R
spark-sql --master yarn --hiveconf spark.sql.parquet.datetimeRebaseModeInRead='LEGACY'
	--hiveconf spark.sql.parquet.datetimeRebaseModeInWrite='CORRECTED'
	--hiveconf spark.sql.parquet.int96RebaseModeInRead='LEGACY'
	--hiveconf spark.sql.parquet.int96RebaseModeInWrite='CORRECTED' -f "Coloque su código extensión sql".sql
```

### Corrida de Códigos Anidados
se hace la ejecución de un código tras otro, sirve para procesos de automatización en horarios alternativos.

```R
spark-sql --master yarn --queue root.sha9cogp -f "codigo1".sql
	&& spark-sql --master yarn --queue root.sha9cogp -f "codigo2".sql
	&& spark-sql --master yarn --queue root.sha9cogp -f "codigo3".sql 
```



```
