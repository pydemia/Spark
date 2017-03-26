# Spark

```scala
import org.apache.spakr.sql.SQLContext

val sqlContext = new SQLContext(Sc)

import sqlContext.implicits._

val dfs = sqlContext.read.json("iot_device.json")


var df = sqlContext.read
.format("con.databricks.spark.csv")
.option("header", "true")
.option("inferSchema", "true")
.load("")

dfs.show()

dfs.groupBy($"cn")

dfs.rdd.take(5)

dfs.where($"cn")

val cndf = dfs.select("cn").distinct.collect(flatMap(_.toSeq)
val cnArray = cndf.map(state => dfs.where($"cn") <=> state))
cnArray.take(5)

cnArray(1)

val cnMap = cndf.map(cn => (cn -> dfs.where($"cn" ,=> cn))).toMap
cnMap.take(5)

var smp = cnArray(5)

import org.apache.spark.sql.functions._

smp.withColumn("rownum", monotonically_increasing_id())

val rowDF = sc.parallelize(1 to smp.count().toint).toDF("rowID")
rowDF("rawID")

smp.rdd.zipWithIndex.foreach(println)

val dfr = dfs.rdd

val convdfr = dfr.flatMap(row => row.toSeq.zipWithIndex)
convdfr.take(100)

val codfr = dfr.zipWithIndex
codfr.take(20)

import org.apache.spark.sql.functions.{col, lit, when}

var df_new = df.withColumn(""unit", when($"area" === "1", when($"area" === "2", $"zn").otherwise($"ch")).otherwize("na"))

val df_pvt = df.withColumn("comColumn", concat($"fa", $"ltc")).groupBy("lti", "ww").pivot("comColumn").max("value")
df_pvt.take(20)


val df_pck = df_pvt.select("col1", "col2").filter("col1 is not null").filter("col2 is not null")
df_pck.take(10)

val corr = Statistics.corr(df_pck.select("col1").map(row => row.getDouble(0)), df_pck.select("col2").map(row => row.getDouble(0)), "spearman")

val target = df_pvt.drop("idx0").drop("idx1").columns(0)
val cols = df_pvt.drop("idx0").drop("idx1").columns

val mapped = cols.map { colld =>
val resultDF = df_pvt.select(target, colld).na.drop("any")
(resultDF.stat.corr(target, colld), colld)
}

mapped.take(5)
```
