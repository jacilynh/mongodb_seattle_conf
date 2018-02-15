#The Path to Truly Understanding Your MongoDB Data
    - @samuel_weaver, product mgr, mondodb
###Terminology
    - business intelligence: uses data to look at what happened, historically
    - business analytics: uses data to look at what happend, to predict/look ahead
    - the intersection is WHY ("analytics")
    - data growth is explosive 
        - more data created in last 2 yrs than entire previous history of human race
        - by 2020 1.7MB created per person every second
        - $130B in 2016
        - $200B+ by 2020
        - less than 0.5% of data is being analyzed and used - imagine the 
        potential

###evolution of analytics
    - 2012: dedicated reporting team, desktop access, hadoop, batch analytics, on prem only, monthly reports
    - 2018: self service, mobile access, spark, real time analytics, on-prem & cloud, on demand reporting
    - early data visualization: charles minard (1869) Naolean's march and retreat on Moscow in 1812
    - haskem's quartet: mean, variance, line of best fit (correlation), they should all look the same; outliers can really throw off your data 
    **the human eye can process 10M data bits / second; it's much more efficient for you to visualize data than to read the same data in text**

###Things to think about
    - relational vs non relational
    - use correct arch
    - choose right solution

###Hidden Replicas
    P=0 Hidden=True
    - hiddens secondary's maintain copy of primaries data set
    - hiddens sec. used for workloads w/ difference access patterns
    - can't become primary
    - can sit in cluster, you can run analytics off of it, but it'll never become the primary

###Tooling
    - how to get data out of MDB, what are our options?
    - build your own is an option; custom solution, but high investment, maintenance, deep understanding of underlying tech & its language(s)
    - Compass: dev tool, data management & manipulation, interesting schema analysis, used daily; good first place to start
    - use when: day to day dev, adding inexes, viewing server stats, data manipulation, 10,000 -> 1ft view of data
    - BI Connector: visualize & explore MongoDB data in SQL-basd BI tools
        - auto discovers schema
        - "mongosqld" (b/w mongodb & tableau)
        - use with multiple data sources, business analysts, extremely powerful but high ramp
    - MongoDB Charts
        - lightwt
        - intuitive
        - bld vis. in MDB data (nested, polym.)
        - share on dashboard
        - when you want quick answers
        - no need to flatten/ETL your MDB data
        - self service for technical audience

###Demo of Tooling: Compass
    - airbnb listings

Q&A