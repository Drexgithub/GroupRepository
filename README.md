Name: Kiel Hedrix V. Relos,
       ,Arbie Ancheta
       ,Marx Ervic Delima
       ,Kenneth Borjal

Lab No: Spark RDD Pipeline 01

Git Repo/ Colab Link: [Insert Your Link Here]


Date: February 14, 2026 

Objective
The objective of this lab is to understand and implement a functional data processing pipeline using Apache Spark RDDs. Specifically, the activity aims to demonstrate the chaining of multiple transformations—including filtering, mapping, and aggregation—to perform frequency analysis on raw log data.
+4

Introduction
This lab explores Apache Spark, a distributed computing framework designed for large-scale data processing. The focus is on the Resilient Distributed Dataset (RDD), the fundamental data structure of Spark. By applying functional programming patterns such as map and reduceByKey, we can transform unstructured log entries into structured, actionable insights through a series of distributed computation steps.
+2

Methodology
The following steps were implemented in the Scala Spark-shell to process the dataset:


Initialize Data: Create a parallelized collection (RDD) from a sequence of raw log strings containing different log levels (ERROR, INFO, DEBUG).


Filter: Apply a .filter() transformation to retain only records starting with the "ERROR" prefix.


Cleanse (Map): Use .map() to strip the "ERROR:" prefix and trim whitespace, leaving only the message body.


Tokenize (FlatMap): Utilize .flatMap() to split the message strings into individual words.


Pairing (Map): Transform each word into a key-value pair format (word, 1) to prepare for aggregation.


Aggregate (ReduceByKey): Use .reduceByKey() to sum the occurrences of each word across the dataset.


Sort: Apply .sortBy() to organize the results by frequency in descending order.

Results and Analysis
The final execution produced an aggregated count of words found within error logs. As shown in the final output, the word "database" was the most frequent, appearing 3 times, followed by "connection" and "failed" appearing twice each.

Final Console Output:

Plaintext
(database,3)
(connection,2)
(failed,2)
(write,1)
(authentication,1)
(conflict,1)
(timeout,1)
Challenges and Solutions
Challenge: Incomplete statement execution. When pasting code line-by-line, the Scala interpreter treated each transformation as a separate, unlinked variable, resulting in the final collect() action only printing the original raw data.

Solution: Used curly braces { } to wrap the entire pipeline into a single block. This forced the interpreter to treat the entire sequence as one continuous expression, correctly chaining the transformations to the finalOutput variable.

Challenge: Excessive logging. The console was flooded with INFO and DEBUG messages from the JVM, making it difficult to see the results.


Solution: Executed sc.setLogLevel("ERROR") to silence non-critical log entries.

Conclusion
This lab successfully demonstrated the power of Spark RDDs for building data pipelines. We learned that RDDs use lazy evaluation, meaning transformations are only executed when an action like .collect() is called. Furthermore, the lab highlighted the importance of statement chaining in Scala to ensure data flows correctly from one transformation to the next
