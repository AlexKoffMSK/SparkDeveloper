# Использование Spark UI

1. Запустить spark-shell в Docker:
   `docker run -it -p 4040:4040 --name spark-container apache/spark:latest /opt/spark/bin/spark-shell`
2. Зайти на http://spark-container:4040
3. В `spark-shell` выполнить команду `:paste`
4. Вставить код:
```scala
      // Generate a DataFrame with random numbers
      val num_rows = 1000
      val df = spark.range(num_rows).selectExpr("id", "rand() as value")

      val skew_factor = 0.2 // Adjust this value to control the skew
      val skewed_value = 10 // The value that will have higher frequency
  
      // Create a new column with skewed data
      val dfSkewed = df.withColumn("skewed_value", when(rand() < skew_factor, skewed_value).otherwise(col("value")))

```
6. Поменять Job description: `sc.setJobDescription('test job')` 
7. Провести операции над датафреймом и посмотреть результат в `Spark UI`
