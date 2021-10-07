# Local Delta Lake Set up

The following content is mainly based on the [official *Delta Lake* documentation](https://docs.delta.io/latest/quick-start.html#set-up-interactive-shell).

## PySpark Shell

1. In your terminal install the `PySpark` version that is compatible with Delta Lake (PySpark 3.0.0 or above needs to be installed):

```bash
pip install pyspark==3.1.2.
```

2. Run `PySpark` with the Delta Lake package and additional configurations:

```bash
pyspark --packages io.delta:delta-core_2.12:1.0.0 --conf "spark.sql.extensions=io.delta.sql.DeltaSparkSessionExtension" --conf "spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog"
```

## Create a table

1. Create example data:

```bash
data = spark.range(0, 5)
```

2. To create a Delta table, write a DataFrame out in the delta format:

```bash
data.write.format("delta").save("/tmp/delta-table")
```

These operations create a new Delta table using the schema that was inferred from your DataFrame. For the full set of options available when you create a new Delta table, see [Create a table](https://docs.delta.io/latest/delta-batch.html#-ddlcreatetable) and [Write to a table](https://docs.delta.io/latest/delta-batch.html#-deltadataframewrites). You can also use existing Spark SQL code and change the format from parquet, csv, json, and so on, to delta.

## Read data

1. You read data in your Delta table by specifying the path to the files: "/tmp/delta-table":

```bash
df = spark.read.format("delta").load("/tmp/delta-table")
```

2. Show data

```bash
df.show()
```

## Retrieve data in a new session

1. Close your PySpark shell:

```bash
exit()
````

2. Start `PySpark` with the Delta Lake package and additional configurations:

```bash
pyspark --packages io.delta:delta-core_2.12:1.0.0 --conf "spark.sql.extensions=io.delta.sql.DeltaSparkSessionExtension" --conf "spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog"
```

3. Read data in your Delta table by specifying the path to the files: "/tmp/delta-table":

```bash
df = spark.read.format("delta").load("/tmp/delta-table")
```

2. Show data

```bash
df.show()
```

# Python examples


- [Python examples](https://github.com/delta-io/delta/tree/master/examples/)


