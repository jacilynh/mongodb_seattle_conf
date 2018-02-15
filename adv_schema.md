#Advanced Schema Design Patterns
(breakout session, keynote security session cancelled)
11:00 by Daniel Coupal, Sr Curriculum Engr

####intro
    - gang of four
    - MongoDB systems can be blt using its own design patterns
    - 10 yrs w/ document model
    - use of a common methodology & vocab when designing schemas for MongoDB
    - ability to model schemas using bldg blocks
    - less art & more methodology
    - why create models?
        - ensure good performance, scalability, despite contraints
            - hardware (RAM faster than disk, disk cheaper than RAM, network latency, reduce costs $$)
            - db server (max size for doc, atomicity of a write)
            - data set (size of data)
    - don't overdesign
        - simplicity at one end of spectrum
            - shared hosted db
            - individual effort level
        - in middle: replica set
        - performance at other end
            - large team
             - large sharded cluster

####example: world movie db
     - pattern 1: attribute, take key value, transfer to pair of key values
        - for use when:
            - lots of sim. fields
            - common characteristic to search across those fields together
            - fields present in only a small subset of documents
        - solution
            - field pairs in array
            - allows for non deterministic list of attr.
            - easy to index
            - easy to extend with qualified, for example:
    - issue 2: working set doesn't fit in RAM (the piece of data that is being read)
        - reduce size of your working set
        - add more RAM
        - start sharding or add more shards
    - pattern 2: subset
        - limit the list of actors and crews to 20
        - subset pattern: there is a 1-N or N-N relationship and only a few documents always need to be shown
        - only infrequently do you need to pll al ofthe depending documents
        - use cases: main actors of movie, list of review or comments
        - which mondodb 3.6 feature will allow me to notify an application if the name of an actor is changed? 
    - issue 3: lots of CPU usage
        - caused by repeat calcs
    - pattern 3: computed
        - apply a sum, count...
        - rollup data by min/hr/day
        - solves:
            - data that needs to be computed
            - same calcs over and over
            - reads outnumber writes: 1K writes/hr vs 1M read/hr
        - use case: have revenues per movie showing, want to display sums
        - use case: time series data, event sourcing
        - which relational db feature typ used ot minic the computed pattern? question!
    - issue 4: lots of writes
        - discs were idled down doing too many writes
        - i.e. 80% of writes were web page counters, maybe used to sell ads
        - for non critical data
    - pattern 4: approximation
        - only increment once in x iterations
        - iterate by X
        // ♥ {$inc: {views:1}}
        go to:
        // ♥ {$inc: {views: 10}}
        using:
        // ♥ if random(0,9) == 0
                increment by 10
    - approx pattern solution:
        - do fewer stronger writes, reduces contention on some documents
    - issue 5: need ot chang eht list of fields in the documents
        - keeping track of the schema versoin of a document
    - pattern 5: schema versioning
        - add field to track schema version number,per document
        - does not have to exist for v1
        - problem: updating schema of db is not atomic, long operation, may not want to update all doucments, only do it on updates
        - use cases: practically any db that will go to production

####aspect of patterns: consistency
        - how duplication is handled
            - update both source & target in real time
        - update target from source at reg. intervals. 
            - most popular items => update nightly
            - revenues from movie => update / hr
            - last 10 reviews => update hrly, daily

####other patterns:
    - bucket
    doc versioning

####takeaways
    - simple grouping from tables to collections is not optimal
    - learn common vocab for designing schemas with MDB
    - use patterns as plug and play

####Resources
    - "mongoDB applied design patters"
    - "the little mondo db schema design book"

check out: university.mongodb.com
(upcoming course on data modeling)


which pattern is used in the following document? (question!)