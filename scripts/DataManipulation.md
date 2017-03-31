# Data Manipulation


## Load Dataset

```spark
import org.apache.spark.sql.SQLContext
import sqlContext.implicits._

val df = sqlContext.read.json("/datasets/iot_devices.json")

```


## as a `DataFrame`

## Glimpse it  

```spark
df.show(5)

+---------------+-------------+---------+----+----+-------------+---------+--------------------+--------+-------------+--------+------+---------+-------+----+-------------+
|_corrupt_record|battery_level|c02_level|cca2|cca3|           cn|device_id|         device_name|humidity|           ip|latitude|   lcd|longitude|  scale|temp|    timestamp|
+---------------+-------------+---------+----+----+-------------+---------+--------------------+--------+-------------+--------+------+---------+-------+----+-------------+
|           null|            8|      868|  US| USA|United States|        1|meter-gauge-1xbYRYcj|      51| 68.161.225.1|    38.0| green|    -97.0|Celsius|  34|1458444054093|
|           null|            7|     1473|  NO| NOR|       Norway|        2|   sensor-pad-2n2Pea|      70|213.161.254.1|   62.47|   red|     6.15|Celsius|  11|1458444054119|
|           null|            2|     1556|  IT| ITA|        Italy|        3| device-mac-36TWSKiT|      44|    88.36.5.1|   42.83|   red|    12.83|Celsius|  19|1458444054120|
|           null|            6|     1080|  US| USA|United States|        4|   sensor-pad-4mzWkz|      32|66.39.173.154|   44.06|yellow|  -121.32|Celsius|  28|1458444054121|
|           null|            4|      931|  PH| PHL|  Philippines|        5|therm-stick-5gimp...|      62|  203.82.41.9|   14.58| green|   120.97|Celsius|  25|1458444054122|
+---------------+-------------+---------+----+----+-------------+---------+--------------------+--------+-------------+--------+------+---------+-------+----+-------------+
only showing top 5 rows
```

### Add a new Column

```spark
df.withColumn("")

```

### Groupby Split

```spark
val states = df.select("State").distinct.collect.flatMap(_.toSeq)
val byStateArray = states.map(state => df.where($"State" <=> state))

```

## as a `RDD`

```spark
val rdd = df.rdd
rdd.take(5)

```

