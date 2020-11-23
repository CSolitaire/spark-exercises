
# Spark / Distributed ML Overview

## How do we work with big data? Apache Spark

    Lessons: overview, env setup, spark api, wrangle, explore

## When or why would I use spark?

    Dealing with big data; 4 Vs velocity, volume, variety, veracity
    When the data can't live on your laptop
    Spark streaming
    Cloud analysis of data that lives in the cloud
    Alternatives: hadoop + dask

## Architecture

    scala on the JVM
    client libraries (pyspark) that talk to a running spark instance
        regardless of the specific library, all the spark code that's run is the same
        cluster manager can optimize queries
    Driver: what kickstarts everythign
    Cluster Manager: a cloud computer that orchestrates all of spark
    Executor: 1+ computers that do the work
    Databricks: notebook environment for managing spark
    Local Mode: everything on one laptop
        use case: data larger than memory, but smaller than storage

## Parallel Work

    parallel work has a higher overhead, but better performance at scale
    two levels: executors (1+) and partitions (1+)

## Spark Dataframes

    abstracts all of the above
    lazy -- don't do work until they have to
    transformations and actions
    efficiency + optimization
        example query using telco_churn (8000 rows)
            Convert tenure to years (tenure / 12) (8000)
            find all the customers w/ greater than 2 years tenure (4000)
            find all the fiber optic customers (2000)
            average monthly charges by payment_type
            show me the results
        spark might re-arrange to be more efficient, to do less work
            find all the fiber optic customers (2000)
            convert tenure to years (tenure / 12)
            gt 2 years tenure
            average by payment_type
            results
    shuffle -- when an operation depends on data in different partitions
        filter (e.g. just fiber optic customers) -- no shuffle
        sort by total charges descending -- shuffle
        biggest the performance concern in spark optimization

