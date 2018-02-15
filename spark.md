#Analytics & ML w/ Spark & MongoDB
    - Bryan Reinero, Product Manager

###Level Setting
    - Spark & MongoDB are both scable & distributed data systems
    - Spark: coarse grained data operatons, framework for processing data in parallel, good for heavy crunching
    - MongoDB is a dist. db designed to operate on fine grained operations, queries for individual items, aggregation on small sets or individual documents
    - Spark: burning bits, take large data problem and distribute smaller sets across large cluster
    - Spark's operative word: parallelism
    - differences:
        Spark: parallelism, ML APIs (supervised, unsupervised), stream processing 
        MongoDB: aggregaton, native processing
    - use the right tool for the right job
    - Spark & its relationship with hadoop
        - hadoop: ecosystem of tools for parallel processing, clustered processing
        - Spark uses a lot of same tools; not a replacement, but more so a new addition to the environment
        - hadoop can be difficult to deal with
        - Spark: offers easier API, better documentation, interactive shell, caching
        - Spark is  not easy, but it's easier
        - Clouderra (?)
        - Spark comes in a number of languages; originally written in scala, API for java, python, & R
        - software engineering radio podcast ep 309 by IEEE

###Distributed Data
    - there is a layer inside spark/hadoop ecosystem for dist. data: HDFS = hadoop dist. file system
    - Core of ecosystem: HDFS 
    - Second layers: "distributed resources", resource negotiator
        - YARN, map 
        - Mesos, more general
        - Spark Stand Alone (w/o cluster managment)
    - Distributed processing: 3rd layer of ecosystem
        - Hadoop, 50%
        - Spark, 50%
        - scala, java system
        - we want an API layer so that it's not just for CS
    - domain specific languages, 4th layer of ecosystem
        - hive (HQL)
        - spark SQL, same as HIVE
        - spark shell
        - pig
    - "ETL" the data out of the structure (ETL pipe) for other situations; Spark does not require that. Process data w/o having to move it
    - github.com/mongodb/mongo-spark

###Unsupervised ML & Clustering Algorithms
    - data set to devlop model
    - Clustering - RDD-based API; use a K-means algorithm to process some weather data
    - clustering algo's to find trends among data sets
    - spacial dimensions can be identifying factor for ID'ing clusters
    - other dimensions: football example; color
    - other dimensions: financial analysis, companies share sim. attributes i.e. employee size, market cap, income --these are dimensions that will cluster together companies even when not in same industry
    - K-means clustering is centroid based. three points randomly selected, stem points / centroids, then the closest points to each one get ass. to that centroid. iterative process, move centroad to mean dist. b/w those centroid, and repeat
    - data refuse: datarefuge.org/dataset/15-minute-precipitation-data-dsi-3260
    - ^^ source of this data example
    - ...(code demo)
    - used tableau through BI connector to visualize clusters

####Resources:
MongoDB university course on Spark